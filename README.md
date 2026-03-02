# NSL-KDD-Network-Intrusion-Detection
Siber saldırı tespiti için Lojistik Regresyon ve istatistiksel anomali analizi projesi.
# NSL-KDD Network Intrusion Detection Project

Bu proje, ağ trafiği verilerini analiz ederek siber saldırıları (DoS, Probe, R2L, U2R) tespit eden bir makine öğrenmesi modelidir.

## Proje Aşamaları
1. **İstatistiksel Veri Temizliği:** Eksik değer kontrolü ve kategorik değişkenlerin Label Encoding yöntemiyle sayısallaştırılması.
2. **Ölçeklendirme:** Değişkenlerin $Z$-skoru standardizasyonu (StandardScaler) ile normalize edilmesi.
3. **Anomali Tespiti:** Lojistik Regresyon ile %96.44 başarı oranına sahip ikili sınıflandırma.
4. **Saldırı Türü Sınıflandırması:** Çok sınıflı (Multinomial) model ve `class_weight='balanced'` stratejisi ile dengesiz veri seti yönetimi.

## Model Başarısı
Model, genel klasmanda **%98 accuracy** oranına ulaşmıştır. 

![Confusion Matrix](confusion_matrix.png)

## Kullanılan Teknolojiler
* Python (Pandas, Scikit-learn, Seaborn)
* İstatistiksel Analiz (Logit Model, Feature Scaling)
