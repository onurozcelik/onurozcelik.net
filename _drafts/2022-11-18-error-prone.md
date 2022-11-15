## Notes
* Error Prone kodumuzdaki hataları veya iyileştirilmesi gereken noktaları tespit eden Google tarafından geliştirilmiş açık kaynak bir derleme zamanı statik kod analiz kütüphanesi.
* -500'den fazla ön tanımlı hata kontrolü içeriyor (link verilebilir) ve aynı zamanda üçüncü parti ve özel eklentilerede izin veriyor-
* -Kodumuzdaki problemleri bölümleri tespit ettikten sonra uyarı mesajı gösterebilir veya problemli kodu otomatik olarak önceden tanımlı bir çözümle güncelleyebilir-
* -Java 8, 11 ve 17 için desteği bulunuyor hem hata düzeltme hemde büyük ölçekli refactoring için kullanılabilir-
* Maven, Bazel, Ant ve Gradle ile beraber kullanılabiliyor
* Derleyici, Error Prone kütüphanesini açımlama (annotation) işlemcisi olarak yapılandırmalı
* Maven yapılandırma örneği verilecek
* Ardından 2 String değerini karşılaştıran bir kod örneği verilecek
* Çalıştırma maven komutu verilecek
* Analiz dokümü verilecek
* Analiz dokümüne uygun olarak kütüphanenin önerdiği çözüm vurgulanacak
* Kütüphanenin otomatik düzeltme yapma ayarı ve ardından gerçekleşen çözüm verilecek
* Komut satırı seçeneklerinden bahsedilebilir
* Kütüphanenin özel veya 3.parti bir eklentiyle zenginleştirilmesi örneği verilecek
* Yukarıdaki madde için gerekli Maven bağımlılıkları verilecek
* Bir hata ile karşılaşılması durumunda (Java 16 ve sonrası muhtemelen) yapılandırma ayarından ve alternatif yapılandırma ayarından bahsedilecek
* IntelliJ IDEA ve Eclipse eklentileri olduğundan bahsedilecek

- - - -
layout:single
title: “Google Error Prone (Java) Kütüphanesi ile Derleme Zamanında Statik Kod Analizi Nasıl Yapılır?”
date:2022-11-18
categories:error prone statik analiz
- - - -
Yazılım sektöründe çalışan her profesyonel tecrübesi ne kadar fazla olursa olsun kod yazmaya devam ettiği sürece basit hatalar yapabilir. Kullanmış olduğumuz derleyiciler kod yazarken bizlere genellikle yardımcı olur. Ama bu yardım çoğunlukla statik tip kontrolünün ötesine geçmez. Google tarafından geliştirilen Error Prone kütüphanesi derleyicinin sınırlı yardım yeteneğini arttıran ve hatalı yazılan kodu hızlıca tespit etmemizi sağlayan bir araç.  

Error Prone kütüphanesi 500’den fazla ön tanımlı hata deseni içeriyor. Ön tanımlı hata desenleri [Error Prone Bug Patterns](https://errorprone.info/bugpatterns)adresinden incelebilir. Kütüphane ön tanımlı hata desenlerinin yanında 3. parti eklentilerin kullanımına ve özel eklentiler geliştirilmesinede olanak sağlıyor. Çalıştırıldığında kodumuzda tespit ettiği hatalarla ilgili uyarı mesajları gösteriyor veya gerekli yapılandırma sağlanırsa kodumuzu ön tanımlı çözümlerle otomatik olarak düzenleyebiliyor. Java 8, 11 ve 17 sürümlerine desteği bulunan kütüphane Maven, Bazel, Ant ve Gradle yük oluşturma araçları ile … Google tarafından hata düzeltmelerinde ve büyük ölçekli kod yeniden yapılandırma (refactoring) çalışmalarında başarıyla kullanılıyor. Peki biz bu aracı nasıl kullanabiliriz?

Kütüphaneyi kullanmak için
Do not forget transitive sentences

## Conclusion / Call to Action