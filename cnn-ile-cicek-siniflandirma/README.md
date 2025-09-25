# CNN-ile-cicek-siniflandirma
## Projenin Amacı

Bu projenin amacı, derin öğrenme tabanlı bir Convolutional Neural Network (CNN) modeliyle farklı çiçek türlerini görselden otomatik olarak ayırt edebilen bir sınıflandırıcı geliştirmektir. Görsel veriler üzerinde temel veri ön işleme, augmentasyon ve modern derin öğrenme yöntemleri kullanılarak yüksek doğrulukta tahmin yapılması hedeflenmiştir.  Bu tür bir model; botanik araştırmaları, tarım uygulamaları veya eğitim amaçlı kullanılabilir. İleride bu ve benzeri modeller kullanılarak çiçek görsellerinden elde edilen verilerle tanımlama yapmayı ve bitki bakımını kolaylaştırmayı sağlayan bir uygulama tasarlanabilir.

## Veri Seti Hakkında Bilgi

Kullanılan veri seti, Kaggle’da barındırılan ve her klasörü farklı bir çiçek türüne karşılık gelen **Flowers Recognition** veri setidir. Veri seti:

- 5 farklı çiçek türü içerir (ör: Daisy, Dandelion, Rose, Sunflower, Tulip).
- Dosya yolu: `/kaggle/input/flowers-recognition/flowers`
- Her alt klasör bir çiçek türünü, içindeki dosyalar da o türe ait görselleri temsil eder.

## Kullanılan Yöntemler

- **Veri ön işleme:** Görseller 150x150 boyutuna ölçeklendi. Piksel değerleri 0-1 aralığına normalize edildi.
- **Veri artırma (Augmentation):** Eğitimin daha sağlam ve verimli olması için görsellere döndürme, kaydırma, zoom, yatay çevirme gibi işlemler uygulandı.
- **Model mimarisi:**
    - 3 adet Conv2D + MaxPooling katmanı
    - Bir sıralı (Sequential) model yapısı
    - Dropout katmanı ile aşırı öğrenmenin önlenmesi
    - Çıkış katmanında softmax aktivasyonu
- **Eğitim:**
    - Adam optimizer ve categorical_crossentropy loss fonksiyonu kullanıldı
    - EarlyStopping ve ReduceLROnPlateau callback’leri ile eğitim süreci optimize edildi
    - Model, eğitim/validasyon seti olarak rastgele %80/%20 ayrımla eğitildi
    - Model 20 epoch boyunca eğitildi.

## Elde Edilen Sonuçlar

Model eğitimi sonucunda:

- Eğitim ve doğrulama doğruluk değerleri çizgi grafiklerle görselleştirildi.
- Sınıflar bazında precision, recall ve f1-score değerleri raporlandı.
- Karışıklık matrisi (confusion matrix) ile modelin hangi sınıfları daha çok karıştırdığı analiz edildi.
- Ortalama doğruluk yaklaşık %74 civarında çıktı; modelin performansı iyileştirilebilir.
- Yanlış tahmin edilen örnek görseller, gerçek ve tahmini etiketleri ile birlikte görselleştirildi.
- Aşağıda örnek bir sonuç özeti:
    - Doğrulama başarı oranı: **%92.50** (örnek)
    - En çok karıştırılan türler: Daisy ↔ Dandelion
    - Model, yeterli sayıda epoch'ta overfitting yapmadı ve istikrarlı doğruluk sağladı.
    
    ## Doğrulama Sonuç Özeti
    
    - **Doğrulama başarı oranı**: %74
    - **Sınıf bazında başarılar**:
        - **Daisy**: Precision %87, recall %72, f1-score %79. Modelin en iyi tanıdığı ve başarı oranı en yüksek sınıf.
        - **Dandelion**: Precision %79, recall %78, f1-score %78. Dandelion için model oldukça tutarlı.
        - **Rose**: Precision %61, recall %64, f1-score %62. Rose sınıfı diğerlerine göre daha zor ayırt edilebiliyor.
        - **Sunflower**: Precision %71, recall %89, f1-score %79. Sunflower tahmininde yüksek recall ve dengeli bir başarı mevcut.
        - **Tulip**: Precision %74, recall %67, f1-score %70. Ortalama bir başarı görülüyor.
    - **Macro ve weighted ortalamalar**: Hepsi %74 civarında ve benzer, modelin genel sınıf dengesinin iyi olduğunu gösteriyor.
    
    ## Modelin Güçlü ve Zayıf Yönleri
    
    **Güçlü Yönler**
    
    - Daisy ve sunflower gibi bazı sınıfları f1-score açısından oldukça yüksek doğrulukla tanıyor.
    - Hiçbir sınıfta çok düşük (örneğin %50’nin altında) başarı gözlenmiyor.
    - Modelin genel doğruluk ve dengesi oldukça iyi, overfitting problemi gözlenmiyor.
    
    **Zayıf Yönler**
    
    - Rose ve tulip sınıflarında model diğerlerine oranla daha düşük başarıda; bu türlerde veri çeşitliliği artırılabilir veya ek regularizasyon denenebilir.
    - Arka plan, renk ve tür benzerliğinden kaynaklanan karışıklıklar söz konusu olabilir.
    
    ## Geliştirme İpuçları
    
    - Model mimarisi daha derin ve karmaşık hale getirilebilir veya transfer learning ile önceden eğitilmiş modeller kullanılabilir.
    - Görsel veri artırımı (augmentation) çeşitliliği ve miktarı geliştirilebilir.
    - Özellikle düşük f1-score’a sahip sınıflarda (rose ve tulip) daha fazla örnek ile veri dengesizliği giderilebilir.
    - Model çıktıları detaylı olarak analiz edilip, benzer türlerin ayrımı için yeni ön işleme teknikleri uygulanabilir.
    
    ---
    

## Kaggle Notebook Linki : https://www.kaggle.com/code/azradavut/cnn-ile-cicek-siniflandirma
