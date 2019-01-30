---
layout: post
title: Java ArrayList Yapısı Part 2
categories: [java]
tags : [java,content-in-turkish]
comments : true
---

*Please Note: This content is in Turkish Language*

### Tek Satırda Initialize  

> Bir diziyi initialize etmek, yani başlatmak, dizi tanımlanırken elemanlarını da aynı anda belirtmektir. 

Önceki çalışmalarda farkettiysen eğer, `int[]` tipinde bir diziyi initialize etmek için şöyle bir ifade yazabiliriz:

```java
int[] array = { 1, 2, 3 };
```

Böylelikle 3 elemanlı bir diziyi tek satırda tanımlamış olursun.

Aynı işlemi `ArrayList` için tanımlayalım;

```java
ArrayList<Integer> array = new ArrayList<>(Arrays.asList(1, 2, 3));
```

`Arrays.asList()` adlı metod parametre olarak bir dizi alıyor. Bu diziyi listeye çeviriyor, `ArrayList` tipine dönüştürme yapılıyor yani.


### Eleman Güncelleme

Elemanını güncelleme `set()` metodu ile yapıyorsun. 2 parametre alıyor, ilkincisi index, kaçıncı eleman olduğu. İkinci parametre de değer, şöyleki;

`array.set(0, 100);`

İfadesi 0. index'teki elemanın değerini 100 olarak değiştir demek oluyor.

### Toplu Ekleme

Tek bir eleman eklemek için add metodunu kullanırsın;

```java
array.add(121);
```

Diyelim ki 2. bir liste var elinde;

```java
ArrayList<Integer> coll = new ArrayList<Integer>(Arrays.asList(30, 40, 50));
```

Bu listeyi diğeri ile birleştirmek için;

```java
array.addAll(coll);
```

### Silme

Bütün elemanları temizlemek için `clear()` metodunu kullan;

`array.clear();`

Belirtilen indisteki elemanı silmek için;

`array.remove(0);`

kullanabilirsin.

### Diziye Dönüştürme
İster bir for döngüsü içerisinde, ya da `toArray()` metodunu kullanabilirsin;


```java
Integer[] arr = new Integer[array.size()];
arr = data.toArray(arr);
```


### Sonuç
Aşağı yukarı ArrayList ile sıkça kullanılabilecek metodları ele almış olduk. Şuanda yaptıklarımı Java 8 versiyonu için kullandım, Java 9 ve daha sonraki versiyonlarda bazı değişiklikler olabilir.

Diziler **primitive types** grubuna girdikleri için daha hızlıdırlar ve daha performanslı uygulamalar için dizi kullanmak tercih sebebidir. Fakat komplike işlemler varsa, dizilere müdahele etmek işkence olabiliyor, bu gibi durumlarda da dinamik olan `ArrayList` yapısını kullanmak işimizi kolaylaştırıyor.