---
layout: single
title:  "Kotlin: Operatörler Bölüm 1"
date:   2017-11-01
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de bulunan çeşitli **operatörleri (operator)** tanımaktır.  Burada operatörden kastığımız değişkenlerin temsil ettiği değerler üzerinde işlem yapmayı sağlayan araçlardır. Bilgisayar bilimleri ve dolayısıyla yazılım geliştirme matematik ile oldukça iç içedir. Bu sebeple ilk tanıyacağımız operatörler sayısal işlemler yapanlar olacaktır.<!--more-->

Aşağıdaki tabloda sayısal işlem yapan operatörler ve açıklamaları verilmiştir.

| Operatör | Açıklama      |
|:-------- |:--------------|
| `+`      | Toplama       |
| `-`      | Çıkarma       |
| `*`      | Çarpma        |
| `/`      | Bölme         |
| `%`      | Kalan         |
| `++`     | Birer Arttırma|
| `--`     | Birer Eksiltme|

Toplama, çıkarma, çarpma ve bölme operatörlerinin işlevleri ortaokul yıllarından bildiğimiz matematikteki dört işlem ile aynıdır. Aşağıda kullanımlarına ilişkin kod örneği verilmiştir.

{% highlight kotlin %}
fun main(args: Array<String>) {
    val a = 3
    val b = 5
    println("a + b = " + (a + b))
    println("a - b = " + (a - b))
    println("a * b = " + (a * b))
    println("a / b = " + (a / b))
}
{% endhighlight %}
Yukarıdaki kodu çalıştırdığımızda  bölme işleminin sonucunun 0 olduğunu görmekteyiz. Bunun nedeni değişkenlere ilk değerleri atanırken örtülü bildirimle veri tiplerinin **Int (Tamsayı)**  olarak belirlenmiş olmasıdır.  Programlama dillerinde tamsayılar ile bölme işlemi yapıldığında eğer bölünen sayı, bölen sayıdan küçükse sonuç 0 olacaktır. Sonucun 0 yerine ondalık sayı olmasını istiyorsak bölünen sayı veya bölen sayı için **Double** veya **Float** veri tipini kullanmalıyız.  Bununla ilgili kod örneği aşağıda verilmektedir.

{% highlight kotlin %}
fun main(args: Array<String>) {
  // x, y Int veri tipini alacaklardir
  var x = 3
  var y = 5
  // z Double veri tipini alacaktir
  var z = 2.0
  println("x / y = " + (x.toDouble() / y))
  println("x / y = " + (x / y.toDouble()))
  println("x / z = " + (x / z))
}
{% endhighlight %}

Yukarıda anlatılan operatörler dışında sayısal veri tipleri üzerinde işlem yapan diğer operatörler kalan, birer artırma ve birer eksiltme operatörleridir. Kalan operatörü bölünen sayının bölen sayıya tam olarak bölünmediği zaman kalan sayının bulunması için kullanılır. Yaygın olarak bir sayının çift veya tek olduğunu bulmak amacıyla kullanılır. Kalan operatörü ile ilgili örnek kod aşağıda verilmiştir.

{% highlight kotlin %}
fun main(args: Array<String>) {
    var x = 11
    var y = 3
  	// Bu islemin sonucu 11 sayisi, 3 sayisina tam bolunemedigi icin 2 olacaktir
  	println("$x % $y = " + (x % y))
}
{% endhighlight %}

Birer arttırma ve birer eksiltme operatörleri adından anlaşılacağı üzere değişkenin temsil ettiği sayının değerini 1 artırır veya azaltır. Bu operatörler yaygın olarak ileride anlatacağımız döngü ifadelerinde kullanılmaktadır. Uygulandıkları değişkenin başına veya sonuna gelmesine göre çalışma zamanında farklı sonuçlar üretmektedirler. Eğer bu operatörler değişkenin başına gelirse önce değişkenin temsil ettiği sayının değeri bir artırılır veya azaltılır, ardından değişken yeni aldığı değerle işlenir. Aksine sonuna gelirse değişken mevcut temsil ettiği değeri ile işlenir ve ardından değeri bir artırılır veya azaltılır. Bu operatörler ile ilgili kod örneği aşağıda verilmektedir.

{% highlight kotlin %}
fun main(args: Array<String>) {
    var x = 5
  	// Terminale 5 yazdirilir, ardindan x degiskeninin temsil ettigi deger 6 olarak guncellenir
    println(x++)
  	/* Once x degiskeninin temsil ettigi deger 7 olarak guncellenir, ardindan terminale yazdirilir*/
  	println(++x)
  	// Terminale 7 yazdirilir, ardindan degisken degeri 6 olarak guncellenir
  	println(x--)
  	/* Once x degiskeninin temsil ettigi deger 5 olarak guncellenir, ardindan terminale yazdirilir */
  	println(--x)
}
{% endhighlight %}

Bir sonraki yazımızda farklı operatörleri tanımaya devam edeceğiz. Görüşmek üzere.