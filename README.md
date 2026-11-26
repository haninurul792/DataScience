![Banner Analisis Sentimen Kebijakan Fiskal — EDA & Pemodelan IndoBERT](images/banner_sentimen_fiskal.png)

# Analisis Sentimen Opini Publik terhadap Kebijakan Fiskal di Media Sosial X

**Exploratory Data Analysis (EDA) dan Klasifikasi Sentimen Berbasis Transformer (IndoBERT)**

_Opini publik media sosial X · Preprocessing teks bahasa Indonesia · Visualisasi EDA · Fine-Tuning IndoBERT_

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![HuggingFace](https://img.shields.io/badge/Model-IndoBERT-FFD21E?style=flat-square&logo=huggingface&logoColor=black)](https://huggingface.co/indobenchmark/indobert-base-p1)
[![Platform](https://img.shields.io/badge/Sumber%20Data-Media%20Sosial%20X-000000?style=flat-square&logo=x&logoColor=white)](https://x.com/)
[![Colab](https://img.shields.io/badge/Notebook-Google%20Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/haninurul792/DataScience/blob/main/EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb)

[Ringkasan](#ringkasan-proyek) · [Temuan EDA](#temuan-utama-eda) · [Grafik EDA](#grafik-eda) · [Alur & Metode](#alur-dan-metode) · [Evaluasi Model](#evaluasi-model) · [Dokumen](#dokumen-proyek) · [Struktur](#struktur-repository) · [Tutorial](#tutorial-menjalankan-notebook)

> [!IMPORTANT]
> Dataset yang dianalisis berasal dari opini publik terbuka di media sosial **X (Twitter)** terkait wacana kebijakan fiskal dan administrasi perpajakan. Seluruh data telah melalui tahap **anonimisasi identitas akun** dan pembersihan teks untuk kepentingan riset akademik.

---

## Ringkasan Proyek

Kebijakan fiskal pemerintah—seperti pembaruan sistem administrasi perpajakan, pengelolaan anggaran negara, subsidi, dan penyesuaian tarif—selalu memicu diskusi dinamis di media sosial **X**. Namun, data teks media sosial memiliki karakteristik tidak terstruktur, penuh dengan bahasa gaul, singkatan, serta nuansa sarkasme yang sulit dipahami oleh metode analisis leksikon konvensional.

Proyek ini melakukan **Exploratory Data Analysis (EDA)** secara mendalam untuk memetakan pola distribusi opini, panjang teks, dan kata kunci dominan, kemudian menerapkan arsitektur *Transformer* lokal **IndoBERT** untuk mengklasifikasikan polaritas sentimen publik secara akurat.

| Komponen | Keterangan |
| :--- | :--- |
| **Objek penelitian** | Opini publik media sosial X terhadap kebijakan fiskal |
| **Unit analisis** | Satu unggahan/cuitan teks bahasa Indonesia yang telah dibersihkan |
| **Fokus EDA** | Distribusi kelas sentimen, frekuensi kata/n-gram, panjang token, dan kualitas data |
| **Arsitektur model** | Fine-Tuning Pre-trained Transformer (**IndoBERT**) |
| **Teknologi** | Python, pandas, NumPy, Matplotlib, seaborn, WordCloud, PyTorch, Hugging Face Transformers |

---

## Temuan Utama EDA

Hasil eksplorasi dan pembersihan data dijalankan melalui notebook [`EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb`](EDA_Sentimen_Kebijakan_Fiskal_X_IndoBERT_Lengkap.ipynb).

| Indikator | Hasil Analisis | Interpretasi |
| :--- | :---: | :--- |
| **Total dataset bersih** | `[Isi jumlah baris bersih]` cuitan | Setelah penghapusan duplikasi, *retweet* identik, dan teks kosong |
| **Distribusi sentimen dominan** | `[Misal: Negatif XX%]` | Mayoritas diskusi publik menyoroti evaluasi dan kritik kebijakan |
| **Rata-rata panjang teks** | `[Isi rata-rata]` kata / token | Sesuai untuk pemrosesan *max_length* 128 token pada IndoBERT |
| **Data kosong & duplikat** | `0` baris setelah cleaning | Seluruh noise URL, mention `@user`, dan karakter non-alfanumerik dibersihkan |
| **Kata kunci paling sering** | `pajak`, `fiskal`, `anggaran`, `kebijakan` | Merepresentasikan topik inti diskursus ekonomi makro di linimasa |

### Karakteristik dan Kualitas Data Teks

- **Pembersihan Teks (*Text Preprocessing*):** Penghapusan tautan (`http/https`), *mention*, tagar berlebihan, tanda baca berulang, serta normalisasi kata tidak baku khas media sosial Indonesia.
- **Penanganan Konteks Bahasa:** Menggunakan tokenizer sub-kata (*WordPiece*) bawaan IndoBERT sehingga mampu mengenali kata berimbuhan kompleks maupun istilah teknis perpajakan/fiskal.
- **Keseimbangan Kelas (*Class Balance*):** Distribusi label sentimen (**Positif**, **Netral**, **Negatif**) diperiksa terlebih dahulu sebelum pembagian data latih (*train*), validasi (*validation*), dan uji (*test*).

---

## Grafik EDA

*(Unggah gambar `.jpg` hasil ekstraksi Google Colab ke dalam folder `images/` dan sesuaikan nama filenya di bawah ini)*

| Distribusi Kelas Sentimen | WordCloud Kata Dominan |
| :---: | :---: |
| ![Distribusi kelas sentimen publik](images/01_distribusi_sentimen.jpg) | ![WordCloud opini kebijakan fiskal](images/02_wordcloud_fiskal.jpg) |

| Distribusi Panjang Teks / Token | Top N-Gram & Frekuensi Kata |
| :---: | :---: |
| ![Distribusi panjang kata dan token](images/03_distribusi_panjang_teks.jpg) | ![Top Bigram dan Trigram](images/04_top_ngram.jpg) |

Seluruh visualisasi beresolusi tinggi tersedia pada folder [`images/`](images/).

---

## Alur dan Metode

```text
Data Opini Publik Media Sosial X (CSV)
                 │
                 ▼
   Pemuatan & Pembersihan Data (Preprocessing)
   • hapus duplikat, URL, mention, & normalisasi teks
                 │
                 ▼
   Exploratory Data Analysis (EDA)
   • distribusi sentimen, panjang token, WordCloud & N-Gram
                 │
                 ▼
   Tokenisasi & Pembagian Dataset
   • IndoBERT WordPiece Tokenizer (Train / Val / Test)
                 │
                 ▼
   Fine-Tuning Model IndoBERT & Evaluasi
   • Accuracy, Precision, Recall, F1-Score, Confusion Matrix
