# Diyabet Tahmini: Veri Ön İşleme ve Topluluk Öğrenme (Ensemble Learning) Analizi

Bu proje, Pima Indians Diabetes veri seti üzerinde eksik verilerin yönetimi (Medyan Doldurma vs. Satır Silme) ve farklı makine öğrenmesi modellerinin performans karşılaştırmasını içermektedir. Projenin ana odağı **AdaBoost** algoritmasıdır.

## Projenin Amacı
Veri setindeki "0" olarak girilmiş hatalı/eksik verilerin (Glikoz, İnsülin, vb.) iki farklı yöntemle ele alınmasının model başarısı üzerindeki etkisini ölçmek:
1. **Medyan Doldurma (Imputation):** Veri bütünlüğünü korumak için eksikleri orta değerle doldurmak.
2. **Satır Silme (Dropping):** Gürültüyü azaltmak için eksik verili satırları tamamen veri setinden çıkarmak.

## Kullanılan Teknolojiler
- **Dil:** Python
- **Kütüphaneler:** Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn
- **Modeller:** AdaBoost, Random Forest, SVC, Logistic Regression

## Deney Sonuçları (Accuracy)

| Model | Medyan Doldurma (Ham) | Satır Silme (Ham) | En İyi (Tuning Sonrası) |
| :--- | :---: | :---: | :---: |
| **AdaBoost** | %75.32 | %74.68 | **%75.56** (Medyan) |
| **Random Forest** | %72.07 | %78.48 | %77.67 (Drop) |
| **SVC** | %74.67 | %73.41 | **%79.26** (Drop) |
| **Logistic Reg.** | %75.32 | %77.21 | - |

##  Algoritma İncelemesi: AdaBoost
AdaBoost (Adaptive Boosting), "zayıf öğrenicileri" (genellikle **decision stumps**) bir araya getirerek güçlü bir model oluşturur.



### Çalışma Mantığı:
1. Her veri noktasına başlangıçta eşit ağırlık verilir.
2. İlk zayıf model eğitilir.
3. Yanlış tahmin edilen örneklerin ağırlığı artırılır, doğru tahmin edilenlerin azaltılır.
4. Bu süreç iteratif olarak devam eder ve modellerin ağırlıklı toplamıyla nihai tahmin yapılır.

## 📝 Sonuç ve Değerlendirme
- **Veri Temizliği:** Satırları silmek (Drop), veri setini küçültmesine rağmen SVC ve Random Forest gibi modellerde daha yüksek "Accuracy" sağlamıştır. Bu durum, gürültülü verinin temizlenmesinin modelin karar sınırlarını (hyperplane) daha net çizmesine yardımcı olduğunu gösterir.
- **AdaBoost Performansı:** AdaBoost, medyan ile doldurulmuş (daha büyük) veri setinde daha stabil bir performans sergilemiştir. Hiperparametre optimizasyonu (`learning_rate: 1.0`, `n_estimators: 100`) ile başarısı %75.56'ya yükseltilmiştir.
- **En İyi Model:** Deney sonucunda elde edilen en yüksek başarı oranı, silinmiş veri seti üzerinde optimize edilen **SVC (%79.26)** modeline aittir.

