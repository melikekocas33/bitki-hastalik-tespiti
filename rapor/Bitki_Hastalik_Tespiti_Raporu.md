# Bitki Hastalık Tespiti Proje Raporu

# 1. Projenin Amacı

Bu projenin amacı, yaprak görüntülerinden bitkinin hangi sınıfa ait olduğunu ve hastalık durumunu tespit eden bir derin öğrenme modeli geliştirmektir. Çalışmada bitki yapraklarına ait görüntüler kullanılarak sağlıklı ve hastalıklı sınıfların otomatik olarak sınıflandırılması hedeflenmiştir.

Tarım alanında bitki hastalıklarının erken tespiti, ürün kaybını azaltmak ve doğru müdahale yöntemlerini belirlemek açısından önemlidir. Bu nedenle görüntü işleme ve derin öğrenme yöntemleri kullanılarak yaprak hastalıklarının tespiti yapılmıştır.

# 2. Kullanılan Veri Seti

Projede PlantVillage veri seti kullanılmıştır. Veri seti ders kapsamında öğretim elemanı tarafından paylaşılmıştır.

Veri setinde farklı bitkilere ait sağlıklı ve hastalıklı yaprak görüntüleri bulunmaktadır. Bu çalışmada toplam 15 sınıf üzerinden sınıflandırma yapılmıştır. Sınıflar içerisinde biber, patates ve domates bitkilerine ait sağlıklı ve hastalıklı yaprak görüntüleri yer almaktadır.

Örnek sınıflar:

- Pepper bell Bacterial spot
- Pepper bell healthy
- Potato Early blight
- Potato Late blight
- Potato healthy
- Tomato Bacterial spot
- Tomato Early blight
- Tomato Late blight
- Tomato Leaf Mold
- Tomato Septoria leaf spot
- Tomato healthy

Veri seti boyutu büyük olduğu için GitHub reposuna doğrudan eklenmemiştir. Çalışmada öğretim elemanı tarafından paylaşılan PlantVillage veri seti kullanılmıştır.

# 3. Kullanılan Teknolojiler

Projede kullanılan başlıca teknolojiler şunlardır:

- Python
- TensorFlow / Keras
- Google Colab
- T4 GPU
- MobileNetV2
- Transfer Learning
- Matplotlib
- PlantVillage veri seti

# 4. Kullanılan Yöntem

Bu projede ilk olarak temel CNN mimarisi denenmiştir. Ancak temel CNN modeli düşük doğruluk değerlerinde kaldığı için daha başarılı sonuç elde etmek amacıyla transfer learning yöntemi tercih edilmiştir.

Transfer learning yönteminde, daha önce büyük bir veri seti üzerinde eğitilmiş hazır bir model kullanılır. Bu projede ImageNet veri seti üzerinde önceden eğitilmiş MobileNetV2 modeli temel alınmıştır.

MobileNetV2 modeli üzerine projeye özel sınıflandırma katmanları eklenmiştir. Bu katmanlar:

- GlobalAveragePooling2D
- BatchNormalization
- Dense
- Dropout
- Softmax çıkış katmanı

şeklindedir.

Modelin son katmanında 15 sınıf için tahmin üreten softmax aktivasyon fonksiyonu kullanılmıştır.

# 5. Veri Hazırlama

Veriler Google Colab ortamında klasör yapısına göre okunmuştur. Görseller eğitim ve doğrulama verisi olarak ayrılmıştır.

Veri hazırlama aşamasında:

- Görseller 224x224 boyutuna getirilmiştir.
- Eğitim ve doğrulama ayrımı yapılmıştır.
- `image_dataset_from_directory` yöntemi kullanılarak veriler belleğe tamamen yüklenmeden batch yapısıyla işlenmiştir.
- Veri artırma işlemleri uygulanmıştır.

Kullanılan veri artırma işlemleri:

- Yatay çevirme
- Döndürme
- Yakınlaştırma
- Kontrast değişimi

