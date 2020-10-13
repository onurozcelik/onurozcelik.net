---
layout: single
title:  "Kotlin: Int Veri Tipi"
date:   2017-09-27
categories: blog eski kotlin
---

Bu yazının amacı Kotlin dilinde **tamsayı (Int)** veri tipini tanıtmaktır. Int, ingilizce Integer kelimesinin kısaltılmış halidir. Integer türkçe olarak tamsayı anlamına gelmektedir.<!--more--> 

Bu veri tipi Kotlin'de tamsayıları tutacak değişkenleri tanımlamak için kullanılır. Aşağıdaki kod parçasında Int veri tipininin kullanımı gösterilmiştir.
{% highlight kotlin %}
fun main(args: Array<String>) {
	var name = "Onur"
	var age = 32 //Örtük bildirim (Implicit declaration)
	var port: Int = 3306 //Açık bildirim (Explicit declaration)
	println("$name $age yasindadir")
	
  //Derleme hatası oluşur daha önce örtük bildirimle veri tipi tamsayı (Int) olarak belirlenen 
  //değişkene Karakter dizisi (String) tipinde veri atanamaz
	age = "32" 
}
{% endhighlight %}
Bir sonraki yazımızda Kotlin dilindeki farklı sayısal veri tiplerini anlatmaya devam edeceğiz. Görüşmek üzere.
