# Laporan Proyek Machine Learning - Radilsha Puspita Maharani

## Project Overview

Sistem rekomendasi adalah suatu teknologi yang di desain untuk mempermudah pengguna dalam menggunakan suatau data yang mungkin sesuai dengan profil pengguna secara cepat dan dapat mengurangi jumlah informasi yang terlalu banyak (Vozalis & Margaritis, 2010). Sistem rekomendasi memiliki kemampuan untuk melakukan prediksi tentang sebuah item yang mungkin disukai pengguna berdasarkan informasi yang didapat dari pengguna tersebut. Item tersebut atau dalam hal ini film dapat disarankan berdasarkan <i>rating</i> film yang diberikan pengguna atau berdasarkan pengguna lain yang memiliki kebebasan yang mirip (Felfernig, et al., 2011). Terdapat beberapa algoritma yang dapat dipakai untuk membangun sistem rekomendasi dengan kelebihan dan kekurangan masing-masing. Salah satu algoritma sistem rekomendasi yang paling banyak digunakan adalah <i>Collaborative Filtering</i>

## Business Understanding

### Problem Statements

- Bagaimana cara membuat sistem rekomendasi film menggunakan metode <i>collaborative filtering</i>
- Bagaimana cara meningkatkan <i>user experience</i> saat mencari film yang ingin ditonton


### Goals
- Dapat menerapkan metode <i>collaborative filtering</i> untuk sistem rekomendasi film
- Meningkatkan <i>user experience</i> saat mencari film yang ingin ditonton.

    ### Solution statements
- Melakukan pembagian data berdasarkan tipe konten sebelum melakukan <i>development</i> model <i>machine learning</i>
-Melakukan <i>pre-processing data</i> dengan baik kemudian membangun model <i>collaborative filtering</i>

