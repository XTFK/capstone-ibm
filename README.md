# 📊 Analisis Sentimen Komentar YouTube

Proyek ini melakukan **analisis sentimen** terhadap komentar YouTube menggunakan pendekatan **Text Mining** dan **berbagai algoritma Machine Learning**, seperti LinearSVC, Naive Bayes, dan Random Forest. Data diproses, divisualisasikan, dan dimodelkan untuk mengklasifikasikan komentar sebagai _positive_, _negative_, atau _neutral_.

## 🧾 Deskripsi Dataset

Dataset berisi komentar YouTube channel beserta atribut seperti `likeCount` dan `publishedAt`, disimpan dalam file CSV `youtube-comments.csv`.

## 🚀 Fitur

- Pembersihan data teks komentar
- Visualisasi panjang komentar, distribusi likes, dan waktu publikasi
- Deteksi outlier
- Analisis sentimen menggunakan **VADER Lexicon**
- Penghapusan komentar netral untuk fokus klasifikasi
- Vektorisasi teks menggunakan **TF-IDF**
- Evaluasi dan perbandingan 12 algoritma klasifikasi
- Penyimpanan model terbaik (LinearSVC) dalam bentuk `.pkl`

## 📦 Instalasi

1. Clone repositori:
   ```bash
   git clone https://github.com/XTFK/capstone-ibm.git
   cd capstone-ibm
