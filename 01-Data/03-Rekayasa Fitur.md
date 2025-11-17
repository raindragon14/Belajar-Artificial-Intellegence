# Meeting 03: Feature Engineering

> **Objective:** Mengubah data mentah menjadi "Fitur" yang memudahkan model menemukan pola. *Machine Learning is mostly Feature Engineering.*

## I. Feature Scaling: Normalization vs Standardization ⚖️
Kenapa kita perlu menyamakan skala? Karena algoritma yang menggunakan jarak (seperti KNN, K-Means, SVM) atau Gradient Descent akan bias ke angka yang besar.

| Feature | Range Asli | Masalah |
| :--- | :--- | :--- |
| Gaji | 1.000.000 - 10.000.000 | Angka raksasa, mendominasi hitungan. |
| Umur | 1 - 100 | Angka kecil, dianggap tidak penting. |

### 1. Min-Max Scaling (Normalization)
Memampatkan data ke range [0, 1].
$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$
* *Kapan dipakai:* Neural Networks, Image Processing.
* *Kelemahan:* Sangat sensitif terhadap outlier.

### 2. Standard Scaling (Standardization)
Mengubah data sehingga Mean = 0 dan Std Dev = 1.
$$X_{std} = \frac{X - \mu}{\sigma}$$
* *Kapan dipakai:* Regresi Linear, Logistik, SVM.
* *Kelebihan:* Menjaga informasi outlier, bentuk distribusi tetap sama.

## II. Encoding Categorical Data 🔠

### 1. One-Hot Encoding (OHE)
Membuat kolom biner baru.
* Merah $\rightarrow$ [1, 0, 0]
* Hijau $\rightarrow$ [0, 1, 0]
* Biru $\rightarrow$ [0, 0, 1]
* *Masalah:* **Curse of Dimensionality**. Jika ada 1.000 kategori, tabel Anda tambah 1.000 kolom. Berat!

### 2. Target/Mean Encoding (Pro Technique)
Mengganti kategori dengan rata-rata targetnya.
* Contoh: Ganti "Kota Surabaya" dengan "Rata-rata Harga Rumah di Surabaya".
* *Kelebihan:* Tidak menambah kolom.
* *Bahaya:* **Data Leakage** (Bocoran jawaban). Harus dilakukan hati-hati.

## III. Feature Creation (Domain Knowledge)
Kadang fitur terbaik tidak ada di data, tapi harus dibuat.
* **Date Parsing:** `2023-10-23` $\rightarrow$ `Is_Weekend?` (1/0).
* **Interaction:** `Panjang` & `Lebar` $\rightarrow$ `Luas`.
* **Binning:** `Umur 23` $\rightarrow$ `Kelompok_Dewasa_Muda`.

---

### 📝 Assignment 3 (Final Project Module 01)
**Kasus:** Prediksi Harga Mobil Bekas.
**Fitur Mentah:**
1.  `Tahun Beli` (Contoh: 2015, 2020)
2.  `Kilometer` (Contoh: 50.000, 120.000)
3.  `Warna` (Contoh: Merah, Hitam, Silver)
4.  `Tipe` (Manual, Otomatis)

**Instruksi:**
Tuliskan dalam poin-poin transformasi apa saja yang akan Anda lakukan pada setiap kolom di atas agar siap masuk ke Neural Network.
