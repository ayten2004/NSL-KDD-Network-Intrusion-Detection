# NSL-KDD Network Intrusion Detection

Ağ trafiği verilerini analiz edip siber saldırıları (DoS, Probe, R2L, U2R) tespit etmeye çalıştığım bir proje. Lojistik regresyon ve istatistiksel anomali analizi üzerine kurulu.

## Ne yaptım
1. Eksik değerleri kontrol ettim, kategorik değişkenleri Label Encoding ile sayısallaştırdım.
2. Değişkenleri Z-skoru ile (StandardScaler) ölçeklendirdim.
3. Önce Normal/Saldırı ayrımı için ikili bir lojistik regresyon kurdum — %96.44 doğruluk çıktı.
4. Sonra saldırı türlerine göre çok sınıflı bir model kurdum, `class_weight='balanced'` ile dengesiz veri setini idare etmeye çalıştım.

## Sonuçlar

### İkili sınıflandırma (Normal vs. Saldırı)
| Metrik | Değer |
|---|---|
| Accuracy | %96 |
| Precision (macro avg) | 0.96 |
| Recall (macro avg) | 0.96 |
| F1-Score (macro avg) | 0.96 |

### Çok sınıflı sınıflandırma
| Sınıf | Precision | Recall | F1-Score | n |
|---|---|---|---|---|
| DoS | 0.99 | 1.00 | 0.99 | 9181 |
| Normal | 1.00 | 0.97 | 0.98 | 13422 |
| Probe | 0.89 | 0.98 | 0.93 | 2357 |
| R2L | 0.78 | 0.98 | 0.87 | 224 |
| U2R | 0.13 | 0.55 | 0.21 | 11 |
| **Accuracy** | | | **0.98** | 25195 |
| Macro avg | 0.76 | 0.89 | 0.80 | 25195 |
| Weighted avg | 0.98 | 0.98 | 0.98 | 25195 |

Genel accuracy %98 ama bu sayı tek başına biraz yanıltıcı, çünkü sınıflar arasında ciddi dengesizlik var. Asıl dikkat çekici olan R2L'de recall'un %98'e çıkması: nadir görülen bu saldırı türünü model neredeyse hiç kaçırmamış. U2R'de durum daha karışık — precision sadece 0.13, çünkü veri setinde yalnızca 11 örnek var ve bunlar normal trafiğe oldukça benziyor. Yine de `class_weight='balanced'` sayesinde bu 11 örneğin yarısından fazlasını (%55) doğru yakalamış. Yani model bir nevi temkinli: şüpheli bir şey gördüğünde "saldırı" demeyi tercih ediyor, ki güvenlik açısından yanlış negatiften daha iyi bir hata türü.

![Confusion Matrix](confusion_matrix.png)

## Kullandıklarım
Python, Pandas, Scikit-learn, Seaborn.
