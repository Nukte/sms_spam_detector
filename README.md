# SMS SPAM DETECTOR
Sadece 5.500 mesajlık bir veri seti ile farklı metotlar ve modeller kullanılarak geliştirilen deneysel bir spam tespit projesi.

Bu repo, Akdeniz Üniversitesi Veri Bilimi Kulübü'nde tartışılan; "Büyük Veri olmadan yüksek performanslı bir model eğitilebilir mi?" sorusuna cevap aramak için oluşturulmuştur.

## Proje Hedefi: 
Genellikle "Big Data" gerektiren metin sınıflandırma problemini, model çeşitliliği ve detaylı önişleme (text processing) teknikleriyle çözmek. 
Az veriyle (%13.4 Spam oranı) çalışırken "Yanlış Alarmları" (False Positive) sıfıra indirmektir.

## Verinin DNA'sı 
Kullanılan Veri Seti: UCI SMS Spam Collection (5.572 Satır)Kodlamadan önce yapılan analizlerde spam mesajların belirgin parmak izleri tespit edildi
:Uzunluk: Normal mesajlar ortalama 71 karakterken, spamler 138 karakterdir (SMS limitini zorlarlar).
Kelime Seçimi: Spamciler "FREE, Call, Claim" gibi agresif kelimeler kullanırken, normal kullanıcılar "Ok, U, Love" gibi kısa ifadeler kullanır.

<img width="1200" height="600" alt="Code_Generated_Image (3)" src="https://github.com/user-attachments/assets/4322a640-d57e-4f08-b348-b2890ba72414" />


## Teknik Yaklaşım ve Strateji 
Modelin öğrenme kapasitesini artırmak için 3 farklı algoritma ve 2 farklı NLP stratejisi karşılaştırılmıştır.
1. Modeller: Multinomial Naive Bayes, Logistic Regression ve Support Vector Machine (SVM)
2. Tarama Stratejisi: Word vs. Char N-GramsSpamciler filtreleri aşmak için kelimeleri bozar (örn: "spam" yerine "s.p.a.m" veya "sp@m").
   Word N-Grams: Klasik kelime bazlı yaklaşım. (Hileleri kaçırabilir) Char N-Grams (2-4): Kelimeleri harf grupları olarak okur.
   Bu projenin kilit noktasıdır; yazım hilelerini bir "örüntü" olarak yakalar.

   <img width="1000" height="600" alt="Code_Generated_Image" src="https://github.com/user-attachments/assets/3406cee8-6fba-4571-a101-9e7b81a12bf7" />

## Sonuçlar
Yaptığım testlerde Char N-Gram (Harf bazlı) yaklaşımın tüm modellerde performansı artırdığı görülmüştür.
<img width="1000" height="600" alt="Code_Generated_Image (2)" src="https://github.com/user-attachments/assets/dbdfca32-1d33-4b89-a871-47a2e8d164fe" />

<img width="1000" height="600" alt="Code_Generated_Image (1)" src="https://github.com/user-attachments/assets/78dc14ad-f090-4dc7-b42d-179ada12c82d" />


## Hata Analizi
Bir spam filtresinde en önemli kural: Önemli bir mesajı asla silme.
Kaçan Spamler: Kelime bazlı modelde 35 spam kaçarken, harf bazlı stratejiyle bu sayı 5'e düşmüştür. 
Yanlış Alarm (False Positive): SVM (Char) modeli test setinde sadece 1 kez yanlış alarm vermiştir.

## Sonuç: Kesinlik (Precision) oranımız %99.4. Sistem bir mesaja "bu bir spam" diyorsa büyük ihitmalle haklıdır.
