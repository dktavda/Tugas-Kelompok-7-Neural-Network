# Tugas Kelompok 7 — Neural Network

**Mata Kuliah:** Machine Learning & Computer Vision  
**Dosen Pengampu:** Herfandi, Ph.D. — Informatika — Universitas Teknologi Sumbawa (UTS)

---

## Profil Kelompok

| No | Nama | NIM |
|----|------|-----|
| 1 | Sherly Novia Indriani | 231001057 |
| 2 | Dinda Oktavia Pratiwi | 231001026 |
| 3 | Ahsanul Ikram | 231001077 |
| 4 | Wanda Setya Budi | 231001008 |

**Kelas:** Informatika — [C]

---

## Deskripsi Proyek

Repositori ini merupakan dokumentasi teknis hasil praktik kelompok mengenai implementasi **Convolutional Neural Network (CNN)** untuk sistem **Face Recognition** berbasis Deep Learning. Praktikum ini merupakan lanjutan dari pendekatan klasik (Haar Cascade + LBPH + SVM) menuju pendekatan modern berbasis jaringan saraf tiruan yang mampu mempelajari fitur wajah secara otomatis dari data.

Materi praktik mencakup seluruh pipeline pembangunan sistem pengenalan wajah, mulai dari persiapan data hingga inferensi real-time menggunakan kamera.

---

## Lingkungan Pengembangan (Environment)

Seluruh kode dalam repositori ini disusun dan diuji menggunakan spesifikasi berikut:

* **Kode Editor:** Jupyter Notebook
* **Interpreter:** Python 3.x
* **Library Utama:** Keras, TensorFlow, OpenCV, scikit-learn, NumPy, Matplotlib
---

## Cakupan Praktikum

Tahapan implementasi yang dilakukan mencakup:

1. **Membaca Dataset & Preprocessing:** Membaca gambar wajah dari dataset LFW, melakukan crop area wajah, konversi ke grayscale, dan resize ke ukuran 50×50 piksel.

2. **Image Augmentation (1.1.A):** Menerapkan transformasi geometris (rotasi, translasi) dan penyesuaian brightness untuk memperbanyak jumlah sampel per kelas dan meningkatkan ketahanan model terhadap variasi kondisi gambar.

3. **Balancing Data (1.1.B):** Menyeimbangkan distribusi data antar kelas menggunakan teknik *undersampling* dengan `np.random.choice` agar setiap kelas memiliki jumlah sampel yang setara (1000 sampel/kelas).

4. **Encoding Label & Kategorikalisasi (1.2):** Mengonversi label nama menjadi representasi numerik melalui dua tahap — *Label Encoding* (nama → integer) dan *One-Hot Encoding* (integer → vektor biner) menggunakan `LabelEncoder` dan `to_categorical`.

5. **Split Dataset (1.3):** Memisahkan data menjadi *training set* (85%) dan *test set* (15%) secara acak menggunakan `train_test_split` untuk mengukur kemampuan generalisasi model.

6. **Reshape Data & Pembuatan Model CNN (1.4):** Menyesuaikan dimensi data ke format 4D `(batch, height, width, channel)` yang dibutuhkan CNN, lalu membangun arsitektur model dengan susunan layer Conv2D → MaxPool2D → Conv2D → MaxPool2D → Flatten → Dense → Softmax.

7. **Training CNN Model (1.5):** Melatih model menggunakan optimizer Adam dan loss `categorical_crossentropy` selama 10 epoch dengan batch size 32, disertai monitoring performa melalui validation split 15%.

8. **Evaluasi Model:** Menganalisis performa model menggunakan grafik *accuracy* dan *loss*, *confusion matrix*, serta *classification report* (Precision, Recall, F1-Score) per kelas.

9. **Face Recognition Real-Time (Video Frame):** Mengintegrasikan model CNN yang telah dilatih ke dalam pipeline real-time menggunakan Haar Cascade untuk deteksi wajah dan CNN untuk identifikasi, dengan threshold confidence 90% sebelum menampilkan nama.

---

## Arsitektur CNN

```
Input (50 × 50 × 1)
        │
  Conv2D (64 filter, 3×3, ReLU)
  Conv2D (64 filter, 3×3, ReLU)
  MaxPool2D (2×2)
        │
  Conv2D (128 filter, 3×3, ReLU)
  Conv2D (128 filter, 3×3, ReLU)
  MaxPool2D (2×2)
        │
     Flatten
        │
   Dense (128, ReLU)
   Dense (64, ReLU)
   Dense (n_classes)
        │
     Softmax
        │
   Output (Probabilitas per Kelas)
```

---

## 🔍 Analisis & Kesimpulan Teknis

1. **Pentingnya Balancing Data:** Ketidakseimbangan kelas (*class imbalance*) dapat membuat model cenderung berpihak pada kelas yang memiliki lebih banyak data. Dengan menyeragamkan jumlah sampel per kelas, model belajar secara adil dari setiap identitas wajah.

2. **Peran Augmentasi:** Dataset wajah yang kecil rentan menghasilkan model yang *overfitting*. Augmentasi melalui rotasi, translasi, dan perubahan brightness secara efektif memperluas keragaman data tanpa perlu mengumpulkan foto baru, meningkatkan kemampuan generalisasi model.

3. **Keunggulan CNN atas LBPH:** Berbeda dengan LBPH yang mengekstraksi fitur secara manual berdasarkan aturan yang telah ditentukan, CNN mempelajari fitur hierarkis secara otomatis — dari tepi dan tekstur di lapisan awal hingga pola wajah yang kompleks di lapisan dalam. Hasilnya, CNN jauh lebih adaptif terhadap variasi pencahayaan, ekspresi, dan pose.

4. **Threshold Confidence pada Inferensi Real-Time:** Penerapan batas kepercayaan 90% sebelum menampilkan identitas adalah mekanisme keamanan yang krusial. Tanpa threshold ini, model akan selalu memaksakan prediksi meskipun wajah yang terdeteksi tidak termasuk dalam dataset, berpotensi menyebabkan kesalahan identifikasi.

5. **Kesimpulan:** Pipeline CNN end-to-end yang dibangun membuktikan bahwa Deep Learning mampu mengenali wajah secara real-time dengan akurasi yang jauh melampaui pendekatan tradisional. Kualitas dan keseimbangan data terbukti menjadi faktor penentu utama performa model, tidak hanya kompleksitas arsitekturnya.

---

## 📽️ Presentasi Video

Demonstrasi lengkap pipeline, penjelasan kode baris demi baris, serta hasil inferensi real-time dapat diakses melalui tautan berikut:

👉 *[ https://youtu.be/2nsJepAdb8A ]*

---
