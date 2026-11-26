<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0F2027,50:203A43,100:2C5364&height=210&section=header&text=Analisis%20Sentimen%20Kebijakan%20Fiskal&fontSize=34&fontColor=FFFFFF&fontAlignY=38&desc=Exploratory%20Data%20Analysis%20(EDA)%20%26%20Klasifikasi%20IndoBERT%20%7C%20Opini%20Publik%20Media%20Sosial%20X&descAlignY=58&descSize=15&animation=fadeIn" width="100%" alt="Banner Analisis Sentimen Kebijakan Fiskal" />
</div>

# Analisis Sentimen Opini Publik terhadap Kebijakan Fiskal di Media Sosial X

**Exploratory Data Analysis (EDA) dan Klasifikasi Sentimen Berbasis Transformer (IndoBERT)**

_Dataset Opini Publik Kebijakan Fiskal · Preprocessing Teks Bahasa Indonesia · Visualisasi EDA · Fine-Tuning IndoBERT_

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![HuggingFace](https://img.shields.io/badge/Model-IndoBERT-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/indobenchmark/indobert-base-p1)
[![Dataset](https://img.shields.io/badge/Dataset-DataTwitter__Purbaya__Fiskal.xlsx-217346?style=flat-square&logo=microsoftexcel&logoColor=white)](DataTwitter_Purbaya_Fiskal.xlsx)
[![Colab](https://img.shields.io/badge/Notebook-Google%20Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)

[Ringkasan](#ringkasan-proyek) · [Temuan EDA](#temuan-utama-eda) · [Grafik EDA](#grafik-eda) · [Alur & Metode](#alur-dan-metode) · [Evaluasi Model](#evaluasi-model) · [Dokumen](#dokumen-proyek) · [Struktur](#struktur-repository) · [Tutorial](#tutorial-menjalankan-notebook)

> [!IMPORTANT]
> Dataset dalam proyek ini (`DataTwitter_Purbaya_Fiskal.xlsx`) bersumber dari opini publik terbuka di media sosial **X (Twitter)** terkait diskursus kebijakan fiskal pada era kepemimpinan Menteri Keuangan Purbaya Yudhi Sadewa. Data telah melalui tahapan pembersihan teks (*text preprocessing*) dan anonimisasi untuk keperluan analisis akademik.

---

## Ringkasan Proyek

Kebijakan fiskal pemerintah—meliputi pengelolaan anggaran negara, perpajakan, subsidi, dan stimulus ekonomi—selalu memicu respons beragam dari masyarakat di media sosial **X**. Karakteristik teks media sosial yang tidak terstruktur, penuh singkatan, bahasa gaul, serta ekspresi sarkasme menuntut tahapan eksplorasi data yang cermat dan arsitektur pemodelan bahasa berbasis konteks seperti **IndoBERT**.

Proyek ini berfokus pada **Exploratory Data Analysis (EDA)** untuk memetakan struktur dataset, kualitas teks, distribusi sentimen, hingga deteksi *outlier* panjang teks sebelum melatih model klasifikasi sentimen berbasis *Transformer*.

| Komponen | Keterangan |
| :--- | :--- |
| **Objek penelitian** | Opini publik media sosial X terhadap kebijakan fiskal |
| **Sumber dataset** | [`DataTwitter_Purbaya_Fiskal.xlsx`](DataTwitter_Purbaya_Fiskal.xlsx) |
| **Fokus EDA** | Kualitas data, missing values, distribusi sentimen, panjang teks/token, deteksi outlier (IQR), & WordCloud |
| **Arsitektur model** | Fine-Tuning Pre-trained Transformer (**IndoBERT**) |
| **Teknologi** | Python, pandas, NumPy, Matplotlib, seaborn, WordCloud, PyTorch, Hugging Face Transformers |

---

## Temuan Utama EDA

Seluruh tahapan pemuatan data, eksplorasi statistik, deteksi *outlier*, dan pemodelan dijalankan pada notebook [`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb).

| Indikator | Hasil Analisis | Interpretasi |
| :--- | :---: | :--- |
| **Dataset utama** | `DataTwitter_Purbaya_Fiskal.xlsx` | Data cuitan opini publik terkait kebijakan fiskal di media sosial X |
| **Pembersihan teks** | Bebas duplikasi & noise URL | Menghapus tautan, *mention*, karakter khusus, dan normalisasi teks |
| **Deteksi outlier panjang teks** | Metode **IQR** (`07 def deteksi outlier iqr series.jpg`) | Mengidentifikasi cuitan yang terlalu panjang/pendek sebelum tokenisasi |
| **Representasi token** | WordPiece Tokenizer (IndoBERT) | Menangani kata berimbuhan dan istilah ekonomi/fiskal bahasa Indonesia |

### Karakteristik dan Kualitas Data Teks

- **Text Preprocessing Terstruktur:** Penghapusan noise media sosial (`http/https`, `@username`, simbol berulang) untuk menjaga kualitas fitur semantik.
- **Deteksi Pencilan (*Outlier Detection*):** Menggunakan metode *Interquartile Range* (IQR) untuk memetakan sebaran panjang karakter/kata agar pemilihan parameter `max_length` pada IndoBERT optimal.
- **Visualisasi Eksploratif:** Seluruh grafik hasil analisis tersimpan rapi pada folder [`Output/`](Output/).

---

## Grafik EDA

*(Catatan: Sesuaikan nama file gambar `.jpg` di bawah ini jika ada penomoran urut `01_` sampai `06_` di dalam folder `Output/` Anda; gunakan `%20` untuk menggantikan spasi pada nama file)*

| Grafik 1 — Distribusi Data / Sentimen | Grafik 2 — Visualisasi Eksplorasi Teks |
| :---: | :---: |
| ![Grafik 1](Output/01_distribusi_sentimen.jpg) | ![Grafik 2](Output/02_wordcloud.jpg) |

| Grafik 3 — Analisis Panjang Teks / N-Gram | Grafik 4 — Deteksi Outlier (IQR Series) |
| :---: | :---: |
| ![Grafik 3](Output/03_panjang_teks.jpg) | ![Deteksi Outlier IQR Series](Output/07%20def%20deteksi%20outlier%20iqr%20series.jpg) |

Seluruh keluaran grafik lengkap dapat dilihat langsung pada folder [`Output/`](Output/).

---

## Alur dan Metode

```text
Dataset Opini Publik X (DataTwitter_Purbaya_Fiskal.xlsx)
                         │
                         ▼
      Pemuatan & Pembersihan Data (Preprocessing)
      • hapus duplikat, URL, mention, & normalisasi teks
                         │
                         ▼
      Exploratory Data Analysis (EDA) & Deteksi Outlier
      • distribusi kelas, panjang teks, IQR outlier, WordCloud
                         │
                         ▼
      Tokenisasi & Pembagian Dataset
      • IndoBERT WordPiece Tokenizer (Train / Val / Test)
                         │
                         ▼
      Fine-Tuning Model IndoBERT & Evaluasi Performa
      • Accuracy, Precision, Recall, F1-Score, Confusion Matrix
