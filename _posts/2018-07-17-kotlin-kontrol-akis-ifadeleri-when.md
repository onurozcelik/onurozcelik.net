---
layout: single
title: "Kotlin: Kontrol Akış İfadeleri - when"
date: 2018-07-17
categories: blog eski kotlin
---

Bu yazıda amacımız Kotlin programlama dilinde kontrol akış ifadelerinden `when`
ifadesini anlatmaktır.  Uzun bir süre önce yazdığım yazıda Kotlin dilinde program akışı esnasında birden fazla seçeneğimiz olduğu durumda `if - else if - else` ifadelerini kullanabileceğimizden bahsetmiştik. Bu ifadelerin yanı sıra kodun okunmasını kolaylaştırmak için bir seçeneğimiz daha bulunmakta. Bu seçenek ise `when` ifadesidir.

`when` ifadesi C programlama dili benzeri C++, Java gibi programlama dillerindeki `switch` ifadesinin yerine kullanılmaktadır. <!--more-->   `switch` ifadesi ile Java dilinde çoklu seçim yapmamız gerektiğinde aşağıdakine benzer bir kod yazarız.

{% highlight java %}
import java.util.Scanner;
System.out.println("1-3 arasi bir sayi giriniz: ")
Scanner scanner = new Scanner(System.in);
int choice = scanner.nextInt();
switch(choice) {
    case 1:
        System.out.println("1 numarali secenegi sectiniz");
    break;
    case 2:
        System.out.println("2 numarali secenegi sectiniz");
    break;
    case 3:
        System.out.println("3 numarali secenegi sectiniz");
    break;
    // ...
    default:
        System.out.println("Hatali bir secim yaptiniz")
    break;
    }
{% endhighlight %}

Aynı örneği Kotlin'de yazacak olursak aşağıdaki gibi yazılacaktır.
{% highlight kotlin %}
print("1-3 arasi bir sayi giriniz: ")
val choice = readLine()!!.toInt()
when(choice) {
    1 -> println("1 numarali secenegi sectiniz")
    2 -> println("2 numarali secenegi sectiniz")
    3 -> println("3 numarali secenegi sectiniz")
    else -> println("Hatali bir secim yaptiniz")
}
{% endhighlight %}
Yazdığımız kod Java dilindeki benzerine göre oldukça kısa olmaktadır. Kotlin dilinin geliştirilme hedefleri arasında kod yazan kişinin daha az ve etkin kod yazması bulunmaktadır. Bu amacın `when` ifadesi için sağlandığını söyleyebiliriz. İki örneği karşılaştırırsak Java diliyle yazılan örnekteki `case` ifadelerinin yerine Kotlin'de `->` işaretinin kullanıldığını `default` deyiminin ise `else`  deyimi ile yer değiştirdiğini görebiliriz. Yukarıda vermiş olduğumuz örnek kod ifadenin kullanımının anlaşılması için yetersiz kalabilir. Bu örneğin yanında ifadenin daha iyi anlaşılması için taze sıkılmış meyve sebze suyu örneğini verebiliriz.

Günümüzde bir çok şehirde taze sıkılmış meyve sebze suyu satan büfeler bulunmaktadır. İşletmeyi yapan kişilerin hakkını teslim etmeliyim bizlere oldukça fazla seçenek sunmaktalar. Seçenekler arasında sade portakal, nar, havuç, elma suları bulunduğu gibi bu meyve ve sebze sularının karışımından meydana gelen atom, bomba vb. isimlerde karışımlar yapmaktalar. Böyle bir büfeye gittinizde satıcı ile aranızda geçecek olan konuşmayı Kotlin'de yazarsak aşağıdakine benzer olacaktır.
{% highlight kotlin %}
package kotlinblog 
    
fun main(args: Array<String>) {
	 println("Hosgeldiniz. Taze hazirlanmis portakal, elma, nar, havuc vb.")
	 println("sularimiz var. Bunun yaninda atom [portakal, elma, havuc karisimi] ")
	 println("ve bomba [portakal nar karisimi] vb. meyve - sebze sularimiz var")
	 print("Hangi meyve - sebze suyunu istersiniz: ")
	 val juice = readLine()
	 print("\n")
	 println("1 - kucuk, 2 - orta, 3 - buyuk boy bardaklarimiz var")
	 print("Hangi boy bardakta icersiniz: ")
	 val size = readLine()!!.toInt()
	 when(juice) {
		"portakal" -> when(size) {
			    1 -> println("Bir tane kucuk boy portakal suyu cek")
			    2 -> println("Bir tane orta boy portakal suyu cek")
			    3 -> println("Bir tane buyuk boy portakal suyu cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		  "elma" -> when(size) {
			    1 -> println("Bir tane kucuk boy elma suyu cek")
			    2 -> println("Bir tane orta boy elma suyu cek")
			    3 -> println("Bir tane buyuk boy elma suyu cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		   "nar" -> when(size) {
			    1 -> println("Bir tane kucuk boy nar suyu cek")
			    2 -> println("Bir tane orta boy nar suyu cek")
			    3 -> println("Bir tane buyuk boy nar suyu cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		   "havuc" -> when(size) {
			    1 -> println("Bir tane kucuk boy havuc suyu cek")
			    2 -> println("Bir tane orta boy havuc suyu cek")
			    3 -> println("Bir tane buyuk boy havuc suyu cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		    "atom" -> when(size) {
			    1 -> println("Bir tane kucuk boy atom cek")
			    2 -> println("Bir tane orta boy atom cek")
			    3 -> println("Bir tane buyuk boy atom cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		    "bomba" -> when(size) {
			    1 -> println("Bir tane kucuk boy bomba cek")
			    2 -> println("Bir tane orta boy bomba cek")
			    3 -> println("Bir tane buyuk boy bomba cek")
			    else -> println("Bu boyda bardagimiz bulunmuyor")
		    }
		    else -> "Istemis oldugunuz meyve-sebze suyu bulunmamaktadir"
	    }
    }
{% endhighlight %}
Bir sonraki yazıda görüşmek üzere. Sağlıcakla kalın.


> Written with [StackEdit](https://stackedit.io/).
