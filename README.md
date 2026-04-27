# 🐾 Klasifikasi Gambar Hewan — Animals-10
 
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
 
- **Base Model:** MobileNetV2 (pretrained ImageNet, frozen)
- **Custom Head (Sequential):**
  - `Conv2D` (256 filter) + `BatchNormalization` + `MaxPooling2D`
  - `GlobalAveragePooling2D`
  - `Dense` + `Dropout`
  - Output layer (10 kelas, softmax)
- **Optimizer:** Adam
- **Loss:** Categorical Crossentropy
- **Metrik:** Accuracy
---
 
## ⚙️ Augmentasi Data
 
Augmentasi diterapkan hanya pada data training untuk mencegah overfitting:
 
| Teknik | Nilai |
|--------|-------|
| Rotasi | ±20° |
| Geser horizontal/vertikal | 10% |
| Shear | 10% |
| Zoom | 10% |
| Flip horizontal | ✅ |
| Normalisasi (rescale) | 1/255 |
 
Data validation dan test hanya dinormalisasi tanpa augmentasi.
 
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

