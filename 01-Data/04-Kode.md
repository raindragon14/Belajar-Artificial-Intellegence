# 04. Implementation in Python 🐍

Ringkasan sintaks praktis untuk menerapkan teori Modul 01 menggunakan library `pandas` dan `scikit-learn`.

## 1. Handling Missing Values (Imputation)
Menerapkan konsep MCAR / MAR / MNAR.

```python
import pandas as pd
from sklearn.impute import SimpleImputer

# Contoh: df = pd.read_csv('data.csv')

# Kasus MCAR: Drop data jika missing bersifat acak dan sedikit
df_clean = df.dropna(subset=['col_random_missing'])

# Kasus MAR: Imputasi dengan median (lebih tahan terhadap outlier dibanding mean)
imputer = SimpleImputer(strategy='median')
df['col_mar'] = imputer.fit_transform(df[['col_mar']])

# Kasus MNAR: Buat flag untuk missing lalu imputasi (atau gunakan nilai penanda)
df['col_mnar_is_missing'] = df['col_mnar'].isnull().astype(int)
df['col_mnar'] = df['col_mnar'].fillna(0)  # atau gunakan nilai di luar rentang valid sebagai penanda
```

## 2. IQR Method (Deteksi Outlier)

```python
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Filter data yang dianggap bersih dari outlier
df_clean = df[
    (df['salary'] >= lower_bound) &
    (df['salary'] <= upper_bound)
]
```

## 3. Feature Scaling

```python
from sklearn.preprocessing import MinMaxScaler, StandardScaler

# A. Min-Max Scaling (0 sampai 1) - bagus untuk Neural Networks
scaler_minmax = MinMaxScaler()
df['age_norm'] = scaler_minmax.fit_transform(df[['age']])

# B. Standard Scaling (Z-Score) - bagus untuk Regresi / SVM
scaler_std = StandardScaler()
df['age_std'] = scaler_std.fit_transform(df[['age']])
```

## 4. Encoding

```python
# One-Hot Encoding (untuk jumlah kategori sedikit)
df = pd.get_dummies(df, columns=['gender', 'color'], drop_first=True)

# Frequency Encoding (untuk kategori banyak)
freq = df['city'].value_counts() / len(df)
df['city_encoded'] = df['city'].map(freq)
```

Catatan singkat:
- Pilih metode penanganan missing berdasarkan pemahaman terhadap mekanisme missing (MCAR/MAR/MNAR).
- Scaling dan encoding sebaiknya dilakukan setelah split train/test untuk menghindari data leakage.
