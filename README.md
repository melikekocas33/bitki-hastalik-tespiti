# Bitki Hastalık Tespiti

Bu projede PlantVillage veri seti kullanılarak yaprak görüntülerinden bitki hastalığı sınıflandırması yapılmıştır.

# Projenin Amacı

Bu çalışmanın amacı, yaprak görüntülerinden bitkinin hangi sınıfa ait olduğunu ve hastalık durumunu tespit eden bir derin öğrenme modeli geliştirmektir.
Model, yaprak görüntülerini analiz ederek sağlıklı ve hastalıklı bitki sınıflarını ayırt etmektedir.

# Kullanılan Teknolojiler

- Python
- TensorFlow / Keras
- Google Colab
- MobileNetV2
- Transfer Learning
- PlantVillage veri seti

# Kullanılan Yöntem

Bu projede transfer learning yöntemi kullanılmıştır. Önceden ImageNet veri seti üzerinde eğitilmiş MobileNetV2 modeli temel alınmış ve bu modelin üzerine projeye özel sınıflandırma katmanları eklenmiştir.

Model yapısında Dense, Dropout ve BatchNormalization katmanları kullanılmıştır.

# Veri Seti

Projede PlantVillage veri seti kullanılmıştır. Veri setinde 15 farklı sınıfa ait yaprak görüntüleri bulunmaktadır.

# Model Eğitimi

Model Google Colab ortamında T4 GPU kullanılarak eğitilmiştir. Eğitim sürecinde veri seti eğitim ve doğrulama verisi olarak ayrılmıştır.

Model 10 epoch boyunca eğitilmiştir.

# Sonuçlar

Elde edilen sonuçlar:

- Eğitim doğruluğu: %88.88
- Doğrulama doğruluğu: %91.25
- Doğrulama kaybı: 0.2517

## Grafik Yorumu

Accuracy grafiğinde eğitim ve doğrulama başarılarının epoch sayısı arttıkça yükseldiği görülmektedir. Loss grafiğinde ise hata değerlerinin düzenli olarak azaldığı gözlemlenmiştir. Bu sonuçlar modelin öğrenme gerçekleştirdiğini ve doğrulama verisi üzerinde başarılı bir genelleme yapabildiğini göstermektedir.

## Proje Dosyaları

Bu repoda projeye ait Google Colab notebook dosyası yer almaktadır.
- `Bitki_Hastalik_Tespiti_MobileNetV2.ipynb`

## Not

Veri seti boyutu büyük olduğu için GitHub reposuna yüklenmemiştir. Çalışmada Kaggle üzerinde bulunan PlantVillage veri seti kullanılmıştır.
