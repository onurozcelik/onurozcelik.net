---
layout: single
title: "ArchUnit (Java) kütüphanesi ile birim testlerin yazılım mimarisine uygulanması"
date: 2022-11-14
categories: yazılım mimari birim test
---

Yazılım geliştirme sektörüne emek veren çoğu profesyonel yazılım birim testlerinin önemi bilir. Yazılım birim testleri en basit anlamıyla kodumuz içinde en küçük birime uygulanır. Bu birim genellikle kodumuzdaki metotlardır. Peki, yazılım birim testlerini tasarlamış olduğunuz yazılım mimarisi üzerinde koşturmaya ne dersiniz?

Büyük ölçekli yazılım projelerinde başlangıçta gereksinimlere uygun yazılım mimarisi belirlenirken şirkette eğer varsa yazılım mimarı yoksa kıdemli yazılım mühendisleri/uzmanları yazılım bileşenlerini, bu bileşenler arasındaki erişim kurallarını göze hoş görünen diyagramlar çizerek, ortaya koyarlar. Proje süresince zaman ve maliyet kısıtları ile beraber yeni gereksinimler ortaya çıktıkça ve özellikle bileşenler arasındaki erişim kurallarını bilen ve uygulayan tecrübeli çalışanlar ayrılıp, yerine daha az tecrübeli çalışanlar katıldıkça bileşenler arasındaki erişim kuralları göz ardı edilir ve bileşenler arasındaki erişim tam bir karmaşaya dönüşür. Böyle durumlarda tecrübeli bir çalışanın devamlı yazılan kodları gözden geçirmesi ve bileşenler arası yapılan erişim hatalarını tespit etmesi yararlı olabilirdi ama genellikle hiç bir projede bu kaynak bulun(a)maz. Bundan çok daha etkili bir yöntem olarak bileşenler ilk başta belirlendikten sonra bu bileşeneler arasındaki erişim kuralları birim testler olarak yazılsa ve bu testler sürekli olarak koşturulabilse iyi olmaz mıydı? İşte karşınızda ArchUnit (Java) kütüphanesi.

ArchUnit, yazılım mimarisi için birim testler yazmaya olanak sağlayan açık kaynak bir Java test kütüphanesi. _Java_ programlama diliyle _Java_ geliştiricileri için yazılmış. Ama _C#_ geliştiricileri içinde bir dalı bulunuyor. Bu blog kapsamında kütüphanenin _Java_ için kullanımını anlatmaya çalışacağım. Kütüphaneyi kullanabilmek için öncelikle kütüphaneyi projemize eklememiz gerekmektedir. _Maven_ ve _Gradle_ için gerekli bağımlıklar aşağıda verilmektedir.

**Maven**
```
<dependency>
    <groupId>com.tngtech.archunit</groupId>
    <artifactId>archunit</artifactId>
    <version>1.0.0</version>
    <scope>test</scope>
</dependency>
```

**Gradle**
```
dependencies {
    testImplementation ‘com.tngtech.archunit:archunit:1.0.0’
}
```

İlgili bağımlılıklardan birini projemize ekledikten sonra ilk mimari birim testimizi yazabiliriz.  Örneğin aşağıdaki mimari birim teste _controllers_ paketi içerisinde yer alan herhangi bir sınıfın _repositories_ paketi içindeki sınıflara erişmemesini istiyoruz.

```
public class ArchUnitDemoApplicationArchitectureTest {
    @Test
    public void architectureRule1Test() {
        JavaClasses importedClasses = new ClassFileImporter().importPackages("net.onurozcelik.archunitdemo");
        ArchRule rule = noClasses().that().resideInAPackage("..controllers..").should()
                .accessClassesThat()
                .resideInAnyPackage("..repositories..");
        rule.check(importedClasses);
    }
}
```

Paket bağımlılık testleri ile beraber sınıf bağımlılık testleri, paket sınıf içerme testleri, sınıf kalıtım testleri, açımlama (annotation) testleri ve katmanlı mimari (layered architecture) ve altıgen (hexagonal) / soğan (onion) mimari için katman erişim testleri yazabiliyoruz.

Her bir testimizde mimarimize dâhil olan sınıfları tekrar tekrar yüklememek için _JUnit_ birim test kütüphanesinin sunmuş olduğu _@BeforeAll_ açımlamasını kullanabiliriz. Bunun için aşağıdakine benzer bir metot yazmamız yeterli. Kodu incelediğinizde _ClassFileImporter_ sınıfının örneğini oluştururken parametre olarak _ImportOption_ sınıfının örneklerini içeren bir liste vermiş olduğumuzu fark etmişsinizdir. Bunun amacı birim test sınıflarını analize dâhil etmemektir.
```
...
private static JavaClasses importedClasses;

    @BeforeAll
    public static void beforeAll() {
        List<ImportOption> importOptions = new ArrayList<>();
        importOptions.add(ImportOption.Predefined.DO_NOT_INCLUDE_TESTS);
        importedClasses = new ClassFileImporter(importOptions).importPackages("net.onurozcelik.archunitdemo");
    }
...
```

