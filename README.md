# Prediksi Jumlah Perjalanan Wisatawan Nusantara
## Berdasarkan Kabupaten/Kota di Provinsi Sulawesi Tengah  
### Menggunakan Metode Regresi Linear
---
### Informasi Tugas
Mata Kuliah : Statistika & Probabilitas  
Mahasiswa : Putri Alma Rizki  
NIM : F5512520077  

---
## Deskripsi
Project ini merupakan tugas akhir mata kuliah Statistika & Probabilitas yang bertujuan untuk memprediksi jumlah perjalanan wisatawan nusantara berdasarkan kabupaten/kota tujuan di Provinsi Sulawesi Tengah menggunakan metode **Regresi Linear Berganda**. Analisis mencakup eksplorasi data (EDA), pembersihan, transformasi, pemodelan, evaluasi model, serta proyeksi total kunjungan tahunan 2026 berdasarkan data Januari–April yang tersedia.

---
## Dataset
Dataset yang digunakan dalam penelitian ini berasal dari Badan Pusat Statistik (BPS) Provinsi Sulawesi Tengah, yaitu data "Jumlah Perjalanan Wisatawan Nusantara Berdasarkan Kabupaten/Kota Tujuan di Provinsi Sulawesi Tengah". Data diperoleh melalui publikasi statistik resmi BPS dan kemudian dilakukan proses penggabungan, transformasi, serta pembersihan data untuk keperluan analisis dan pemodelan regresi linear.

| Atribut | Nilai |
|---|---|
| Instansi | Badan Pusat Statistik (BPS) Provinsi Sulawesi Tengah |
| Nama Dataset | Jumlah Perjalanan Wisatawan Nusantara Berdasarkan Kabupaten/Kota Tujuan di Provinsi Sulawesi Tengah |
| Sumber Data | https://sulteng.bps.go.id/id/statistics-table/2/MzE2IzI=/jumlah-perjalanan-wisatawan-nusantara-berdasarkan-kabupaten-kota-tujuan-di-provinsi-sulawesi-tengah.html |
| Cakupan Waktu | Januari 2024 – April 2026 |
| Jumlah Kabupaten/Kota | 13 |
| Total Baris Data (Sumber) | 42 baris (14 wilayah × 3 tahun, termasuk total provinsi) |
| Format Asli Data | Wide (bulan sebagai kolom, baris ke-5 sebagai header) |

**Variabel utama:**
- `Tahun` — Tahun pengamatan (2024, 2025, 2026)
- `Kabupaten_Kota` — Nama daerah tujuan wisata (13 kabupaten/kota)
- `Januari` s.d. `Desember` — Jumlah kunjungan tiap bulan
- `Tahunan` — Total jumlah perjalanan wisatawan per tahun (target/label)

---
## Struktur File
```
project/
├── analysis.ipynb                                  ← Notebook utama (semua analisis)
├── Gabungan_Data_Wisatawan_Sulteng_2024_2026.xlsx  ← Dataset sumber
├── prediksi_2026.csv                               ← Output tabel prediksi per kabupaten/kota
├── README.md
├── requirements.txt
├── CARA_PENGGUNAAN.txt
└── grafik/
    ├── 01_total_wisatawan_provinsi.png
    ├── 02_perbandingan_kabkota_2024_2025.png
    ├── 03_tren_bulanan_provinsi.png
    ├── 04_heatmap_korelasi.png
    ├── 05_distribusi_tahunan_kabkota.png
    ├── 06_aktual_vs_prediksi.png
    ├── 07_prediksi_2026_vs_aktual.png
    └── 08_analisis_residual.png
```

---
## Alur Analisis
1. **Load Data** — Membaca file Excel, parsing baris mulai index 4 (baris ke-5 sebagai header), menangani nilai `-` pada data 2026 sebagai missing (NaN)
2. **EDA & Visualisasi** — Statistik deskriptif, tren bulanan, heatmap korelasi antar bulan, boxplot distribusi, dan bar chart perbandingan per kabupaten/kota
3. **Preprocessing** — Filtering data lengkap (2024–2025), konversi tipe data numerik, pemisahan data provinsi vs kabupaten/kota, train-test split 80:20
4. **Pemodelan** — Regresi Linear Berganda menggunakan fitur data bulanan Januari–April sebagai prediktor total wisatawan tahunan (26 sampel training dari data 2024–2025)
5. **Evaluasi Model** — R², MAE, RMSE, MAPE pada test set (20% data)
6. **Visualisasi Hasil** — Plot aktual vs prediksi, analisis residual, bar chart prediksi 2026 vs aktual 2024–2025
7. **Interpretasi & Kesimpulan** — Temuan utama, koefisien model, dan rekomendasi praktis

---
## Metrik Evaluasi
Model Regresi Linear Berganda dibangun dengan 4 fitur input (Januari, Februari, Maret, April) dan target output total wisatawan tahunan. Evaluasi dilakukan pada test set (20% data = 6 sampel).

| Metrik | Nilai | Keterangan |
|--------|-------|-----------|
| R² | 0.9722 | Model menjelaskan 97,22% variansi data |
| MAE | 42.994 | Rata-rata error absolut per prediksi (wisatawan) |
| RMSE | 48.709 | Root mean square error (wisatawan) |
| MAPE | 7,52% | Rata-rata persentase error |

**Persamaan model:**  
Ŷ = −89.816,65 + 1,6747·Jan + 6,8601·Feb + 1,2347·Mar + 2,8220·Apr

---
## Temuan Utama
- Wisatawan naik **+25,08%** dari 2024 ke 2025 (9.329.221 → 11.668.933 perjalanan)
- **Kota Palu** mendominasi ~30% total kunjungan provinsi, tumbuh +37,58% YoY
- **Banggai Kepulauan** satu-satunya daerah yang mengalami penurunan pada 2024→2025 (−5,87%)
- Puncak kunjungan konsisten di **bulan April** setiap tahun (musim Lebaran)
- Data 4 bulan pertama (Jan–Apr) sudah sangat prediktif terhadap total tahunan, terbukti dari R² = 0,9722
- Prediksi 2026 tertinggi: **Kota Palu** (3.277.544), **Sigi** (1.367.743), **Donggala** (1.303.610)

---
## Teknologi
```
Python 3.x | pandas | numpy | matplotlib | seaborn | scikit-learn | jupyter
```

---
## Kesimpulan Singkat
Model Regresi Linear Berganda yang menggunakan data bulanan Januari–April sebagai fitur prediktor menghasilkan performa sangat baik dengan R² = 0,9722, MAE = 42.994, RMSE = 48.709, dan MAPE = 7,52%. Model berhasil menangkap hubungan linear yang kuat antara kunjungan awal tahun dengan total tahunan. Kota Palu mendominasi kunjungan wisatawan Sulawesi Tengah, dan tren pertumbuhan dari 2024 ke 2025 menunjukkan pemulihan serta ekspansi sektor pariwisata yang signifikan di provinsi ini.

---
## Referensi
Badan Pusat Statistik Provinsi Sulawesi Tengah. (2026). *Jumlah Perjalanan Wisatawan Nusantara Berdasarkan Kabupaten/Kota Tujuan di Provinsi Sulawesi Tengah*. Diakses dari:  
https://sulteng.bps.go.id/id/statistics-table/2/MzE2IzI=/jumlah-perjalanan-wisatawan-nusantara-berdasarkan-kabupaten-kota-tujuan-di-provinsi-sulawesi-tengah.html
