---
layout: single
title:  "Kotlin: Kullanıcıdan Veri Okumak"
date:   2017-10-25
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de kullanıcıdan nasıl veri okunabileceğini anlamaktır. Daha önceki yazılarımızdan bildiğiniz üzere istediğimiz bir mesajı ekrana yazdırmak için **println** işlevini kullanıyorduk. Bu işlevi kullanarak yazılan kod ile kullanıcı arasında tek yönlü bir iletişim yolu oluşturmuş oluyoruz. Bazı durumlarda bu iletişim yolunun çift yönlü olmasınıda isteyebiliriz. <!--more-->

Bu tip durumlarda kullanmamız gereken işlev **readLine** olmaktadır. Bu işlevi kullanılırken dikkat edilmesi gereken nokta, kullanıcı veri girişi yapana kadar işlevin programın akışını durdurmasıdır. Konuyu bir örnekle açıklamaya çalışalım.

{% highlight kotlin %}
fun main(args: Array<String>) {
    println("Adiniz nedir?")
  	var name = readLine()
  	println("Adiniz: $name")
  	println("Kac yasindasiniz?")
  	var age = readLine()
  	println("Yasiniz: $age")
}
{% endhighlight %}

Örnekte kullanıcıya önce adı ve ardından yaşı sorulmaktadır. Kullanıcı terminal penceresinden ilgili verileri girmedikçe programın akışı duracaktır. Örneğimizde kullanıcı verisini **String** olarak okuduk. Bu **readLine** işlevi için varsayılan veri tipidir. Kodu yazan kişi bazı durumlarda kullanıcıdan okuduğu veriyi farklı bir veri tipine çevirerek kullanmak isteyebilir. Bu durumda aşağıdakine benzer bir kod yazmamız gerekir.

{% highlight kotlin %}
fun main(args: Array<String>) {
  	var petrolLiterPrice = 5.29
    println("Su an itibariyle benzinin litre fiyati $petrolLiterPrice'dur")
  	println("Bu aksam 00:00 itibariyle gelecek zam miktarini giriniz:")
  	var raise: Double = readLine()!!.toDouble()
  	petrolLiterPrice = petrolLiterPrice + raise
  	println("Yarin 00:01 itibariyle benzinin litre fiyati $petrolLiterPrice olacaktir")
}
{% endhighlight %}

Örnekte zam miktarını okuduktan sonra **Double** veri tipine çevirmek için **toDouble** işlevini kullandık. Burada dikkatinizi çekebilecek bir nokta **readLine** işlevinin ardına eklenen iki adet **!!** işareti olmaktadır. Bu işaretleri koymamız zorunludur ve koyulmazsa kod derlenmeyecektir. İşaretlerin kullanılmasının amacı Kotlin derleyicisine terminalden okunacak verinin **boş değer (null)** olmayacağını garanti ettiğimizi belirtmektir. Peki kullanıcı bu garantiyi vermesine rağmen eğer boş bir değer girilirse ne olur? 

Bu durumda ileride anlatacağımız üzere bir **istisnai durum (exception)** oluşmakta ve program anında sonlanmaktadır. Bir sonraki yazımızda görüşmek üzere.