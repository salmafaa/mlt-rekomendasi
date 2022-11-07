# Laporan Proyek Machine Learning - Salma Fauziah Azzahra

## Project Overview

Buku menurut Kamus Besar Bahasa Indonesia Balai Pustaka adalah lembar kertas yang berjilid, berisi tulisan atau kosong. Sedangkan menurut Oxford Dictionary, buku adalah hasil karya yang ditulis atau dicetak dengan halaman-halaman yang dijilid pada satu sisi atau hasil karya yang ditujukan untuk penerbitan. Buku yang dianggap berhasil jika dapat menggugah minat dari khalayak sasaran dalam memahami isi dari buku tersebut[1].

Ketika selesai membaca suatu buku dan buku itu dianggap menarik dan menggugah selera baca, maka tak jarang jika pembaca ingin membaca buku serupa, baik dalam hal kesamaan genre atau oleh siapa buku tersebut ditulis. Oleh karena itu, untuk memudahkan para pembaca buku dalam mendapatkan buku serupa maka diperlukan sistem rekomendasi untuk memudahkan dalam proses pencarian. 

Pengertian dari Sistem Rekomendasi sendiri adalah suatu _system_ yang digunakan oleh para user/customer/pelanggan untuk mendapatkan produk yang diinginkan[2]. Dengan banyaknya data yang tersebar, maka dengan adanya sistem rekomendasi ini dapat memperkecil ruang lingkup data sesuai dengan _history_ atau kegiatan yang dilakukan pengguna di masa lalu.


## Business Understanding

### Problem Statements

- Bagaimana pengguna dapat mendapatkan rekomendasi buku serupa?
- Bagaimana membuat model rekomendasi berdasarkan kesamaan penulis (_author_)?
- Bagaimana membuat model rekomendasi berdasarkan rating?

### Goals

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

- Mengubah fitur 'user_id' dan 'book_id' menjadi list tanpa nilai yang sama.
- Menyandikan (encode) fitur 'user_id' dan 'book_id' ke dalam indeks integer.
- Memetakan (mapping) 'user_id' dan 'book_id' ke dataframe yang berkaitan.
- Mengecek jumlah user, jumlah buku, kemudian mengubah nilai rating menjadi float.

## Modeling and Result

### Content Based Filtering

Sistem rekomendasi yang dibangun pada proyek ini adalah sistem rekomendasi sederhana berdasarkan kesamaan nama penulis dengan mendekatan content based filtering. Content Based Filtering adalah algoritma yang merekomendasikan item serupa dengan apa yang disukai pengguna, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit. 

**TF-IDF**

TF-IDF atau _Term Frequency - Inverse Document Frequency_, adalah ukuran statistik yang menggambarkan pentingnya istilah dalam dokumen dalam kumpulan atau korpus. Metrik ini biasanya digunakan sebagai faktor pembobotan untuk pencarian informasi, penambangan teks, dan pemodelan pengguna. Nilai TF-IDF meningkat secara linier dengan jumlah kemunculan suatu term dan bergantung pada jumlah dokumen dalam korpus yang memuat term tersebut.

TF-IDF digunakan pada sistem rekomendasi buku untuk menentukan representasi fitur penting dari setiap fitur authors. Untuk menjalankan TF-IDF digunakan fungsi tfidfvectorizer() dari library sklearn.

Setelah inisialisasi tfidfvectorizer, lakukan perhitungan idf pada data authors kemudian mapping array dari fitur index integer ke fitur nama. Output pada tahap ini dapat dilihat pada Gambar 9. Pada Gambar tersebut hanya ditampilkan sebagian data karena terlalu banyaknya data jika ditampilkan seluruhnya.

Gambar 9. **Mapping array**

