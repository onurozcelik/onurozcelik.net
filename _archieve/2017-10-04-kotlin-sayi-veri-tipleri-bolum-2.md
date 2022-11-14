---
layout: single
title:  "Kotlin: Sayı Veri Tipleri Bölüm 2"
date:   2017-10-04
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de gerçel (reel) sayıları temsil eden veri tiplerini tanımak. Gerçel sayıların modern programlama dillerinde temsil edilmesi kayan noktalı sayılar ile yapılmaktadır. Kotlin'de gerçel bir sayıyı temsil eden bir değişken tanımlamak istediğimizde iki ayrı seçeneğimiz bulunmaktadır. Bu seçenekler **Float** ve **Double** veri tipleridir. Her iki veri tipide kayan noktalı sayıları temsil etmek için geliştirilmişlerdir.<!--more-->  Aralarındaki fark **Double** veri tipinin **Float** veri tipine göre daha geniş aralıkta gerçel sayıları temsil edebilmesidir.  Tabi bu temsil işlemi sırasında **Float** veri tipine göre bellekte daha fazla alanı işgal eder.

Günümüzde bilgisayar bellekleri yazılım geliştiren kişiler için oldukça bonkördür. Bu sebeple Kotlin kodu yazarken bir gerçel sayıyı temsil eden değişken tanımladığımızda eğer açık tanımlama yapmamışsak derleyici varsayılan olarak veri tipini  **Double** olarak seçecektir. Aşağıda bunun örneği verilmiştir.
{% highlight kotlin %}
fun main(args: Array<String>) {
	// Örtülü tanımlama (Implicit declaration)
	var myVar = 0.5
	// Ekrana double yazılır (Prints double)
	println(myVar.javaClass.toString())
}
{% endhighlight %}
Örtülü tanımlama yaparak **Float** veri tipinde bir değişken tanımlamak istediğimizde bunu derleyiciye açıkça ifade etmeliyiz. Bu ifade işlemi aşağıdaki gibi yapılmaktadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
	// Değerin sonuna f veya F karakteri eklenir
	var myVar = 0.5f
	var myOtherVar = 3.5F
	// Ekrana float yazılır (Prints float)
	println(myVar.javaClass.toString())
	println(myOtherVar.javaClass.toString())
}
{% endhighlight %}
Her iki veri tipininde kullanıma ilişkin örnek aşağıdadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
	var aDouble = 21.99
	// Açık tanımlama (Explicit declaration)
	var anotherDouble: Double = 79.90
	var aFloat = 29.9f
	// Açık tanımlama (Explicit declaration)
	var anotherFloat: Float = 99.90
	...
}
{% endhighlight %}
Bir sonraki yazımızda Kotlin'de **Boolean** veri tipini anlatmaya çalışacağız. Görüşmek üzere.
