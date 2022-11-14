---
layout: single
title:  "Kotlin: Değişkenler"
date:   2017-09-25 23:20:00 +0300
categories: blog eski kotlin
---

Herhangi bir programlama dilinde olduğu gibi Kotlin dilinde de değişkenler önemli bir kavramdır. Değişken deyince aklımıza bellekte belirli bir bilgiyi saklamak için ayrılmış alanlar gelmelidir. 

Kavramı anlamak için mutfaklarda kullanılan kap kacağı düşünün. Çeşitli gıda ürünlerini çeşitli boyutlardaki kaplarda saklarız ve ihtiyacımız olduğunda kullanırız.<!--more--> 

Kotlin dilinde degişken tanımlamak için aşağıdaki kod parçası kullanılır.

{% highlight kotlin %}
package basics

fun main(args: Array<String>) {
	var name = "Onur"
	var lastName = "Ozcelik"
}
{% endhighlight %}

Bu örnekte main kısmını yazmak durumundayız. Çünkü derleyici yazılan bir kodu işlemek için bir giriş noktasına ihtiyaç duyar. Bu giriş noktası Kotlin dili için **main** kısmıdır. Kotlin dilinde değişken tanımlamak için **var** kelimesi ile beraber değişken için seçilen benzersiz bir isim kullanılır. Örnekte isimleri name ve lastName olmak üzere iki adet değişken tanımlanmış ve sırasıyla bu değişkenlere veri olarak karakter dizisi tipinde değerler atanmıştır.

Derleyici değişkene atanan veriye göre çıkarım yaparak değişkenin tutabileceği veri tipini otamatik olarak belirleyebilmektedir. Bu sebeple bu dilde diğer bazı programlama dillerde olduğu gibi ``` int, char, float ``` vb. veri tipi tanımlama kelimeleri bulunmamaktadır. Kodu yazan kişi isterse ``` var name: String = "Onur" ``` veya ```var age: Int = 32 ``` ifadelerinde olduğu gibi veri tipi tanımlama işini derleyiciye bırakmadan kendisi üstlenebilir.

Değişkenler, yazılım geliştirirken bir çok iş kullanılırlar. Yukarıdaki örneği biraz geliştirerek yazarsak kişinin adını soyadı ile beraber ekrana yazdıran kod parçası aşağıdaki gibi olmaktadır.
{% highlight kotlin %}
package basics
 
fun main(args: Array<String>) {
	var name = "Onur"
	var lastName = "Ozcelik"
	println("Benim adım: " + name + " " + lastName)
}
{% endhighlight %}
Bir sonraki yazıda Kotlin programlama dilindeki veri tiplerini anlatmaya çalışacağım. Görüşmek üzere.
