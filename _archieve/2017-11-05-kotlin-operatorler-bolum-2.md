---
layout: single
title: "Kotlin: Operatörler Bölüm 2"
date: 2017-11-05
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de koşullu operatörleri (conditional operators) tanımaktır. Yazılım geliştirirken çoğu zaman bir değişkenin temsil ettiği değeri, başka bir değişkenin temsil ettiği değerle, sabit bir sayı ile veya doğru (true) / false (yanlış) değeri ile karşılaştırma gereği duyarız. Programlama dilleri arasında söz dizimsel açısından ufak farklar bulunsa da bu tip karşılaştırma işlemleri koşullu operatörler yardımıyla yapılmaktadır. <!--more--> 

Java, C++ ve C gibi yaygın kullanılan dillerde tanımlı olan koşullu operatölerin benzerleri Kotlin'de de tanımlıdır. Aslında Kotlin, Java sanal makinesi üzerinde çalıştığı için temel işlemlerde Java'dan çok farklı değildir. Kotlin'de tanımlı olan koşullu operatörler aşağıdaki tabloda verilmiştir.

| Operatör | Açıklama      |
| -------- | ------------- |
| `<`      | Küçüktür      |
| `>`      | Büyüktür      |
| `==`     | Eşittir       |
| `!=`     | Eşit Değildir |
| `<=`     | Küçük Eşittir |
| `>=`     | Büyük Eşittir |

Tablodaki operatörleri bir yerlerden tanıyor gibi olduğunuzu tahmin ediyorum. Evet doğru cevap matematik. Matematiğin temelleri programlama dillerinin de temelini oluşturur. Koşullu operatörler ile yapılan işlemler temelinde matematiksel işlemlerdir. Bunu en iyi örnek vererek anlatabiliriz. Buyurunuz kod örneğiniz!

{% highlight kotlin %}
fun main(args: Array<String>) {
  	// Grup 1
    val myInt = 9
    val myOtherInt = 6
    println(myInt < myOtherInt)
    println(myInt > myOtherInt)
	// Grup 2
    val myDouble = 2.0
    val myOtherDouble = 3.0
    println(myDouble == myOtherDouble)
    println(myDouble != myOtherDouble)
	// Grup 3
    val myFloat = 3.14f
    val myOtherFloat = 3.78f
    println(myFloat <= myOtherFloat)
    println(myFloat >= myOtherFloat)
	// Grup 4
    val myChar = 'a'
    val myOtherChar = 'z'
    println(myChar < myOtherChar)
    println(myChar > myOtherChar)
	// Grup 5
    val myBool = false
    val myOtherBool = true
    println(myBool <= myOtherBool)
    println(myBool >= myOtherBool)
	//Grup 6
    val myString = "limon"
    val myOtherString = "limonata"

    println(myString < myOtherString)
    println(myString > myOtherString)
}
{% endhighlight %}

Verilen kod örneği çalıştırıldığında terminale her bir karşılaştırma ifadesi için doğru (true) veya yanlış (false) değerinin yazıldığını görürüz. Bunun nedeni bu operatörlerin karşılaştırma yaptıktan sonra geri dönüş değerinin true ya da false olmasıdır. Örneği satır satır incelediğimizde  ilk üç gruptaki karşılaştırmaların sonuçlarının anlamak zor olmasa gerek. İşlerin ilginç hale gelmeye başladığı gruplar 4, 5 ve 6.

Grup 4'te veri tipi **Char** olan iki adet değişken tanımlanmakta ve değerleri sırasıyla a ve z olarak atanmakta.  Peki bu iki değişkenin değeri nasıl karşılaştırılır. Bunun cevabını bilmek için **Char** veri tipinin bellekte nasıl temsil edildiğini bilmek gerekir. **Char** veri tipi ile bir değişken tanımlandığında bellekte saklanan değer karakter değil karaktere karşılık gelen sayı değeri olmaktadır. Bu değer ise 1960'ta bilgi alışverişi için bir standart getirmek amacıyla tanımlanan [ASCII](https://www.smashingmagazine.com/2012/06/all-about-unicode-utf8-character-sets/) tablosundan gelmektedir. Örneğin temsil ettiği değer A olan bir değişken tanımlandığında bellekte değişkenin temsil ettiği değer ASCII tablosundaki 65 sayısı olmaktadır.

Grup 5'te veri tipi **Boolean** olan iki adet değişken tanımlanmakta ve değerleri sırasıyla false ve true olarak atanmaktadır. Karşılaştırma yapıldığında [Boolean veri tipi](http://www.onurozcelik.net/kotlin/2017/10/04/kotlin-temelleri-boolean-veri-tipi) yazımızdan da hatırlayacağınız üzere değeri false olan değişken bellekte 0 ile temsil edilirken, değeri true olan değişken 1 ile temsil edilmekte ve karşılaştırma bu değerler üzerinden yapılmaktadır.

Grup 6'da veri tipi **String** olan iki adet değişken tanımlanmakta ve değeri sırasıyla **limon** ve **limonata** olarak atanmaktadır. Karşılaştırma yapılırken derleyici String veri tipini karakter dizisine çevirmekte ve karakter dizisinde bulunan her bir karakterin sayısal değerini diğer karakter dizisindeki karşılık düşen karakterin sayısal değeri ile karşılaştırmaktadır. Bu karşılaştırma karşılaştırılan karakterlerin sayısal değerleri farklı olana veya karakter dizilerinden herhangi birisinin içerdiği karakterler bitene kadar devam etmektedir. **Limon** ve **Limonata** değerleri karşılaştırıldığında ilk 5 karakter için karşılaştırma sonucu eşit olmaktadır. Sonrasında Limonata karakter dizisinde daha fazla karakter olduğu için temsil ettiği değer Limon karakter dizisinden daha büyük olmaktadır.  Artık günümüzde kullanımı çok yaygın olmasa da basılı sözlükler de kelimeleri sıralarken benzer bir yaklaşım kullanmaktadırlar.

Bir sonraki yazıda Kotlin'de if - else ifadelerini tanıyacak ve koşullu operatörlerin bu ifadelerle kullanımını anlamaya çalışacağız. Görüşmek üzere.

