# Amazon Zaman Serisi Analizi

Bu klasörde, Amazon hisse senedi fiyatlarının zaman serisi analizi yapılmaktadır. Analiz kapsamında temel istatistiksel incelemeler, durağanlık testleri, trend ve mevsimsellik ayrıştırması, ARIMA ve SARIMA gibi modellerle tahmin ve model karşılaştırmaları yer almaktadır.

## İçerik
- `zamansal_seri_analizi.ipynb`: Tüm analiz adımlarını ve kodları içeren Jupyter not defteri.
- `../Amazon_stock_data.csv`: Kullanılan ham veri dosyası.

## Adımlar
1. **Veri Yükleme ve Ön İşleme**: Ham verinin yüklenmesi, tarih formatı ve eksik veri işlemleri.
2. **Görselleştirme**: Kapanış fiyatlarının zaman içindeki değişimi.
3. **Durağanlık Testi**: ADF testi ile serinin durağanlığının kontrolü.
4. **Durağanlık Sağlama**: Gerekirse birinci fark alma işlemi.
5. **Trend ve Mevsimsellik Analizi**: Decomposition ile serinin bileşenlerine ayrılması.
6. **Modelleme**: ARIMA ve SARIMA ile tahmin.
7. **Model Karşılaştırması**: Son 10 gün için tahminlerin ve hata metriklerinin karşılaştırılması.

## Kullanım
1. Gerekli Python kütüphanelerini yükleyin (`pandas`, `matplotlib`, `statsmodels`, `scikit-learn`).
2. Not defterini açın ve hücreleri sırasıyla çalıştırın.
3. Sonuçları grafikler ve metrikler üzerinden inceleyin.

## Notlar
- Veri dosyasının yolunun doğru olduğundan emin olun ("../Amazon_stock_data.csv").
- Analiz, örnek veriyle yapılmıştır. Kendi verinizle de aynı adımları uygulayabilirsiniz.

