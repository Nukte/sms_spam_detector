# SMS SPAM DETECTOR: 5.500 Mesajlık Küçük Veriyle Spam Avı

> **"Spamciler, sistemleri aşmak için bazen 'bedava' yerine 'bed@va' yazarlar... Kelime bazlı modeller bunu kaçırır ama harf bazlı modelim yakalar..."**
> — *Bir spam avcısı.*

Bu proje, **Akdeniz Üniversitesi Veri Bilimi Kulübü**'nde çayımızı yudumlarken tartıştığımız o sorudan doğdu: **"Büyük Veri (Big Data) olmadan, gerçekten yüksek performanslı ve güvenilir bir model eğitilebilir mi?"**

Elimde sadece 5.500 satırlık, üstelik dengesiz (%13.4 Spam) bir veri seti vardı. Hedefim netti: Veri azlığını stratejik hamlelerle telafi etmek ve gerçek dünyada kullanılabilecek bir sistem kurmaktı.

---

## Verinin DNA'sı
Kodlamaya geçmeden önce veriyi masaya yatırdığımda, spamcilerin belirgin bir parmak izi bıraktığını gördüm:

* **Agresiflik:** Biz normal insanlar "Ok, tmm, geliyorum" gibi kısa ve sakin konuşurken; spamciler SMS limitini sonuna kadar zorluyor (Ortalama 138 karakter) ve "FREE, CLAIM, URGENT" diye bağırıyorlar.
* **Gizlenme:** Kelimeleri bilerek bozuyorlar. İşte projeyi şekillendiren fikir buradan çıktı.

<img width="1200" height="600" alt="EDA Analysis" src="https://github.com/user-attachments/assets/4322a640-d57e-4f08-b348-b2890ba72414" />

---

## Strateji
Modelin öğrenme kapasitesini artırmak için sadece kelimelere bakmadım, kelimelerin içindeki hilelere odaklandım.

1.  **Modeller Ringte:** Naive Bayes, Logistic Regression ve SVM modellerini kıyasladım.
2.  **Kritik Hamle (Char N-Grams):** Klasik modeller "spam" kelimesini ararken, saldırganlar "s.p.a.m" veya "sp@m" yazıp filtreleri deliyordu. Ben de taktiğimi değiştirdim: Kelimeleri değil, **harflerin dizilişini ve o gizli örüntüleri** okuyan bir yapı kurdum.

<img width="1000" height="600" alt="Technical Approach" src="https://github.com/user-attachments/assets/3406cee8-6fba-4571-a101-9e7b81a12bf7" />

---

## Sonuçlar
Yaptığım testler sonucunda harf bazlı (**Char N-Gram**) yaklaşımın tüm modellerde performansı uçurduğunu gördüm. Şampiyonumuz ise net bir skorla **SVM** oldu.

<img width="1000" height="600" alt="Results Graph 1" src="https://github.com/user-attachments/assets/dbdfca32-1d33-4b89-a871-47a2e8d164fe" />

<img width="1000" height="600" alt="Results Graph 2" src="https://github.com/user-attachments/assets/78dc14ad-f090-4dc7-b42d-179ada12c82d" />

### Güvenilirlik ve Hata Analizi
Sadece başarı oranına bakmak yetmezdi. Bir spam filtresinde en büyük günah, kullanıcının önemli bir mesajını yanlışlıkla silmektir.
* **Kaçan Spamler:** Kelime bazlı modelde 35 spam kaçarken, geliştirdiğim stratejiyle bu sayıyı **5'e düşürdüm.**
* **Yanlış Alarmlar (False Positive):** En büyük gurur tablom burası; SVM (Char) modeli test setinde **sadece 1 kez** yanlış alarm verdi.

> **Sonuç:** Kesinlik (Precision) oranımız **%99.4**. Yani bu sistem bir mesaja "Bu bir spam" diyorsa, büyük ihtimalle haklıdır.

---

## Deneyimlediğim Yanıt
**"Evet, devasa verilere sahip olmasanız bile, doğru veri işleme stratejileriyle gerçek hayatta kullanılabilecek modeller yapabilirsiniz."**

İyi çalışmalar.

---
**Geliştiren:** Ali Kemal Kara
