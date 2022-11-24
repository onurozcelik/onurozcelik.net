## Spring Boot Migrator (Java) ile Eski, Kalıt (Legacy) Bileşenler Spring Boot Çatısına (Framework) Nasıl Dönüştürülür?
Yazılım sektörüne emek veren profesyoneller her gün binlerce satır kod yazıyor. Peki ertesi gün ne oluyor. Yeni çatılar, kütüphaneler ortaya çıkıyor ve kısa sürede popülerlik kazanıyor. Eski çatılarla, kütüphanelerle yazılan binlerce satır kod eski, kalıt koda dönüşüyor. Belki bu süreç bir gün içinde gerçekleşmiyor ama kısa sürede çoğu profesyonelin başına gelen bu oluyor. Bu durumla başa çıkılabilir mi? Çoğunlukla hayır. Ama Java ekosistemi içerisindeyseniz ve JAX-RS, EJB veya JMS gibi Java EE teknolojileri veya eski Spring Boot çatı sürümleri kullanarak yazılmış satırlarca kodunuz varsa bir şansınız olabilir. Spring Boot Migrator derdimize derman olabilir. 

Spring Boot Migrator (SBM) ilk sürümü Mart 2022’de yayınlanan deneysel bir proje. Proje kapsamında geliştirilen aracın iddisı Spring Boot çatısını kullanılmadan JAX-RS, EJB veya JMS gibi Java EE teknolojileri kullanılarak geliştirilmiş olan bileşenleri veya eski Spring Boot çatı sürümleri kullanarak geliştirilmiş bileşenleri otomatik olarak güncel Spring Boot çatısına dönüştürmek. Bu dönüştürme işlemi için kodlarınızı içeren dizini yolunu sunulan araca göstermek. Söz konusu araç kodlarınızı analiz edip, dönüştürme işlemi için size ön tanımlı tarifler öneriyor. Ardından yapmanız gereken önerilen tarifleri kodlarınız üzerine uygulamak ve sonuçları görmek. Araç, kusursuz bir dönüştürme işlemi yapacağını iddia etmiyor. Zaman zaman aracın uyguladığı tariflerde oluşan aksaklıkları gidermek için dönüşen kodlar üzerinde işlemler yapmanız gerekebiliyor. Hep beraber aracın detaylarını öğrenelim ve örnek bir projeye uygulayalım.

Aracı kullanabilmek için önce aracı sistemimize indirmeliyiz. Araca ait en güncel sürümlere [Spring Boot Migrator](https://github.com/pivotal/spring-boot-migrator/releases) adresinden ulaşabiliriz. Aracı indirdikten sonra kullanabilmek için dönüştürme işlemi uygulamak istediğimiz kodların bazı ön şartları sağlaması gerekiyor. Bunlar;

* Maven proje yönetim sistemi kullanıyor olmalı (Maalesef şu an için Gradle desteği bulunmuyor)
* Maven dizin yapısı kullanılıyor olmalı
* Kodlar bir Git deposu içerisinde bulunmalı
* Maven reaktör desteği bulunmuyor (Sadece bir pom.xml bulunmalı)
* `mvn clean package` komutlarıyla kod yakın zamanda derlenmiş ve target dizini bulunuyor olmalı
* Sisteminizde Java 11 veya ileri bir Java sürümü yüklü olmalı

Ön şartları sağladığımızdan emin olduktan sonra aracı indirdiğimizde dizinde bir terminal uygulaması açıyoruz ve `java -jar spring-boot-migrator.java `komutuyla aracı çalıştırıyoruz.  Bu ve benzer araçlar için çoğunlukla en temel ve en yararlı komut `help` komutu oluyor. `help` komutuyla araçla ilgili temel yardım bilgisine ulaşabiliyoruz. Dönüştürme işlemi yapmadan önce aracın ön tanımlı tariflerini incelemekte fayda var. Bu tarifleri listelemek için `list`  veya kısaca `l` komutunu girebiliriz. Tarifler arasında işimize yarayacağını düşündüğümüz bir tarif varsa eğer araca `scan` komutu ile beraber kodlarımıza ait yolu verirsek araç kodlarımızı analiz etmeye başlıyor. Analiz işlemi süresi bizim kodumuzun satır sayısı ve kodumuzu bulunduran dosya sayısına bağlı olarak değişebiliyor. Analiz işlemi tamamladıktan sonra araç bize analiz ettiği kodlarımız için uygulayabileceği tarifler listesini gösteriyor. Aracın uygun gördüğü tarifelerden birini uygulamak için `apply` komutu ile beraber tarifin ismini yazmamız yeterli. Araç ilgili tarifi kodlarımıza uyguluyor ve güncellenen kodlar otomatik olarak yerel git depomuza `commit` ediliyor.  
Dikkat etmemiz gereken bir nokta olarak araç kodlarımız üzerinde analiz yaparken kodlar farklı bir kişi veya araç tarafından değiştirilse kodlarımızı tekrar analiz etmektir. Aksi takdirde araç yapılan değişiklikleri dönüştürme işlemine dahil etmeyecektir. Birden fazla tarifi kodlarımız üzerinde tek bir seferde uygulamak istediğimizde `recipe.txt` isimli bir dosyayı araçla aynı dizinde oluşturup, içerisine aşağıdakine benzer komutlar yazmalıyız.
```
scan <application-to-scan>
apply recipe1
apply recipe2
exit 
```
Ardından aracı `java -jar spring-boot-migrator.java @recipes.txt` komutuyla terminal üzerinden çalıştırmalıyız. Yukarıdaki örnek kod bloğuna göre `<application-to-scan>` yolundaki kodlar araç tarafından incelenecek ve sırasıyla `recipe1` ve `recipe2 `adlı tarifler ile kodlar dönüştürülecektir. 
## Conclusion / Call to action
