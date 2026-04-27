# 🐾 Klasifikasi Gambar Hewan pada Data Animals-10
 
Proyek machine learning untuk mengklasifikasikan gambar hewan ke dalam 10 kategori menggunakan transfer learning dengan arsitektur **MobileNetV2**.
 
---
 
## 📋 Deskripsi Proyek
 
Klasifikasi gambar hewan memiliki berbagai aplikasi nyata, mulai dari identifikasi satwa liar hingga media pembelajaran interaktif. Proyek ini menggunakan dataset **Animals-10** dari Kaggle yang berisi gambar 10 jenis hewan dengan nama kelas dalam bahasa Italia.
 
Model dibangun dengan pendekatan **transfer learning** menggunakan MobileNetV2 yang telah dilatih pada ImageNet, dipilih karena arsitekturnya yang ringan dan efisien — cocok untuk perangkat dengan sumber daya terbatas.
 
---
 
## 🐘 Kelas yang Diklasifikasikan
 
| Label | Hewan |
|-------|-------|
| `cane` | Anjing |
| `cavallo` | Kuda |
| `elefante` | Gajah |
| `farfalla` | Kupu-kupu |
| `gallina` | Ayam |
| `gatto` | Kucing |
| `mucca` | Sapi |
| `pecora` | Domba |
| `ragno` | Laba-laba |
| `scoiattolo` | Tupai |
 
---
 
## 🗂️ Dataset
 
- **Sumber:** [Animals-10 — Kaggle](https://www.kaggle.com/datasets/alessiocorrado99/animals10)
- **Resolusi:** Beragam (174×300 hingga 640×442), paling umum 300×225
- **Split:** 70% Training / 15% Validation / 15% Testing
- **Input Model:** Di-resize ke **224×224 piksel**, batch size 32
---
 
## 🏗️ Arsitektur Model

Model dibangun menggunakan **MobileNetV2** (pretrained ImageNet) sebagai base model yang di-*freeze*, kemudian ditambahkan **Sequential head**:

```
MobileNetV2 (pretrained ImageNet, frozen)
    └── Sequential Head:
            ├── Conv2D (256 filter, 3x3, ReLU)
            ├── BatchNormalization
            ├── MaxPooling2D (2x2)
            ├── GlobalAveragePooling2D
            ├── Dense (256, ReLU) + Dropout (0.5)
            ├── Dense (128, ReLU) + Dropout (0.3)
            └── Dense (10, Softmax)
```

- **Optimizer:** Adam (learning rate = 0.001)
- **Loss:** Categorical Crossentropy
- **Metrik:** Accuracy
---
 
## ⚙️ Training

**Konfigurasi:**

| Parameter    | Nilai      |
|--------------|------------|
| Image Size   | 224 × 224  |
| Batch Size   | 32         |
| Max Epochs   | 20         |

**Augmentasi data training:** rotasi (±20°), geser horizontal & vertikal (±10%), shear (±10%), zoom (±10%), dan flip horizontal. Data validation dan testing hanya dinormalisasi tanpa augmentasi.

**Callback yang digunakan:**

| Callback            | Konfigurasi                                          |
|---------------------|------------------------------------------------------|
| `EarlyStopping`     | monitor=`val_loss`, patience=5, restore best weights |
| `ReduceLROnPlateau` | monitor=`val_loss`, factor=0.5, patience=3, min_lr=1e-5 |
| `ModelCheckpoint`   | monitor=`val_accuracy`, save best only → `best_model.h5` |
 
---
 
## 📊 Hasil Evaluasi
 
| Dataset | Akurasi | Loss |
|---------|---------|------|
| Training | **98.07%** | 0.0607 |
| Validation | **95.44%** | 0.1789 |
| Test | **95.53%** | 0.1533 |
 
Selisih akurasi antara training dan test hanya ~2–3%, menandakan model **tidak overfitting** dan mampu generalisasi dengan baik.
 
### Per-Kelas (Test Set)
- 🏆 Terbaik: `farfalla`, `gallina`, `ragno` — F1-score **97–98%**
- 📉 Terendah: `mucca`, `pecora` — F1-score **90%**
- ✅ Akurasi keseluruhan: **96%**
---
 
## 💾 Format Model yang Disimpan
 
Model disimpan dalam tiga format untuk keperluan deployment berbeda:
 
| Format | Kegunaan |
|--------|----------|
| **SavedModel** | Deployment server (TensorFlow Serving) |
| **TF-Lite** (`.tflite`) | Aplikasi mobile / edge device |
| **TensorFlow.js** | Deployment di browser / website |
 
---
 
## 🛠️ Library yang Digunakan
 
```
tensorflow
numpy
matplotlib
scikit-learn
Pillow (PIL)
tensorflowjs
```
 
---
 
## 👤 Author
 
**Aliyah Nadhratunnaim**
📧 [aliyah180606@gmail.com](mailto:aliyah180606@gmail.com)
🔗 [LinkedIn](https://linkedin.com/in/aliyahnadhratunnaim) | [GitHub](https://github.com/aliyahnadh)

---

> 🏫 Proyek ini merupakan hasil dari DBS Coding Camp Learning Path AI Engineer 2026

