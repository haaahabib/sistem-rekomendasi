# Laporan Proyek Machine Learning - Muhammad Habibulloh

![download](https://github.com/user-attachments/assets/c4d9e51a-5cd4-47e3-a5ef-d18eee6cedf3)

## Project Overview

Sistem rekomendasi buku menjadi kunci penting untuk meningkatkan pengalaman pengguna (experience) di platform literasi digital. Pembaca sering kali kesulitan menemukan buku baru yang sesuai preferensi karena banyaknya pilihan [[1]](https://jurnal.itbsemarang.ac.id/index.php/JPTIS/article/view/818), [[2]](https://jurnal.uns.ac.id/joive/article/view/53618), [[3]](https://jurnal.polgan.ac.id/index.php/remik/article/view/14515). Proyek ini bertujuan untuk membangun sistem rekomendasi berbasis konten dan popularitas untuk memecahkan masalah tersebut. Dataset yang digunakan mencakup 10.000 buku dari Goodreads, dengan referensi utama dari daftar "Books That Everyone Should Read At Least Once" [[4]](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv).

## Referensi

1. F. Ertandi and M. Akbar, "Sistem Pendukung Keputusan Rekomendasi Buku Novel menggunakan Metode Weighted Product," Renik: Riset dan E-Jurnal Manajemen Informatika Komputer, vol. 9, no. 1, pp. 366–381, Jan. 2025. doi: 10.33395/renik.v9i1.14515.
2. E. G. E. Devara et al., "Pengembangan Teknologi Rekomendasi Kecerdasan Buatan yang Digunakan pada Perpustakaan," Journal of Informatics and Vocational Education (JOIVE), vol. 4, no. 3, pp. 87–92, Oct. 2021. doi: 10.20961/joive.v4i3.53618.
3. K. Harahap et al., "Aplikasi Baca Buku Platform Digital Yang Dirancang Untuk Memfasilitasi Pengguna Dalam Membaca Berbagai Jenis Buku Elektronik," Jurnal Penelitian Teknologi Informasi Dan Sains, vol. 1, no. 3, pp. 94–102, Sep. 2023. doi: 10.54066/jptis.v1i3.818.
4. Dataset: Best Books (10k) Multi-Genre Data, [Kaggle](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv)

## Business Understanding

### Problem Statements

- Pengguna/pembaca kesulitan menemukan buku sesuai preferensi genre
- Platform membutuhkan rekomendasi buku populer untuk meningkatkan engagement

### Goals

- Membangun sistem rekomendasi berbasis genre dan deskripsi buku (content-based filtering)
- Menyediakan daftar buku populer berdasarkan rating dan jumlah ulasan (popularity-based filtering)

## Solution statements

- Content-Based Filtering, menggunakan TF-IDF dan cosine similarity untuk merekomendasikan buku dengan konten serupa.
- Popularity-Based Filtering, merekomendasikan buku dengan skor popularitas tertinggi (Num_Ratings x Avg_Rating).

## Data Understanding

### Sumber Dataset

Dataset diambil dari Kaggle
[Best Books (10k) Multi-Genre Data](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv), Dataset memiliki 10.000 baris dan 8 kolom, dengan variabel sebagai berikut:
- unnamed column (hanya no. urutan)
- Book: Judul buku
- Author: Penulis
- Genres: Daftar genre (multi-label)
- Description: Deskripsi buku
- Avg_Rating: Rata-rata rating (0-5)
- Num_Ratings: Jumlah ulasan
- URL: Goodreads URL

### Eksplorasi Data 

- Jumlah Data total yaitu 10.000 buku.
- Missing Values: Terdapat 77 data hilang pada kolom Description, yang diatasi dengan penghapusan baris
- Distribusi Genre yang sangat beragam, namun ini adalah top 15 atau 15 genre terbanyak dari dataset yang bisa ditampilkan
  ![image](https://github.com/user-attachments/assets/c6038cb5-1546-479e-a4f7-21aba10170da)

## Data Preparation

Berikut tahapan dalam data preparation yang dilakukan:

1. Data Cleaning
- Menghapus baris dengan nilai kosong pada kolom ```Description``` dan ```Genres``` menggunakan ```df.dropna()```
- Memformat kolom 'Genres' dengan menghapus karakter yang tidak diinginkan
- 
  
2. Menggabungkan Fitur Teks
- Menggabungkan kolom 'Genres' dan 'Description' menjadi satu kolom 'content' untuk digunakan dalam model berbasis konten

Tujuan dari tahapan ini adalah untuk memastikan data bersih, konsisten, dan dalam format yang sesuai untuk analisis dan pemodelan, yang penting untuk akurasi sistem rekomendasi. 

## Modeling

1. Content-Based Filtering Model
- Implementasi
  Model ini merekomendasikan buku berdasarkan kesamaan konten (genre dan deskripsi)
    a. Menggunakan TF-IDF Vectorizer untuk mengubah teks (genre dan deskripsi) menjadi matriks TF-IDF
    b. Menghitung Cosine Similarity antara matriks TF-IDF untuk mengetahui tingkat kemiripan antar buku
    c. Fungsi get_content_recommendations mengambil judul buku dan mengembalikan daftar rekomendasi buku serupa berdasarkan skor kesamaan
- Kelebihan: mampu merekomendasikan item yang disukai pengguna/pembaca bahkan jika item tersebut jarang atau baru dan juga rekomendasi relevan dengan preferensi pengguna/pembaca terhadap konten.
- Kekurangan: cenderung merekomendasikan item yang sangat mirip atau yang sudah dibaca maupun diketahui pengguna/pembaca

2. Popularity-Based Recommendation
- Implementasi
  Model ini merekomendasikan buku yang paling populer di antara semua buku, dengan
    a. Popularitas dihitung berdasarkan kombinasi Num_Ratings dan Avg_Rating (popularity_score)
    b. Fungsi get_popular_books mengembalikan daftar buku teratas berdasarkan skor popularitas tertinggi
- Kelebihan: mudah diimplementasikan dan memberikan rekomendasi yang relevan untuk pengguna baru dan cocok untuk menyoroti item yang sedang tren atau disukai banyak orang
- Kekurangan: tidak mempertimbangkan preferensi individu pengguna/pembaca, berdasarakan popularity score.

## Evaluation

1. Content-Based Filtering
- Menggunakan metrik precision@k (k=5). Precision dihitung dengan mengambil sampel buku secara acak. Untuk setiap buku sampel, model merekomendasikan buku-buku lain. Kemudian, diukur berapa persentase rekomendasi tersebut yang memiliki setidaknya satu genre yang sama dengan buku sampel. Rata-rata persentase = nilai Precision.
- Hasilnya  Precision: 56.00%. artinya model Content-Based Filtering memiliki kemampuan di atas 50% untuk merekomendasikan buku dengan genre yang serupa atau berarti model cenderung merekomendasikan buku yang relevan secara genre

2. Popularity-Based Recommendation
- Metrik: Bestseller Ratio in Top N (N=10)
- Hasilnya 100% yang menunjukkan bahwa semua 10 buku teratas yang direkomendasikan adalah "bestseller" (berdasarkan kriteria Num_Ratings > 900 (asumsi 900 adalah rating top)).

## Kesimpulan

Proyek ini membangun dua model rekomendasi buku:

1. Content-Based Filtering:
   Merekomendasikan buku berdasarkan kesamaan konten (genre, deskripsi). Evaluasi menunjukkan Precision@5 sebesar 56.00%, efektif untuk merekomendasikan buku dengan konten serupa.
2. Popularity-Based Recommendation
   Merekomendasikan buku terpopuler. Evaluasi menunjukkan Bestseller Ratio dalam Top 10 sebesar 100%, berhasil mengidentifikasi buku bestseller.
   
Kedua model ini memberikan cara untuk merekomendasikan buku berdasarkan preferensi konten atau popularitas

**---Terima Kasih---**
