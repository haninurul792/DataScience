![Banner Analisis Sentimen Kebijakan Fiskal — EDA & Pemodelan IndoBERT](Output/00_banner_header.jpg)

# Analisis Sentimen Opini Publik terhadap Kebijakan Fiskal di Media Sosial X

**Web Scraping, Exploratory Data Analysis (EDA), dan Klasifikasi Sentimen Berbasis Pre-Trained Transformer (IndoBERT)**

_Scraping Opini Publik Media Sosial X · Text Preprocessing Bahasa Indonesia · Deteksi Outlier (IQR) · Fine-Tuning IndoBERT_

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![HuggingFace](https://img.shields.io/badge/Pretrained-IndoBERT-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/indobenchmark/indobert-base-p1)
[![Dataset](https://img.shields.io/badge/Dataset-DataTwitter__Purbaya__Fiskal.xlsx-217346?style=flat-square&logo=microsoftexcel&logoColor=white)](DataTwitter_Purbaya_Fiskal.xlsx)
[![Colab Scraping](https://img.shields.io/badge/Colab-1.%20Scraping%20%26%20EDA-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/Scraping%20EDA.ipynb)
[![Colab IndoBERT](https://img.shields.io/badge/Colab-2.%20EDA%20%26%20IndoBERT-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)

[Ringkasan](#ringkasan-proyek) · [Latar Belakang](#latar-belakang-dan-tujuan) · [Temuan EDA](#temuan-utama-eda) · [Galeri Visualisasi](#galeri-visualisasi-eda) · [Metodologi](#alur-dan-metodologi) · [Evaluasi Model](#evaluasi-model-indobert) · [Dokumen & Repo](#dokumen-dan-artefak-proyek) · [Tutorial](#tutorial-menjalankan-proyek)

> [!IMPORTANT]
> Seluruh data pada repositori ini (`DataTwitter_Purbaya_Fiskal.xlsx`) dikumpulkan melalui proses *scraping* opini publik terbuka di media sosial **X (Twitter)** terkait diskursus kebijakan fiskal pada masa jabatan Menteri Keuangan Purbaya Yudhi Sadewa. Dataset telah melewati proses **anonimisasi identitas akun** dan pembersihan teks untuk kepentingan riset akademik Mata Kuliah Data Science.

---

## Ringkasan Proyek

Diskursus kebijakan fiskal pemerintah—seperti pengelolaan anggaran negara (APBN), kebijakan perpajakan, subsidi, dan stimulus ekonomi—menghasilkan arus opini publik yang dinamis di media sosial **X**. Namun, data teks media sosial memiliki karakteristik tidak terstruktur, penuh singkatan, bahasa gaul, serta nuansa sarkasme yang sering gagal dipahami oleh pendekatan analisis berbasis leksikon maupun statistik kata konvensional.

Repositori ini mendokumentasikan alur *end-to-end* mulai dari **pengumpulan data (*Web Scraping*) dan eksplorasi awal** pada notebook [`Scraping EDA.ipynb`](Scraping%20EDA.ipynb), dilanjutkan dengan **Exploratory Data Analysis (EDA) mendalam, deteksi pencilan (*outlier*), serta klasifikasi sentimen berbasis Transformer (IndoBERT)** pada notebook [`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb).

| Komponen Penelitian | Spesifikasi & Keterangan |
| :--- | :--- |
| **Domain & Objek** | Opini publik media sosial X terhadap kebijakan fiskal nasional |
| **Tahap 1 — Akuisisi Data** | Web Scraping cuitan media sosial X ([`Scraping EDA.ipynb`](Scraping%20EDA.ipynb)) |
| **Sumber Dataset** | [`DataTwitter_Purbaya_Fiskal.xlsx`](DataTwitter_Purbaya_Fiskal.xlsx) |
| **Tahap 2 — EDA & Pemodelan** | Pembersihan teks, deteksi outlier (IQR), WordCloud, & Fine-Tuning **IndoBERT** ([`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)) |
| **Ekosistem Pustaka** | `pandas`, `openpyxl`, `numpy`, `matplotlib`, `seaborn`, `wordcloud`, `scikit-learn`, `torch`, `transformers` |

---

## Latar Belakang dan Tujuan

1. **Akuisisi Data Opini Publik Terarah (*Targeted Scraping*):** Mengumpulkan korpus cuitan berbahasa Indonesia yang relevan dengan wacana kebijakan fiskal dan perpajakan di media sosial X sebagai fondasi empiris penelitian.
2. **Pemetaan Kualitas & Struktur Data Teks (EDA):** Mengidentifikasi pola distribusi kelas sentimen, frekuensi kata dominan, serta anomali panjang teks sebelum memasuki tahap pemodelan *deep learning*.
3. **Klasifikasi Sentimen Kontekstual dengan IndoBERT:** Memanfaatkan mekanisme *self-attention* dua arah (*bidirectional*) dan tokenisasi sub-kata (*WordPiece*) pada **IndoBERT** untuk menangkap istilah teknis ekonomi/fiskal serta struktur kalimat tidak baku di media sosial.

---

## Temuan Utama EDA

Seluruh proses pengumpulan data, inspeksi statistik, pembersihan teks, dan pelatihan model terdokumentasi di dalam kedua notebook pada repositori ini.

| Dimensi Analisis | Temuan & Metode | Implikasi Pemodelan |
| :--- | :--- | :--- |
| **Akuisisi & Korpus Data** | Pengumpulan cuitan melalui [`Scraping EDA.ipynb`](Scraping%20EDA.ipynb) dan penyimpanan terstruktur ke [`DataTwitter_Purbaya_Fiskal.xlsx`](DataTwitter_Purbaya_Fiskal.xlsx). | Menyediakan dataset domain-spesifik kebijakan fiskal berbahasa Indonesia. |
| **Integritas & Kebersihan Data** | Penghapusan baris duplikat, *retweet* identik, tautan URL (`http/https`), *mention* (`@user`), dan karakter non-alfanumerik. | Mencegah kebocoran data (*data leakage*) dan mengurangi *noise* pada bobot token. |
| **Deteksi Outlier Panjang Teks** | Analisis *Interquartile Range* (**IQR**) pada distribusi panjang karakter dan jumlah kata per cuitan. | Menjadi dasar empiris penentuan batas panjang urutan (*`max_length`*) pada tokenizer IndoBERT agar efisien di GPU. |
| **Eksplorasi Leksikal & Topik** | Visualisasi *WordCloud* dan distribusi frekuensi kata kunci utama seputar kebijakan fiskal dan perpajakan. | Mengonfirmasi relevansi korpus terhadap isu ekonomi makro dan respons publik. |
| **Representasi Sub-Kata** | Tokenisasi *WordPiece* dengan penyisipan token khusus `[CLS]`, `[SEP]`, dan `[PAD]`. | Mampu memecah kata berimbuhan kompleks dan istilah baru tanpa memicu masalah *Out-of-Vocabulary* (OOV). |

---

## Galeri Visualisasi EDA

Seluruh grafik hasil analisis diekspor dalam resolusi tinggi ke dalam folder [`Output/`](Output/).

> [!NOTE]
> Sesuaikan nama file gambar nomor `01`, `02`, dan `03` di bawah ini dengan nama persis file `.jpg` di dalam folder [`Output/`](Output/) Anda (gunakan `%20` untuk menggantikan spasi).

| Distribusi Kelas Sentimen | WordCloud Opini Kebijakan Fiskal |
| :---: | :---: |
| ![Distribusi Sentimen](Output/01_distribusi_sentimen.jpg) | ![WordCloud Fiskal](Output/02_wordcloud.jpg) |

| Distribusi Panjang Teks & Token | Deteksi Outlier Panjang Teks (IQR Series) |
| :---: | :---: |
| ![Distribusi Panjang Teks](Output/03_panjang_teks.jpg) | ![Deteksi Outlier IQR Series](Output/07%20def%20deteksi%20outlier%20iqr%20series.jpg) |

---

## Alur dan Metodologi

```text
┌─────────────────────────────────────────────────────────────────┐
│  1. DATA SCRAPING & INITIAL EDA (Scraping EDA.ipynb)            │
│     • Pengumpulan cuitan opini publik dari media sosial X       │
│     • Inspeksi struktur awal & ekspor ke Excel (.xlsx)          │
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. TEXT PREPROCESSING & CLEANING                               │
│     • Case folding, hapus URL, mention, tagar, & tanda baca     │
│     • Penghapusan duplikasi & normalisasi teks bahasa Indonesia │
└────────────────────────────────┬────────────────────────────────┘
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. EXPLORATORY DATA ANALYSIS (EDA) LANJUTAN                    │
│     • Proporsi kelas sentimen (Positif / Netral / Negatif)      │
│     • Deteksi outlier panjang teks (IQR) & WordCloud            │
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
