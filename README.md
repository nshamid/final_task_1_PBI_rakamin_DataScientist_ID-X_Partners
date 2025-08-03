# Proyek Model Prediksi Risiko Kredit

## Deskripsi Proyek

Proyek ini bertujuan untuk membangun model *machine learning* yang dapat memprediksi risiko kredit (*credit risk*) seorang peminjam. Model ini dikembangkan sebagai bagian dari *Project-Based Internship* bersama ID/X Partners untuk klien dari industri *multifinance*. Tujuannya adalah untuk meningkatkan akurasi dalam menilai kelayakan kredit calon peminjam, sehingga dapat mengoptimalkan keputusan bisnis dan mengurangi potensi kerugian.

Dataset yang digunakan adalah data pinjaman historis dari tahun 2007-2014 yang mencakup pinjaman yang lunas (*Fully Paid*) dan yang gagal bayar (*Charged Off*).

-----

## Alur Pengerjaan Proyek

Proyek ini dibagi menjadi lima tahapan utama sesuai dengan metodologi data science:

### 1\. Data Understanding

  - **Tujuan:** Memahami struktur dan karakteristik awal dari dataset.
  - **Aktivitas:**
      - Memuat dataset `loan_data_2007_2014.csv` yang berisi 466.285 baris dan 75 kolom.
      - Menganalisis tipe data dan statistik deskriptif dari setiap kolom.
      - Mengidentifikasi adanya *missing values* dalam jumlah besar pada beberapa kolom.

### 2\. Exploratory Data Analysis (EDA)

  - **Tujuan:** Menemukan pola, hubungan, dan wawasan dari data melalui visualisasi.
  - **Aktivitas:**
      - Menentukan variabel target `credit_risk_label` berdasarkan kolom `loan_status`, di mana `Charged Off` dianggap sebagai "Bad Loan" (1) dan `Fully Paid` sebagai "Good Loan" (0).
      - Menganalisis hubungan antara `grade` pinjaman dengan `int_rate` (suku bunga) dan risiko kredit.
      - Membuat heatmap korelasi untuk memahami hubungan antar fitur numerik.

### 3\. Data Preparation

  - **Tujuan:** Membersihkan dan mentransformasi data agar siap untuk pemodelan.
  - **Aktivitas:**
      - Menghapus kolom yang tidak relevan, memiliki *missing values* tinggi, atau menyebabkan kebocoran data (*data leakage*) seperti `total_pymnt` dan `recoveries`.
      - Membersihkan dan mengubah kolom `term` dan `emp_length` menjadi format numerik.
      - Melakukan *feature engineering* dengan membuat fitur baru `credit_history_length` dari kolom tanggal.
      - Melakukan *one-hot encoding* pada semua fitur kategorikal yang tersisa.

### 4\. Data Modelling

  - **Tujuan:** Membangun dan melatih model *machine learning*.
  - **Aktivitas:**
      - Membagi data yang sudah bersih menjadi data latih (80%) dan data uji (20%).
      - Melakukan *scaling* pada fitur menggunakan `StandardScaler` untuk menstandarkan rentang nilai.
      - Melatih dua model klasifikasi:
        1.  **Logistic Regression** (Model Wajib)
        2.  **Random Forest Classifier** (Model Pembanding)

### 5\. Evaluation

  - **Tujuan:** Mengevaluasi dan membandingkan performa model.
  - **Aktivitas:**
      - Menguji kedua model pada data uji yang belum pernah dilihat sebelumnya.
      - Menganalisis metrik performa seperti *Accuracy*, *Precision*, *Recall*, dan *ROC-AUC Score*.
      - Membuat *Confusion Matrix* untuk melihat detail kesalahan prediksi.

-----

## Hasil dan Kesimpulan

Setelah perbaikan *data leakage*, kedua model memberikan hasil yang realistis:

| Model | Accuracy | Precision (Bad Loan) | Recall (Bad Loan) | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: |
| **Logistic Regression** | 82.59% | 97.35% | 5.14% | 71.85% |
| **Random Forest** | 82.51% | 94.13% | 6.17% | 75.98% |

**Kesimpulan:**

  - **Random Forest** menunjukkan performa keseluruhan yang sedikit lebih baik, terutama pada metrik **ROC-AUC (75.98%)**.
  - Kedua model memiliki kelemahan pada **recall** untuk kelas "Bad Loan" yang rendah, yang menandakan adanya tantangan dalam mendeteksi semua pinjaman berisiko karena sifat data yang tidak seimbang.
  - Untuk pengembangan lebih lanjut, disarankan untuk menerapkan teknik penanganan *imbalanced data* seperti **SMOTE**.