Tüm testlerimizde ihtiyacımıza uygun olarak kurallı ifadeleri (regular expression) kullanabiliyoruz. Aşağıdaki örnekte adında _Repository_ kelimesi geçen sınıfların adında _Service_ kelimesi geçen sınıflara bağımlı olmaması gerektiğini test ediyoruz.

```
@Test
    void architectureRule2Test() {
        ArchRule rule = noClasses().that().haveNameMatching(".*Repository")
                .should().dependOnClassesThat().haveNameMatching(".*Service");
        rule.check(importedClasses);
    }
```
Adında _Service_ kelimesi geçen sınıfların _services_ paketinin içerisine eklendiğini doğrulamak istediğimizde aşağıdakine benzer bir test yazmamız yeterli.
```
 @Test
    void architectureRule3Test() {
        ArchRule rule = classes().that().haveSimpleNameEndingWith("Service")
                .should().resideInAPackage("..services..");
        rule.check(importedClasses);
    }
```
Bu örnekte dikkat edilmesi gereken husus paket isminin başına ve sonuna birbirini takip eden iki adet nokta eklenmiş olması. Kütüphane bu noktaları çözümlediğinde _services_ paketinden önce ve sonra gelen paketleri analize dâhil ediyor. Böylece paketin tam adını yazmaktan kurtuluyoruz.

Mimarimizde belirli bir arayüzü gerçekleştiren bir sınıfın isminin belirli kurallara uygun olarak verilmesi istediğimizde aşağıdaki gibi bir test yazabiliriz. Bu testte _UserService_ arayüzünü uygulayan bir sınıfın adında _UserService_ ve _Impl_ kelimelerinin geçtiğini doğrulamak istiyoruz.
```
  @Test
    void architectureRule4Test() {
        ArchRule rule = classes().that().implement(UserService.class)
                .should().haveSimpleNameContaining("UserService")
                .andShould().haveSimpleNameEndingWith("Impl");
        rule.check(importedClasses);
    }
```

Kütüphane açımlama (annotation) doğrulama testlerinede destek veriyor. Örneğin _UserService_ sınıfına atanabilecek ve adında _Impl_ kelimesi geçen sınıfların _@Service_ açımlamasını içermesini istersek aşağıdaki gibi bir test yazmamız yeterli.
```
 @Test
    void architectureRule5Test() {
        ArchRule rule = classes().that().areAssignableTo(UserService.class)
                .and().haveSimpleNameEndingWith("Impl").should().beAnnotatedWith(Service.class);
        rule.check(importedClasses);
    }
```
Kütüphanede şu an için sektörde çokça tercih edilen katmanlı mimari ve test edilebilirliğin önemsendiği projelerde daha çok tercih edilen altıgen/soğan mimari için tanımlı katmanlar arası erişim testleri desteği de bulunuyor. Katmanlı mimari için test yazmak istersek aşağıdaki gibi önce mimarimizi kütüphaneye tanıtıyoruz sonrasında ise istediğimiz katman erişim kurallarını test ediyoruz.
```
  @Test
    void architectureRule6Test() {
        layeredArchitecture().consideringAllDependencies()
                .layer("Controllers").definedBy("..controllers..")
                .layer("Services").definedBy("..services..")
                .layer("Repositories").definedBy("..repositories..")
                .layer("Entities").definedBy("..entities..")
                .whereLayer("Controllers").mayNotBeAccessedByAnyLayer()
                .whereLayer("Services").mayOnlyBeAccessedByLayers("Controllers")
                .whereLayer("Repositories").mayOnlyBeAccessedByLayers("Services")
                .whereLayer("Entities").mayOnlyBeAccessedByLayers("Repositories");
    }
```
Kütüphane örneklerle anlatmaya çalıştıklarımdan çok daha yetenekli elbette. Bunlardan çok daha fazlasına [ArchUnit](http://www.archunit.org) üzerinden erişebilirsiniz.

ArchUnit, birden fazla kişinin çalıştığı _Java/C#_ programlama dilleri ile geliştirilen projeler için biçilmiş kaftan. Eğer sizde yazılım kodunda kaliteyi önemseyen, temiz kod ilkelerine uygun yazılım geliştirmek isteyen bir profesyonelseniz bu kütüphaneye ve yapabileceklerine muhakkak göz atmalısınız.

Kod örneklerine [onurozcelik/archunitdemo](https://github.com/onurozcelik/archunitdemo) adresinden erişebilirsiniz.