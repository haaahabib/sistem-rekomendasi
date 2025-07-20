# Sistem Rekomendasi Film [Content-Based & Collaborative Filtering]

Proyek ini bertujuan untuk membangun dan membandingkan dua jenis sistem rekomendasi film yang populer: **Content-Based Filtering** dan **Collaborative Filtering**. Tujuannya adalah untuk memberikan rekomendasi film yang paling relevan kepada pengguna berdasarkan data historis.

---

## Daftar Isi

1.  [Latar Belakang](#latar-belakang)
2.  [Tujuan Proyek](#tujuan-proyek)
3.  [Dataset](#dataset)
4.  [Metodologi](#metodologi)
5.  [Hasil & Perbandingan Model](#hasil--perbandingan-model)
6.  [Tech Stack](#tech-stack)
7.  [Cara Menjalankan Proyek](#cara-menjalankan-proyek)
   
---

## Latar Belakang

Di tengah melimpahnya pilihan film yang tersedia di berbagai platform, sistem rekomendasi menjadi alat yang sangat penting. Sistem ini membantu pengguna menemukan film baru yang mungkin mereka sukai, sehingga meningkatkan pengalaman pengguna dan keterlibatan (engagement) pada platform. Proyek ini mengeksplorasi dua pendekatan utama dalam membangun sistem rekomendasi.

## Tujuan Proyek

-   Menerapkan **Content-Based Filtering** untuk merekomendasikan film berdasarkan kemiripan atribut (seperti genre, sutradara, dan aktor).
-   Menerapkan **Collaborative Filtering** untuk merekomendasikan film berdasarkan kemiripan pola rating antar pengguna.
-   Mengevaluasi dan membandingkan performa kedua metode menggunakan metrik **RMSE (Root Mean Squared Error)**.
-   Menentukan pendekatan mana yang memberikan rekomendasi paling akurat untuk dataset yang digunakan.

---

## Dataset

Dataset yang digunakan dalam proyek ini adalah **"The Movies Dataset"** yang bersumber dari Kaggle. Dataset ini berisi informasi metadata dari puluhan ribu film, termasuk genre, rating, judul, dan lain-lain.

-   **Sumber Dataset**: [The Movies Dataset - Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset)

---

## Metodologi

Dua pendekatan sistem rekomendasi dibangun dan dibandingkan dalam proyek ini:

1.  **Content-Based Filtering**
    -   **Konsep**: Merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu.
    -   **Proses**:
        1.  Fitur-fitur teks dari film (seperti judul, genre, dan kata kunci) digabungkan.
        2.  Teks tersebut diubah menjadi representasi vektor numerik menggunakan **TF-IDF (Term Frequency-Inverse Document Frequency)**.
        3.  Kemiripan antar film dihitung menggunakan **Cosine Similarity**.

2.  **Collaborative Filtering**
    -   **Konsep**: Merekomendasikan item berdasarkan preferensi dari pengguna lain yang memiliki selera serupa.
    -   **Proses**:
        1.  Menggunakan data rating yang diberikan oleh pengguna ke film.
        2.  Algoritma **Singular Value Decomposition (SVD)** dari library Surprise digunakan untuk memprediksi rating yang mungkin diberikan pengguna pada film yang belum ia tonton.

---

## Hasil & Perbandingan Model

Evaluasi dilakukan dengan mengukur **RMSE (Root Mean Squared Error)**, di mana nilai yang lebih rendah menunjukkan performa model yang lebih baik dalam memprediksi rating.

| Metode Rekomendasi | RMSE (Error) | Keterangan |
| :--- | :---: | :--- |
| **Collaborative Filtering (SVD)** | **0.89** | **Performa Terbaik**. Model ini lebih akurat dalam memprediksi rating pengguna. |
| **Content-Based Filtering** | 2.88 | Tingkat error lebih tinggi, kurang akurat dibandingkan Collaborative Filtering. |

**Kesimpulan**: Untuk dataset ini, **Collaborative Filtering** terbukti menjadi pendekatan yang lebih unggul karena mampu menangkap preferensi pengguna secara lebih akurat.

---

## Tech Stack

-   **Bahasa Pemrograman**: Python
-   **Library Utama**:
    -   Pandas & NumPy (Manipulasi Data)
    -   Scikit-learn (TF-IDF & Cosine Similarity)
    -   Surprise (Untuk Collaborative Filtering - SVD)
    -   Matplotlib & Seaborn (Visualisasi)

---

## Cara Menjalankan Proyek

1.  **Clone Repositori Ini**
    ```bash
    git clone https://github.com/haaahabib/sistem-rekomendasi.git
    ```
2.  **Masuk ke Direktori Proyek**
    ```bash
    cd sistem-rekomendasi
    ```
3.  **Install Library yang Dibutuhkan**
    ```bash
    pip install pandas numpy scikit-learn scikit-surprise matplotlib seaborn jupyter
    ```
4.  **Jalankan Jupyter Notebook**
    Buka dan jalankan file `main.ipynb` untuk melihat keseluruhan alur kerja proyek.
    ```bash
    jupyter notebook main.ipynb
    ```
