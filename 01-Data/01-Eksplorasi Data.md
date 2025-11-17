# Meeting 01: Exploratory Data Analysis (EDA) & Statistical Foundations

> **Objective:** Sebelum menyentuh algoritma, mahasiswa harus mampu melakukan "audit" terhadap kualitas dan karakter data menggunakan statistik deskriptif dan inferensial.

## I. Kenapa harus divisualisasikan?
Manusia tidak berevolusi untuk memahami tabel angka berisi 1.000 baris. Kita berevolusi untuk melihat pola visual.
* **Anscombe's Quartet:** Pembuktian bahwa 4 dataset dengan Mean dan Variance yang sama persis bisa memiliki bentuk grafik yang berbeda total.
* **Insight:** Jangan percaya pada `df.describe()` saja. Plot datanya!

## II. Distribusi Data 📊
Algoritma Machine Learning terutama yang Linear sangat peduli pada bentuk data.

### 1. Normal Distribution (Gaussian)
Bentuk lonceng sempurna. Banyak algoritma berasumsi data berbentuk ini.
$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2}$$
* **Sifat:** Simetris. Mean = Median = Mode.

### 2. Skewness (Kemiringan)
Ukuran ketidaksimetrisan distribusi.
* **Positive Skew (Right):** Ekor memanjang ke kanan. (Contoh: Distribusi Kekayaan, Harga Rumah).
* **Negative Skew (Left):** Ekor memanjang ke kiri. (Contoh: Usia Pensiun).
* **Rule of Thumb:** Jika Skewness > 1 atau < -1, data sangat miring. Anda perlu melakukan *Log Transformation*.

### 3. Kurtosis (Kuncupan)
Mengukur "ekor" data (seberapa sering outlier terjadi).
* **Leptokurtic:** Runcing tinggi, ekor tebal (Banyak outlier).
* **Platykurtic:** Datar, ekor tipis (Sedikit outlier).

## III. Univariate dan Bivariate Analysis
Di industri, gunakan *checklist* ini:

1.  **Categorical Data:** Gunakan *Bar Chart* atau *Count Plot*. Cari kategori yang mendominasi (>90%) karena itu tidak membawa informasi (Low Variance).
2.  **Numerical Data:** Gunakan *Histogram* (untuk bentuk) dan *Boxplot* (untuk outlier).
3.  **Correlation:** Gunakan *Heatmap*.
    * Hati-hati dengan **Multicollinearity**: Jika Fitur A dan Fitur B berkorelasi > 0.8, hapus salah satu. Model akan bingung jika ada dua informasi yang redundan.

---

### 📝 Assignment 1
**Skenario:** Anda menganalisis data gaji karyawan startup.
1.  Rata-rata (Mean) gaji adalah Rp 50 Juta.
2.  Median gaji adalah Rp 15 Juta.
3.  Gaji terendah Rp 5 Juta, tertinggi Rp 8 Miliar.

**Pertanyaan:**
1.  Apakah distribusi ini Normal atau Skewed? Ke arah mana?
2.  Jika Anda harus mengisi data gaji yang kosong, apakah aman menggunakan Mean (50 Juta)? Mengapa?
