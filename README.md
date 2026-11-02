# Hands-On 3: Pandas Lanjutan — Customer Churn Analysis

## Dataset yang dipilih
- **Kasus:** 02 — Customer Churn Analysis
- **Sektor:** Telekomunikasi
- **File data asli:** `data/case2_customer_churn.csv`
- **Ukuran data:** 5.000 baris × 12 kolom
- **Target klasifikasi:** `status_pelanggan` (`Aktif` atau `Churn`)

## Isi folder
- `notebook.ipynb` — kode lengkap beserta penjelasan dan hasil analisis.
- `data/case2_customer_churn.csv` — dataset asli yang digunakan.
- `output/data_bersih.csv` — hasil pembersihan data.
- `output/kamus_data.csv` — kamus data berisi nama kolom, tipe data, missing value, jumlah nilai unik, dan keterangan.
- `laporan_kualitas.csv` — ringkasan kualitas data sebelum dan sesudah pembersihan.

## Tools dan Library
- Google Colab sebagai lingkungan pengembangan dan eksekusi kode.
- Python sebagai bahasa pemrograman.
- Pandas untuk manipulasi dan pengolahan data.
- NumPy untuk komputasi numerik.
- Matplotlib dan Seaborn untuk visualisasi data.
- Scikit-learn untuk pemodelan dan evaluasi klasifikasi.

## Struktur Repository
```text
tugas-hands-on-3/
│
├── README.md
├── notebook.ipynb
│
├── data/
│   └── case2_customer_churn.csv
│
├── output/
│   ├── data_bersih.csv
│   └── kamus_data.csv
│
└── laporan_kualitas.csv
```

## Tahapan Pengerjaan
- Memuat dan mengeksplorasi dataset.
- Memeriksa kualitas dan karakteristik data.
- Menangani missing values.
- Memeriksa dan menangani data duplikat.
- Mendeteksi dan menangani outlier.
- Melakukan analisis dan visualisasi data.
- Membangun serta mengevaluasi model klasifikasi.

## Temuan Utama
- Total dataset terdiri dari 5.000 data pelanggan.
- Tingkat churn keseluruhan sebesar 43,62%.
- Pelanggan dengan kontrak bulanan memiliki tingkat churn sebesar 58,39%.
- Pelanggan dengan 12–15 keluhan memiliki tingkat churn sebesar 56,97%.
- Missing values berhasil ditangani sehingga jumlahnya menjadi 0.
- Tidak ditemukan data duplikat berdasarkan ID pelanggan.

## Ringkasan hasil
- Data awal memiliki 5.000 baris dan 12 kolom.
- Tidak ditemukan duplikat berdasarkan `customer_id`.
- Terdapat 1.638 sel missing pada data awal; setelah pembersihan menjadi 0.
- Ditemukan 55 nilai outlier berdasarkan aturan IQR per `status_pelanggan` pada data awal; setelah clipping dan audit ulang, jumlah outlier yang melewati batas IQR menjadi 0.
- Tingkat churn keseluruhan sekitar 43,62%.
- Tingkat churn berdasarkan kontrak: Bulanan 58,39%; Tahunan 39,67%; Dua Tahun 31,27%.
- Tingkat churn meningkat pada kelompok dengan jumlah komplain tinggi: 0–3 komplain 23,93%; 8–11 komplain 55,22%; 12–15 komplain 56,97%.
- Model baseline Logistic Regression dengan split 80:20 menghasilkan accuracy 0,644 dan F1 kelas Churn sekitar 0,546 pada eksekusi ini. Hasil ini adalah baseline, bukan klaim model terbaik.

## Cara menjalankan
- Buka Google Colab melalui https://colab.research.google.com/.
- Pilih menu File → Upload notebook.
- Unggah file notebook.ipynb.
- Unggah dataset asli sesuai struktur folder yang digunakan dalam notebook.
- Sesuaikan lokasi file jika diperlukan.
- Jalankan seluruh cell secara berurutan menggunakan Runtime → Run all.

## Catatan metodologi
- Missing numerik diisi median dan missing kategorik diisi modus untuk menghasilkan CSV bersih.
- Nilai outlier numerik ditangani dengan clipping batas IQR per status pelanggan, bukan menghapus baris.
- Tidak ada kolom tanggal transaksi, sehingga analisis time series tidak diterapkan. RFM juga tidak digunakan karena dataset tidak berisi catatan transaksi individual.
- Untuk pemodelan, notebook kembali menggunakan data mentah (setelah duplikat dihapus). `train_test_split` dilakukan sebelum imputasi, scaling, dan encoding. Parameter preprocessing di-fit hanya pada data train melalui `Pipeline` dan `ColumnTransformer`, sehingga menghindari data leakage.
- Hubungan yang ditemukan pada analisis eksploratif tidak membuktikan sebab-akibat.
