---
layout: post
title: HACKER101 CTF ÇÖZÜMÜ
date: 2021-03-24 00:00:00 +0300
---


----------------------------------------------

( Siteye <a href="https://ctf.hacker101.com/">buradan</a> ulaşabilirsiniz. )


## 1 - A Little Something to Get You Started / Web

### 1.1 - Flag (1/1)

![image](/blog/images/hackerone/1/1.JPG)

Aşağıda görüldüğü gibi sayfayı incele dediğimiz zaman 'background.png' dosyasını gözlemliyoruz.

![image](/blog/images/hackerone/1/2.JPG)

İşe yarar bir şeyler olup olmadığını gözlemlemek adına dosyayı gözlemliyoruz.

![image](/blog/images/hackerone/1/3.JPG)

Dosyaya gittiğimiz zaman çıktı aşağıdaki şekildedir.

![image](/blog/images/hackerone/1/4.JPG)

Sonrasında elde ettiğimiz Flag i kontrol ediyoruz.

![image](/blog/images/hackerone/1/5.JPG)

Aşağıda da görüldüğü üzere elde ettiğimiz flag doğru.

![image](/blog/images/hackerone/1/6.JPG)

## 2 - Micro-CMS v1 / Web

### 2.1 - Flag (1/4)

![image](/blog/images/hackerone/2/Flag 1/1.JPG)

Bizi aşağıdaki gibi bir sayfa karşılamaktadır.

![image](/blog/images/hackerone/2/Flag 1/2.JPG)

Mevcut sayfaların içeriğini gözlemlediğimiz zaman karşımıza aşağıdaki sayfalar çıkmaktadır. 

![image](/blog/images/hackerone/2/Flag 1/3.JPG)  ![image](/blog/images/hackerone/2/Flag 1/4.JPG)

Create a New Page seçeneği ile yeni sayfalar oluşturuyoruz.

![image](/blog/images/hackerone/2/Flag 1/5.JPG)

Oluşturduğumuz sayfaların başarılı bir şekilde oluşturulmuş olduğunu ana sayfada gözlemliyoruz.

![image](/blog/images/hackerone/2/Flag 1/6.JPG)

Sayfaları açtığımız zaman sıralı bir şekilde tutulduğu göze çarpmaktadır fakat sayfalarımızın sıralamasın 2 den 10 a arttığı göze çarpmaktadır. 

![image](/blog/images/hackerone/2/Flag 1/7.JPG)

![image](/blog/images/hackerone/2/Flag 1/8.JPG)

Link üzerinden sırayla sayfaları denediğimiz çoğunda sayfa bulunmuyordu,

![image](/blog/images/hackerone/2/Flag 1/9.JPG)

fakat yetkimiz olmayan bir sayfaya denk geldim.

![image](/blog/images/hackerone/2/Flag 1/10.JPG)

Sonrasında  Markdown Test sayfasında 'Edit this page' seçeneğini kullanarak link kısmından yetkimiz olmayan sayfaya giderek düzenleme yapıp yapamayacağımızı test ediyoruz.

![image](/blog/images/hackerone/2/Flag 1/11.JPG) ![image](/blog/images/hackerone/2/Flag 1/12.JPG)

Sayfaya gittiğimiz zaman Flag elde ediyoruz.

![image](/blog/images/hackerone/2/Flag 1/13.JPG)

Flag i kontrol ettiğimiz zaman doğru olduğunu gözlemleyebiliriz.

![image](/blog/images/hackerone/2/Flag 1/14.JPG)

### 2.2 - Flag (2/4)

Sql açığı olup olmadığını kontrol ettiğimizde düzenleme sayfasında açık olduğunu gözlemliyoruz ve Flag elde ediyoruz.

![image](/blog/images/hackerone/2/Flag 2/1.JPG)

### 2.3 - Flag (3/4)

XSS açığı olup olmadığını kontrol etmek adına girdi ekleyebildiğimiz (Edit Page) alana *< script > alert (10Nisan)< \script >* yazarak kaydediyoruz.

![image](/blog/images/hackerone/2/Flag 3/1.JPG)

![image](/blog/images/hackerone/2/Flag 3/2.JPG)

Ana sayfaya döndüğümüzde 3. Flag i de elde etmiş oluyoruz.

![image](/blog/images/hackerone/2/Flag 3/3.JPG)

### 2.4 - Flag (4/4)

Başlık kısmında xss açığından yararlanmıştık. Şimdi ise açıklama kısmı için deniyoruz. Bu deneme için kullanacağımız payload ==> *< img src=xss onerror=alert(1) >*

![image](/blog/images/hackerone/2/Flag 4/1.JPG)

Kaydettikten sonra sayfadan bir çıktı alıyoruz.

![image](/blog/images/hackerone/2/Flag 4/2.JPG)

Sayfayı incelediğimiz zaman son Flag i de elde ediyoruz.

![image](/blog/images/hackerone/2/Flag 4/3.JPG)
