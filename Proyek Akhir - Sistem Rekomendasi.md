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

### Data Preparation pada Content Based Filtering

- Melakukan pengecekan missing value pada all_books menggunakan fungsi isnull()

![cek-all_books](https://user-images.githubusercontent.com/109077279/200176488-f4dc5592-2745-4335-81af-57ad8910ffa8.png)

Gambar 6. **Cek missing value pada all_books**

Pada Gambar 6, terlihat bahwa tidak ada missing value pada setiap fitur.

- Mengurutkan buku berdasarkan book_id kemudian memasukkannya ke dalam variabel fix_books, dapat dilihat pada Tabel 3. Data pada Tabel 3 memiliki jumlah data sebanyak 5976479 _rows_ × 5 _columns_

Tabel 3. **Data pada fix_books**
|         | user_id | book_id | rating |         authors |                                   title |
|--------:|--------:|--------:|-------:|----------------:|----------------------------------------:|
| 2174136 |   29300 |       1 |      4 | Suzanne Collins | The Hunger Games (The Hunger Games, #1) |
|  433265 |    6590 |       1 |      3 | Suzanne Collins | The Hunger Games (The Hunger Games, #1) |
| 1907014 |    7546 |       1 |      5 | Suzanne Collins | The Hunger Games (The Hunger Games, #1) |
| 3743260 |   43484 |       1 |      1 | Suzanne Collins | The Hunger Games (The Hunger Games, #1) |
| 1266846 |   18689 |       1 |      5 | Suzanne Collins | The Hunger Games (The Hunger Games, #1) |
|   ...   |     ... |     ... |    ... |             ... |                                     ... |
| 2366366 |   31293 |   10000 |      3 |     John Keegan |                     The First World War |
| 3376022 |   12272 |   10000 |      4 |     John Keegan |                     The First World War |
| 2811513 |   35330 |   10000 |      4 |     John Keegan |                     The First World War |
| 4134364 |   46337 |   10000 |      5 |     John Keegan |                     The First World War |
| 4047777 |   42537 |   10000 |      4 |     John Keegan |                     The First World War |

- Mengecek berapa jumlah entri unik pada fix_books berdasarkan book_id dan diketahui bahwa jumlahnya adalah 10000
- Mengecek kategori authors yang unik

![data-authors](https://user-images.githubusercontent.com/109077279/200177448-a3b734cb-1f19-42e3-85e1-eb6d18b5979a.png)

Gambar 7. **Authors**

Pada Gambar 7, dapat dilihat beberapa nama penulis dengan tipe data object. Pada gambar hanya ditampilkan beberapa nama penulis karena terlalu banyaknya data pada authors.

- Membuang data duplikat pada variabel preparation, sehingga tampilannya akan seperti pada Tabel 4. Data pada Tabel 4 memiliki jumlah data sebanyak 10000 _rows_ × 5 _columns_. Jumlah ini sudah berkurang cukup banyak dibandingkan data pada Tabel 3 karena sudah tidak ada duplikasi data berdasarkan book_id.

Tabel 4. **Preparation**
|         | user_id | book_id | rating |                     authors |                                             title |
|--------:|--------:|--------:|-------:|----------------------------:|--------------------------------------------------:|
| 2174136 |   29300 |       1 |      4 |             Suzanne Collins |           The Hunger Games (The Hunger Games, #1) |
|  161112 |    3183 |       2 |      5 | J.K. Rowling, Mary GrandPré | Harry Potter and the Sorcerer's Stone (Harry P... |
|  672652 |    5651 |       3 |      2 |             Stephenie Meyer |                           Twilight (Twilight, #1) |
| 3350794 |   27109 |       4 |      5 |                  Harper Lee |                             To Kill a Mockingbird |
|   4367  |     232 |       5 |      4 |         F. Scott Fitzgerald |                                  The Great Gatsby |
|   ...   |     ... |     ... |    ... |                         ... |                                               ... |
| 5289649 |    2543 |    9996 |      3 |               Ilona Andrews |                         Bayou Moon (The Edge, #2) |
| 3101597 |   38254 |    9997 |      4 |              Robert A. Caro | Means of Ascent (The Years of Lyndon Johnson, #2) |
|  403472 |    3056 |    9998 |      4 |             Patrick O'Brian |                             The Mauritius Command |
| 3362996 |   12187 |    9999 |      5 |             Peggy Orenstein | Cinderella Ate My Daughter: Dispatches from th... |
| 5637174 |   49007 |   10000 |      4 |                 John Keegan |                               The First World War |

- Mengonversi data series ‘book_id’, 'authors', dan 'title' menjadi dalam bentuk list menggunakan fungsi tolist(). Output yang dihasilkan dapat dilihat pada Gambar 8.

Gambar 8. **Hasil konversi data ke list**

![tolist](https://user-images.githubusercontent.com/109077279/200178397-531c1ddb-f575-46fb-b385-1624569fdcb6.png)

- Membuat dictionary untuk data ‘id_book’, ‘book_author’, dan ‘book_title’. Dictionary di simpan ke dalam variable books_news dapat dilihat pada Tabel 5.

Tabel 5. **books_new**
|      |    id |                                        book_title |                 book_author |
|-----:|------:|--------------------------------------------------:|----------------------------:|
|   0  |     1 |           The Hunger Games (The Hunger Games, #1) |             Suzanne Collins |
|   1  |     2 | Harry Potter and the Sorcerer's Stone (Harry P... | J.K. Rowling, Mary GrandPré |
|   2  |     3 |                           Twilight (Twilight, #1) |             Stephenie Meyer |
|   3  |     4 |                             To Kill a Mockingbird |                  Harper Lee |
|   4  |     5 |                                  The Great Gatsby |         F. Scott Fitzgerald |
|  ... |   ... |                                               ... |                         ... |
| 9995 |  9996 |                         Bayou Moon (The Edge, #2) |               Ilona Andrews |
| 9996 |  9997 | Means of Ascent (The Years of Lyndon Johnson, #2) |              Robert A. Caro |
| 9997 |  9998 |                             The Mauritius Command |             Patrick O'Brian |
| 9998 |  9999 | Cinderella Ate My Daughter: Dispatches from th... |             Peggy Orenstein |
| 9999 | 10000 |                               The First World War |                 John Keegan |

### Data Preparation pada Collaborative Filtering

- Menyandikan (encode) fitur 'user_id' dan 'book_id' ke dalam indeks integer.
- Memetakan 'user_id' dan 'book_id' ke dataframe yang berkaitan.
- Mengecek jumlah user, jumlah buku, kemudian mengubah nilai rating menjadi float.

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


# REFERENCE

[1] dosenpendidikan. (2022, Agustus 14). Pengertian Buku. Diakses dari https://www.dosenpendidikan.co.id/pengertian-buku/

[2] Girsang, Abba Suganda. (2020, November 17). Sistem rekomendasi- Content Based. Diakses dari https://mti.binus.ac.id/2020/11/17/sistem-rekomendasi-content-based/




