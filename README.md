# Sistem Rekomendasi Buku

## Deskripsi Proyek
Proyek ini bertujuan untuk membangun sistem rekomendasi buku menggunakan yaitu Content-Based Filtering (berdasarkan genre dan deskripsi buku) dan Popularity-Based Filtering (berdasarkan rating dan jumlah ulasan). Sistem ini membantu pengguna menemukan buku yang relevan dengan preferensi mereka atau buku populer berdasarkan rating.

## Laporan Proyek
[Laporan Proyek](https://github.com/haaahabib/sistem-rekomendasi/blob/main/laporan_project.md)

## Teknik dan Algoritma yang Digunakan
1. **Content-Based Filtering**  
   - TF-IDF Vectorization untuk ekstraksi fitur teks (genre + deskripsi)
   - Cosine Similarity untuk menghitung kemiripan (similiarity) antar buku
2. **Popularity-Based Filtering**  
   - Skor popularitas dihitung dari `Num_Ratings x Avg_Rating`

## Dataset
**Sumber Dataset**: [Best Books (10k) Multi-Genre Data](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv)  
