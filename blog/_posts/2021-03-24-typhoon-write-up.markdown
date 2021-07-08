---
layout: post
title: TYPHOON WRITE-UP
date: 2021-03-24 00:00:00 +0300
---


----------------------------------------------

( Zafiyetli makineyi <a href="https://www.prismacsi.com/typhoon-vulnerable-vm/">buradan</a> indirebilirsiniz. )


*ifconfig* komutu ile ip adresimi kontrol ettiğimde ip adresimin '10.0.2.5' olduğunu gözlemledim. Öncelikle *netdiscover -r 10.0.0.0/16* komutu ile cihazımızın bulunduğu ağdaki hostları gözlemleyerek hedef makinamızın ip sini tespit ediyoruz.

![image](/blog/images/tomcat/1.JPG)

Ayrıca zafiyetli makinanın ip sini tespitte *nmap -sP 10.0.2.0/24* komutunu da kullanabilmemiz mümkündür.

![image](/blog/images/tomcat/1.1.JPG)

Elde ettiğimiz ip adresini tarayıcımıza yazarak kontrolünü sağlayabilmemiz mümkündür.

![image](/blog/images/tomcat/2.JPG)

IP adresini tespit ettikten sonra *nmap -sV 10.0.2.15* komutu ile makinamızdaki açık portları versiyonları ile beraber gözlemleyebiliriz.

![image](/blog/images/tomcat/3.JPG)

Metaspoiti açarak,

![image](/blog/images/tomcat/4.JPG)

tomcat ile ilgili auxiliary ve exploitleri araştırdım. Çıktılar aşağıdaki şekildedir;

![image](/blog/images/tomcat/5.JPG)

Öncelikle tomcat_mgr_login auxiliary ile tomcat servisinin default şifrelerini denedim. (Şifre tespiti brute force ile tespit edilmeye çalışılmaktadır.)

![image](/blog/images/tomcat/6.JPG)

![image](/blog/images/tomcat/7.JPG)

![image](/blog/images/tomcat/8.JPG)

Görselde de görüldüğü üzere 'tomcat:tomcat' olarak kullanıcı adı - şifremizi elde ettik.

![image](/blog/images/tomcat/9.JPG)

Şimdi ise *exploit/multi/http/tomcat_mgr_upload* ı kullanarak exploit aşamasına geçiyoruz.

![image](/blog/images/tomcat/10.JPG)

Exploit kullanımı gözlemlemek adına *options* komutunu kullanabiliriz.

![image](/blog/images/tomcat/11.JPG)

Aşağıda görüldüğü üzere hedef makinamızın ip adresi ile beraber giriş işlemlerini gerçekleştirilerek exploit işlemini başlatıyoruz.

![image](/blog/images/tomcat/12.1.JPG)

![image](/blog/images/tomcat/12.2.JPG)

İşlem ile beraber meterpreter ekranına düşüyoruz.

![image](/blog/images/tomcat/13.JPG)

Hangi kullanıcı ile oturum elde ettiğimizi gözlemlemek adına *whoami* komutunu kullanabiliriz.
Ayrıca *id* komutu ile kullanıcının grup bilgileri gibi bilgileri elde edebilmemiz mümkündür.

![image](/blog/images/tomcat/15.JPG)

Hedef makinamızın işletim sistemi sürüm özelliklerini öğrenmek adına *uname -a* komutunu kullanıyoruz; bunu yapmamızda ki amaç root yetkisi elde etmek için zafiyet araştırması yapabilmek.

![image](/blog/images/tomcat/16.JPG)

Sonrasında işletim sistemine uygun exploit bulup çalıştırarak root yetkisi elde edebiliriz.

------------------------------------------------------------------------------------------------------------

## SSH

Hedef IP = 10.0.2.15

SSH a *hydra -L user.txt -P rockyou.txt 10.0.2.15 ssh -V* komutu ile brute force uygulayarak kullanıcı adı - parola tespiti yapmaya çalışabiliriz. (rockyou.txt geniş kapsamlı bir wordlistir.)

![image](/blog/images/tomcat/ssh/1.JPG)

Tarama sonucunda kullanıcı adı - parolanın 'admin - metallica' olduğunu gözlemliyoruz.

![image](/blog/images/tomcat/ssh/2.JPG)

Bulunan bilgiler ile giriş denemesi yapmak adına öncelikle *ssh admin@10.0.2.15* komutunu kullanıyoruz.

![image](/blog/images/tomcat/ssh/3.1.JPG)

Elde ettiğimiz password bilgisini girdikten sonra başarılı bir şekilde giriş elde etmiş oluyoruz.

![image](/blog/images/tomcat/ssh/3.2.JPG)

*******************************root****************************************
------------------------------------------------------------------------------------------------------------


