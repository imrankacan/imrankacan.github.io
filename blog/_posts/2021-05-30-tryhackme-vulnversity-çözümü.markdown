---
layout: post
title: TryHackMe – Vulnversity Çözümü
date: 2021-05-30 00:00:00 +0300
---


----------------------------------------------

Start Machine ile makinemizi başlattık.

![image](/blog/images/vulnversity/1.JPG)
#### Şekil 1.1 Makineyi Başlatma

Task 2 de nmap ile bilgi toplamamızı istemektedir.

![image](/blog/images/vulnversity/2.JPG)
#### Şekil 1.2 Task 2 

Öncelikle aşağıdaki komutu kullanarak versiyon taraması gerçekleştireceğiz.

![image](/blog/images/vulnversity/3.JPG)
#### Şekil 1.3

Tarama sonucunda elde ettiğimiz veriler aşağıdaki gibidir. (Makine IP = 10.10.168.30 (Makinanın her başlatılışında ip adresi değişecektir))

![image](/blog/images/vulnversity/4.JPG)
#### Şekil 1.4 Tarama Çıktısı

Şekil 1.4 ten de görüleceği üzere açık portlarımızın sayıdır 6 adettir.

![image](/blog/images/vulnversity/5.JPG)
#### Şekil 1.5

Squid proxy in versiyon bilgisine de şekil 1.4 te ki taramada gözlemleyebilmekteyiz. (3.*.**)

![image](/blog/images/vulnversity/6.JPG)
#### Şekil 1.6

Bir sonraki soru da ise –p-400 parametresi ile nmap in kaç adet bağlantı noktasını tarayacağını sormaktadır. Bu da –p parametresinden sonra verilen değer kadar noktayı tarayacağından dolayı cevabımız 400 olacaktır.

![image](/blog/images/vulnversity/7.JPG)
#### Şekil 1.7

Bir sonraki soruda ise –n parametresinin neyi çözümlemeyeceği sorulmaktadır. Bu sorunun cevabına ise nmap –help ile ulaşabilmemiz mümkündür.

![image](/blog/images/vulnversity/8.JPG)
#### Şekil 1.8

Şekil 1.8 den de anlaşılacağı üzere bu soruya cevabımız ‘DNS’ dir.

![image](/blog/images/vulnversity/9.JPG)
#### Şekil 1.9

Bir sonraki soruda ise işletim sistemi bilgisini sormaktadır. Bu soru için ise - O parametresini kullanabiliriz.

![image](/blog/images/vulnversity/10.JPG)
#### Şekil 1.10

Çıktımız bize tam olarak işletim sistemi bilgisini verememiş olsada ssh servisinden işletim sistemi bilgimizin ‘Ubuntu’ olduğunu söyleyebilmemiz mümkündür.

![image](/blog/images/vulnversity/11.JPG)
#### Şekil 1.11

Task 2 deki son sorumuz ise web server ın hangi portta çalıştığı ile ilgili. Yine bu sorunun cevabına da Şekil 1.4 te yaptığımız taramadan ulaşabilmekteyiz.

![image](/blog/images/vulnversity/12.JPG)
#### Şekil 1.12

![image](/blog/images/vulnversity/13.JPG)
#### Şekil 1.13

Bir sonraki task ise GoBuster i kullanmaya yönelik.

![image](/blog/images/vulnversity/14.JPG)
#### Şekil 1.14

Bu araç kalide kurulu olarak gelmektedir. Kurulu olmaması durumunda <a href="https://github.com/OJ/gobuster">buradan</a> ya da Kali Linux 2020.1 ve üzeri bir sürüm kullanılması durumunda sudo apt-get install gobuster komutu ile kurulumu gerçekletirebilmek mümkündür. 

![image](/blog/images/vulnversity/15.JPG)
#### Şekil 1.15

‘common.txt’ wordlistini kullanarak taramamızı başlatıyoruz. (Wordlist makinede hazır olarak bulunmaktadır.)

![image](/blog/images/vulnversity/16.JPG)
#### Şekil 1.16

Tarama sonucunda bir adet index.html elde ettik.

![image](/blog/images/vulnversity/17.JPG)
#### Şekil 1.17

Tarayıcıdan index.html e gittiğimizde karşımıza aşağıdaki sayfa çıktı. 

![image](/blog/images/vulnversity/18.JPG)
#### Şekil 1.18

Fakat bizden yükleme yapabileceğimiz alana sahip sayfa istenmektedir ve index.html sayfasında böyle bir alan bulunmamaktadır.

