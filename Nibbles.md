# HackTheBox Nibbles Writeup

Benim bu sanal makine için çözümüm aşağıda anlatacağım şekilde olmuştur.

## 1)
İlk olarak sanal makinemin ipsine bir nmap taraması yapıyorum.Bu şekilde  hangi portların açık olduğunu ve hangi servislerin çalıştığını öğreniyorum.

![image](/resim/1.png)

## 2)
Daha sonra ip adresini ziyaret ediyorum.Ana sayfada böyle bir sayfa bizi karşılıyor

![image2](/resim/2.png)

## 3)
Sayfanın kaynak kodlarına baktığımızda bir not olduğunu görüyoruz.Bu notta bir dizinden bahsediyor.

![image3](/resim/3.png)

## 4)
Belirtilen dizine gidiyoruz ve hemen bu sayfanında kaynak kodlarına göz atıyoruz.
Bu sırada bir img etiketine denk geliyorum.Böyle bir img elemanı var ama sayfada
etkisi yok ve ayrıca img etiketinin kaynak olarak belirttiği adres dikkat çekici.
Buradan bu bilgileri toplayıp sonraki adıma geçiyorum.

![image4](/resim/4.png)

## 5)
Bir önceki aşamada dikkatimizi çeken adrese  gittiğimizde böyle bir sayfayla karşılaşıyoruz.Daha sonra bu bilgiyi kullanmak üzere sonraki adıma geçiyorum.

![image5](/resim/5.png)

## 6)
Bu adımda dirbuster araçını kullanarak nibbleblog dizinin altında başka hangi dizinlerin bulunduğuna bakıyorum.Tabiki burada direk olarak admin dizini ve admin.php sayfası dikkatimi çekiyor

![image6](/resim/6.png)

## 7)
Admin.php sayfasına geldiğimizde bizi bir admin girişi karşılıyor.Aslında
çok kolay bir engel olan bu sayfada haddinden fazla zaman harcadım.En
sonunda htb forum sayfalarından topladığım ipuçlarıyla başarılı bir şekilde
giriş yaptım.İpucu şu şekildeydi hackthebox'ın genel olarak makinelerinde
kullandığı varsayımsal kullanıcı adı ve şifresiydi(usernmae:admin-password:nibbles)

![image7](/resim/7.png)

## 8)
Admin girişini yaptıktan sonra karşımıza bu sayfa geliyor.Burada direk olarak aklıma 5.adımdaki adres geliyor.Çünkü o adresle bu sayfadaki bir kelime eşleşiyor. O kelime Plugins.Bu yüzden bu yoldan devam ediyorum.

![image8](/resim/8.png)

## 9)
Plugins sayfasına geldiğimizde yine aynı adrste bulunan My image ifadesi göze  çarpıyor ve tıklayarak devam ediyorum.

![image9](/resim/9.png)

## 10)
Burada dosya yükleme imkanı veren bir formla karşılaşıyorum ve hemen php reverse
shell yüklemeye çalışıyorum.İlk olarak php-reverse-shell.php olarak 
yüklemeye çalışıyorum ama kabul etmedi.Daha sonra ismini 5.adımda da gördüğüm
isimlerden biri olan image.php yaparak değiştiriyorum ve başarılı bir şekilde 
sunucuya yükleniyor.Bu arada shell'in içini düzenlemeyi unuttmayın kendi ip adresinizi
ve portunuzu belirtin.

![image10](/resim/10.png)

## 11)
Yüklediğimiz sayfaya gittiğimizde image.php tıklayarak reverse bağlantısını kurmaya başlıyorum.

![image11](/resim/11.png)

## 12)
Bu arada bellirtiğim portu dinlemeye aldım ve direk olarak bağlantının
kurulduğunu görebilirsiniz.Ama buradaki "can't access tty" ifadesi dikkatimi
çekiyor.Bu ifadenin anlamı sahip olduğum shell'le yapabileceklerimin kısıtlı olmasıdır.
Bunu daha sonra çözmek üzere sonraki adıma geçiyorum.

![image12](/resim/12.png)

