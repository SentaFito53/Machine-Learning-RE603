# USA Housing Price Prediction
### Supervised Learning — Linear Regression

---

Model regresi linear untuk memprediksi harga rumah di Amerika Serikat berdasarkan 5 fitur area, menggunakan dataset `USA_Housing.csv` (5.000 data).

---

## Metrik Evaluasi Model

| Metrik | Nilai |
|--------|-------|
| MAE | 81,739 |
| RMSE | 102,418 |
| R² Train | 0.917 |
| R² Test | 0.919 |

---

## Kesimpulan Tambahan

### 1. Model Berperforma Baik
Model mampu menjelaskan **91.9% variansi harga rumah**. Selisih R² train dan test yang sangat kecil (0.002) menunjukkan model **tidak overfit maupun underfit** dan mampu generalisasi dengan baik ke data baru.

### 2. Fitur Paling Berpengaruh
- **Avg. Area Income** → prediktor paling stabil dan signifikan secara statistik (t-statistic = 134.68, korelasi = 0.64)
- **Avg. Area House Age** & **Avg. Area Number of Rooms** → dampak absolut terbesar terhadap harga (koefisien > 100.000)

### 3. Fitur Paling Lemah
**Avg. Area Number of Bedrooms** memiliki korelasi terendah (0.17) dan t-statistic terkecil (2.33). Fitur ini bersifat diskrit dan hampir tidak berkontribusi pada prediksi

### 4. Asumsi Regresi Terpenuhi
- ✅ **Normalitas residuals** — Shapiro-Wilk p-value = 0.62 (jauh > 0.05)
- ✅ **Homoskedastisitas** — residuals menyebar merata tanpa pola sistematis
- ✅ Model regresi linear adalah pilihan yang **tepat** untuk dataset ini

### 5. Keterbatasan Model
- Sisa **8.1% variansi** yang belum bisa dijelaskan kemungkinan berasal dari faktor-faktor tersebut

---

## Saran Pengembangan

1. **Hapus fitur lemah** — coba latih ulang model tanpa `Avg. Area Number of Bedrooms`
2. **Feature engineering** — buat fitur baru dari kombinasi fitur yang sudah ada untuk meningkatkan akurasi

---
## Menghapus Fitur Lemah
Berdasarkan kesimpulan poin 3, dilakukan train ulang dengan menghapus Avg. Area Number of Bedrooms.
### Perbandingan Hasil
| Metrik | Model Awal (5 fitur) | Model Baru (4 fitur) | Perubahan |
|--------|---------------------|---------------------|-----------|
| MAE | 81,739 | 81,629 | ↓ 110 ✅ |
| RMSE | 102,418 | 102,282 | ↓ 136 ✅ |
| R² Test | 0.919 | 0.920 | ↑ 0.001 ✅ |
| R² Train | 0.917 | 0.917 | → sama |
| Shapiro p-value | 0.6245 | 0.6245 | → sama persis |

Menghapus Avg. Area Number of Bedrooms tidak menurunkan performa model — semua metrik tetap atau sedikit membaik, dan asumsi normalitas residuals tetap terpenuhi (p-value = 0.6245).

Ini mengkonfirmasi bahwa fitur tersebut memang tidak berkontribusi berarti. Model dengan 4 fitur lebih sederhana dan efisien tanpa mengorbankan akurasi — sesuai prinsip Occam's Razor dalam machine learning: pilih model yang lebih sederhana jika performanya setara.
