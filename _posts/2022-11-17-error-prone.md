---
layout: single
title: "Google Error Prone (Java) Eklentisi ile Derleme Zamanında Statik Kod Analizi Nasıl Yapılır"
date: 2022-11-17
categories: error prone statik analiz
---

Yazılım sektöründe çalışan her profesyonel tecrübesi ne kadar fazla olursa olsun kod yazmaya devam ettiği sürece basit hatalar yapabilir. Kullanmış olduğumuz derleyiciler kod yazarken bizlere genellikle yardımcı olur. Ama bu yardım çoğunlukla statik tip kontrolünün ötesine geçmez. Google tarafından geliştirilen Error Prone eklentisi derleyicinin sınırlı yardım yeteneğini arttıran ve hatalı yazılan kodu hızlıca tespit etmemizi sağlayan bir araç.

Error Prone eklentisi 500’den fazla ön tanımlı hata deseni içeriyor. Ön tanımlı hata desenleri [Error Prone Bug Patterns](https://errorprone.info/bugpatterns) adresinden incelebilir. Eklenti ön tanımlı hata desenlerinin yanında 3. parti eklentilerin kullanımına ve özel hata desenlerinin geliştirilmesinede olanak sağlıyor. Çalıştırıldığında kodumuzda tespit ettiği hatalarla ilgili hata ve uyarı mesajları gösteriyor veya gerekli yapılandırma sağlanırsa kodumuzu ön tanımlı çözümlerle otomatik olarak düzenleyebiliyor. Java 8, 11 ve 17 sürümlerine desteği bulunan kütüphane Maven, Bazel, Ant ve Gradle yük oluşturma araçları ile tümleşik çalışabiliyor. Google tarafından hata düzeltmelerinde ve büyük ölçekli kod yeniden yapılandırma (refactoring) çalışmalarında halihazırda kullanılıyor. Eklentiyi kullanmak için derleyicinin eklentiyi açımlama (annotation) işlemcisi olarak yapılandırması gerekiyor. Maven için bir test projesi birlikte hazırlamaya çalışalım.

Öncelikle pom.xml dosyamıza aşağıdaki gibi bir bölüm ekliyoruz.
```
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.6.1</version>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                    <release>8</release>
                    <encoding>UTF-8</encoding>
                    <showWarnings>true</showWarnings>
                    <compilerArgs>
                        <arg>-XDcompilePolicy=simple</arg>
                        <arg>-Xplugin:ErrorProne</arg>
                    </compilerArgs>
                    <annotationProcessorPaths>
                        <path>
                            <groupId>com.google.errorprone</groupId>
                            <artifactId>error_prone_core</artifactId>
                            <version>2.16</version>
                        </path>
                    </annotationProcessorPaths>
                </configuration>
            </plugin>
        </plugins>
    </build>
```
Ben testlerimi Java 11 derleyicisi ile yaptığım halde derlenen kodun Java 8 uyumlu olmasını istediğim için benim pom.xml dosyamda aşağıdaki bölümde ayrıca bulunmakta.
```
<properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
```
Eklentinin kodumuzda bulmayı vadettiği hatalardan birini aşağıdaki gibi yazabiliriz. Bu kod örneğinde String sınıfının concat metodu kullanıldığı halde metodun geri dönüş değeri kullanılmamış.
```
...
 String str = "Test";
 str.concat("\n");
...
```
Ardından komut satırından aşağıdaki komutu yazdığımızda;
```
mvn clean verify
``````
```
[ERROR] /C:/Users/onur.ozcelik/Desktop/Others/errorpronedemo/src/main/java/net/onurozcelik/errorpronedemo/CheckReturnValue.java:[7,19] [ReturnValueIgnored] Return value of 'concat' must be used
    (see https://errorprone.info/bugpattern/ReturnValueIgnored)
  Did you mean 'str = str.concat("\n");' or 'var unused = str.concat("\n");' or to remove this line?
```
çıktısını alıyoruz. Eklenti kod bloğunu hata ağırlık tipinde başarıyla tespit etti ve hatayı çözmemiz bir çözüm önerisi yaptı. Aşağıdaki gibi bir başka örnekle devam edelim.
```
...
enum Colors {RED, GREEN, BLUE}

   Colors color = Colors.BLUE;
        switch (color) {
            case RED:
            case GREEN:
                paint(color);
                break;
        }
...
```
Komut satırından yukarıdaki çalıştırma komutlarını yazdığımızda;
```
[WARNING] /C:/Users/onur.ozcelik/Desktop/Others/errorpronedemo/src/main/java/net/onurozcelik/errorpronedemo/MissingCasesInEnumSwitch.java:[9,9] [MissingCasesInEnumSwitch] Non-exhaustive switch; either add a default or handle the remaining cases: BLUE
```
çıktısını alıyoruz. Eklenti bu defa kod bloğunu uyarı ağırlık tipi ile başarıyla tespit etti. 

Eklentinin kodumuzdaki hataları ve dikkat etmemiz gereken noktaları göstermesi yardımcı oluyor. Bunula beraber eklenti isteğe bağlı olarak istediğimiz hata desenleri için önermiş olduğu kod düzenleme çözümlerini otomatik olarak uygulayabiliyor. Bunun için ilk başta hazırlamış olduğumuz yapılandırmada ufak bir güncelleme yapmamız gerekli. Aşağıda bu güncelleme verilmiştir.
```
<compilerArgs>
    <arg>-XDcompilePolicy=simple</arg>
    <arg>-Xplugin:ErrorProne -XepPatchChecks:ReturnValueIgnored,MissingCasesInEnumSwitch
	 -XepPatchLocation:IN_PLACE</arg>
</compilerArgs>
```
Güncellemeyi yaptıktan sonra yukarıdaki çalıştırma komutlarını yazdığımızda;
```
Refactoring changes were successfully applied to file:///C:/Users/onur.ozcelik/Desktop/Others/errorpronedemo/src/main/java/net/onurozcelik/errorpronedemo/CheckReturnValue.java, please check the refactored code and recompile.
[WARNING] /C:/Users/onur.ozcelik/Desktop/Others/errorpronedemo/src/main/java/net/onurozcelik/errorpronedemo/CheckReturnValue.java:[7,19] [ReturnValueIgnored] Return value of 'concat' must be used
    (see https://errorprone.info/bugpattern/ReturnValueIgnored)
  Did you mean 'str = str.concat("\n");' or to remove this line?
```
çıktısını alıyoruz. Yazdığımız kodu kontrol ettiğimizde eklentinin aşağıdaki gibi düzeltmeyi ağırlığı hata olarak tespit edilen hata deseni için otomatik yaptığını görüyoruz. 
```
...
String str = "Test";
str = str.concat("\n");
...  
```
Yaptığım testlerde ağırlığı uyarı tipi olan hata desenleri için otomatik düzeltmenin çalışmadığını tespit ettim. Eğer istersek eklenti yapılandırmasında ağırlığı uyarı tipi olan bir hata desenininin ağırlık tipini hata olarak değiştirebiliriz. Bunun için yapılandırmamızda aşağıdaki güncellemeyi yapmalıyız.
```
<compilerArgs>
    <arg>-XDcompilePolicy=simple</arg>
    <arg>-Xplugin:ErrorProne -Xep:MissingCasesInEnumSwitch:ERROR
  -XepPatchChecks:ReturnValueIgnored,MissingCasesInEnumSwitch -XepPatchLocation:IN_PLACE
    </arg>
</compilerArgs> 
```
Bu güncellemeden sonra dahi otomatik düzeltme varsayılan ağırlık tipi uyarı olan hata desenleri için çalışmadı. Tüm bunların yanında dokümantasyona göre eklentinin Java 8 derleyicisi ile çalışan son sürümü 2.10.0 fakat yaptığım testlerde eklentinin 2.10.0 sürümünü Java 8 derleyicisinin hiç bir sürümü ile çalıştıramadım.

Error Prone ,temiz kod yazmayı bir ilke olarak kabul etmiş profesyoneller veya takımlar için yararlı bir eklenti. Açık kaynak kod yaklaşımı ile geliştirilmeye devam ettiği için yapılandırılmasını biraz uğraştırıcı bulduğumu söyleyebilirim. Mevcut dokümantasyonu asgari metin anlayışı ile hazırlandığı için karşılaştığınız her problemin çözümünü bulamıyorsunuz. Keza Google aramalarıda çok açık sonuçlar vermiyor. Bana kalırsa yapılandırma anlamında biraz daha olgunlaştığında çok daha yararlı olabilir. Meraklısına not eklenti yukarıdaki gibi uğraşmaya gerek kalmadan IntelliJ IDEA tümleşik geliştirme ortamı için Error Prone Compiler adıyla bir eklenti olarak sunuluyor. Eklenti ile ilgili detaylı bilgiye [Error Prone](https://errorprone.info) adresinden erişebilirsiniz. Blog içinde kullanılan kod örneklerine [Error Prone Demo](https://github.com/onurozcelik/errorpronedemo) adresinden ulaşabilirsiniz.