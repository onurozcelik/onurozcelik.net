---
layout: single
title:  "Kotlin: Boolean Veri Tipi"
date:   2017-10-04 23:58
categories: blog eski kotlin
---

Bu yazımızda amacımız Kotlin'de **Boolean** veri tipini tanıtmaya çalışmak. **Boolean** sadece iki değeri temsil edebilen özel bir veri tipidir. Değeri sadece **true** yani 1 veya **false** yani 0 olabilir.

Bilgisayarların <u>ikili sayı sisteminin</u> üzerine inşa edildiği düşünülürse **Boolean** veri tipinin önemi daha net anlaşılacaktır. Bu tip sonraki yazılarımızda tanıtmaya çalışacağımız <u>koşul</u> ifadeleri ile birlikte yaygın olarak kullanılmaktadır. Şu an için vereceğimiz örnek bu tipte değişkenlerin nasıl tanımlanabileceği üzerine olacak.

{% highlight kotlin %}
fun main(args: Array<String>) {
 // Örtülü tanımlama (Implicit declaration)
 var aBool = true
 // Açık tanımlama (Explicit declaration)
 var anotherBool: Boolean = false
 println(aBool)
 println(anotherBool)
}
{% endhighlight %}

Hatırlatmakta fayda var. Verdiğimiz kod örneklerini [Try Kotlin](https://try.kotlinlang.org) adresinde deneyebilirsiniz.

Bir sonraki yazımızda Kotlin'de **Char** veri tipini anlatmaya çalışacağız. Görüşmek üzere.