## Data Understanding
* Informasi Dataset
Dataset yang digunakan pada proyek ini adalah <i>Movie Recomendation</i> yang dapat diunduh melalui link [berikut ini](https://www.kaggle.com/datasets/rohan4050/movie-recommendation-data)
Adapun penjelasan dari variabel maupun kolom yang ada pada dataset yang digunakan yaitu :
  + movies.csv 
    - movieId : Unique ID yang disediakan untuk setiap film
    - title : Nama film beserta tahun penayangan film
    - genres : Jenis genre pada film
  + ratings.csv
    - userId : Unique ID yang disediakan untuk setiap pengguna
    - movieId :  Unique ID yang disediakan untuk setiap film
    - rating : Penilaian pengguna terhadap film terkait
    - timestap : Kode waktu pada film
  + tags.csv
    - UserId : Unique ID yang disediakan untuk setiap pengguna 
    - movieId : Unique ID yang disediakan untuk setiap film
    - tag : Metadata yang dibuat pengguna tentang film
    - timestap : Kode waktu film

* <i>Feature</i> yang digunakan
Dalam sistem rekomendasi film ini, dari 3 file data yang digunakan sistem rekomendasi ini hanya menggunakan  movieId, userId, title, genres, rating, dan tag. 


## Data Preparation
Dataframe baru dibuat berdasarkan dengan tiga type yaitu <i>movies</i>, <i>ratings</i>, dan <i>tags</i> untuk melakukan permodelan <i>machine learning</i> berdasarkan tipe.

Pada bagian ini dilakukan pengecekan informasi data kemudian <i>missing value</i> dan duplikat data. Berikut penjelasan dari masing-masing proses
- <i>Removing Missing Value</i>, pada tahap ini dilakukan karena apabila pada program tidak terdapat <i>missing value</i> maka itu akan membuat performa dalam pembuatan model menjadi lebih baik. Tahapan ini dilakukan menggunakan kode dataframe.dropna(). Kode ini berfungsi untuk menghapus data yang memiliki <i>null values</i> di dalam baris setiap data
- Normalisasi, dilakukan untuk mengubah nilai kolom numerik dalam kumpulan data ke skala umum, tanpa mendistorsi perbedaan dalam rentang nilai. Proses normalisasi dilakukan dengan metode <i>Min Max</i>.Cara kerja <i>Min Max</i> adalah setiap nilai pada sebuah fitur dikurangi dengan nilai minimum fitur tersebut, kemudian dibagi dengan rentang nilai atau nilai maksimum dikurangi nilai minimum dari fitur tersebut.  
Pada program yang telah dijalankan, method max() digunakan untuk mengambil nilai maksimum dari fitur atau kolom tersebut dan method min() digunakan untuk mengambil nilai minimum dari fitur tersebut.

## Modeling

Pada sistem rekomendasi ini menggunakan teknik <i>embedding</i>. Saya menggunakan model <i>Neural Collaborative Filtering (NCF)</i> yang merupakan jaringan saraf (<i>Neural Network</i>) yang menyediakan <i>Collaborative Filtering</i> berdasarkan umpan balik implisit. Secara khusus, ini memberikan rekomendasi produk berdasarkan interaksi pengguna dan item. Data pelatihan untuk model ini harus berisi urutan pasangan (ID pengguna, ID anime) yang menunjukkan bahwa pengguna yang ditentukan telah berinteraksi dengan item, misalnya, dengan memberi peringkat atau mengklik. Secara khusus, ini memberikan rekomendasi produk berdasarkan interaksi pengguna dan item. Data pelatihan untuk model ini harus berisi urutan pasangan (ID pengguna, ID anime) yang menunjukkan bahwa pengguna yang ditentukan telah berinteraksi dengan item, misalnya, dengan memberi peringkat atau mengklik. 

Pada proses ini model yang digunakan adalah <i>Deep Learning</i> untuk <i>Collaborative Filtering</i>. Aplikasi dari <i>deep learning</i> pada project ini adalah <i>layer embedding</i>. <i>Embedding  adalah pemetaan variabel diskrit — kategoris — ke vektor bilangan kontinu sehingga dapat digunakan untuk proses selanjutnya. Kemudian, setelah didapatkanlah nilai vektornya, lakukan operasi perkalian dot product antara hasil embeddingnya (user dan movie). Selain itu, kita juga dapat menambahkan bias untuk setiap user dan movie. kecocokan ditetapkan dalam skala 0 hingga 1 dengan fungsi aktivasi sigmoid. Pada model ini, Optimizer yang digunakan adalah optimizer adam dan loss function yang digunakan adalah Loss Binary Crossentropy. 

Tahapan pada proses ini yaitu :
* Memberikan ID baru pada setiap baris pada dataframe dengan membuat <i>unique value</i> dari userId kemudian membuat nilai sama dengan jumlah userId, membuat kolom user yang nilainya dihasilkan berdasarkan proses generate nilai userId dan membuat kolom user yang nilainya dihasilkan berdasarkan proses generate nilai movieId
* Membagi data yang akan digunakan untuk proses training dan testing  k

Langkah-langkah yang digunakan untuk mendapatkan list rekomendasi film berdasarkan aktivitas user berdasarkan <i>rate</i> yang diberikan oleh <i>user</i> 
  <ol><li> Mencari data <i>movie</i> apa saja yang telah ditonton oleh user lalu memasukkannya kedalam dataframe yang baru</li>
  <li>Mencari rating terendah dari film</li>
  <li>Tahap selanjutnya yaitu membuat top_movie_reference dengan mengurutkannya berdasarkan rating dari film</li>
  <li>Selanjutnya adalah membuat dataframe baru berdasarkan dataframe utama dan melakukan seleksi yang mana data yang dimasukkan adalah film yang termasuk kedalam top_movie_reference</li>
  <li>Tahap terakhir adalah menghitung rata-rata rating yang diberikan oleh user</li></ol>

Berikut adalah daftar 10 rekoemndasi dari yang dihasilkan
|     | movieId |                                     title |                                               genres |
|-----|--------:|------------------------------------------:|-----------------------------------------------------:|
|  0  |       1 |                          Toy Story (1995) |      Adventure\|Animation\|Children\|Comedy\|Fantasy |
| 138 |     165 |         Die Hard: With a Vengeance (1995) |                              Action\|Crime\|Thriller |
| 224 |     260 | Star Wars: Episode IV - A New Hope (1977) |                            Action\|Adventure\|Sci-Fi |
| 277 |     318 |          Shawshank Redemption, The (1994) |                                         Crime\|Drama |
| 314 |     356 |                       Forrest Gump (1994) |                          Comedy\|Drama\|Romance\|War |
| 398 |     457 |                      Fugitive, The (1993) |                                             Thriller |
| 506 |     588 |                            Aladdin (1992) |      Adventure\|Animation\|Children\|Comedy\|Musical |
| 508 |     590 |                 Dances with Wolves (1990) |                            Adventure\|Drama\|Western |
| 512 |     595 |               Beauty and the Beast (1991) | Animation\|Children\|Fantasy\|Musical\|Romance\|IMAX |
| 546 |     648 |                Mission: Impossible (1996) |                 Action\|Adventure\|Mystery\|Thriller |

## Evaluation
Pada bagian ini, saya menguji performa model dengan <i>Mean Squared Error</i>, <i>precision</i>, dan <i>recall</i>. Kedua metrik ini sangat cocok untuk mengukur performa model <i>machine learning</i>. Adapun penjelasan dari setiap metrik yaitu :
* <i>Mean Squared Error</i> adalah fungsi loss yang paling sederhana dan paling umum, sering diajarkan dalam kursus pengantar Machine Learning. Metode Mean Squared Error secara umum digunakan untuk mengecek estimasi berapa nilai kesalahan pada peramalan. Nilai <i>Mean Squared Error</i> yang rendah atau nilai <i>mean squared error</i> mendekati nol menunjukkan bahwa hasil peramalan sesuai dengan data aktual dan bisa dijadikan untuk perhitungan peramalan di periode mendatang. Metode <i>Mean Squared Error</i> biasanya digunakan untuk mengevaluasi metode pengukuran dengan model regressi atau model peramalan seperti <i>Moving Average</i>, <i>Weighted Moving Average</i> dan <i>Analisis Trendline</i>. Cara menghitung <i>Mean Squared Error</i> (MSE) adalah melakukan pengurangan nilai data aktual dengan data peramalan dan hasilnya dikuadratkan (<i>squared</i>) kemudian dijumlahkan secara keseluruhan dan membaginya dengan banyaknya data yang ada. Nilai MSE yang didapatkan dari proyek ini adalah 0.0083
Grafik MSE yang dihasilkan dari proses training model yang dibuat adalah
<img width="294" alt="image" src="https://user-images.githubusercontent.com/97927496/205106871-45541901-1fed-4bc4-9cbb-38d09a343ab6.png">

* <i>Recall</i> adalah tingkat keberhasilan sistem dalam menemukan kembali sebuah informasi. Nilai <i>recall</i> yang didapatkan dari proyek ini adalah 0.6907.
Grafik <i>recall</i> yang dihasilkan dari proses training model yang dibuat adalah
<img width="295" alt="image" src="https://user-images.githubusercontent.com/97927496/205107786-5275eafc-47e3-4c43-890c-8a61c6d521cd.png">

* <i>Precision</i> adalah tingkat ketepatan antara informasi yang diminta oleh pengguna dengan jawaban yang diberikan oleh sistem. Sedangkan <i>recall</i> adalah tingkat keberhasilan sistem dalam menemukan kembali sebuah informasi. Nilai Precision yang didapatkan dari proyek ini adalah 1.0000
Grafik <i>precision</i> yang dihasilkan dari proses training model yang dibuat adalah
<img width="298" alt="image" src="https://user-images.githubusercontent.com/97927496/205107287-60dab3c2-2418-4ca2-80a6-c31a9ce5c3c9.png">

