# Yapay Zeka ile Emlak İlanlarında Benzerlik Analizi

## 1. Giriş

### 1.1 Ödevin Amacı

Bu çalışmanın amacı, emlak ilanları arasındaki metinsel benzerlikleri doğal dil işleme yöntemleri kullanarak tespit etmek ve farklı metin temsil tekniklerinin performanslarını karşılaştırmaktır. Günümüzde emlak platformlarında binlerce ilan bulunmakta ve kullanıcıların benzer özelliklere sahip ilanları bulması giderek zorlaşmaktadır. Bu nedenle metin tabanlı benzerlik sistemleri önemli bir ihtiyaç haline gelmiştir.

Bu proje kapsamında emlak ilanları üzerinde TF-IDF ve Word2Vec yöntemleri uygulanarak benzer ilanların belirlenmesi amaçlanmıştır. Ayrıca farklı model yapılandırmalarının sonuçları karşılaştırılmış, elde edilen çıktılar semantik açıdan değerlendirilmiş ve modeller arasındaki tutarlılık analiz edilmiştir.

### 1.2 Kullanılan Veri Seti

Çalışmada emlak ilanlarından oluşan bir veri seti kullanılmıştır. Veri seti `emlakodev.csv` dosyasında yer almaktadır. Her kayıt bir emlak ilanına ait metinsel açıklamaları içermektedir.

Veri seti üzerinde analiz yapılabilmesi için çeşitli ön işleme adımları uygulanmıştır. Bu işlemler sonucunda:

* Lemmatize edilmiş metinler
* Stem edilmiş metinler

ayrı veri kümeleri halinde hazırlanmıştır.

### 1.3 Kullanılan Teknolojiler

Projede aşağıdaki teknolojiler ve kütüphaneler kullanılmıştır:

* Python
* Pandas
* NLTK
* Gensim
* Scikit-Learn
* Zeyrek
* Snowball Stemmer
* Jupyter Notebook

## 2. Veri Ön İşleme Süreci

Makine öğrenmesi modellerinin daha sağlıklı sonuçlar üretebilmesi amacıyla veri setine çeşitli ön işleme adımları uygulanmıştır.

Bu işlemler:

* Metinlerin küçük harfe dönüştürülmesi
* Noktalama işaretlerinin temizlenmesi
* Kelimelere ayrıştırma (Tokenization)
* Durak kelimelerin temizlenmesi
* Kök bulma işlemi (Stemming)
* Lemmatizasyon

şeklindedir.

Bu işlemler sonucunda elde edilen veri kümeleri daha sonra TF-IDF ve Word2Vec modellerinin eğitilmesinde kullanılmıştır.

## 3. Kullanılan Yöntemler

### 3.1 TF-IDF

TF-IDF (Term Frequency - Inverse Document Frequency), bir kelimenin doküman içerisindeki önemini ölçmek amacıyla kullanılan bir yöntemdir.

Bu çalışmada ilan metinleri TF-IDF yöntemi kullanılarak sayısal vektörlere dönüştürülmüştür. Daha sonra ilanlar arasındaki benzerlikler Kosinüs Benzerliği yöntemi ile hesaplanmıştır.

TF-IDF analizi iki farklı veri kümesi üzerinde gerçekleştirilmiştir:

* Lemmatized veri seti
* Stemmed veri seti

### 3.2 Word2Vec

Word2Vec yöntemi kelimeleri anlamsal ilişkilerine göre vektör uzayında temsil etmektedir.

Projede CBOW ve Skip-Gram mimarileri kullanılarak farklı parametre kombinasyonlarında modeller oluşturulmuştur.

Kullanılan parametreler:

| Parametre     | Değerler            |
| ------------- | ------------------- |
| Mimari        | CBOW, Skip-Gram     |
| Window        | 2, 4                |
| Vektör Boyutu | 100, 300            |
| Veri Türü     | Stemmed, Lemmatized |

Bu kombinasyonlar sonucunda toplam 16 farklı Word2Vec modeli oluşturulmuş ve her model için benzerlik hesaplamaları gerçekleştirilmiştir.

## 4. Değerlendirme Yöntemleri

### 4.1 Semantik Değerlendirme

Her model tarafından önerilen benzer ilanlar içerik bakımından incelenmiş ve aşağıdaki ölçeğe göre puanlandırılmıştır.

| Puan | Anlamı   |
| ---- | -------- |
| 1    | Çok Kötü |
| 2    | Kötü     |
| 3    | Orta     |
| 4    | İyi      |
| 5    | Çok İyi  |

Bu değerlendirme sayesinde modellerin yalnızca matematiksel benzerlik değil, anlamsal benzerlik açısından da performansları karşılaştırılmıştır.

### 4.2 Jaccard Benzerlik Analizi

Farklı modellerin ürettiği ilk beş sonuç karşılaştırılarak Jaccard Benzerliği hesaplanmıştır.

Bu analiz sayesinde:

* Modeller arasındaki tutarlılık,
* Benzer sonuç üreten modeller,
* Birbirinden farklı davranan modeller

tespit edilmiştir.

## 5. Bulgular ve Sonuç

Yapılan analizler sonucunda TF-IDF ve Word2Vec yöntemlerinin emlak ilanları arasında benzerlik belirlemede başarılı sonuçlar ürettiği gözlemlenmiştir. Özellikle Word2Vec modelleri anlamsal ilişkileri dikkate aldığı için bazı durumlarda TF-IDF yöntemine göre daha anlamlı eşleşmeler oluşturmuştur.

Semantik değerlendirme sonuçları ve Jaccard analizleri birlikte incelendiğinde, farklı parametrelerle eğitilen modeller arasında belirli düzeylerde benzerlikler olduğu görülmüştür. Bununla birlikte bazı modeller daha çeşitli sonuçlar üretmiş ve farklı ilanları öne çıkarmıştır.

Genel olarak proje, doğal dil işleme yöntemlerinin emlak ilanlarının eşleştirilmesinde etkili bir şekilde kullanılabileceğini göstermiştir. Elde edilen sonuçlar, benzer ilan öneri sistemlerinin geliştirilmesinde kullanılabilecek önemli bilgiler sağlamaktadır.

### Kullanılan Dosyaların Paylaşımı

Proje kapsamında kullanılan bazı veri ve model dosyaları yüksek boyutlu olduğundan GitHub deposuna yüklenememiştir. Bu nedenle gerekli dosyalar Google Drive üzerinden paylaşılmıştır. Projeyi incelemek veya yeniden çalıştırmak isteyen kullanıcılar ilgili Drive bağlantısından dosyaları indirerek proje klasörüne ekleyebilirler.

Drive bağlantısı:
[https://drive.google.com/drive/folders/1Ia2ES9RHUAqS6TDlZNPg3BeCDVidI8HJ?usp=drive_link]


