# Twitter Entity Sentiment Analysis

## Project Overview

Proyek ini bertujuan untuk melakukan analisis sentimen terhadap tweet berdasarkan entitas yang berupa game, device, platform media sosial. Setiap tweet dalam dataset telah diberi label sentimen (`Positive`, `Negative`, `Neutral`) ada juga tambaan label `irrelevant` yaitu data komentar yang tidak mengandung sentimen yang relevan terhadap entitas yang disebutkan. Analisis ini dapat digunakan untuk mengetahui bagaimana persepsi publik terhadap suatu entitas di media sosial yaitu tweet(X).

Pipeline ini mencakup preprocessing teks, eksplorasi data, pembandingan berbagai model machine learning, dan penyimpanan model akhir.

---

## Raw Dataset

- **Sumber:** [Kaggle - Twitter Entity Sentiment Analysis](https://www.kaggle.com/datasets/jp797498e/twitter-entity-sentiment-analysis/data)
- **Jumlah data:** 74.682 baris (setelah dibersihkan: ~62.000)
- **Fitur:**
  - `ID` — ID unik komentar
  - `Name` — Nama entitas (contoh: *Microsoft*, *Facebook*, *CallOfDuty*)
  - `Sentiment` — Label sentimen (`positive`, `negative`, `neutral`)
  - `Comment` — Teks asli dari komentar
    
- beberapa fitur tambahan dataset yaitu :
  - `cleaned` — Komentar yang telah dibersihkan dari noise
  - `vader_score` & `vader_sentiment` — Sentimen tambahan dari analisis VADER (unsupervised)

---

## Insight & Findings

### Distribusi Sentimen
Visualisasi menunjukkan distribusi label sentimen cukup seimbang:
- `Positive`: dominan pada beberapa entitas
- `Negative` dan `Neutral`: juga cukup signifikan

### Panjang Komentar
Sebagian besar komentar memiliki panjang kurang dari 150 karakter, sesuai dengan batasan Twitter.

### Entitas Populer (Top 10 by Frequency)
| Entitas                   | Jumlah Tweet |
|---------------------------|--------------|
| TomClancysRainbowSix      | 2400         |
| MaddenNFL                 | 2400         |
| Microsoft                 | 2400         |
| LeagueOfLegends           | 2394         |
| CallOfDuty                | 2394         |
| Verizon                   | 2382         |
| CallOfDutyBlackopsColdWar | 2376         |
| ApexLegends               | 2376         |
| Facebook                  | 2370         |
| WorldOfCraft              | 2364         |

### Kualitas Data
- Ditemukan **686 komentar kosong** yang telah dihapus.
- Ditemukan **~8.000 duplikat komentar**, juga telah dihapus.
- Preprocessing dilakukan melalui pembersihan URL, mention, hashtag, dan simbol.

---

## AI Support Explanation

### Preprocessing
- Cleaning teks: menghapus URL, mention, hashtag, tanda baca, huruf kecil
- Tokenisasi + TF-IDF (`max_features=5000`)
- Label dikonversi ke huruf kecil untuk konsistensi

### Model Pembanding
Sebanyak **11 model machine learning** diuji dan dibandingkan:
- **Linear Models**: Logistic Regression, SGD, LinearSVC
- **Tree-based Models**: Decision Tree, Random Forest, Gradient Boosting, AdaBoost
- **Others**: K-Nearest Neighbors, MLPClassifier, Naive Bayes, DummyClassifier

### Evaluasi
Metrik yang digunakan:
- Accuracy
- Precision (weighted)
- Recall (weighted)
- F1-Score (weighted)
- Confusion Matrix

### Hasil Terbaik
- Model **Random Forest Classifier** menunjukkan **kinerja terbaik**, dengan skor akurasi dan F1 yang konsisten tinggi.

### Ekstra: VADER Analysis
Selain model supervised, proyek ini juga menggunakan **VADER (Valence Aware Dictionary and sEntiment Reasoner)** untuk memberikan sudut pandang tambahan terhadap sentimen secara leksikal.

---

## Model Deployment

- Model dan vectorizer disimpan menggunakan `joblib`:
  ```python
  joblib.dump(model, 'sentiment_model.pkl')
  joblib.dump(tfidf, 'vectorizer.pkl')
