---
layout: post
title: Java ArrayList Yapısı 
categories: [java]
tags : [java,content-in-turkish]
comments : true
---

*Please Note: This content is in Turkish Language and is written for a specific purpose, 1-1 tutorial kinda thing. If you desire, you may look at my other post, they are mostly in English*

### Dinamik Bir Dizi Yapısı: ArrayList

Uzun bir aradan sonra, tekrar merhaba. Daha önceki çalışmalarımızda genelde `Array` yapısı olan, uzunluğu (eleman sayısı) belirtilmek zorunda olan tipi kullanmıştık. Fakat bazende elimizdeki nesnelerin sayıları değişebilir, dolayısıyla varolan diziye yeni elemanlar eklemek isteriz veya silmek isteriz.

 Şöyle bir örneği ele alacak olursak; diyelim ki başlangıçta 3 `String` elemanlı bir dizimiz var, bir yerlerde buna 3 eleman ekleyeceğiz. Bunu normal dizilerle şöyle yaparsın;

 ```java
 	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		String[] array = new String[3];

        array[0] = "A";
		array[1] = "B";
		array[2] = "C";
		
		// Yeni elemanlar eklemek için geçici bir dizi tutmak zorundayım
		String[] temp = array;
		// Yeni eleman sayısını (Yani 6 oluyor) burada belirtiyorum.
		// Dikkat et burada "new" ifadesini kullandık ve artık önceki elemanları yok oldu!
		array = new String[temp.length + 3];
		// Yeni uzunluğu belirttikten sonra ilk işim önceki elemanları geçici olan diziden almak
		for(int i = 0; i < temp.length; i++) {
			array[i] = temp[i];
		}
		
		// Artık burada yeni elemanları ekleyebilirim, nihayet!
		array[3] = "D";
		array[4] = "E";
		array[5] = "F";
		
		// Aşağıdaki kodu da çalıştırırsan eğer  java.lang.ArrayIndexOutOfBoundsException hatası alacaksın
		// Yani olmayan bir indexe çalıştın hatası, dizinin sınırlarını aştın demek oluyor
		// array[6] = "G";
		
		// Bir de ekrana yazdıralım
		for (int i = 0; i < array.length; i++) {
			ekranaYazdir(array[i]);
		}
	}
	
	public static void ekranaYazdir(Object obj) {

		System.out.println(obj);
	}
 ``` 

 Görüldüğü üzere, bir zaman kaybı söz konusu, her defasında böyle uğraşmak saçma. İstediğimde `ekle()` diye bir metod olmalı, kolayca eklemeliyim. Veya `sonElemanıSil()` gibi bir metod olmalı, ve bu ekleme silme işlemlerini tek satır kod ile halledebilmeliyim. 

 İşte bu sorunu çözen yapı `ArrayList` yapısı. Elbette diğer Liste yapıları da var `LinkedList` gibi, ilerlerleyen yazılarda onları da kullanabiliriz.

 Şimdi yukarıdaki örneğin aynısını `ArrayList` ile yapalım;

```java
                // String tipinde bir ArrayList oluşturuyoruz, yazım şekli bu şekilde. Küçüktür Büyüktür ifadesi < > içerisinde ArrayList'in tipi yer alıyor
		// Dikkat edersen herhangi bir uzunluk belirtmedik, çünkü normal diziler gibi sabit bir uzunluğa sahip değil, sürekli değişebilir
		ArrayList<String> list = new ArrayList<String>();
		list.add("A");
		list.add("B");
		list.add("C");
		
		// 3 Eleman daha ekliyorum
		list.add("D");
		list.add("E");
		list.add("F");
		
		// İlk elemanını silelim
		list.remove(0);
		
		// Yazdıralım
		for(int i = 0; i < list.size(); i++) {
			ekranaYazdir(list.get(i));
		}
```

En altta yazdırma kodunda,  `for` döngüsünün içine dikkat edersen, liste elemenlarına `ArrayList` yapılarının kendinde bulunan `.get(index)` adlı metod ile ulaşıyoruz. _index_ adlı parametresi de adı üstünde, kaçıncı eleman olduğudur.

Önceki yazımda sorduğum sorunun aynısını `ArrayList` ile yapabilir misin? Yani;

> Verilen ArrayList içerisindeki en büyük `int` elemanı bulan metodu tanımlar mısın? Aşağıda kodun iskelet halini bulabilirsin.

```java
                ArrayList<Integer> numbers = new ArrayList<Integer>();
		Random rnd = new Random();
		for(int i = 0; i < 10; i++) {
			// Random 10 sayı ekleyelim
			numbers.add((int)(Math.random() * 50 + 1));
			
		}

                public int minMax(ArrayList<Integer> list, Boolean returnMin) {
		// Eğer 'returnMin' adlı değişken 'true' ise en küçüğünü
		    if(returnMin == true) {
			return -1;
		    }  
		    // 'false' ise en büyüğünü döndür
	            return 0;
	}
```