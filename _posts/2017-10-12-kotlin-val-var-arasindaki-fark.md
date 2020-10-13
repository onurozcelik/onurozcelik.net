---
layout: single
title:  "Kotlin: var ve val Arasındaki Fark"
date:   2017-10-12
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin'de **var** ve **val** anahtar sözcükleri arasındaki farkı anlamaktır. Kotlin'de herhangi bir veriyi tutmak için değişken tanımlamak istediğimizde kullanılan anahtar sözcüğün **var** olduğunu önceki yazılarımızda belirtmiştik.  Bununla beraber bir anahtar sözcük daha kullanılabilir. Bu anahtar sözcük **val**'dir.<!--more-->  Peki ikisi arasındaki fark nedir? Bunu en güzel şekilde kod örneği ile anlatabiliriz diye düşünüyorum.
{% highlight kotlin %}
fun main(args: Array<String>) {
	// Degiskene Onur degeri atanir
	var myName = "Onur"
	// Degisken degeri Ahmet olarak degistirilir
	myName = "Ahmet"
	// Degisken degeri Mehmet olarak degistirilir
	myName = "Mehmet"
	// Ekrana son deger olan Mehmet yazilir
	println(myName)
}
{% endhighlight %}
Yukarıdaki örnektede görüleceği üzere **var** anahtar sözcüğü ile tanımlanan değişkenlerin değerleri biz istediğimiz sürece değiştirilebilmektedir. Fakat bazı durumlarda değişkeni bir defa tanımlamak ve temsil ettiği değeri değiştirmemek isteriz. Örneğin bir dairenin matematiksel olarak çevresini ve/veya alanını hesaplamak istediğimiz zaman **PI** sabitine ihtiyaç duyarız. Bu sabitin değerinin yaklaşık olarak 3.14 olduğunu ortaokul yıllarımızdan biliriz. Bu tip sabitleri Kotlin'de tanımlamak için **val** anahtar sözcüğü kullanılır. Kod örneği vererek konunun daha iyi anlaşılmasını sağlamaya çalışalım.
{% highlight kotlin %}
fun main(args: Array<String>) {
	/* Degisken val anahtar sozcugu ile tanimlanmis
	ve deger olarak 3.14 atanmis
	*/
	val PI = 3.14
	// Yaricap degiskeni
	var radius = 3
	// Dairenin cevresinin hesaplanmasi (Ortaokul yillarindan)
	var circumference = 2 * radius * PI
	// Derleme hatasi, val ile tanimlanan degiskenin degeri degistirilemez
	PI = 5.34
	...
}
{% endhighlight %}
Benzer destek **Java** programlama dilinde **final** anahtar sözcüğü ile sağlanırken, **C/C++** programlama dillerinde **const** anahtar sözcüğü ile sağlanır. 

Kotlin kodu yazarken unutmamamız gereken önemli bir nokta **var** anahtar sözcüğü ile tanımlanan değişkenin temsil ettiği değer değiştirilebilirken **val** anahtar sözcüğü ile tanımlanan değişkenin temsil ettiği ilk değer belirlendikten sonra değiştirilememektedir.

Bir sonraki yazımızda görüşmek üzere.