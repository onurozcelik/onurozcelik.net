---
layout: single
title:  "Kotlin: Sayı Veri Tipleri Bölüm 1"
date:   2017-10-02
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'deki sayı veri tiplerini tanımaya devam etmek. Kotlin'de **Int** dışında **Byte, Short, Long, Float ve Double** olmak üzere sayılara ilişkin 5 farklı sayı veri tipi daha bulunmaktadır.

Bu veri tiplerinin geliştirilmesinin amacı farklı büyüklükteki sayıları bellekte temsil etmektir.<!--more--> İlk olarak **Byte** veri tipini tanıyalım. **Byte** veri tipi diğer sayılara ilişkin veri tiplerine göre temsil edebileceği sayı değerleri en az olandır. -128 ile 127 arasındaki tam sayıları temsil edebilir. Kullanımı için örnek kod parçası aşağıdadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
	var myNumber: Byte = 110
	println(myNumber.javaClass.toString())
	...
}
{% endhighlight %}
Örneğimizde açık tanımlama (explicit declaration) yapmak durumundayız. Eğer veri tipi seçimini Kotlin derleyicisine bırakırsak **myNumber** değişkeninin veri tipi **Int** olarak seçilirdi.

Bir diğer tip olan **Short** veri tipinin temsil edebileceği tamsayı değerleri aralığı **Byte** veri tipine göre oldukça büyük **Int** veri tipine göre ise oldukça küçüktür. Bu veri tipi -32768 ile 32767 arasındaki tam sayıları temsil edebilir. Kullanımı için örnek kod parçası aşağıdadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
	var myNumber: Short = 1000
	println(myNumber.javaClass.toString())
	...
}
{% endhighlight %}
**Int** veri tipini bir önceki yazımızda tanıtmaya çalışmıştık. Fakat temsil edebileceği tamsayılarla ilgili bir aralıktan bahsetmemiştik. Bu açığımızı bu yazıda kapatalım. **Int** veri tipi -2147483648 ile 2147483647 aralığındaki tam sayıları temsil edebilir.

**Int** veri tipinin temsil edebileceği aralığın ihtiyacımızı karşılamaması durumunda **Long** veri tipi yardımımıza yetişmekte. **Long** veri tipi -9223372036854775808 ile 9223372036854775807 arasındaki tam sayıları temsil edebilmektedir. Kullanımı için örnek kod parçası aşağıdadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
	// Long veri tipi icin tanimladigimiz degerlerin sonuna 'L' eklememiz gerekmekte 
	var myNumber: Long = 100L
	var bigNumber = 200L
	...
}
{% endhighlight %}
Bir sonraki yazımızda kayan noktalı sayıları (floating point numbers) temsil etmek için geliştirilmiş **Float** ve **Double** veri tiplerini anlatmaya çalışacağız. Görüşmek üzere.
