---
layout: post
title: Java Giriş  
categories: [java]
tags : [java,content-in-turkish]
comments : true
---

*Please Note: This content is in Turkish Language and is written for a specific purpose, 1-1 tutorial kinda thing. If you desire, you may look at my other post, they are mostly in English*

### new Anahtar Kelimesi(keyword)

Şöyle bir sınıfımız olduğunu hayal et:

```java
public class Character {
	
}
```

Biz sınıfı tanımlarken aslında tekrar tekrar yazmamak adına bir tür belirtiyoruz, eylemleri olan, bazı özellikleri olan ve bunları kolayca değiştirebileceğimiz bir prototip gibi düşünebilirsin. Ve bu sınıftan bir obje oluşturmak için `new` anahtarını kullanıyoruz:

```java
Character ilkKarakter = new Character();
Character ikinciKarakter = new Character();
```

### Constructor (Yapıcı) Metodlar

`Construct` inşa etmek demektir. Adından anlayabileceğin üzere, inşa edilmeden önce, bazı ayarlamalar yapmak istersen bu metodlara ihtiyacın var demektir. `Character` sınıfını şöyle düzenleyelim :

```java

public class Character {
	public int height = 0;
	
	// 1. Yapıcı Metod
	public Character() { // Bu metod kullanılırsa, height 0 olarak kalacaktır
		
	}
	
	// 2. Yapıcı Metod
	public Character(int height) { // Yada, bu metodu kullanacak olursan, parametreden gelen değer ne ise, height o olacaktır
		this.height = height;
	}
}

```

Şimdi artık `Character`  sınıfından **2** farklı şekilde nesne üretebilirsin, şöyle ki:

```java
Character c1 = new Character();
Character c2 = new Character(15);

System.out.println(c1); // 0 Yazdıracaktır
System.out.println(c2); // 15 Yazdıracaktır
```

**NOT:** Burada dikkat etmen gereken constructor metodları nasıl tanımladığımız. Farkettiysen bir dönüş tipi yada void anahtarı yok:

```java
public Character() {

}
```

Ama normal metodları tanımlarken nasıl yapıyorduk:

```java
public void metod1() { 
    // geri birşey döndürmeyen bir metod
}

public int metod2() {
    return 15;
    // Geriye int tipinde sayı döndüren bir metod
}
```


### static anahtarı

Bir konsol uygulamasında static anahtarı bol bol kullanıyoruz, fakat gerçek uygulamalarda bu kadar sık kullanmayız bu anahtarı. Kısaca program çalışırken yok edilmesini istemediğimiz metodları ve sınıfları tanımlarken, `static` olarak tanımlarız.

Konsol uygulamalarında çalışmalar yaparken, main metodunu bilirsin. Bütün metodları işleri bunun içerisinde yapıyoruz ama bu pek doğru bir yaklaşım değil. `Class` lar yardımıyla, daha modüler bir yapı kurmak gerekiyor. Mesela Character sınıfını ayrı bir `.java` dosyasına taşıyalım:

- Sol taraftaki menüden `src` ye sağ tıkla
- Açılan pencerede `New` ifadesine gel
- Orada `Class` ifadesini seç

Daha sonra main metodunda bunları kullanabilirsin.

```java
public static void main(String[] args) {
	Character c1 = new Character();
    Character c2 = new Character();

    // ... Vesaire 
}
```

### Metod Parametreleri

```java
public static void main(String[] args) {
	int s1 = 5;
    // Metoda parametre olarak 5 değerine sahip bir değişken gönderiyoruz
    karesiniAl(s1);
}


public int karesiniAl(int sayi){
    // Metodun içindeyken, bu parametreyi kullanırız, ve buna argüman denilir
    // Yani metodun içine girince, burada kullanılmaya hazır olunca, argüman olarak adlandırılır.
    // Bunu bilmekte çok önemli değil, sadece not etmek istedim
    return sayi * sayi;
}
```

Bir metodu çağıracakken (invoke method) o metoda parametre göndeririz. O metodun içinde bu parametreyi kullanacağız fakat, metodun parametre alıp almadığından emin olmalısın.


### Sınıflarda Kalıtım (Class Inheritance)

Bir sınıfı kalıtmak demek, onu zenginleştirmektir kısaca. 2 sınıfımız var şu şekilde:

```java
public class Character {
    public int height = 0;
}

public class Enemy extends Character {
    public int location = 0;
	public Enemy(){
		System.out.println(height); // Dikkat edersen this.height, kalıtım yaptığımız Character sınıfından geliyor
	}
}
```

Bu kalıtımı `extends` anahtarı ile yapıyoruz. Kelime olarak `genişlemek` demektir. Character sınıfını genişletiyoruz, ve biz `height` adında bir değişkeni tanımlamadan bizde var olmuş oldu. 

Kalıtımın kullanılma amacı aynı şeyleri tekrar tekrar yazmaktan kurtulmak ve ayrıca benzeri yapıları bir arada tutmaktır. Bir de şöyle bir sınıf düşün:

```java
public class Player extends Character {
	public String userName = "";
	public Player(){
		height = 150;
		userName = "Kullanıcı Adı sadece Player için mantıklı.";
	}
}
```

Hem Enemy sınıf türünden nesneler, hemde Player sınıfı türünden nesneler, hepsi aslında  `Character` sınıfından türediler. Ve onları birşekilde ortak bir noktada tuttum. Diyelimki uygulamada biryerde bütün objelerin özelliklerine ihtiyacın var. Hepsi Character türünden olduğu için, şöyle bir dizide bunları tutabilirsin:

```java
Enemy enemy = new Enemy();
Player player = new Player();
		
Character[] butunKarakterler = new Character[] { 
	enemy,
	player
};
```

Bu olayı anlayabilmek için daha fazla örneğe bakman faydalı olacaktır.

Nesne Yönelimli Programlama (OOP) oldukça basittir, bir kaç kuraldan ibarettir. Sadece eğitimini tamamladıktan sonra açık kaynaklı bir kaç örnek projede kullanımına bakman yeterli olacaktır. Kalan bölümleri bir sonraki yazıda tamamlamayı düşünüyorum ve algoritma soruları ile devam etmeyi planlıyorum.

