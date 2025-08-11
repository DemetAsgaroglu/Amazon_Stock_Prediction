# Amazon Stock Price Prediction 📈

Bu proje, Amazon'un geçmiş hisse senedi verilerini kullanarak **ertesi günün kapanış fiyatını** tahmin etmek için makine öğrenmesi algoritmalarını karşılaştırır.

## 🎯 Proje Amacı
Bu proje, finansal piyasalarda makine öğrenmesi tekniklerinin etkinliğini araştırmak ve farklı algoritmaların hisse senedi fiyat tahminindeki performanslarını karşılaştırmak amacıyla geliştirilmiştir. Proje, Amazon hisse senedinin tarihsel verilerini analiz ederek, teknik göstergeler ve özellik mühendisliği yöntemleriyle gelecekteki fiyat hareketlerini tahmin etmeye odaklanır.

## 📊 Veri Seti Detayları
- **Kaynak**: Amazon (AMZN) hisse senedi geçmiş verileri
- **Özellikler**: 
  - `Open`: Günün açılış fiyatı
  - `High`: Günün en yüksek fiyatı
  - `Low`: Günün en düşük fiyatı
  - `Close`: Günün kapanış fiyatı (hedef değişken)
  - `Volume`: Günlük işlem hacmi
- **Zaman Aralığı**: Günlük veriler
- **Veri Boyutu**: [Veri setinizin boyutunu buraya ekleyin]
- **Hedef Değişken**: Ertesi günün kapanış fiyatı (Close_t+1)

## 🔧 Özellik Mühendisliği (Feature Engineering)

Modelin tahmin gücünü artırmak için orijinal verilere ek özellikler eklenmiştir:

### Teknik Göstergeler
- **Daily_Change**: `(Close - Open) / Open` - Günlük fiyat değişim yüzdesi
- **Volume_Change**: `Volume.pct_change()` - Hacim değişim yüzdesi
- **Volatility**: `High - Low` - Gün içi fiyat dalgalanması
- **High_Low_Pct**: `(High - Low) / Close` - Gün içi volatilite oranı
- **Open_Close_Pct**: `(Close - Open) / Open` - Açılış-kapanış fiyat oranı

### Zaman Serisi Özellikleri
- **Close_Lag1**: 1 gün önceki kapanış fiyatı
- **Close_Lag2**: 2 gün önceki kapanış fiyatı
- **Volume_Lag1**: 1 gün önceki işlem hacmi

### Hareketli Ortalamalar
- **MA_5**: 5 günlük basit hareketli ortalama
- **MA_10**: 10 günlük basit hareketli ortalama

> **Not**: Veri sızıntısını (data leakage) önlemek için tüm özellikler geçmiş verileri kullanarak oluşturulmuştur.

## 🤖 Kullanılan Modeller ve Yöntemler

### 1. Linear Regression
- **Açıklama**: Basit doğrusal regresyon modeli
- **Avantajlar**: Hızlı, yorumlanabilir, trend yakalama yeteneği
- **Kullanım Alanı**: Baseline model olarak

### 2. Random Forest Regressor
- **Açıklama**: Ensemble ağaç tabanlı algoritma
- **Hiperparametre Optimizasyonu**: GridSearchCV ile
- **Parametreler**: 
  - `n_estimators`: [100, 200]
  - `max_depth`: [10, 20]
  - `min_samples_split`: [2, 5]
  - `max_features`: ['sqrt', None]

### 3. XGBoost Regressor
- **Açıklama**: Gradient boosting algoritması
- **Hiperparametre Optimizasyonu**: GridSearchCV ile
- **Parametreler**:
  - `n_estimators`: [100, 200]
  - `max_depth`: [3, 6]
  - `learning_rate`: [0.1, 0.2]
  - `subsample`: [0.8, 1.0]

### Veri Ön İşleme
- **Standardizasyon**: StandardScaler kullanılarak feature scaling
- **Zaman Serisi Bölme**: Shuffle=False ile kronolojik sırayı koruma
- **Train-Test Oranı**: %70 - %30

## 📈 Sonuçlar ve Performans Analizi

### Model Performansları

Model Karşılaştırması:
Model                MAE        RMSE       R2        
LinearRegression     1.8846     2.7731     0.9967
RandomForest         84.6492     97.6093     -3.0318
XGBoost              85.2862     98.2208     -3.0824

