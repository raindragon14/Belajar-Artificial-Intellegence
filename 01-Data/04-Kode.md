# 04. Implementation in Python 🐍

Ringkasan sintaks praktis untuk menerapkan teori Module 01 menggunakan Library `pandas` dan `scikit-learn`.

## 1. Handling Missing Values (Imputation)
Menerapkan konsep MCAR/MAR.

```python
import pandas as pd
from sklearn.impute import SimpleImputer

# Kasus MCAR: Drop data
df_clean = df.dropna(subset=['col_random_missing'])

# Kasus MAR: Imputasi dengan Median (Lebih aman dari Mean)
imputer = SimpleImputer(strategy='median')
df['col_mar'] = imputer.fit_transform(df[['col_mar']])

# Kasus MNAR: Flagging + Imputasi
df['col_mnar_is_missing'] = df['col_mnar'].isnull().astype(int)
df['col_mnar'] = df['col_mnar'].fillna(0) # Atau nilai di luar range'''

## 2. IQR Method (Deteksi Outlier)

'''python
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Filter data bersih
df_clean = df[
    (df['salary'] >= lower_bound) &
    (df['salary'] <= upper_bound)
] '''

## 3. Feature Scaling

'''python
from sklearn.preprocessing import MinMaxScaler, StandardScaler

# A. Min-Max Scaling (0 s/d 1) - Bagus untuk Neural Networks
scaler_minmax = MinMaxScaler()
df['age_norm'] = scaler_minmax.fit_transform(df[['age']])

# B. Standard Scaling (Z-Score) - Bagus untuk Regresi/SVM
scaler_std = StandardScaler()
df['age_std'] = scaler_std.fit_transform(df[['age']])'''

## 4. Encoding

'''python
# One-Hot Encoding (Untuk kategori sedikit)
df = pd.get_dummies(df, columns=['gender', 'color'], drop_first=True)

# Frequency Encoding (Untuk kategori banyak)
freq = df['city'].value_counts() / len(df)
df['city_encoded'] = df['city'].map(freq)'''
