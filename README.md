# Asal Anahtar Şifreleme
Bu şifreleme algoritması bir anahtar kelime kullanılarak geri dönüşümlü çalışacak şekilde tasarlanmıştır. Program sadece ingilizce alfabe için çalışmaktadır fakat büyük harf girdileri ve türkçe karakter girdileri yazılan bir fonksiyon ile düzeltilerek büyük harfler küçük harfle ve türkçe karakterler de ingilizce alfabedeki karşılığı ile değiştirilmektedir. Çıktı ise tamamen küçük harf ve türkçe karakter olmadan üretilmektedir.
Algoritmada çözülmesi daha zor olması için asal sayılardan faydalanılmıştır. Bir örüntüye sahip olmadıkları için çözümü oldukça zorlaştırmaktadır.
## &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Çalışma Mantığı
Şifreleme ve Deşifre Etme olarak ele alınırsa çalışma mantığı daha rahat kavranacaktır. 
## Şifreleme
Girilen açık metindeki karakterler sırası ile anahtar kelimedeki karakterler kullanılarak sayısal işlemlerden geçirilerek, şifrelenmiş karakterler elde edilmektedir. Aşağıdaki adımlarda örnek olarak kullanılması için<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Açık metin:   **deneme**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Anahtar:      **kriptoloji**<br/>

ifadeleri kullanılacaktır. İlk karakterler ele alınırsa;

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Açık karakter: “**d**” ASCII değeri: **100**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Anahtar karakter: “**k**” ASCII değeri: **107**<br/>
1. Anahtar kelimeden alınan karakterin ascii kodunun sırasında bulunan asal sayı ile açık metinde bulunan karakterin ascii kodunun toplamı bulunur. (Bu değere y diyelim.)<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;y = 107. Asal Sayı + Açık karakter ASCII değeri<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;y = 593 + 100<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yani y = 693 olarak elde edilir.<br/>

2. Hesaplanan y değerinin İngilizce alfabede bulunan harf sayısı olan 26 ya göre bölümünden kalanı hesaplanır. (Bu değere z diyelim.)<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z = y % 26<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yani z = 17 olarak elde edilir.<br/>

3. Elde edilen z değeri kullanılarak ASCII tablosuna ulaşılmaya çalışılırsa tablodaki ilk 26 karaktere gidilir. Fakat istenilen ingilizce küçük harfler ASCII tablosunda 97’den başlamaktadır. Bu yüzden z değerine 97 ekleyerek ASCII tablosuna ulaşılırsa, ingilizce alfabedeki harfler elde edilir. Örneğe göre elde edilen şifrelenmiş harf aşağıdaki python kod satırı ile elde edilir.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sifreli_karakter = chr(z+97)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yani ASCII değeri 17+97 = 114 olan karakter: “**r**” olarak bulunur.<br/>

4. Bu adımlar girilen metnin sonuna kadar tekrarlanarak şifrelenmiş metin oluşturulur. Anahtar kelimenin uzunluğu metin uzunluğundan kısa ise anahtar kelimenin son harfinden sonra ilk harfe geçerek baştan devam edilecektir.<br/>
Uygulanan adımlar sonucunda elde edilen şifreli metin aşağıdaki gibidir.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Açık Metin → Şifrelenmiş Metin<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;“**deneme**” → “**relqym**”<br/>

## Deşifre Etme
Şifreli metni deşifre ederken ise sadece şifreli karakterler ve şifrelenirken kullanılan anahtar kullanılması yeterlidir. Yine aynı şekilde şifreli karater ve anahtar karakterler belirlenir ve ASCII tablodaki karşılıkları kaydedilir. Anahtar kelimenin aynısı olmadan şifrenin çözülemeyeceğine dikkat edilir.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şifreli metin: **relqym**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Anahtar: **kriptoloji**<br/>
ifadeleri kullanılacaktır. İlk karakterler ele alınırsa;<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şifreli karakter: “**r**” ASCII değeri: **114**<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Anahtar karakter: “**k**” ASCII değeri: **107**<br/>

1. İlk olarak şifreli karakterin ASCII değerinden 97 çıkarılarak 26’lık dilimdeki payı elde edilir. Bu paydan 107. asal sayının (anahtar karakter ASCII değerinden) 26 ile bölümünden kalan çıkarılarak bir fark değeri elde edilir.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z = Sifreli karakter ASCII değeri – 97<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z = 17<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(107. asal sayı = 593 ve bu sayının 26 ile bölümünden kalan 21 dir.)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fark = z – 21<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fark = -4<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Burada dikkat edilemesi gereken husus z değerinin 0 (sıfır) olabileceğidir. Program yazılırken bir sorgu ile eğer 0 (sıfır) ise fark hesaplanırken z değeri yerine 26 sayısından çıkarılarak fark bulunur.<br/>

2. Bir önceki adımda elde edilen fark, bulmamız gereken açık karakterin 26 ile bölümünden kalandır. Fakat 26’nın kaç katına fark ekleneceğini bulmak için bir katsayı değeri gerekmektedir. Alfabedeki son harfin ASCII değeri 122’dir. Bu sayıdan fark değeri çıkarıldıktan sonra elde edilen sayı 26’ya bölünerek ondalıklı kısma dikkat edilmeksizin, tamsayı kısmı bizim katsayı değerimiz olacaktır.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;katsayı = (122 - fark)/26<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;katsayı = (126)/26<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;katsayı = 4.846<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Sayının sadece tamsayı kısmı alınması için alt satırdaki python komutu kullanılır.)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;katsayi = int(katsayi)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;katsayı = 4 olarak elde edilir.<br/>

3. Açık karakterin ASCII değerini hesaplamak için katsayı ve fark değerleri bulunduğuna göre artık hesaplanabilir.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yeni karakter ASCII değeri = 26*katsayi + fark<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yeni karakter ASCII değeri = 104 + (-4)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yeni karakter ASCII değeri =100<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Yani ASCII değeri 100 olan karakter yeni karakter (şifresiz karakter)’dir. Bunun için alt satırdaki python kodu kullanılır.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yeni_karakter= chr(yeni_ascii)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sonuç olarak “**d**” harfi elde edilmiş olur.<br/>

4. Bu adımlar girilen metnin sonuna kadar tekrarlanarak şifrelenmiş metin karşılığı olan yeni (şifresiz) metin elde edilir. Anahtar kelimenin uzunluğu metin uzunluğundan kısa ise anahtar kelimenin son harfinden sonra ilk harfe geçerek baştan devam edilecektir. <br/>
Uygulanan adımlar sonucunda elde edilen şifreli metin aşağıdaki gibidir.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Şifreli Metin → Yeni (Şifresiz) Metin<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;“**relqym**” → “**deneme**”<br/>