Bu işlemler modelin farklı görüntü koşullarına karşı daha dayanıklı öğrenmesini sağlamak amacıyla kullanılmıştır.

# 6. Model Eğitimi

Model Google Colab ortamında T4 GPU kullanılarak eğitilmiştir. Eğitim 10 epoch boyunca gerçekleştirilmiştir.

Model derleme aşamasında:

- Optimizer: Adam
- Loss fonksiyonu: Sparse Categorical Crossentropy
- Metrik: Accuracy

kullanılmıştır.

Ayrıca eğitim sürecinde EarlyStopping, ModelCheckpoint ve ReduceLROnPlateau callback yapıları kullanılmıştır. Bu yapılar modelin daha kararlı eğitilmesi ve en iyi sonucun korunması için tercih edilmiştir.

## 7. Elde Edilen Sonuçlar

Modelin eğitim sonunda elde ettiği sonuçlar şu şekildedir:

- Eğitim doğruluğu: %88.88
- Doğrulama doğruluğu: %91.25
- Doğrulama kaybı: 0.2517

Eğitim sürecinde doğruluk değerinin arttığı, loss değerinin ise azaldığı gözlemlenmiştir. Bu durum modelin eğitim süreci boyunca öğrenme gerçekleştirdiğini göstermektedir.

## 8. Grafiklerin Yorumlanması

Accuracy grafiğinde eğitim ve doğrulama doğruluklarının epoch sayısı arttıkça yükseldiği görülmektedir. Bu durum modelin yaprak görüntülerinden anlamlı özellikler öğrendiğini göstermektedir.

Loss grafiğinde ise eğitim ve doğrulama kayıplarının düzenli olarak azaldığı görülmektedir. Bu da modelin hata oranının azaldığını ve öğrenmenin başarılı şekilde gerçekleştiğini göstermektedir.

Doğrulama doğruluğunun yaklaşık %91 seviyesine ulaşması, modelin yalnızca eğitim verisini ezberlemediğini, aynı zamanda doğrulama verisi üzerinde de başarılı genelleme yapabildiğini göstermektedir.

# 9. Sonuç

Bu projede yaprak görüntülerinden bitki hastalıklarını tespit etmek amacıyla MobileNetV2 tabanlı transfer learning modeli geliştirilmiştir.

İlk temel CNN denemelerine göre MobileNetV2 modeli daha başarılı sonuç vermiştir. Model, 15 farklı sınıf üzerinde yaklaşık %91.25 doğrulama doğruluğuna ulaşmıştır.

Elde edilen sonuçlar, derin öğrenme ve transfer learning yöntemlerinin bitki hastalıklarının görüntü tabanlı tespitinde etkili şekilde kullanılabileceğini göstermektedir.

# 10. Gelecek Çalışmalar

Bu çalışma ilerleyen aşamalarda geliştirilebilir. Gelecek çalışmalar kapsamında:

- Daha fazla bitki türü eklenebilir.
- Gerçek saha görüntüleriyle test yapılabilir.
- Mobil uygulama entegrasyonu sağlanabilir.
- Hastalıklı bölgelerin görüntü üzerinde işaretlenmesi için nesne tespiti modelleri kullanılabilir.
- Model farklı CNN mimarileriyle karşılaştırılabilir.

# 11. Proje Dosyaları

GitHub reposunda yer alan dosyalar:

- `Bitki_Hastalik_Tespiti_MobileNetV2.ipynb`
- `README.md`
- `cikti_gorselleri/accuracy_loss_grafigi.png`
- `cikti_gorselleri/egitimsonucu.png`
- `cikti_gorselleri/validation_sonucu.png`

# 12. Kısa Özet

Bu projede öğretim elemanı tarafından paylaşılan PlantVillage veri seti kullanılarak bitki hastalıklarının yaprak görüntülerinden tespiti yapılmıştır. MobileNetV2 tabanlı transfer learning modeli ile 15 sınıflı sınıflandırma gerçekleştirilmiş ve yaklaşık %91.25 doğrulama doğruluğu elde edilmiştir.
