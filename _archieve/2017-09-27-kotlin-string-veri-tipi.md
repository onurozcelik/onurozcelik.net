---
layout: single
title:  "Kotlin: String Veri Tipi"
date:   2017-09-27
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin dilinde karakter dizisi (String) veri tipini tanıtmaktır. Peki karakter dizisi ne demektir?

Bu soruya cevap vermeden önce karakter ve dizi kavramlarını anlamaya çalışalım. Türkiye Dil Kurumu'na göre karakter, basımda harf türü olarak tanımlanmaktadır. Harf ise dildeki bir sesi gösteren ve alfabeyi oluşturan işaretlerden her biri, kod olarak tanımlanmaktadır. Dizi ise yan yana, art arda veya zaman sırasına göre sıralanmış birbiriyle ilişkili nesne veya olayların oluşturduğu bütün sıra olarak tanımlanmaktadır.<!--more--> Bu durumda karakter dizisi, yanyana sıralanmış alfabedeki işaretlerin oluşturduğu sıra şeklinde tanımlanabilir. Burada alfabe deyince programlama dilinin desteklediği alfabeden bahsedilmektedir.

Örnek olarak **onur** ve **pass!39** karakter dizilerini ele alalım. Her iki örnekte Kotlin ve bir çok farklı programlama dili için geçerli karakter dizileridir.

Kotlin dilinde karakter dizileri iki adet çift tırnak (" ") işareti arasında tanımlanır. Aşağıdaki kod parçasında bazı örnekler verilmiştir.
{% highlight kotlin %}
package basics

fun main(args: Array<String>) {
  var ip = "127.0.0.1"
  var port = "3306"
  var db = "test"
  var password = "pass!39"
  var sql: String = ""
  var myString: String?
}	
{% endhighlight %}
Bir önceki yazımda da bahsettiğim gibi Kotlin dili değişken tanımlarken kodu yazan kişiden açıkça veri tipi bilgisi istemez. Bununla beraber kişi isterse değişkenin karakter dizisi (String) tipinde olduğunu **sql** ve **myString** değişkenlerinde olduğu gibi belirtebilir. Son iki değişkenin ilkinde boş bir karakter dizisi tanımlanırken, ikincisinde ise **myString** değişkenine **geçersiz (null)** değeri atanmıştır. Geçersiz (null) değerlere daha sonraki yazılarımızda ayrıca değineceğiz.

Karakter dizileri, yazılım geliştirirken bir çok amaç için kullanılabilir. Dilin temellerini anlatmayı tamamladığımızda somut örnekler vermeye çalışarak; konunun daha iyi anlaşılması için çalışacağım. Şu an için bir önceki yazıda verdiğim örneğin aynısını Kotlin, Java vb. dillerde **karakter dizisi ekleme yapma (String interpolation)** olarak isimlendirilen işlevsellik ile verelim.
{% highlight kotlin %}
package basics

fun main(args: Array<String>) {
  var name = "Onur"
  var surname = "Ozcelik"
  println("Benim adim: $name $surname")
}
{% endhighlight %}
Kotlin karakter dizisi veri tipinin kullanımını kolaylaştırmak için standart kütüphanesinde birçok yardımcı işlev (fonksiyon) ile gelmektedir. Bu işlevlerden yaygın olarak kullanılanlardan bazıları aşağıdaki örnekte verilmektedir.
{% highlight kotlin %}
package basics

fun main(args: Array<String>) {
  var name = "onur"
  var surname = "OZCELIK"
  var fullName = name + " " + surname
    
  println(name.toUpperCase())
  println(surname.toLowerCase())
  println(fullName.length)
}
{% endhighlight %}

Yazılarda geçen kod örneklerini her zaman [Try Kotlin](https://try.kotlinlang.org) adresinde deneyebilirsiniz.

Bir sonraki yazımda Kotlin dilindeki sayısal veri tiplerinden biri olan **tam sayı (Int)** veri tipini anlatmaya çalışacağım. Görüşmek üzere.
