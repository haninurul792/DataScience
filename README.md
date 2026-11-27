![Banner Analisis Sentimen Kebijakan Fiskal — EDA & Pemodelan IndoBERT](Output/00_banner_header.jpg)

# Analisis Sentimen Opini Publik terhadap Kebijakan Fiskal di Media Sosial X

**Web Scraping, Exploratory Data Analysis (EDA), dan Klasifikasi Sentimen Berbasis Pre-Trained Transformer (IndoBERT)**

_Scraping Opini Publik Media Sosial X · Text Preprocessing Bahasa Indonesia · Deteksi Outlier (IQR) · Fine-Tuning IndoBERT_

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![HuggingFace](https://img.shields.io/badge/Pretrained-IndoBERT-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/indobenchmark/indobert-base-p1)
[![Dataset Bersih](https://img.shields.io/badge/Dataset%20Bersih-IndoBERT%20Ready-217346?style=flat-square&logo=microsoftexcel&logoColor=white)](Dataset%20X%20Fiskal%20Bersih%20IndoBERT.xlsx)
[![Colab Scraping](https://img.shields.io/badge/Colab-1.%20Scraping%20%26%20EDA-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/Scraping%20EDA.ipynb)
[![Colab IndoBERT](https://img.shields.io/badge/Colab-2.%20EDA%20%26%20IndoBERT-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)

[Ringkasan](#ringkasan-proyek) · [Latar Belakang](#latar-belakang-dan-tujuan) · [Temuan EDA](#temuan-utama-eda) · [Galeri Visualisasi](#galeri-visualisasi-eda) · [Metodologi](#alur-dan-metodologi) · [Kesimpulan & Rekomendasi](#kesimpulan-dan-rekomendasi-langkah-selanjutnya) · [Dokumen & Repo](#dokumen-dan-artefak-proyek) · [Tutorial](#tutorial-menjalankan-proyek)

> [!IMPORTANT]
> Seluruh data pada repositori ini dikumpulkan melalui proses *scraping* opini publik terbuka di media sosial **X (Twitter)** terkait diskursus kebijakan fiskal pada masa jabatan Menteri Keuangan Purbaya Yudhi Sadewa (`Data_Mentah_Twitter_Purbaya_Fiskal.xlsx`) dan telah diproses menjadi korpus terkurasi (`Dataset X Fiskal Bersih IndoBERT.xlsx`) melalui tahapan **anonimisasi identitas akun**, penghapusan *noise*, serta seleksi panjang teks untuk kepentingan riset akademik Mata Kuliah Data Science.

---

## Ringkasan Proyek

Diskursus kebijakan fiskal pemerintah—seperti pengelolaan anggaran negara (APBN), kebijakan perpajakan, subsidi, dan stimulus ekonomi—menghasilkan arus opini publik yang dinamis di media sosial **X**. Namun, data teks media sosial memiliki karakteristik tidak terstruktur, penuh singkatan, bahasa gaul, serta nuansa sarkasme yang sering gagal dipahami oleh pendekatan analisis berbasis leksikon maupun statistik kata konvensional.

Repositori ini mendokumentasikan alur *end-to-end* mulai dari **pengumpulan data (*Web Scraping*) dan eksplorasi awal** pada notebook [`Scraping EDA.ipynb`](Scraping%20EDA.ipynb), dilanjutkan dengan **Exploratory Data Analysis (EDA) mendalam, pembersihan korpus siap latih, deteksi pencilan (*outlier*), serta klasifikasi sentimen berbasis Transformer (IndoBERT)** pada notebook [`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb) beserta dokumentasi ilmiahnya dalam **Laporan EDA Analisis Sentimen Kebijakan Fiskal**.

| Komponen Penelitian | Spesifikasi & Keterangan |
| :--- | :--- |
| **Domain & Objek** | Opini publik media sosial X terhadap kebijakan fiskal nasional |
| **Tahap 1 — Akuisisi Data** | Web Scraping cuitan media sosial X ([`Scraping EDA.ipynb`](Scraping%20EDA.ipynb)) menghasilkan [`Data_Mentah_Twitter_Purbaya_Fiskal.xlsx`](Data_Mentah_Twitter_Purbaya_Fiskal.xlsx) |
| **Tahap 2 — EDA & Pemodelan** | Pembersihan teks, korelasi Spearman, deteksi outlier (IQR), & Fine-Tuning **IndoBERT** ([`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)) |
| **Dataset Bersih Siap Latih** | [`Dataset X Fiskal Bersih IndoBERT.xlsx`](Dataset%20X%20Fiskal%20Bersih%20IndoBERT.xlsx) |
| **Laporan Dokumentasi EDA** | **Laporan EDA Analisis Sentimen Kebijakan Fiskal** *(tersedia di direktori utama repositori)* |
| **Ekosistem Pustaka** | `pandas`, `openpyxl`, `numpy`, `matplotlib`, `seaborn`, `wordcloud`, `scikit-learn`, `torch`, `transformers` |

---

## Latar Belakang dan Tujuan

1. **Akuisisi Data Opini Publik Terarah (*Targeted Scraping*):** Mengumpulkan korpus cuitan berbahasa Indonesia yang relevan dengan wacana kebijakan fiskal dan perpajakan di media sosial X sebagai fondasi empiris penelitian.
2. **Pemetaan Kualitas & Struktur Data Teks (EDA):** Mengidentifikasi nilai hilang (*missing values*), kemiringan distribusi (*skewness & kurtosis*), korelasi antarvariabel (*Spearman*), serta anomali panjang teks (*outlier IQR*) sebelum memasuki tahap pemodelan *deep learning*.
3. **Klasifikasi Sentimen Kontekstual dengan IndoBERT:** Memanfaatkan mekanisme *self-attention* dua arah (*bidirectional*) dan tokenisasi sub-kata (*WordPiece*) pada **IndoBERT** untuk menangkap istilah teknis ekonomi/fiskal serta struktur kalimat tidak baku di media sosial.

---

## Temuan Utama EDA

Seluruh proses pengumpulan data, inspeksi statistik, pembersihan teks, dan pelatihan model terdokumentasi di dalam kedua notebook serta laporan EDA pada repositori ini.

| Dimensi Analisis | Temuan & Metode | Implikasi Pemodelan |
| :--- | :--- | :--- |
| **Akuisisi & Korpus Data** | Pengumpulan 3.972 observasi cuitan (35 kolom) melalui [`Scraping EDA.ipynb`](Scraping%20EDA.ipynb) ke dalam [`Data_Mentah_Twitter_Purbaya_Fiskal.xlsx`](Data_Mentah_Twitter_Purbaya_Fiskal.xlsx). | Menyediakan korpus awal domain-spesifik kebijakan fiskal berbahasa Indonesia. |
| **Pembersihan & Trimming Korpus** | Audit missing values, normalisasi tipe waktu (`datetime64[ns, UTC]`), penghapusan duplikasi/URL/mention, serta *trimming* teks `< 3` kata menjadi [`Dataset X Fiskal Bersih IndoBERT.xlsx`](Dataset%20X%20Fiskal%20Bersih%20IndoBERT.xlsx). | Menjamin setiap sampel memiliki konteks semantik yang utuh sebelum proses tokenisasi. |
| **Distribusi, Skewness & Transformasi** | Analisis *Skewness & Kurtosis* serta penerapan *Log Transformation* (`np.log1p`) pada variabel numerik interaksi. | Menormalkan distribusi fitur pendukung yang miring ekstrem (*right-skewed*). |
| **Korelasi Non-Parametrik & Outlier** | Uji **Korelasi Spearman** dan deteksi pencilan metode **IQR** pada jumlah kata (`word_count`) dan interaksi (`favorite_count`). | Menjadi dasar empiris penentuan batas panjang urutan (*`max_length`*) pada tokenizer IndoBERT. |

---

## Galeri Visualisasi EDA

Seluruh grafik hasil analisis diekspor dalam resolusi tinggi ke dalam folder [`Output/`](Output/) dan ditautkan langsung di bawah ini:

| 1. Audit Missing Values | 2. Analisis Skewness & Kurtosis |
| :---: | :---: |
| ![Tabel Jumlah dan Persentase Missing](Output/01%20Tabel%20jumlah%20dan%20persentase%20missing.jpg) | ![Menghitung Skewness dan Kurtosis](Output/02%20Menghitung%20Skewness%20dan%20Kurtosis.jpg) |

| 3. Penerapan Log Transformation | 4. Distribusi Fitur Numerik & Teks |
| :---: | :---: |
| ![Menerapkan Log Transformation](Output/03%20Menerapkan%20Log%20Transformation%20np%20lo.jpg) | ![Visualisasi Subplots 1](Output/04%20fig%20axes%20plt%20subplots%201%202%20figs.jpg) |

| 5. Perbandingan Distribusi Lanjutan | 6. Matriks Korelasi Spearman |
| :---: | :---: |
| ![Visualisasi Subplots 2](Output/05%20fig%20axes%20plt%20subplots%201%202%20figs.jpg) | ![Korelasi Spearman](Output/06%20Menggunakan%20Korelasi%20Spearman%20karen.jpg) |

| 7. Deteksi Outlier Panjang Teks & Likes (IQR Series) |
| :---: |
| ![Deteksi Outlier IQR Series](Output/07%20def%20deteksi%20outlier%20iqr%20series.jpg) |

---

## Alur dan Metodologi

```text
┌─────────────────────────────────────────────────────────────────┐
│  1. DATA SCRAPING & INITIAL EDA (Scraping EDA.ipynb)            │
│     • Pengumpulan cuitan opini publik dari media sosial X       │
│     • Ekspor data mentah: Data_Mentah_Twitter_Purbaya_Fiskal.xlsx│
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. TEXT PREPROCESSING, DATA QUALITY AUDIT & TRIMMING           │
│     • Audit missing values, konversi datetime, hapus URL/mention│
│     • Trimming teks < 3 kata -> Dataset X Fiskal Bersih IndoBERT│
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. EXPLORATORY DATA ANALYSIS (EDA) STATISTIK & VISUAL          │
│     • Skewness, Kurtosis, Log Transformation, & Korelasi Spearman│
│     • Deteksi outlier IQR (word_count & favorite_count)         │
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  4. TOKENIZATION & DATA SPLITTING                               │
│     • IndoBERT WordPiece Tokenizer ([CLS], [SEP], Attention Mask)│
│     • Pembagian Stratified Train / Validation / Test Set        │
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  5. FINE-TUNING INDOBERT & EVALUATION                           │
│     • Pelatihan klasifikasi berbasis PyTorch / Hugging Face     │
│     • Evaluasi Accuracy, Precision, Recall, F1 & Confusion Matrix│
└─────────────────────────────────────────────────────────────────┘
````
---

## Kesimpulan dan Rekomendasi Langkah Selanjutnya

### Ringkasan Temuan Utama
1. **Ketidakseimbangan Kelas (*Class Imbalance*):** Distribusi opini publik terhadap kebijakan fiskal Menteri Keuangan Purbaya didominasi oleh kelas **Netral** (65–70%) dan kelas **Negatif** (15–20%), sedangkan opini **Positif** merupakan kelas minoritas. Oleh karena itu, penggunaan metrik evaluasi **Macro F1-Score** pada pengujian model IndoBERT sangat krusial.
2. **Karakteristik Panjang Teks & Tokenisasi:** Rata-rata panjang cuitan adalah **82,87 kata** (median: **37 kata**). Setelah diuji menggunakan *WordPiece Tokenizer* dari `indobenchmark/indobert-base-p1`, penetapan batas maksimal `max_length = 128` token merupakan keputusan yang optimal karena mampu mengover lebih dari **99%** data teks bersih tanpa terjadi pemotongan (*truncation*) informasi kontekstual yang penting.
3. **Pola Viralitas & *Skewness* Ekstrem:** Variabel interaksi seperti *likes* (`favorite_count`) dan *retweets* (`retweet_count`) memiliki nilai *skewness* positif yang sangat ekstrem (masing-masing sebesar **22,29** dan **24,95**). Hal ini menunjukkan adanya fenomena *power-law* di platform X, di mana sebagian besar cuitan hampir tidak mendapatkan interaksi (median `favorite = 4`), sedangkan diskusi publik didominasi oleh segelintir opini kritis yang sangat viral.
4. **Korelasi & Fokus Isu:** Berdasarkan korelasi **Spearman**, metrik keterlibatan publik berkorelasi kuat satu sama lain tetapi memiliki korelasi yang sangat lemah dengan panjang cuitan. Diskursus publik didominasi oleh kata kunci utama **"purbaya"** (**5.307** kemunculan) dan **"pajak"** (**3.405** kemunculan), mengindikasikan bahwa perhatian utama masyarakat tertuju pada regulasi perpajakan nasional.

### Keterbatasan dan Kendala Analisis
* **Bahasa Non-formal dan Sarkasme:** Teks opini di platform X kaya akan penggunaan bahasa *slang*, singkatan, dan sarkasme politik-ekonomi yang membutuhkan penanganan khusus agar tidak salah diinterpretasikan oleh model NLP.
* **Keterbatasan API & Dimensi Multimodal:** Analisis dibatasi pada konten berbasis teks berbahasa Indonesia tanpa menyertakan media gambar, infografis, atau video yang sering dilampirkan pengguna untuk mendukung argumen mereka.

### Rekomendasi Langkah Selanjutnya (Pemodelan)
* **Arsitektur Model:** Menggunakan model *pre-trained* **IndoBERT** (`indobenchmark/indobert-base-p1`) yang telah dilatih pada miliaran token bahasa Indonesia formal dan kolokial.
* **Fungsi Kerugian Kustom (*Custom Loss Function*):** Menerapkan ***Class-Weighted Cross-Entropy Loss*** pada data latih (80% *training set*) guna mengompensasi ketidakseimbangan kelas (*class imbalance*) yang terdeteksi pada EDA, sehingga model tidak bias dalam mendeteksi opini **Positif** dan **Negatif**.
