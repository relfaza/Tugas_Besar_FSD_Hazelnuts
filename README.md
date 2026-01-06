# Tugas_Besar_FSD_Hazelnuts
# Laporan Klasifikasi Ujaran Kebencian pada Twitter (X)

## 1. Latar Belakang Masalah

Media sosial, khususnya Twitter (X), menjadi salah satu platform utama bagi masyarakat untuk mengekspresikan opini dan pandangan. Namun, kebebasan berekspresi ini juga memunculkan berbagai permasalahan, salah satunya adalah maraknya **ujaran kebencian (hate speech)** dan **bahasa kasar (abusive language)**.

Identifikasi ujaran kebencian secara manual memiliki beberapa keterbatasan, seperti:
- Bersifat subjektif
- Memerlukan waktu dan tenaga yang besar
- Tidak konsisten dalam penilaian

Oleh karena itu, diperlukan sebuah **sistem klasifikasi otomatis berbasis Machine Learning** yang mampu mengklasifikasikan teks tweet ke dalam beberapa kategori, sehingga dapat membantu proses moderasi konten digital secara lebih objektif dan efisien.

---

## 2. Pengumpulan Data

Dataset yang digunakan dalam penelitian ini diperoleh dari **Kaggle**, yaitu dataset *Indonesian Abusive and Hate Speech Twitter Text*. Dataset ini berisi kumpulan tweet berbahasa Indonesia yang telah diberi label secara manual.

### Karakteristik Dataset:
- **Sumber**: Kaggle  
- **Jenis Data**: Teks (tweet)
- **Label Kelas**:
  - `0` → Non-Hate Speech
  - `1` → Hate Speech
  - `2` → Abusive

Dataset diunduh menggunakan `kagglehub` dan dimuat ke dalam bentuk **Pandas DataFrame**. Selain itu, dilakukan *Exploratory Data Analysis (EDA)* untuk:
- Melihat distribusi data pada setiap kelas
- Mengidentifikasi kata-kata yang sering muncul melalui *word cloud*

---

## 3. Pre-processing Data

Tahap pre-processing bertujuan untuk mempersiapkan data teks agar dapat digunakan oleh model Machine Learning.

Langkah-langkah pre-processing yang dilakukan:
- Pembersihan teks tweet dari karakter yang tidak relevan
- Transformasi teks ke dalam bentuk numerik menggunakan **TF-IDF (Term Frequency – Inverse Document Frequency)**

TF-IDF digunakan karena:
- Mampu merepresentasikan tingkat kepentingan suatu kata dalam dokumen
- Mengurangi pengaruh kata-kata umum yang sering muncul
- Efektif untuk data teks berdimensi tinggi

---

## 4. Klasifikasi (Metode yang Dipilih)

Pada penelitian ini digunakan dua metode klasifikasi utama:

### 4.1 Naive Bayes Multinomial
- Cocok untuk klasifikasi teks
- Memiliki kompleksitas rendah
- Efisien dan cepat dalam proses pelatihan
- Mendukung klasifikasi multi-kelas

### 4.2 Support Vector Machine (SVM) Multi-class
- Mampu menangani data berdimensi tinggi
- Menghasilkan batas keputusan yang optimal
- Memiliki performa yang baik pada klasifikasi teks

### Strategi Evaluasi Model:
- Menggunakan **K-Fold Cross Validation (K = 5)**
- Bertujuan untuk:
  - Mengurangi bias pembagian data
  - Menghasilkan evaluasi performa yang lebih stabil dan reliabel

---

## 5. Evaluasi dan Pembahasan Hasil Klasifikasi

### 5.1 Metrik Evaluasi

Model dievaluasi menggunakan beberapa metrik, yaitu:
- **Accuracy**
- **Precision**
- **Recall**
- **F1-Score**

Penggunaan metrik ini penting karena pada kasus ujaran kebencian, kesalahan klasifikasi dapat berdampak sosial sehingga tidak cukup hanya mengandalkan akurasi saja.

### 5.2 Hasil Evaluasi

- Model **SVM Multi-class** menunjukkan performa yang lebih stabil dan cenderung lebih baik dibandingkan Naive Bayes.
- Model **Naive Bayes** tetap memberikan hasil yang cukup baik dengan waktu komputasi yang lebih cepat, namun kurang optimal dalam menangani kelas yang saling tumpang tindih.
- Hasil K-Fold Cross Validation menunjukkan bahwa SVM memiliki rata-rata nilai evaluasi yang lebih tinggi dengan variasi antar fold yang lebih kecil.

### 5.3 Pembahasan

- Kata-kata tertentu memiliki dominasi yang kuat pada kelas Hate Speech dan Abusive.
- Beberapa tweet sulit diklasifikasikan secara akurat karena:
  - Ambiguitas bahasa
  - Penggunaan sarkasme
- Secara keseluruhan, model yang dibangun sudah cukup baik untuk dijadikan **baseline sistem klasifikasi ujaran kebencian otomatis**.

---

## 6. Kesimpulan

- Sistem klasifikasi ujaran kebencian berbasis Machine Learning berhasil dibangun.
- Representasi fitur menggunakan **TF-IDF** terbukti efektif untuk data teks.
- Model **Support Vector Machine (SVM)** memberikan performa terbaik dibandingkan Naive Bayes.
- Sistem ini berpotensi untuk dikembangkan lebih lanjut dengan:
  - Dataset yang lebih besar
  - Model Deep Learning seperti LSTM atau Transformer
  - Analisis konteks bahasa yang lebih kompleks

