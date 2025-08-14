# 🖋️ MNIST CNN Digit Classification

## CNN (Convolutional Neural Network)
Görsel verilerdeki kenar, köşe, şekil gibi özellikleri otomatik olarak öğrenebilen derin öğrenme mimarisidir.
Özellikle görüntü sınıflandırma, nesne tespiti ve el yazısı tanıma gibi görevlerde yaygın olarak kullanılır.
Bu projede CNN, MNIST el yazısı rakamlarını yüksek doğrulukla tanımak için tercih edilmiştir.

> **MNIST veri seti** kullanılarak el yazısı rakamları (0-9) sınıflandırmak için geliştirilmiş bir **Convolutional Neural Network (CNN)** projesidir.
> TensorFlow ve Keras ile derin öğrenme uygulamasıdır.
> Model ayrıca kendi eklediğim el yazısı rakam görselleri üzerinde de test edilmiştir.



## 📖 Proje Açıklaması
Bu proje, **derin öğrenme** tekniklerinden biri olan **CNN** kullanarak el yazısı rakam tanıma problemi üzerinde çalışmaktadır.  
MNIST veri seti üzerinde eğitilen model, yüksek doğruluk oranı ile rakamları sınıflandırabilmektedir.  
Ek olarak, kendi çektiğim/oluşturduğum test görselleri ile modelin gerçek dünya senaryolarındaki performansı ölçülmüştür.



## 📊 Veri Seti
- **MNIST**: 28x28 piksel boyutunda, gri tonlamalı el yazısı rakam görüntüleri.
- **Eğitim Verisi**: 60,000 görüntü
- **Test Verisi**: 10,000 görüntü

![MNIST Örnek Görseller](https://upload.wikimedia.org/wikipedia/commons/2/27/MnistExamples.png)



## 🛠 Kullanılan Teknolojiler
- **Python 3.x**
- **TensorFlow / Keras**
- **Matplotlib**



## 🧠 Model Mimarisi
| Katman | Parametreler | Aktivasyon |
|--------|-------------|------------|
| Conv2D | 32 filtre, 3x3 kernel | ReLU |
| MaxPooling2D | 2x2 | - |
| Conv2D | 64 filtre, 3x3 kernel | ReLU |
| MaxPooling2D | 2x2 | - |
| Flatten | - | - |
| Dense | 128 nöron | ReLU |
| Dense | 10 nöron | Softmax |


## 📈 Eğitim Süreci
```python
model.compile(optimizer='adam',
              loss='categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=5, validation_data=(x_test, y_test))
````



## 🖼 Kendi Görsellerim ile Test
Bu sayede modelin gerçek hayattaki veri üzerinde ne kadar başarılı olduğu gözlemlenmiştir.

Örnek test görselleri ve modelin tahmin sonuçları:
GÖrsellerde eklenmiştir.
Eklenen ikinci görselde başka sayılar da olmasına rağmen sekiz şeklinde tahmin etmiştir.

### 📌Peki neden 8 Olarak Tahmin Edildi?

Modelin bu görseli **8 olarak tahmin etmesinin nedenleri**:

1. **Görüntüde baskın öğe 8**
   * Model piksellere bakarak sınıflandırma yapar. Bu resimde en belirgin ve kontrastı en yüksek şekil, ortadaki kalın siyah “8”dir.
   * Yanındaki yazılar çok küçük ve ince çizgilere sahip olduğundan model için önemsiz hale gelir.
     
2. **MNIST modeli yalnızca rakam tanımak için eğitildi**
   * Model, 0-9 arası rakamlar dışında hiçbir şeyi tanımayacak şekilde eğitildi.
   * Rakam dışındaki metinleri “gürültü” (noise) gibi görür.
  
3. **Ön işlem sırasında küçültme etkisi**
   * Görsel, modele girmeden önce **28x28 piksel gri tonlamaya** küçültülür.
   * Küçük yazılar bu küçültme sırasında neredeyse tamamen kaybolur, geriye sadece 8’in şekli kalır.

📌 **Sonuç olarak**: Model, en büyük ve baskın şekli algılar, diğer detayları yok sayar.


## ✅ Sonuçlar

* **Eğitim Doğruluğu**: \~%99
* **Test Doğruluğu**: \~%98+
* Kendi görsellerim üzerinde de yüksek doğruluk gözlemlenmiştir.


Bu proje [MIT Lisansı](LICENSE) ile lisanslanmıştır.
