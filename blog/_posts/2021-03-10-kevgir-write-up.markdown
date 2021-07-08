---
layout: post
title: KEVGİR WRITE-UP
date: 2021-03-10 00:00:00 +0300
---


----------------------------------------------

( Zafiyetli makineyi <a href="https://canyoupwn.me/kevgir-vulnerable-vm/">buradan</a> indirebilirsiniz. )


• Kali Linux ve Kevgir makinesini aynı NAT ağına bağladım.

Makineler aynı NAT ağında olduğu için; makinenin IP adresinin tespiti için netdiscover aracını kullandım.


![image](/blog/images/kevgir/1.jpg)

Elde edilen ip adreslerinden 10.0.2.14 hedef makinemize ait olduğu aşağıdaki görselden de anlayabiliriz.

![image](/blog/images/kevgir/2.jpg)

Nmap aracı ile *nmap –sS –sV –p- 10.0.2.14*  komutunu kullanarak port taraması gerçekleştirebiliriz.

![image](/blog/images/kevgir/3.jpg)

Metaspoiti açarak,

![image](/blog/images/kevgir/4.jpg)

tomcat ile ilgili auxiliary ve exploitleri araştırdım. Çıktılar aşağıdaki şekildedir;

![image](/blog/images/kevgir/5.jpg)

Öncelikle *tomcat_mgr_login auxiliary* ile tomcat servisinin default şifrelerini denedim. (Şifre tespiti brute force ile tespit edilmeye çalışılmaktadır.) 

![image](/blog/images/kevgir/6.jpg)

Hedef makinenin IP adresini girerek işlemimizi başlatıyoruz.

![image](/blog/images/kevgir/7.jpg)

İşlem sonucunda kullanıcı adı – şifremizin tomcat-tomcat olduğunu gözlemliyoruz.

![image](/blog/images/kevgir/8.jpg)

Kullanıcı adı – şifre tespitinden sonra *tomcat_mgr_upload* exploitini kullanarak sisteme sızmaya çalıyoruz. Bu işlemle beraber tarıyıcıdan *10.0.2.14:8080/manager* adresine de giriş yapıyoruz. Bunu yaparak shell atabilmekteyiz.

![image](/blog/images/kevgir/9.jpg)

Yukurıdaki görselde de görüldüğü üzere  exploit kullanımı gözlemlemek adına show options komutunu kullanabiliriz.

![image](/blog/images/kevgir/10.jpg)

Exploit ile beraber meterpreter ekranına düşmüş bulunuyoruz.
Meterpreter komut satırına shell yazarak linux komut satırına geçiş yapıyoruz. Fakat etkileşimli komut satırına henüz geçemedik.

![image](/blog/images/kevgir/11.jpg)

python –c *import pty;pty.swan (“/bin/sh”)*  komutunu kullanarak shellimizi etkileşimli shell e çeviriyoruz.

![image](/blog/images/kevgir/12.jpg)

Kullanıcıları listeleyerek admin kullanıcısına geçiş yapıyoruz.

![image](/blog/images/kevgir/13.jpg)

Admin kullanıcının şifresini elde etmek için pypmyadmin sayfasına tarayıcıdan giriş yaptık. 

![image](/blog/images/kevgir/14.jpg)

Kullanıcı adı-şifre defaulttaki (root-toor) bilgiler olduğu için sisteme giriş yapabildik ve kullanıcıların şifrelerinin hash değerlerini elde ettik.

![image](/blog/images/kevgir/15.jpg)

Hash değerinin çözümlemesini hashcat gibi toollar ile yapabileceğimiz gibi online çözümleyiciler de kullanabiliriz. (hashes.com adresini kullandım)

![image](/blog/images/kevgir/16.jpg)

Sistemin çekirdek bilgisini öğrenmek için *uname –a* komutunu kullanıyoruz.

![image](/blog/images/kevgir/17.jpg)

Sisteme uygun exploit dosyası indirip, çalıştırarak root yetkisi elde edebiliriz. 
