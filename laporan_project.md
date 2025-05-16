# Laporan Proyek Machine Learning - Muhammad Habibulloh

## Project Overview

Sistem rekomendasi buku menjadi kunci penting untuk meningkatkan pengalaman pengguna (experience) di platform literasi digital. Pembaca sering kali kesulitan menemukan buku baru yang sesuai preferensi karena banyaknya pilihan [[1]](https://jurnal.itbsemarang.ac.id/index.php/JPTIS/article/view/818), [[2]](https://jurnal.uns.ac.id/joive/article/view/53618), [[3]](https://jurnal.polgan.ac.id/index.php/remik/article/view/14515). Proyek ini bertujuan untuk membangun sistem rekomendasi berbasis konten dan popularitas untuk memecahkan masalah tersebut. Dataset yang digunakan mencakup 10.000 buku dari Goodreads, dengan referensi utama dari daftar "Books That Everyone Should Read At Least Once" [[4]](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv).

## Referensi

1. F. Ertandi and M. Akbar, "Sistem Pendukung Keputusan Rekomendasi Buku Novel menggunakan Metode Weighted Product," Renik: Riset dan E-Jurnal Manajemen Informatika Komputer, vol. 9, no. 1, pp. 366–381, Jan. 2025. doi: 10.33395/renik.v9i1.14515.
2. E. G. E. Devara et al., "Pengembangan Teknologi Rekomendasi Kecerdasan Buatan yang Digunakan pada Perpustakaan," Journal of Informatics and Vocational Education (JOIVE), vol. 4, no. 3, pp. 87–92, Oct. 2021. doi: 10.20961/joive.v4i3.53618.
3. K. Harahap et al., "Aplikasi Baca Buku Platform Digital Yang Dirancang Untuk Memfasilitasi Pengguna Dalam Membaca Berbagai Jenis Buku Elektronik," Jurnal Penelitian Teknologi Informasi Dan Sains, vol. 1, no. 3, pp. 94–102, Sep. 2023. doi: 10.54066/jptis.v1i3.818.
4. Dataset: Best Books (10k) Multi-Genre Data, [Kaggle](https://www.kaggle.com/datasets/ishikajohari/best-books-10k-multi-genre-data?select=goodreads_data.csv)

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
