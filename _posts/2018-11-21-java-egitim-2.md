---
layout: post
title: Java Giriş Part 2 
categories: [java]
tags : [java,content-in-turkish]
comments : true
---

*Please Note: This content is in Turkish Language and is written for a specific purpose, 1-1 tutorial kinda thing. If you desire, you may look at my other post, they are mostly in English*

### Modüler Yapının Önemi

Bir önceki yazımda da bahsetmiştim, mümkün olduğu kadar her bir nesnenin kendine ait sınıfının olması önemli vesaire. Bunun önemini şuanda anlaman zor belki de bu kadar `class` a veya metoda neden ihtiyaç var diye düşünüyorsun, haklısın, bunu anca büyük bir projeyi bitirdikten sonra, 2 ay bekleyip projede güncelleme gerektiği zaman anlarsın. Kendi yazdığın kodu ben bunu yazmadım deyip inkar eder hale geliyorsun :) 

Fakat bu duruma düşmemek adına uygulamanın başında itibaren doğru `class` lar yazmak, metod ve değişken isimlerini herhangi birinin anlayacağı şekilde, yorum yazmaya gerek kalmayacak kadar açık yazarak kendi yöntemlerini geliştirmelisin. Mesela önceki yazıdaki kodları da kullanarak yapacağımız projenin anatomisi şeklinde şöyle bir örnek ile başlayalım:

```java
public class Character {
    // Aşağıdaki 2 değişken (property) yükseklik ve enini temsil eder 
    public int height = 0;
    public int width = 0;

    // Kalan canını temsil eder
    public int health = 0;
    // (Identifier) ayırt edici bir isim olabilir mesela
    public String id = "Bir Kişi"; 

    public void Walk() {
		
	}
	
	public void Attack(Character target) {
		
	}
	
	public void TakeDamage(int damage) {
		
	}
    
}

```

Şimdi, yukarıdaki sınıf ana bir sınıf, yani bir karakterde bulunabilecek genel özellikleri barındırıyor ve içlerini bilerek boş bıraktım.

Şöyle düşün, mesela senin yönlendirdiğin **Hero** adlı sınıf ve düşmanları temsil eden **Enemy** adlı sınıflar bundan türeyecekler. Madem bu sınıfları da yazacağım, onların içinde doldururum bu metodları, neden bu ana sınıfta metodların için doldurayım ki?

İşte burada **overriding** adı verilen olay devreye giriyor. Modüler yapı için oldukça önemli bir konu. Adı üstünde, bir şeyin diğerine üstün gelmesi gibi düşün. Çocuk sınıf ya da türetilen sınıftaki metod, ana sınıftaki metoda üstün gelir, ve onu devre dışı bırakır. Şöyle ki:

```java
public class Hero extends Character {
	public int walkSpeed = 2;
	public int power = 10;
	
	@Override
	public void Walk() {
		this.walkSpeed += 1;
	}
	
	

	

	@Override
	public void TakeDamage(int damage) {
		// TODO Auto-generated method stub
		
	}

	



	@Override
	public void Attack(Character target) {
		// TODO Auto-generated method stub
		target.TakeDamage(this.power);
	}

	
}
```

Metodların üzerlerindeki `@Override` ifadesini farketmişsindir, bu şu demek oluyor, ana sınıftaki falanca metodu iptal et, orasını çalıştırma, bu metodu çağır demek oluyor. 

İlerleyen örneklerde daha net şekilde anlayacaksın.

### this Anahtarı

Mesela hemen yukarıdaki örnekte `Attack()` metodunun içinde şöyle bir ifade var:

```java
target.TakeDamage(this.power);
```

İşte buradaki **this**, bu sınıfın içindeki `power` adlı değişkeni işaret ediyor. Kimileri kodun okunaklığı açısından bunu kullanmaktadır, ama kullanmak zorunda değilsin, fakat kullanmak zorunda olduğun istisna bir durum var.

Düşün ki şöyle bir metod var;

```java
public void metod(Character c) {

}
```

Farkettiğin üzere bu metod `Character` class tipinde bir parametre alıyor, ve sen bunu `Character` sınıfının **constructor** metodunda çağıracaksın, işte bu işlemde **this** anahtarı kullanışlı olacaktır;

```java
public class Character {
	// Dikkat Et: Constructor metodların tipi olmaz! Yani void gibi veya int gibi tipleri olmazlar! 
	public Character() { 
		metod(this);
	}
}
```

Çağırdımız (invoke) metod `Character` class tipinde bir parametre istiyordu, sen de this yazınca oraya `bunu` gönder demek gibi bir şey yapıyorsun, gayet mantıklı :)

İşte bu durumda **this** anahtarını mecbur kullanmak zorundasın.


### Interface'ler

OOP'nin (Object Oriented Programming) çok fazla konusu kalmadı, son olarak bu interface konusuna da değinmek istedim. 

Interface arayüz demektir. Class'lara uygulanır bu interface'ler. Interface'lerin içinde içi boş metod tanımlamaları bulunur;

```java
public interface ICharacter {
	public void Respawn();
    public int GetHealth(); 
}
```
Farkettiysen süslü parantezler `{ }` yok, yani metodun gövdesi yok.

Birde sınıflara nasıl uygulandığına bakalım, yani interface'lerin nasıl kullanıldığına;

```java
public class Enemy extends Character implements ICharacter {
    @Override
	public void Respawn() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public int GetHealth() {
		// TODO Auto-generated method stub
		return 0;
	}
}
```

Aslında kurallar belirlemekten farksızdır interface tanımlamak. Başta karmaşık gelir ama hiç öyle değil, kodu düzenli tutmak adına belli kurallar olsun istersin. Yani `Character` sınıfından türeyen bütün sınıflar yukarıdaki `Respawn()` ve `GetHealth()` metodları olmak zorunda dersen, o sınıflara `implements ICharacter` ifadesini eklersin ve o metodları sınıfında tanımlarsın.

Not etmeliyim ki, interface'i uyguladıktan sonra, metodları o sınıfta tanımlamazsan, hata alırsın, o metodlar tanımlanmak zorunda.

> Interface olayına çok takılma, bende çok kullandığımı söyleyemem, ilerleyen aşamalarda örneklerle pekiştirirsin diye düşünüyorum.

### Kod Yazma Zamanı

Artık Nesne Yönelimli konularını aşağı yukarı ele aldık, çok kısa anlattım fakat, örneklerle devam etmeyi düşünüyorum. 

Bir sonraki yazıdan önce senden isteğim, aşağıdaki problemi çözümlemen:

> Verilen dizideki en büyük `int` elemanı bulan metodu tanımlar mısın? Aşağıda kodun iskelet halini bulabilirsin.

```java
int[] array = {10, -2, 3, 0, 129, 88,11, -1};
public int minMax(int[] array) {
    return 0;
}
```