### Temel Bulgular
- **🏆 En İyi Model**: Linear Regression (R² ≈ 0.997)
- **📊 Performans Sıralaması**: Linear Regression > Random Forest > XGBoost
- **💡 Önemli Bulgu**: Hisse senedi verilerinde Linear modeller ağaç tabanlı modellerden daha başarılıdır

### Analiz ve Yorumlar
1. **Linear Regression Üstünlüğü**: 
   - Hisse senedi verilerinin güçlü trend özelliği göstermesi
   - Linear modellerin extrapolation (trend devam ettirme) yeteneği
   
2. **Ağaç Tabanlı Model Sınırlamaları**:
   - Extrapolation yapamama sorunu
   - Yeni veri noktalarında sadece eğitim setindeki değerleri tekrarlama

3. **Feature Engineering Etkisi**:
   - Lag features ve moving averages modelin performansını artırdı
   - Teknik göstergeler trend yakalamada etkili oldu

## 🛠️ Kurulum ve Kullanım

### Sistem Gereksinimleri
- Python 3.8 veya üzeri
- Jupyter Notebook
- Git (opsiyonel)

### Gerekli Kütüphaneler

**Manuel kurulum:**
```bash
pip install pandas>=1.3.0 numpy>=1.21.0 matplotlib>=3.4.0 seaborn>=0.11.0 scikit-learn>=1.0.0 xgboost>=1.5.0 jupyter>=1.0.0
```

### Adım Adım Kullanım

1. **Repository'yi klonlayın:**
```bash
git clone [repository-url]
cd Amazon_Stock_Prediction
```

2. **Veri dosyasını kontrol edin:**
   - `Amazon_stock_data.csv` dosyasının proje klasöründe olduğundan emin olun

3. **Jupyter Notebook'u başlatın:**
```bash
jupyter notebook
```

4. **Analizi çalıştırın:**
   - `amazon_stock_prediction_analysis.ipynb` dosyasını açın
   - Hücreleri sırayla çalıştırın (Shift + Enter)

### Beklenen Çıktılar
- Veri görselleştirmeleri (fiyat grafikleri, hacim analizi)
- Model performans metrikleri
- Hyperparameter tuning sonuçları
- Model karşılaştırma tabloları

## 📁 Proje Yapısı
```
Amazon_Stock_Prediction/
├── 📓 amazon_stock_prediction_analysis.ipynb    # Ana analiz notebook'u
├── 📊 Amazon_stock_data.csv                     # Amazon hisse senedi veri seti
├── 📋 requirements.txt                          # Python kütüphane gereksinimleri
├── 📄 README.md                                 # Proje dokümantasyonu
└── 📜 .gitignore                                # Git ignore dosyası
```

### Notebook İçeriği
1. **Veri Keşfi**: İlk analiz ve görselleştirmeler
2. **Veri Ön İşleme**: Tarih dönüşümü, eksik veri kontrolü
3. **Feature Engineering**: Yeni özelliklerin oluşturulması
4. **Modelleme**: 3 farklı algoritmanın uygulanması
5. **Hiperparametre Optimizasyonu**: GridSearchCV ile model iyileştirme
6. **Performans Analizi**: Detaylı model karşılaştırması
7. **Sonuç ve Değerlendirme**: Bulgular ve öneriler


## 📊 Model Değerlendirme Metrikleri

### Kullanılan Metrikler
- **MAE (Mean Absolute Error)**: Ortalama mutlak hata
- **RMSE (Root Mean Square Error)**: Kök ortalama kare hata
- **R² Score**: Belirlilik katsayısı (0-1 arası, 1'e yakın daha iyi)

### Metrik Seçim Nedenleri
- **MAE**: Outlier'lara daha az duyarlı, yorumlanması kolay
- **RMSE**: Büyük hataları cezalandırır, model karşılaştırması için uygun
- **R²**: Modelin açıklama gücünü gösterir


---

## 📝 Son Notlar

Bu proje, makine öğrenmesi ve finansal analiz konularında öğrenme amacıyla geliştirilmiştir. **Gerçek yatırım kararları için kullanılmamalıdır.**

**⭐ Projeyi beğendiyseniz yıldız vermeyi unutmayın!**

---
*Son güncelleme: Temmuz 2025*