![mapping-array](https://user-images.githubusercontent.com/109077279/200288819-deba0886-cf81-42df-9df5-01e8756bcd33.png)

Selanjutkan lakukan fit lalu tranformasikan ke dalam bentuk matriks. Ukuran matriks dapat dilihat pada Gambar 10. Pada Gambar 10, nilai 10000 merupakan ukuran data dan 6193 merupakan matriks authors.

Gambar 10. **Ukuran makriks tfidf**

![ukuran matriks tfidf](https://user-images.githubusercontent.com/109077279/200289769-b7e5ba6c-7583-4a14-a07a-bf9aab7555e2.png)

Selanjutnya ubah vektor tf-idf dalam bentuk matriks dengan fungsi todense(). Output pada tahap ini dapat dilihat pada Gambar 11.

Gambar 11. **matriks tf-idf**

![matriks-tfidf](https://user-images.githubusercontent.com/109077279/200292310-0203e237-efce-4e99-8fd0-61e5b5c97c02.png)

Membuat Dataframe untuk melihat tf-idf matriks. Dataframe baru dibuat untuk menunjukkan matriks TF-IDF untuk beberapa title dan authors. Semakin tinggi nilai matriks menunjukkan semakin erat hubungan antara title dengan authors tersebut. Dataframe dapat dilihat pada Gambar 12. Pada Gambar 12, hanya disajikan beberapa data dari keseluruhan data sehingga belum terlihat hubungan antara title dengan authors.

Gambar 12. **Dataframe matriks tf-idf**

![dataframe](https://user-images.githubusercontent.com/109077279/200292860-3535dc24-2726-448b-b0f4-7e872866b364.png)

**Cosine Similarity**

Cosine Similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor menunjuk ke arah yang sama. Teknik ini bekerja dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus antara dua vektor, semakin besar nilai kemiripan cosinusnya. Cosine Similarity dapat dilihat pada Gambar 13.

Gambar 13. **Cosine Similarity**

![cosine-similarity](https://user-images.githubusercontent.com/109077279/200303110-2d1d3baf-3f1d-4fa8-b37b-057136dc89de.png)

Cosine similarity digunakan untuk menghitung derajat kesamaan antar judul buku. Untuk menjalankan cosine similarity digunakan fungsi cosine_similarity dari library sklearn. Output menghitung cosine similarity pada matriks tf-idf dapat dilihat pada Gambar 14.

Gambar 14. **Cosine similarity pada matriks tf-idf**

![cosine-similarity-matriks](https://user-images.githubusercontent.com/109077279/200304127-4a636820-6d4a-404c-8af3-60511f01498f.png)

Selanjutnya membuat dataframe dari variable cosine_sim (variable yang menyimpan perhitungan cosine similarity pada matriks tf-idf) dengan baris dan kolom berupa judul - judul buku. Dataframe dapat dilihat pada Gambar 15. Pada Gambar 15, hanya ditampilkan beberapa data sehingga belum terlihat kesamaan.

Gambar 15. **Dataframe matriks**

![cosine-similarity-dataframe](https://user-images.githubusercontent.com/109077279/200305354-8c706e9f-1183-498d-82b6-65f78260c76f.png)

### Result

Fungsi books_recommendations dibuat untuk menemukan rekomendasi buku menggunakan similarity yang telah didefinisikan sebelumnya. Fungsi ini bekerja dengan cara mengambil buku dengan similarity terbesar dari index yang ada.

Selanjutnya adalah menemukan rekomendasi yang mirip dengan buku pada Tabel 6.

Tabel 6. **Suzanne Collins**

|   | id |                              book_title |     book_author |
|--:|---:|----------------------------------------:|----------------:|
| 0 |  1 | The Hunger Games (The Hunger Games, #1) | Suzanne Collins |

Berikut top 5 rekomendasi dapat dilihat pada Tabel 7. Pada Tabel 7, terlihat bahwa 5 rekomendasi teratas memiliki kesamaan penulis yaitu Suzanne Collins.

Tabel 7. **5 Rekomendasi teratas**
|   |                                        book_title |     book_author |
|--:|--------------------------------------------------:|----------------:|
| 0 |                 Mockingjay (The Hunger Games, #3) | Suzanne Collins |
| 1 | The Hunger Games Trilogy Boxset (The Hunger Ga... | Suzanne Collins |
| 2 | Gregor and the Marks of Secret (Underland Chro... | Suzanne Collins |
| 3 | Gregor and the Code of Claw (Underland Chronic... | Suzanne Collins |
| 4 | Gregor and the Prophecy of Bane (Underland Chr... | Suzanne Collins |

**Kelebihan :**
- Tidak tergantung pada user lain karena mampu merekomendasikan item yang belum dinilai oleh pengguna lain
- Memunculkan item yang relevan dengan kegiatan pengguna di masa lalu

**Kekurangan :**
- Memiliki keterbatasan dalam jenis fitur terkait
- Sistem tidak akan memberikan rekomendasi yang dapat diandalkan pada pengguna baru, karena membutuhkan penelurusan atau data pada preferensi pengguna

### Collaborative Filtering

Sistem rekomendasi yang dibangun pada proyek ini adalah sistem rekomendasi berdasarkan rating yang diberikan oleh pengguna dengan pendekatan collaborative filtering. Collaborative Filtering adalah algoritma yang bergantung pada pendapat komunitas pengguna. Dia tidak memerlukan atribut untuk setiap itemnya.

**Membagi Data untuk Training dan Validasi**

Sebelum membagi data, acak data terlebih dahulu agar distribusinya menjadi random. Hasil mengacak dataset dapat dilihat pada Tabel 8. Pada Tabel 8, dapat dilihat beberapa isi data yang telah diacak. Keseluruhan tabel memiliki jumlah 5976479 _rows_ × 5 _columns_

Tabel 8. **Dataset acak**
|         | user_id | book_id | rating |  user | books |
|--------:|--------:|--------:|-------:|------:|------:|
| 3623535 |   42562 |    2757 |    3.0 | 39510 |   777 |
| 3985638 |   43232 |     134 |    4.0 | 40292 |  5862 |
| 2983642 |   37244 |    1463 |    5.0 | 33569 |  3222 |
| 5812251 |   53366 |      71 |    2.0 | 52456 |   179 |
| 2208852 |   29634 |    3339 |    4.0 | 25709 |  6783 |
|   ...   |     ... |     ... |    ... |   ... |   ... |
| 1570006 |   22331 |    2621 |    5.0 | 18788 |   296 |
| 2234489 |   26562 |    8110 |    5.0 | 22690 |  8225 |
| 4926484 |   51127 |     125 |    4.0 | 49766 |   484 |
| 4304572 |   10933 |    1752 |    4.0 |  8854 |   232 |
| 1692743 |   10327 |     445 |    4.0 | 14110 |  7444 |


Selanjutnya memetakan (mapping) data user dan buku menjadi satu value terlebih dahulu. Lalu, membuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training. Kemudian bagi data menjadi 80% data train dan 20% data validasi. Output untuk tahap ini dapat dilihat pada Gambar 16.

Gambar 16. **Membagi data**

![Membagi data](https://user-images.githubusercontent.com/109077279/200310963-417969fd-a3b2-4114-8eff-0f7a3b39814a.png)


**Proses Training**

Membuat class RecommenderNet dengan keras Model class. Pada tahap ini, model menghitung skor kecocokan dengan teknik embedding. Pertama, lakukan proses embbeding terhadap user dan books. Selanjutnya, lakukan operasi perkalian dot product antara embedding user dan books. Selain itu, dapat menambahkan bias untuk setiap user dan books. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi altivasi sigmoid.

Selanjutnya, lakukan proses compile terhadap model. Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan RMSE sebagai metrics evaluation. Output hasil training dapat dilihat pada Gambar 17.

Gambar 17. **Hasil training**

![hasil training](https://user-images.githubusercontent.com/109077279/200313564-1d48e907-db54-4e52-8c0d-b25a5f4ef438.png)

### Result

Untuk memperoleh rekomendasi buku, gunakan fungsi model.predict() dari library Keras. Berikut adalah 10 Hasil Rekomendasi berdasarkan rating dapat dilihat pada Gambar 18. Pada Gambar 18, dapat dilihat bahwa terdapat satu buku dengan penulis yang sama, yaitu Judith McNaught. 

Gambar 18. **10 Rekomendasi buku**

![10 rekomendasi berdasarkan rating](https://user-images.githubusercontent.com/109077279/200316064-03cbe0ad-5269-400a-aef8-e51ebb6d5851.png)

**Kelebihan :**
- Rekomedasi tetap akan bekerja dalam keadaan konten sulit dianalisis sekalipun

**Kekurangan :**
- Membutuhkan parameter rating, sehingga jika ada item baru sistem tidak akan merekomendasikan item tersebut

## Evaluation

### Content Based Filtering

Teknik Evaluasi yang digunakan adalah precision. Precision dapat diartikan sebagai derajat reliabilitas model ketika ia memberikan prediksi “Positif”. Rumus dari teknik ini adalah :

Recommender system precision :  

$$ P =  { of-our-recommendations-that-are-relevant \over of-items-we-recommended} $$  

Dari hasil rekomendasi pada Tabel 6 sebelumnya, diketahui bahwa buku dengan judul The Hunger Games (The Hunger Games, #1) ditulis oleh Suzanne Collins. Dari 5 buku yang direkomendasikan pada Tabel 7, 5 buku memiliki kesamaan penulis, yaitu Suzanne Collins. Artinya, precision sistem sebesar 5/5 atau 100%.


### Collaborative Filtering

Evaluasi metrik yang digunakan untuk mengukur kinerja model adalah metrik RMSE (Root Mean Squared Error).

RMSE adalah metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi. Root Mean Square Error adalah hasil dari akar kuadrat Mean Square Error. Keakuratan metode estimasi kesalahan pengukuran ditandai dengan adanya nilai RMSE yang kecil. Metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih kecil dikatakan lebih akurat daripada metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih besar

formula dari matriks RMSE adalah sebagai berikut.

$$ RMSE = { \sqrt { Σ_{t}^{n} (A_{t} - F_{t})^2 } \over n} $$

keterangan :

At : Nilai Aktual.

ft = Nilai hasil peramalan.

N = banyaknya dataset

Cara menerapkan metrik tersebut adalah dengan menambahkan 'metrics=[tf.keras.metrics.RootMeanSquaredError()]' pada model.compile. Hasil dari model evaluasi visualisasi matriks dapat dilihat pada Gambar 19. Pada Gambar 19, terlihat bahwa terjadi kenaikan pada model, namun nilai akhir masih di bawah 0.5, yaitu root_mean_squared_error: 0.4160 dan val_root_mean_squared_error: 0.3842. 

Gambar 19. **Visualisasi Matriks**

![model matriks](https://user-images.githubusercontent.com/109077279/200329600-24476e45-352d-48bc-ada9-7e75fa59eab5.png)


# Conclusion

Proyek _Machine Learning_ sistem rekomendasi dibuat untuk membantu dalam memudahkan pengguna agar mendapat rekomendasi buku yang memiliki kemipiran dengan buku yang telah dibaca sebelumnya, maka dibuatlah model dengan pendekatan Content Based Filtering, yang membuat model rekomendasi dapat memunculkan rekomendasi buku sesuai kesamaan pada penulis buku tersebut dan model dengan pendekatan Collaborative Filtering, yang membuat model dapat memunculkan rekomendasi buku berdasarkan rating yang diberikan pengguna. Dengan adanya model sistem rekomendasi dengan kedua pendekatan tersebut, maka user dapat mendapatkan rekomendasi buku yang sesuai.


# REFERENCE

[1] dosenpendidikan. (2022, Agustus 14). Pengertian Buku. Diakses dari https://www.dosenpendidikan.co.id/pengertian-buku/

[2] Girsang, Abba Suganda. (2020, November 17). Sistem rekomendasi- Content Based. Diakses dari https://mti.binus.ac.id/2020/11/17/sistem-rekomendasi-content-based/




