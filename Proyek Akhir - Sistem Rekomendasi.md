# Laporan Proyek Machine Learning - Salma Fauziah Azzahra

## Project Overview

Buku menurut Kamus Besar Bahasa Indonesia Balai Pustaka adalah lembar kertas yang berjilid, berisi tulisan atau kosong. Sedangkan menurut Oxford Dictionary, buku adalah hasil karya yang ditulis atau dicetak dengan halaman-halaman yang dijilid pada satu sisi atau hasil karya yang ditujukan untuk penerbitan. Buku yang dianggap berhasil jika dapat menggugah minat dari khalayak sasaran dalam memahami isi dari buku tersebut[1].

Ketika selesai membaca suatu buku dan buku itu dianggap menarik dan menggugah selera baca, maka tak jarang jika pembaca ingin membaca buku serupa, baik dalam hal kesamaan genre atau oleh siapa buku tersebut ditulis. Oleh karena itu, untuk memudahkan para pembaca buku dalam mendapatkan buku serupa maka diperlukan sistem rekomendasi untuk memudahkan dalam proses pencarian. 

Pengertian dari Sistem Rekomendasi sendiri adalah suatu _system_ yang digunakan oleh para user/customer/pelanggan untuk mendapatkan produk yang diinginkan[2]. Dengan banyaknya data yang tersebar, maka dengan adanya sistem rekomendasi ini dapat memperkecil ruang lingkup data sesuai dengan _history_ atau kegiatan yang dilakukan pengguna di masa lalu.


## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- Bagaimana pengguna dapat mendapatkan rekomendasi buku serupa?
- Bagaimana membuat model rekomendasi berdasarkan kesamaan penulis (_author_)?
- Bagaimana membuat model rekomendasi berdasarkan rating?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Membuat model _Machine learning_ sistem rekomendasi untuk menghasilkan rekomendasi buku serupa
- Membuat model rekomendasi berdasarkan kesamaan penulis (_author_) dengan pendekatan Content Based Filtering
- Membuat model rekomendasi berdasarkan rating dengan pendekatan Collaborative Filtering


### Solution statements
- Menyiapkan data agar bisa digunakan untuk membangun model
- Menganalisis data dengan melakukan Univariate Analyst untuk lebih memahami data
- menggunakan 2 algoritma _Machine Learning_ sistem rekomendasi, yaitu :

  - Content Based Filtering adalah algoritma yang merekomendasikan item serupa dengan apa yang disukai pengguna, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit.
  - Collaborative Filtering. adalah algoritma yang bergantung pada pendapat komunitas pengguna. Dia tidak memerlukan atribut untuk setiap itemnya.


