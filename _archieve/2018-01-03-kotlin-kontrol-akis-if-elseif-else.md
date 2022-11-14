---
layout: single
title: "Kotlin: Kontrol Akış İfadeleri - if, else-if, else"
date: 2018-01-03
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de If - 'Else If' - Else ifadelerini tanımaya çalışmaktır. Hayatımızda seçimlerimiz büyük bir yer tutmaktır. Hayatımız bir nevi seçimlerimize göre şekillenmektedir. Peki seçimlerimizi neye göre yaparız. Çoğunlukla seçim yapmamız gereken durumlardaki koşullarımızı değerlendiririz. Seçim yapma işi hayatımızın her alanında varken bu kavramın programlama dillerine aktarılmamış olması olası değildir. <!--more--> 

Akşam yemeği için dışarı çıktığımızı düşünelim. Bulunduğumuz adrese göre bir çok seçeneğimiz olmaktadır. Bunun yanında canımızın çektiği yiyeceklerde yemek seçimi için etkili olabilmektedir. 
Demek ki seçimlerimiz için birden fazla koşulun aynı anda gerçekleşmesi etkili olabilmektedir. Yeme, içme örneği üzerinden devam edersek eminim ki bir çok kişi içecek içmek için dışarı çıktığında içecek  A veya içecek B’yi tercih edebileceğini söylemiştir. Benzer bir şekilde ben dahil bir çok kişi olumsuz bir olayın gerçeklememesi durumunda yapacağı bir eylemi dile getirmiştir. Bu saydığım örnekler seçimler ve koşullar dünyası için basit bazı örneklerdir.

Yaygın kullanılan programlama dillerinin hepsinde (C++, Java, C# vb.) koşullara göre seçim yapma işi **if**, **else if** ve **else** ifadeleri ile yapılır. Ana koşul **if** ifadesi ile yazılırken alternatif seçenekler seçenek sayısına göre **else** veya **else if** ifadesi ile yazılır.  Sadece bir alternatif olduğu durumda **else** ifadesi yeterli olurken birden fazla alternatif varsa **else if** ifadesi de kullanılır.  Birden fazla koşulun bir seçim için etkili olması durumunda **if** ve **else if** ile bu koşulların geçerliliğini sınayabiliriz. Koşulların geçerliliğini sınamak için Kotlin bize `&& (ve)`, `|| (veya)` ve `! (değil)` operatörlerini sunmaktadır. Yukarıdaki metinde verdiğimiz örnekleri Kotlin’de yazalım.

{% highlight kotlin %}
// If - Else Ornegi
fun main(args: Array<String>) { 
	var location = "Besiktas"
	if (location == "Besiktas")
		println("Balik tercih edebilirsin")
	else
		println("Kebab tercih edebilirsin")
}
{% endhighlight %}

{% highlight kotlin %}
// Kosul 1 ve kosul 2 ornegi
fun main(args: Array<String>) {
    var location = "Besiktas"
    var mood = "WantingToEatSeaFood"
    if (location == "Besiktas" && mood == "WantingToEatSeaFood") {
        println("Balik yemelisin")
    } else if (location == "Fatih" && mood == "WantingToEatKebap") {
        println("Kebap yemelisin")
    } else {
        println("Canin ne cekiyorsa onu ye")
    }
}
{% endhighlight %}

{% highlight kotlin %}
// Kosul 1 yada kosul 2 Ornegi
fun main(args: Array<String>) {
  	var sahlepExists = true
    var greenTeaExists = false
    if (sahlepExists || greenTeaExists) {
        println("Sahlep yada yesil cay istiyorum")
    } else {
        println("Siyah cay istiyorum")
    }
}
{% endhighlight %}

{% highlight kotlin %}
// If - Else If - Else Ornegi
fun main(args: Array<String>) {
    var number1 = 6
    var number2 = 9
  	if (number1 > number2) {
        println("Sayi 1 sayi 2'den buyuktur")
    } else if (number1 < number2) {
        println("Sayi 2 sayi 1'den kucuktur")
    } else {
        println("Sayi 1 ve sayi 2 esittir")
    }
}
{% endhighlight %}

{% highlight kotlin %}
fun main(args: Array<String>) {
  	var examFailureExists = false
    if (!examFailureExists)
        println("Kurban kesecegim")
}
{% endhighlight %}

Bir sonraki yazımızda Kotlin'de when ifadesini tanıtmaya çalışacağız. Görüşmek üzere.






































































































































































































































































































































































































































































































