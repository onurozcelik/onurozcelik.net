---
layout: single
title: "Kotlin'de Kontrol Akış Kontrolü"
date: 2018-11-07
categories: blog eski kotlin
comments: true
---
Kotlin programlama dilinde yapısal olarak üç tane kontrol akış kontrol (geri dönüş ve sıçrama) anahtar sözcüğü bulunmaktadır. Bunlar:

- return. Varsayılan olarak kapsamı içinde bulunduğu en yakın işlevden / isimsiz işlevden (anonymous function) geri dönüş sağlar.
- break. Kapsamı içinde bulunduğu en yakın döngüyü sonlandırır.
- continue. Kapsamı içinde bulunduğu en yakın döngünün bir sonraki  adımın çalışmasını sağlar.

Bu kontrol anahtar sözcüklerinin kullanımı Java programlama dili ile benzerdir. Kotlin programlama dilinin Java programlama dilinden bu hususta ayrılmasını sağlayan özelliği return,  break ve continue anahtar sözcüklerinin etiketlerle işaretlenerek kullanılabilmesinin sağlanmasıdır.

Aslında Kotlin programlama dilinde herhangi bir ifade (expression) bir etiket ile işaretlenebilmektedir. Bir ifadenin etiketle işaretlenebilmesi için bir etiket belirleyicisi (identifier) ve bunu takip eden '@' işareti gereklidir. Örneğin abc@ veya fooBar@ geçerli etiket tanımlarıdır. Bir ifadenin etiket ile işaretlenmesi için önüne geçerli bir etiket tanımı eklememiz yeterlidir.

{% highlight kotlin %}
loop@ for(i in 1..100) {
    // ...
}
{% endhighlight %}

Yukarıdaki kod örneğini verdikten sonra kodumuza ekleyeceğimiz break ve continue anahtar sözcüklerini etiket ile beraber kullanabiliriz.

{% highlight kotlin %}
loop@ for(i in 1..100) {
    for (j in 1..100) {
        if (...) break@loop //@ işareti başa gelmiş
    }
}
{% endhighlight %}

Bu örnekte eğer döngüyü sonlandırma koşulu gerçekleşirse içteki döngü yerine loop@ ile işaretlenen döngü sonlanacaktır. Benzer şekilde örnek continue anahtar sözcüğünü içerseydi etiket ile işaretlenen döngünün bir sonraki adımı çalıştırılacaktı.

Etiketlerle işaretlenmiş return anahtar sözcüklerinin en önemli kullanım durumu lambda ifadeleri içinde olmaktadır.  Aşağıdaki kodu yazdığımızda:

{% highlight kotlin %}
/*Koşul gerçekleştiğinde foo işlevini çağıran koda geri dönüş yapılır*/
fun foo() {
    listOf(1,2,3,4,5).forEach {
        if (it == 3) return
        print(it)
    }
    println("kodun bu kısımı erişilmezdir")
}
{% endhighlight %}

Eğer lambda ifadesinden geri dönüş yapmak istersek, ifadeyi etiket ile işaretlememiz yeterli olacaktır.

{% highlight kotlin %}
/*Koşul gerçekleştiğinde lambda ifadesinin çağıran koda geri dönüş yapılır. Bu örnekte forEach işlevi*/
fun foo() {
    listOf(1,2,3,4,5).forEach lit@{
        if (it == 3) return@lit
        print(it)
    }
    println("Bu kısma etiket ile işaretleme sonrası erişilecektir")
}
{% endhighlight %}

Etiket tanımı yapılırken geri dönüş yapılacak işlevin adını vermek kodun okunabilirliğini artıracaktır. Yukarıdaki örneği yeniden yazarsak:

{% highlight kotlin %}
fun foo() {
    listOf(1,2,3,4,5).forEach forEach@{
        if (it == 3) return@forEach
        print(it)
    }
    println("Bu kısma etiket ile işaretleme sonrası erişilecektir")
}
{% endhighlight %}

Yukarıdaki örneği lambda ifadesi yerine isimsiz işlev ile yazacak olursak etiket ile işaretleme yapmamıza gerek kalmayacaktır.

{% highlight kotlin %}
fun foo() {
    listOf(1,2,3,4,5).forEach(fun (value: Int) {
        if (value == 3) return
        print(value)
    })
    println("Bu kısma isimsiz işlev kullanımı sonrası erişilecektir")
}
{% endhighlight %}

return anahtar sözcüğünden bir değer geri döndürmek istediğimizde ayrıştırıcı, etiket işaretinden sonraki değeri geri döndürmektedir.

{% highlight kotlin %}
return @a 1 // Bu örnekte a@ etiketine geri dönüş değeri (@a 1) yerine 1 olmaktadır
{% endhighlight %}

Bir sonraki yazıda görüşmek üzere.