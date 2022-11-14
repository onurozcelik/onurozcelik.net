---
layout: single
title:  "Kotlin: Char Veri Tipi"
date:   2017-10-06 11:00
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de **Char** veri tipini tanımaktır.  Bu veri tipi basitçe tek bir karakteri temsil etmek için geliştirilmiştir. [String](http://bit.ly/2xm1Rc4) veri tipini anlattığımız yazımızda karakterin tanımı vermiştik. Hatırlayacak olursak karakter, basitçe bir alfabedeki tanımlı bir işaret olarak tanımlanmaktadır.<!--more--> 

**String** veri tipinin iki adet çift tırnak (") işareti arasında tanımlandığını söylemiştik. **Char** veri tipi ise iki adet tek tırnak (') işareti arasında tanımlanır. Aşağıda bu veri tipinin kullanımına ilişkin kod örneği bulunmaktadır.
{% highlight kotlin %}
fun main(args: Array<String>) {
    var aChar = 'O'
    var anotherChar: Char = 'N'
    // Derleme hatası olusur. Char veri tipi sadece tek bir karakteri temsil edebilir
    var invalidChar = 'ON'
    // Gecerli bir tanim. Char veri tipi bosluk karakterini temsil edilebilir
    var spaceChar = ' '
    // Gecerli bir tanim. Char veri tipi bos olarak tanimlanabilir
    var emptyChar = ''
    // Gecerli bir tanim. String veri tipi bir tek karakteri de temsil edebilir
    var aString = "U"
    ... 
}
{% endhighlight %}
Bir sonraki yazımızda Kotlin'de **var** ve **val** anahtar sözcüklerinin arasındaki farkı anlatmaya çalışacağız. Görüşmek üzere.