![image](/blog/images/vulnversity/19.JPG)
#### Şekil 1.19

Şimdi ise şekil 1.17 deki taramada elde ettiğimiz internal sayfasını kontrol ediyoruz.

![image](/blog/images/vulnversity/20.JPG)
#### Şekil 1.20

Bunun sonucunda aradımızın sayfanın ‘internal’ dizini olduğunu gözlemliyoruz.

![image](/blog/images/vulnversity/21.JPG)
#### Şekil 1.21

Bir sonraki task e geçtiğimzde ilk soruda elde ettiğimiz yüklenebilir sayfada hangi uzantılı sayfanın engellenmiş olduğunu sormaktadır. Bir kaç farklı uzantılı sayfayı yuklemeyi denedikten sonra ‘.php’ uzantılı sayfaların engellenmiş olduğunu gözlemledik.

![image](/blog/images/vulnversity/22.JPG)
#### Şekil 1.22

Bir sonraki işlem için bir adet wordlist oluşturuyoruz.

![image](/blog/images/vulnversity/23.JPG)
#### Şekil 1.23

Sonrasında trafiği yakalamak adına Burp Suite yi aktif ediyoruz.

![image](/blog/images/vulnversity/24.JPG)
#### Şekil 1.24

Sayfamıza dosya yükleyerek trafiğin oluşmasını sağlıyoruz.

![image](/blog/images/vulnversity/25.JPG)
#### Şekil 1.25

İşlem sonrasında Burp Suite trafiği yakalamaktadır.

![image](/blog/images/vulnversity/26.JPG)
#### Şekil 1.26

Sağ tıklayıp ‘Send to Intruder’ seçeneğini seçiyoruz.

![image](/blog/images/vulnversity/27.JPG)
#### Şekil 1.27

Çıkan ekranda ‘Possitions’ seçeneğinden atak tipini ‘sniper’ seçiyoruz ve atak yapılacak kısmı seçiyoruz.

![image](/blog/images/vulnversity/28.JPG)
#### Şekil 1.28

Payloads sekmesinden ise hazırladığımız word list i ekliyoruz. (Bu ekrandan elle girişte yapabilmemiz mümkündür.)

![image](/blog/images/vulnversity/29.JPG)
#### Şekil 1.29

Sonrasında ‘Start Attack’ diyerek saydırıyı başlatıyoruz.
Atak sonucunda tüm değerler 200 döndürdü fakat elle tek tek denedikten sonra aradığımız cevabın ‘.phtml’ olduğunu gözlemliyoruz. 

![image](/blog/images/vulnversity/30.JPG)
#### Şekil 1.30

Bir sonraki işlem için sayfamıza ‘.phtml’ uzantılı shell dosyamızı yüklüyoruz.

![image](/blog/images/vulnversity/32.JPG)
#### Şekil 1.31

Internal ın altında ‘uploads’ dizini olduğunu gözlemliyoruz. Ayrıca yüklediğimiz shell in de başarılı bir şekilde yüklenmiş olduğunu buradan gözlemleyebiliyoruz.

![image](/blog/images/vulnversity/33.JPG)
#### Şekil 1.32

Shell imizdeki port u dinlemeye alıp, sayfanın /uploads dizininden shellimizi çalıştırıyoruz.

![image](/blog/images/vulnversity/34.JPG)
#### Şekil 1.33

Bunun sonucunda bağlantı sağlamış oluyoruz.

![image](/blog/images/vulnversity/35.JPG)
#### Şekil 1.34

Web sunucusunu yöneten kullanıcıyı bulmak için /etc/passwd dizininden kullanıcıları inceleyerek ilgili kullanıcıyı elde ediyoruz.

![image](/blog/images/vulnversity/36.JPG)
#### Şekil 1.35

Task içerisindeki flag i de user.txt dosyası içerisinden elde ediyoruz.

![image](/blog/images/vulnversity/38.JPG)
#### Şekil 1.36

Son Task imizde SUID özelliğine sahip dosyaları listelemek için;
![image](/blog/images/vulnversity/a.JPG) komutunu kullanabiliriz.

Bunun sonucunda aşağıdaki gibi bir çıktı elde ediyoruz.

![image](/blog/images/vulnversity/40.JPG)
#### Şekil 1.37


‘/bin/systemctl’ root yetkisi elde etme işlemlerinde kullanabileceğimiz bir dizin olduğu için ilgili cevabın bu olduğunu düşündüm ve cevap alanına yazdığımızda zaman doğru olduğunu gözlemliyoruz.

![image](/blog/images/vulnversity/41.JPG)
#### Şekil 1.38