## Data Understanding
Dataset yang digunakan dalam proyek ini merupakan data yang berisi informasi dan penilaian (_rating_) untuk sepuluh ribu buku populer. Umumnya, ada 100 ulasan untuk setiap buku, meskipun beberapa memiliki _less - fewer - ratings_. Penilaian dimulai dari satu hingga lima. Dataset ini dapat diunduh di [Goodbooks 10k Updated](https://www.kaggle.com/datasets/alexanderfrosati/goodbooks-10k-updated)

Berikut informasi pada dataset :
Terdapat dua dataset yang digunakan, yaitu dataset books dan dataset ratings.

**Dataset books :**
- Dataset memiliki format CSV
- Dataset memiliki 10000 sample dengan 5 fitur (dari 23 fitur) yang akan digunakan
- Dari ke 5 fitur tersebut, 1 fitur bertipe int64 dan 4 fitur bertipe object

**Dataset ratings :**
- Dataset memiliki format CSV
- Dataset memiliki 5976479 sample dengan 3 fitur
- Dataset memiliki 3 fitur bertipe int64

### Variabel-variabel pada dataset adalah sebagai berikut:

**Dataset books :**
- book_id: ID unik dari setiap buku
- authors: Nama penulis buku
- original_title: Judul buku original dari setiap series buku
- title: Judul dari setiap series buku
- language_code: Bahasa yang digunakan dalam buku

**Dataset ratings :**
- user_id: ID unik dari setiap user
- book_id: ID unik dari setiap buku
- rating: Penilaian yang diberikan oleh user


### Univariate Analyst
Univariate Analyst adalah menganalisis setiap fitur secara terpisah.

**Analisis setiap atribut pada dataset books**

Berikut adalah beberapa isi data dari dataset books dapat dilihat pada Tabel 1.

Tabel 1. **Data books**
|   | book_id |                     authors |                           original_title |                                             title | language_code |
|--:|--------:|----------------------------:|-----------------------------------------:|--------------------------------------------------:|--------------:|
| 0 |       1 |             Suzanne Collins |                         The Hunger Games |           The Hunger Games (The Hunger Games, #1) |           eng |
| 1 |       2 | J.K. Rowling, Mary GrandPré | Harry Potter and the Philosopher's Stone | Harry Potter and the Sorcerer's Stone (Harry P... |           eng |
| 2 |       3 |             Stephenie Meyer |                                 Twilight |                           Twilight (Twilight, #1) |         en-US |
| 3 |       4 |                  Harper Lee |                    To Kill a Mockingbird |                             To Kill a Mockingbird |           eng |
| 4 |       5 |         F. Scott Fitzgerald |                         The Great Gatsby |                                  The Great Gatsby |           eng |


![Analyst-books](https://user-images.githubusercontent.com/109077279/200172546-b849fa59-f553-40cb-898a-735a84d232ff.png)

Gambar 1. **Analisis dataset books**

Pada Gambar 1, dapat dilihat jumlah entri unik dari setiap fitur pada dataset books. Terlihat bahwa banyaknya data penulis adalah 4664 dan banyaknya judul buku keseluruhan adalah 9964, artinya terdapat penulis yang menulis lebih dari satu buku.

**Analisis setiap atribut pada dataset ratings**

Berikut adalah beberapa isi dari dataset ratings dapat dilihat pada Tabel 2.

Tabel 2. **Data ratings**
|   | user_id | book_id | rating |   |
|--:|--------:|--------:|-------:|---|
| 0 |    0    |       1 |    258 | 5 |
| 1 |    1    |       2 |   4081 | 4 |
| 2 |    2    |       2 |    260 | 5 |
| 3 |    3    |       2 |   9296 | 5 |
| 4 |    4    |       2 |   2318 | 3 |


![describe-rating](https://user-images.githubusercontent.com/109077279/200175098-adc24962-1231-4429-8279-76a3fd028012.png)

Gambar 2. **Describe rating**

Pada Gambar 2, terlihat bahwa nilai minimal dari rating adalah 1 dan maksimalnya adalah 5.

![analyst-ratings](https://user-images.githubusercontent.com/109077279/200175196-1bd9fea9-a490-4340-848c-11b524bd2c4e.png)

Gambar 3. **Analisis dataset rating**

Pada Gambar 3, dapat dilihat jumlah entri unik pada fitur user_id dan book_id, serta jumlah keseluruhan rating yang diberikan oleh pengguna.

![presentase-rating](https://user-images.githubusercontent.com/109077279/200175289-e74e2d20-1931-43f7-845c-fe50de297ca8.png)

Gambar 4. **Presentase rating**

Pada Gambar 4, terlihat jumlah pengguna yang memberi penilaian di setiap rating, Dapat dilihat bahwa pengguna paling banyak memberikan rating 4.

![countplot-rating](https://user-images.githubusercontent.com/109077279/200175372-dff8199c-1d68-43f9-8f8e-53261209743d.png)

Gambar 5. **Grafik rating**

Pada Gambar 5, dapat dilihat bahwa pengguna paling banyak memberikan rating 4 pada buku, sesuai dengan jumlah dan presentase pada Gambar 4.

### Data Prepocessing
- Menggabungkan dataframe ratings dengan books berdasarkan nilai book_id ke dalam variable book
- Mengecek missing value, terdapat missing value pada original_title dan language_code
- Memasukkan ratings ke dalam variable all_books_rate
- Menggabungkan all_books_rate dengan authors dan title berdasarkan book_id ke dalam variable all_books


## Data Preparation
- Melakukan pengecekan missing value pada all_books menggunakan fungsi isnull()

![cek-all_books](https://user-images.githubusercontent.com/109077279/200176337-73ab935c-3076-41f9-8222-da5142f852c8.png)

Gambar 6. **Cek missing value pada all_books**

Pada Gambar 6, terlihat bahwa tidak ada missing value pada setiap fitur.

- 



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

# Conclusion


#REFERENCE

[1] dosenpendidikan. (2022, Agustus 14). Pengertian Buku. Diakses dari https://www.dosenpendidikan.co.id/pengertian-buku/

[2] Girsang, Abba Suganda. (2020, November 17). Sistem rekomendasi- Content Based. Diakses dari https://mti.binus.ac.id/2020/11/17/sistem-rekomendasi-content-based/




