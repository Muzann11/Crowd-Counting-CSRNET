# 👥 Crowd Counting using CSRNet (Density Map Regression)

**Final Project Mata Kuliah Pengolahan Citra Digital & Visi Komputer** *Fakultas Ilmu Komputer, Universitas Brawijaya*

---

## 🖼️ Project Poster
![Final Project Poster](crowd%20counting%20poster.png)


---

## 📝 Deskripsi Proyek
Proyek ini bertujuan untuk membangun sistem **Estimasi Kepadatan Massa (Crowd Counting)** otomatis menggunakan teknik *Deep Learning*. Sistem ini dirancang sebagai solusi *Early Warning System* untuk mencegah overkapasitas di area publik.

Kami menggunakan pendekatan **Density Map Regression** dengan arsitektur **CSRNet** (Congested Scene Recognition Network), yang terbukti lebih efektif menangani oklusi pada kerumunan padat dibandingkan metode deteksi objek konvensional.

---

## 🛠️ Materi & Metode Utama
Sesuai ketentuan proyek, kami mengintegrasikan 3 materi utama perkuliahan dalam pipeline ini:

### 1. Transformasi Citra (Preprocessing)
* **Teknik:** **Resize with Padding**.
* **Implementasi:** Mengubah dimensi input menjadi **360x640** piksel.
* **Tujuan:** Menyeragamkan ukuran input untuk CNN tanpa mendistorsi rasio aspek (*aspect ratio*) objek, mencegah gambar menjadi gepeng.

### 2. Filtering (Domain Spasial)
* **Teknik:** **Gaussian Filter** ($\sigma=5$).
* **Implementasi:** Mengonversi anotasi titik koordinat kepala (*dot annotation*) menjadi **Density Map** kontinu.
* **Tujuan:** Memberikan informasi spasial volume objek kepada model, sehingga model tidak belajar dari matriks yang terlalu *sparse* (kosong).

### 3. Deep Learning (CNN Ringan)
* **Arsitektur:** **CSRNet** (Fully Convolutional Network).
    * **Frontend:** 10 Layer pertama **VGG-16 dengan Batch Normalization** (ekstraksi fitur).
    * **Backend:** 6 Layer **Dilated Convolution** (Rate=2).
* **Tujuan:** *Dilated convolution* memungkinkan model memperluas jangkauan pandang (*receptive field*) untuk memahami konteks kerumunan tanpa mengurangi resolusi spasial (tanpa Pooling berlebih).

---

## 📊 Hasil & Evaluasi

### Metrik Kinerja
* **Loss Function:** Mean Squared Error (MSE) - Digunakan saat training.
* **Evaluasi Akhir:** **Mean Absolute Error (MAE): 1.93**
    * *Artinya: Rata-rata prediksi model hanya meleset sekitar 1-2 orang per gambar.*

### Analisis
Berdasarkan Scatter Plot hasil pengujian:
* ✅ **Akurasi Tinggi:** Pada kepadatan rendah - sedang (0-30 orang).
* ⚠️ **Isu Saturasi:** Terjadi *undercounting* (prediksi lebih rendah dari asli) pada kepadatan tinggi (>40 orang) akibat variasi skala ekstrem.

---

## 🚀 Rencana Pengembangan (Future Work)
Untuk mengatasi limitasi saat ini, pengembangan selanjutnya akan difokuskan pada:
1.  **Multi-Scale Network:** Mengganti backend dengan MCNN atau FPN untuk menangani variasi skala objek (orang jauh vs dekat).
2.  **Real-time Edge Optimization:** Kompresi model (Quantization) agar dapat berjalan *real-time* pada perangkat CCTV/IoT.

---
