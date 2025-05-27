# 🏭 Makine Arızası Tahmini - AI4I 2020 Dataset Analizi

Bu projede, üretim hattındaki makinelerde meydana gelebilecek arızaları önceden tahmin edebilmek amacıyla **AI4I 2020 Predictive Maintenance** veri seti üzerinde kapsamlı bir veri analizi ve makine öğrenmesi uygulaması gerçekleştirilmiştir.

---

## 🔍 Proje Hedefi

- Arıza türlerini (Takım Aşınması, Isı Dağılımı, Güç Kesintisi, Aşırı Zorlanma, Rastgele Arıza) belirlemek
- Makine arızasını etkileyen parametreleri analiz etmek
- Makine arızalarını sınıflandırmak ve tahmin etmek için en iyi modeli belirlemek
- Zaman ve doğruluk bazlı performans karşılaştırmaları yapmak

---

## 📊 Kullanılan Veri Seti

- **Kaynak**: AI4I 2020 - Predictive Maintenance Dataset
- **Özellikler**:
  - İşlem ve hava sıcaklığı
  - Dönme hızı (rpm)
  - Tork (Nm)
  - Alet aşınması süresi (dk)
  - Ürün tipi (H, M, L)
  - Arıza türleri (0/1): `TAA`, `IDA`, `GK`, `AZA`, `RA`
  - Hedef değişken: `Makine Arızası`

---

## 🔬 Yapılan İşlemler

### 1. 📌 Veri Ön İşleme
- Eksik verilerin kontrolü
- Aykırı değer tespiti: Z-Score ve IQR yöntemleri
- Veri ölçekleme ve istatistiksel özetleme

### 2. 📈 Keşifsel Veri Analizi (EDA)
- Ürün tipine göre arıza oranları
- Parametreler ile arıza türleri arasındaki korelasyon
- Korelasyon matrisi ve ısı haritaları ile görselleştirme

### 3. ⚙️ Özellik Mühendisliği
- Her arıza türü için özel kurallar tanımlanarak sınıflar oluşturuldu:
  - **TAA**: Alet aşınması 200–240 dk arası
  - **IDA**: Isı farkı > 8.6°C ve dönüş hızı < 1380 rpm
  - **GK**: Güç 3500–9000 Wh arası
  - **AZA**: Tork ve aşınma eşiği ürün tipine göre kontrol
  - **RA**: Rastgele %10 oranla eklenen arızalar

---

## 🧠 Kullanılan Modeller

| Model                  | Accuracy | Recall | Precision | F1 Score | MCC   | Train Time (s) | Predict Time (s) |
|------------------------|---------:|-------:|----------:|---------:|------:|---------------:|-----------------:|
| Logistic Regression    | 0.9200   | 0.3366 | 0.7234    | 0.4595   | 0.08  | 0.00           | 0.08             |
| Decision Tree          | 0.9920   | 0.9740 | 0.9500    | 0.9620   | 0.97  | 0.03           | 0.03             |
| Random Forest          | 0.9925   | 0.9459 | 0.9845    | 0.9621   | 0.96  | 0.02           | 0.02             |
| Gradient Boosting      | 0.9935   | 0.9455 | 0.9860    | 0.9659   | 0.96  | 0.01           | 0.01             |
| SVM                    | 0.8990   | 0.0000 | 0.0000    | 0.0000   | 0.00  | 0.24           | 0.74             |
| KNN                    | 0.9345   | 0.5247 | 0.7518    | 0.6108   | 0.59  | 0.01           | 0.10             |
| LSTM (Neural Network)  | 0.9710   | 0.8218 | 0.8829    | 0.8513   | 0.83  | 5.78           | 6.23             |

---

## 🎯 Hiperparametre Optimizasyonu

`GradientBoostingClassifier` için 5 farklı hiperparametre seti ile `GridSearchCV` kullanılarak eğitim yapıldı:

- Basit ve Genel Optimizasyon
- Daha Fazla Öğrenme
- Hızlı Öğrenme
- Denge ve Budama
- Daha Yaratıcı ve Geniş Optimizasyon

Her set için:
- **Eğitim süresi**
- **Doğruluk, F1 Skoru, MCC**
- **Confusion Matrix** görselleri oluşturuldu

---

## 📊 Görselleştirmeler

- Arıza türlerine göre dağılım grafikleri
- Korelasyon ısı haritaları
- Performans metriklerinin çizgi ve çubuk grafiklerle karşılaştırılması

---

## 📌 Sonuçlar

- **Gradient Boosting** ve **Random Forest**, en yüksek doğruluk ve MCC skorlarını sağladı.
- **LSTM**, daha yüksek doğruluk sunmasına rağmen yüksek eğitim ve tahmin süresine sahip.
- **SVM** modelinin başarısı, veri setindeki dengesizlikten etkilenmiştir.
- **En yüksek başarı** Gradient Boosting ile hiperparametre optimizasyonu yapılan modellerden elde edilmiştir (`Accuracy ≈ 0.995`).

---