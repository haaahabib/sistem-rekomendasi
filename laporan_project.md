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
- Memformat kolom ```Genres``` dengan menghapus karakter khusus (misal koma (,)) menggunakan regex
  ```
  df_clean = df.dropna(subset=['Description', 'Genres']).copy()  
  df_clean['Genres'] = df_clean['Genres'].str.replace(r'[\[\]\']', '', regex=True)
  ```
  
2. Penggabungan Fitur Teks
- Menggabungkan kolom ```Genres``` dan ```Description``` menjadi satu kolom ```content``` untuk merepresentasikan konten buku
  ```
  df_clean['content'] = df_clean['Genres'] + ' ' + df_clean['Description']  
  ```

3. Ekstraksi Fitur dengan TF-IDF
- Tujuannya mengubah teks dalam kolom ```content``` menjadi representasi numerik agar bisa diproses oleh model
- Menggunakan TF-IDF Vectorizer dengan parameter berikut:
  - stop_words='english' (menghapus kata umum inggris seperti "the", "and")
  - ngram_range=(1,2) (mempertimbangkan kata tunggal dan pasangan kata)
    ```
    from sklearn.feature_extraction.text import TfidfVectorizer  
    tfidf = TfidfVectorizer(stop_words='english', ngram_range=(1,2))  
    tfidf_matrix = tfidf.fit_transform(df_clean['content'])  
    ```
- Outputnya nanti adalah matriks TF-IDF yang merepresentasikan bobot kata dalam setiap dokumen
   
Tujuan dari tahapan ini adalah memastikan data bersih, konsisten, dan siap untuk pemodelan dan membangun representasi teks yang optimal untuk sistem rekomendasi berbasis konten.

## Modeling

1. Content-Based Filtering Model

   Sistem rekomendasi yang menyarankan buku berdasarkan kemiripan konten (genre dan deskripsi)
   
   Algoritma:
  - Cosine Similarity digunakan untuk menghitung kemiripan antar buku berdasarkan vektor TF-IDF.
  - Buku dengan skor kesamaan (similiarity) tertinggi direkomendasikan.
  - Contoh Hasil Rekomendasi (Top 5 untuk The Help):

 Book                                             | Author           | Genres                                                                                    
--------------------------------------------------|------------------|-------------------------------------------------------------------------------------------
 Kerri's War (The King Trilogy, #3)               | Stephen Douglass | Thriller, Romance, Crime, Amazon                                                          
 The Joy Luck Club                                | Amy Tan          | Fiction, Historical Fiction, Classics, China, Contemporary, Adult Fiction, Adult          
 Lean In: Women, Work, and the Will to Lead       | Sheryl Sandberg  | Nonfiction, Business, Feminism, Self Help, Leadership, Audiobook, Womens                  
 World Without End (Kingsbridge, #2)              | Ken Follett      | Historical Fiction, Fiction, Historical, Medieval, Audiobook, British Literature, Fantasy 
 Penis Politics: A Memoir of Women, Men and Power | Karen  Hinton    | Nonfiction                                                                                

2. Popularity-Based Recommendation

   Sistem rekomendasi yang menampilkan buku berdasarkan popularitas

   Algoritma:

  - Popularity Score dihitung dengan ```Num_Ratings``` x ```Avg_Rating```.
  - Buku dengan skor tertinggi ditampilkan sebagai rekomendasi.
  - Contoh Hasil Rekomendasi (Top 10 Buku Populer):

 Book                                                                                            | Author             | Avg_Rating | Num_Ratings 
-------------------------------------------------------------------------------------------------|--------------------|------------|-------------
 The Raj Quartet                                                                                 | Paul Scott         | 4.48       | 995.0       
 Living The Best Day Ever                                                                        | Hendri Coetzee     | 4.34       | 997.0       
 Hometown Girl After All (Hometown, #2)                                                          | Kirsten Fullmer    | 4.32       | 999.0       
 Hometown Girl After All (Hometown, #2)                                                          | Kirsten Fullmer    | 4.32       | 999.0       
 Glucose Control Eating: Lose Weight Stay Slimmer Live Healthier Live Longer                     | Rick Mystrom       | 4.31       | 984.0       
 The Chain Between Worlds (The Lost Artefacts #1)                                                | Johnathon Nicolaou | 4.62       | 915.0       
 Ryan White: My Own Story                                                                        | Ryan White         | 4.27       | 971.0       
 Christmas in Smithville (Hometown, #4)                                                          | Kirsten Fullmer    | 4.3        | 964.0       
 Proud Pada (The Last Lumenian, #3)                                                              | S.G. Blaise        | 4.33       | 950.0       
 The Search for Mother Missing: A Peek Inside International Adoption (Adoption Books for Adults) | Janine Vance       | 4.46       | 921.0       
    
    
3. Penjelasan Model
   
  a. Content-Based Filtering:
    - Setiap buku direpresentasikan sebagai vektor TF-IDF dari konten (genre + deskripsi).
    - Cosine similarity menghitung kemiripan antara vektor buku target dan buku lainnya.
    - Rekomendasi diambil dari 5 buku dengan skor tertinggi.
    - Kelebihannya yaitu relevan untuk pengguna yang mencari buku dengan tema/genre spesifik.

  b. Popularity-Based Recommendation:
    - Skor popularitas menggabungkan jumlah rating (Num_Ratings) dan rata-rata rating (Avg_Rating).
    - Buku diurutkan berdasarkan skor ini, lalu diambil peringkat teratas.
    - Kelebihannya cocok untuk menyoroti tren/item populer

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