## 13)
Burada id komutunu çalıştırarak yekilerime bakıyorum.ls komutuyla hangi dizinlerin
olduğuna bakıyorum.Buradan sonra 2 text dosyasını bulmamız lazım.Bunlar user.txt ve
root.txt dosyaları. root.txt dosyası root dizininin altında bulunur ve okumak
için root yetkilerine sahip olmamız lazım.user.txt dosyasının nerede
olduğunu bilmiyoruz ve ilk olarak onu aramaya başlıyorum.

![image13](/resim/13.png)

## 14)
Ben tamamen rastgele olarak home dizininden ilerlemeyi seçtim. ve /home/nibbler
yolunu izleyerek user.txt dosyasına ulaştım.Text dosyasını okuyunca karşımıza
bir hash çıktı ve direk olarak bu şekilde kabul ettiği için decode etmeden kullanıyoruz.
Ayrıca bu dizinde personal.zip dosyasıda bulunuyor.Bu dosyayıda zip 
dosyasından çıkarınca personal dosyası çıkıyor.(Bu arada ip:port dosyasını
bu makinenin üzerinde uğraşan diğer akadaşlar bırakmış :) )

![image14](/resim/14.png)

## 15)
Bir önceki adımda zip dosyasının içinden çıkan personal dosyasından ilerlediğimizde
stuff dizini ve en sonunda monitor.sh adında bash script karşımıza çıkıyor.
Burada bu scriptle baya bir uğraşıyorum ama sonuç olarak birşeyler elde edemiyorum
ve başka neler yapabilirim diye düşünüyorum.

![image15](/resim/15.png)

## 16)
Bu sefer direk olarak işletim sistemine odaklanıyorum daha fazla bilgi toplamak
için uname -an komutunu çalıştırdım.Burada kullanılan kernel versiyonu
hakkında bilgi alıyorum ve bundan faydalanmak için exploit arıyorum.

![image16](/resim/16.png)

## 17)
Bu exploiti ararken linux'un en secdiğim araçlardan biri olan searchsploit araçını
kullanıyorum.Ve basit bir sorgu yazarak arama işlemine başlıyorum.Karşıma
çıkan sonuçlardan 4.sıradaki exploiti seçerek yoluma devam ediyorum.

![image17](/resim/17.png)

## 18)
Bu exploiti www.exploit-db.com sitesinde aratarak detaylı bilgisine ulaşıyorum. Buradan indirme işlemine başlatıp kendi bilgisayarıma indiyorum.

![image18](/resim/18.png)

## 19)
Kendi bilgisayarıma indirdiğim bu exploiti yine kendi bilgisayarımda derleyip çıktısını alıyorum.

![image19](/resim/19.png)

## 20)
Zafiyetli makineye indirmek için çıktının bulunduğu dizinde bir python http sunucusu 8081 portundan başlatıyorum.

![image20](/resim/20.png)

## 21)
Burada home dizininden çıkıp wget araçıyla indirmeye çalışıyorum ama bir yetki engellmesi karşıma çıkıyor

![image21](/resim/21.png)

## 22)
Daha sonra /home dizinine tekrardan dönüp yine indirmeye çalıştığımda engellemeyle karşılaşıyorum.Sonra bash scriptin bulunduğu dizine ilerliyorum ve son olarak burada indirme işlemini
yapıyorum ve başarılı bir şekilde karşı makineye yüklemiş oluyorum. 

![image22](/resim/22.png)

## 23)
İndirdiğim out dosyasını çalıştırmaya başladığımda yine bir yetki kısıtlamasıyla 
karşılaşıyoum ama bu sefer root olmadığım için çalışmadı,dosyanın yetkilerinden kaynaklanan
bir hataydı.chmod +x out komutuyla yetki vererek çalıştırdım ve sonuç
olarak root yetkilerine ulaşmıştım.Böylece son hedefim olan root.txt
dosyasına ulaşabilirdim.

![image23](/resim/23.png)

## 24)
Ve en son olarak root.txt dosyasını da okuyarak bu makinedeki işimi bitirdim.

![image24](/resim/24.png)
