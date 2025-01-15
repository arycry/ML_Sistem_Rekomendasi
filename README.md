# Sistem Rekomendasi Wisata Indonesia - Dita Ary Crystian

# Domain Projek

Perkembangan teknologi membawa perubahan pesat sehingga semua informasi dapat diakses dengan mudah. Salah satu sektor yang terdampak perkembangan teknologi yaitu sektor pariwisata. Indonesia memiliki potensi pariwisata yang sangat besar, dengan beragam destinasi menarik. Namun, banyaknya pilihan destinasi terkadang membuat wisatawan kesulitan menentukan tempat yang tepat untuk dikunjungi. Oleh karena itu, dibutuhkan sebuah sistem rekomendasi yang dapat membantu wisatawan menemukan destinasi yang sesuai dengan preferensi mereka. Proyek ini bertujuan membangun sistem rekomendasi destinasi wisata di Indonesia menggunakan dataset yang berisi informasi detail mengenai berbagai tempat wisata di Indonesia. 

Referensi: [Jurnal rekomendasi wisata](https://ejournal.unama.ac.id/index.php/jurnalmsi/article/download/1262/1071).

# Business Understanding

## Problem Statement

Berdasarkan latar belakang yang dijelaskan di atas, kita mendapatkan rumusan masalah sebagai berikut:
1. Bagaimana sistem dapat merekomendasikan destinasi wisata di Indonesia berdasarkan deskripsi, kategori, dan fasilitas yang tersedia di dataset?
2. Bagaimana sistem dapat menyederhanakan proses pencarian informasi dan memberikan rekomendasi yang relevan secara efisien?

## Goals
Berdasarkan rumusan masalah yang dijelaskan di atas, kita mendapatkan tujuan sebagai berikut:
1. Membangun sistem rekomendasi yang efektif menggunakan informasi deskripsi, kategori, dan fasilitas destinasi.
2. Membangun sistem rekomendasi yang efisien dan efektif menggunakan rating destinasi wisata.

## Solution 
Berdasarkan tujuan di atas, ada beberapa solusi yang bisa dilakukan, yaitu:
1. Membuat sistem menggunakan Content-Based Filtering. Metode ini merekomendasikan destinasi yang serupa dengan destinasi yang sebelumnya disukai oleh pengguna, berdasarkan deskripsi dan fitur destinasi tersebut (misalnya, kategori, fasilitas).
2. Membuat sistem menggunakan Collaborative Filtering. Metode ini merekomendasikan destinasi berdasarkan preferensi pengguna lain yang memiliki selera yang mirip. Dalam konteks ini, kita bisa menggunakan user-item interaction untuk memprediksi rating yang mungkin diberikan user ke suatu destinasi.


# Data Understanding
Pada tahap ini, kita akan melakukan hal- hal berikut:
1. Mendeskripsikan dataset
2. Mengecek masing-masing variabel dari semua dataset
3. Melakukan EDA dari masing-masing dataset
4. Mengetahui jumlah *user* dan *location*
5. Mengetahui jumlah rating
6. Melakukan data preprocessing untuk modeling

Berikut adalah masing-masing penjelasan nya:

## Deskripsi Dataset

![1](https://github.com/user-attachments/assets/b99faa58-d2ae-43f4-adbf-d3bdc8bacc26)

Dataset pada projek ini diambil dari kaggle, yaitu [Sistem Rekomendasi Wisata](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=tourism_with_id.csv). Pada dataset ini berisi 4 *file* dengan nama `package_tourism`, `tourism_rating`, `tourism_with_id`, dan `user` dengan ekstensi `csv` `(*Comma Separated Values*)`, dengan masing-masing banyaknya data yaitu 100 data dan 7 variabel untuk `package_tourism(package)`, 1000 data dan 3 variabel untuk `tourism_rating(rating)`, 437 data dan 13 variabel untuk `tourism_with_id(location)`, serta 300 data dan 3 variabel untuk `user`.
Berikut adalah penjelasan variabel dari masing-masing dataset:
## package_tourism(package)
Berikut merupakan deskripsi variabel dari dataset `package_tourism(package)`:
- Package: ID unik untuk setiap paket wisata.
- City: Kota di mana tempat wisata berada.
- Place_Tourism1 : Destinasi wisata pertama yang termasuk dalam paket
- Place_Tourism2 : Destinasi wisata kedua yang termasuk dalam paket
- Place_Tourism3 : Destinasi wisata ketiga yang termasuk dalam paket
- Place_Tourism4 : Destinasi wisata keempat yang termasuk dalam paket
- Place_Tourism5 : Destinasi wisata kelima yang termasuk dalam paket
## tourism_rating(rating)
Berikut merupakan deskripsi variabel dari dataset `tourism_rating(rating)`:
- User_Id       : ID unik untuk setiap user.
- Place_Id      : ID unik untuk setiap tempat wisata.
- Place_Ratings : Rating untuk setiap tempat wisata dari user.
## tourism_with_id(location)
- Place_Id      : ID unik untuk setiap tempat wisata.
- Place_Name    : Nama tempat wisata.
- Description   : Deskripsi singkat mengenai tempat wisata.
- Category      : Kategori tempat wisata (misalnya, Budaya, Taman Hiburan, Cagar Alam).
- City          : Kota di mana tempat wisata berada.
- Price         : Harga tiket masuk ke tempat wisata (dalam rupiah).
- Rating        : Penilaian rata-rata dari pengunjung (skala 1-5).
- Time_Minutes  : Waktu yang diperlukan untuk mengunjungi tempat wisata (dalam menit).
- Coordinate    : Koordinat geografis tempat wisata.
- Lat           : Garis lintang lokasi tempat wisata.
- Long          : Garis bujur lokasi tempat wisata.
- Unnamed: 11   : Tidak diketahui.
- Unnamed: 12   : Tidak diketahui.
## user
- User_Id       : ID unik untuk setiap pengguna.
- Location      : Kota atau lokasi asal pengguna.
- Age           : Usia pengguna.
### EDA
Pada tahap ini kita akan mengetahui banyaknya data dan mengecek beberapa kolom di semua dataset tersebut. Kita akan mengecek dari 4 dataset terlebih dahulu. 
## package
![2](https://github.com/user-attachments/assets/b7377c46-561f-4dd7-b885-e7f79f9afb4b)

![3](https://github.com/user-attachments/assets/36a4fc12-9863-4014-a24b-9c33d5b79f22)

Terlihat bahwa kita memiliki 100 data dan 7 variabel, dengan ada nya nilai null pada variabel Place_tourism4 dan Place_tourism5. Selain itu, pada dataset ini memiliki 5 data unik untuk variabel City, yaitu Jakarta, Yogyakarta, Bandung, Semarang, Surabaya, dengan banyaknya data di tiap kota adalah 20 paket.
## rating
![4](https://github.com/user-attachments/assets/20835ccb-7274-4f92-b444-525fd328483b)

![5](https://github.com/user-attachments/assets/5560e291-682d-42ae-86b2-c5e6dfff7bdb)

Terlihat bahwa kita memiliki 10000 data dan 3 variabel. Pada dataset ini, kita juga memiliki 300 nilai unik pada variabel User_Id dan 5 nilai unik pada Place_Ratings, dengan nilai 1,2,3,4,5, dengan rating 4 memiliki data paling banyak daripada rating lainnya dengan selisih yang tipis.

## location
![6](https://github.com/user-attachments/assets/29c4ca3a-ec7c-45e1-b69b-9715b708c7c2)

![7](https://github.com/user-attachments/assets/ad0845ab-d561-4146-9355-942c20ca47d5)

Terlihat bahwa kita memiliki 437 data dan 13 variabel, dimana merupakan banyak nya data unik dari tempat wisata yang kita punya, dan adamnya nilai null pada kolom Time_Minutes dan Unnamed: 11. Pada dataset ini, kita memiliki 6 nilai unik pada kolom Category, yaitu Budaya, Taman Hiburan, Cagar Alam, Bahari, Pusat Perbelanjaan, Tempat Ibadah dan Taman hiburan memiliki data paling banyak dibandingkan kategori lain dengan 135 data.

## user
![8](https://github.com/user-attachments/assets/a18bf1d2-81b1-4bb3-96cc-e37b481cb2af)

![9](https://github.com/user-attachments/assets/bfc72d1a-4c99-4031-a45a-8049954eaa14)

![10](https://github.com/user-attachments/assets/b7a13040-abee-43a1-841c-1569a2aff584)

Terlihat bahwa kita memiliki 300 data dan 3 variabel, yang merupakan banyaknya nilai unik pada user. Pada dataset ini, kita memiliki 28 nilai unik untuk asal daerah user, yaitu kolom Location. Selain itu, kita memiliki data di kolom Age, yaitu usia user, dengan rentang 24 sampai dengan 40 tahun. Serta 5 user pemberi rating terbanyak berada di Bekasi, Semarang, Yogyakarta, Lampung, dan Bogor.

## melihat total user dan location
Selanjutnya, kita akan membagi 4 dataset menjadi 2 bagian, yaitu user dan location(tempat wisata). Kita akan menggabungkan dataset rating_df dan user_df untuk mengetahui total dari user, serta kita akan menggabungkan dataset location_df dan rating_df untuk mengetahui total dari location.
Pada tahap ini, kita ingin melihat total *user* dari menggabungkan `User_Id` dari tabel *rating_df* dan *user_df*

![11](https://github.com/user-attachments/assets/daaf8f9e-1e1f-4974-a301-03a3d4d0ceb6)


Terlihat pada gambar, banyaknya *user* yang ada yaitu 300 *user*

Setelah itu, kita akan melihat total tempat wisata dari menggabungkan `Place_Id` dari tabel *location_df* dan *rating_df*

![12](https://github.com/user-attachments/assets/4a1104f3-76ea-4db0-b338-b9359f2fcf60)


Terlihat pada gambar, banyaknya tempat wisata yang ada yaitu 437 tempat.
## melihat total rating
Selanjutnya, kita akan membuat variabel baru, yaitu place, dengan menggabungkan data rating dan place untuk melihat banyaknya rating dari gabungan data yang ada, pada kasus ini data rating_df dan location_df. Setelah itu, kita akanmencoba mengecek variabel setelah prnggabungan data. Terlihat bahwa kita memiliki 10000 data rating dari gabungan dataset rating_df dan location_df, serta data ini memiliki nilai null pada kolom time_minutes dan Unnamed: 11. Setelah itu, kita akan mengambil fitur numerik terlebih dahulu, lalu kita akan mencari jumlah dari fitur numerik tersebut berdasarkan Place-Id. Berikut adalah hasil dari proses ini, yaitu melihat total rating:

![13](https://github.com/user-attachments/assets/5d07624c-f661-4df0-82ec-e8a28c7761d2)

## Data Preprocessing
Pada tahap ini, kita akan melakukan langkah-langkah berikut:
1. Membuat dataframe untuk Modeling *Content Based Learning* 
2. Mengecek nilai null
3. Mengecek nilai duplikat
4. Mengecek deskripsi analisis dan banyaknya data unik
5. Membuat dataframe untuk Modeling *Collaborative Filtering*
Berikut merupakan penjelasan dari masing-masing tahap:
### Membuat dataframe untuk Modeling *Content Based Learning*
Pada tahap ini, kita akan membuat dataframe untuk pembuatan sistem dengan metode *Content Based Filtering*. Langkah pertama, kita akan membuat dataframe bernama `all_place_name` dengan data dari `rating_df`. Setelah itu, kita gabungkan dataframe ini dengan kolom `place_name`, `category`, dan `city` dari tabel *location_df* dengan kunci `Place_Id`. Setelah itu kita akan menggabungkan lagi dengan kolom `age` dari tabel *user_df* dengan kunci `User_Id`. Hasil akhir 4 data pertama dataframe ini yaitu:

![14](https://github.com/user-attachments/assets/fda66346-06e7-4201-b3f7-864c7ecac963)

### Mengecek nilai null
Pada tahap ini, kita akan mengecek nilai null dari dataset yang telah dibuat tadi, berikut merupakan hasil pengecekan nilai null:

![15](https://github.com/user-attachments/assets/4f1f00e0-4642-4ca5-8315-74514676f615)

Terlihat bahwa data kita tidak memiliki nilai null, sehingga kita bisa lanjut ke tahap berikutnya. 

### Mengecek data duplikat
Pada tahap ini, kita akan mengecek nilai duplikat dari dataset yang telah dibuat. Berikut merupakan hasil pengecekan nilai null:

![24](https://github.com/user-attachments/assets/27e4c4c6-6126-4358-a1be-713f2e73d401)

Terlihat bahwa data kita tidak memiliki nilai null, sehingga kita perlu untuk menghapus ni[lai duplikat tersebut dengan fungsi `drop_duplicated()`

### Mengecek deskripsi analisis dan banyaknya data unik
Pada tahap ini, kita akan mengecek deskripsi analisis dan kita akan mengecek banyaknya data unik pada kolom Place_Id, Place_Name, dan Location.
Berikut merupakan deskripsi analisis dari data numerik ini:

![16](https://github.com/user-attachments/assets/bcdd000f-307e-451e-a3fb-b6ba29fc14dc)

Berikut merupakan deskripsi analisis dari data numerik ini:

![17](https://github.com/user-attachments/assets/cb07cf28-91a7-442b-8f34-9fbb5a2fb9ce)

Berdasarkan data diatas, terlihat bahwa banyaknya data unik pada kolom Place_Id sebanyak 437 data unik, Place_Name sebanyak 437 data unik, dan Location sebanyak 6 data unik. 
Sehingga dataset sudah siap untuk masuk ke tahap data preparation.
# Data Preparation
Pada tahap ini, kita akan membuat dataframe yang siap untuk *content based filtering*. Hal ini penting dilakukan karena untuk memastikan data bersih, terhindar dari *error*, dan memastikan model bekerja lebih efektif. 
Berikut adalah langkah-langkah dalam data prparation ini:
## mengecek kembali data
Pada tahap ini, kita akan mengecek kembali data yang telah kita preprocessing di langkah sebelumnya. Kita akan mengurutkan data terlebih dahulu berdasarkan Place_Id. Berikut adalah 5 data pertama data tersebut:

![18](https://github.com/user-attachments/assets/98e67e72-c98d-4e30-978e-be1f72a5f493)

## mengecek nilai unik dari kolom Category
Pada tahap ini, kita akan mengecek nilai unik dari kolom Category untuk mengecek apakah ada kategori tempat wisata. 

![19](https://github.com/user-attachments/assets/598b6bb9-90f3-42b1-891b-0bb3c35a5a9f)

Terlihat bahwa kita mempunyai kategori tempat wisata yaitu Budaya, Taman Hiburan, Cagar Alam, Pusat Perbelanjaan, dan Tempat Ibadah.

## Menghapus duplikat pada Place_Id
Pada tahap ini, kita akan membuat variabel preparation yang berisi data all_place_name. Lalu kita akan mengurutkan data berdasarkan Place_Id. Lalu kita akan menghapus nilai duplikat dari Place_Id karena kita hanya menggunakan data unik dari data yang kita punya.
## Membuat data dictionary untuk modeling
Pada tahap ini, kita akan konversi data series menjadi list, sehingga kita menggunakan fungsi tolist untuk konversi data. Setelah itu, kita akan membuat data dictionary untuk data place_id, place_name, dan place_cat(place_category). Lalu kita akan mengecek data yang telah kita buat. Berikut merupakan 5 data pertama kita untuk modeling. 
![20](https://github.com/user-attachments/assets/8c9e9282-4ae1-44e1-9284-fa1470d35ccd)

Dataframe ini telah siap untuk dibuat sistem dengan model *content based filtering*.  

## Membuat dataframe untuk Modeling *Collaborative Filtering*
Pada tahap ini, kita akan membuat dataframe untuk pembuatan sistem dengan metode *Collaborative Filtering*. Pada tahap pertama, kita akan membuat variabel df yang memuat dataset rating_df. Kemudian kita melakukan persiapan data untuk menyandikan (encode) fitur User_Id ke dalam indeks integer. Berikut merupakan hasil encode User_Id:

![26](https://github.com/user-attachments/assets/1de8c201-d77d-4d7f-8486-ea72d6b5c304)

Setelah itu, kita melakukan persiapan data untuk menyandikan (encode) fitur Place_Id ke dalam indeks integer.  Berikutnya, kita akan memetakan userID dan placeID ke dataframe yang berkaitan. Setelah itu, kita akan mengecek beberapa hal dalam data seperti jumlah user, jumlah tempat wisata, dan mengubah nilai rating menjadi float. Berikut merupakan hasil pengecekan banyaknya *user* dan *place*:

![27](https://github.com/user-attachments/assets/27ef8fac-d732-490c-9b9a-07c025ae8c8a)

Terlihat bahwa kita memiliki data *user* sebanyak 300 data, data *place* sebanyak 437 data, serta data rating dari 1.0 sampai 5.0.

# Data Modeling
Pada tahap ini, kita akan menggunakan *Content Based Filtering* dan *Collaborative Filtering* untuk menjawab problem statement dari tahap business understanding
## *Content Based Filtering*
*Content-based filtering* adalah metode yang digunakan dalam sistem rekomendasi dan analisis data yang berfokus pada karakteristik atau konten dari item-item yang ingin direkomendasikan atau dianalisis. Pendekatan ini menggunakan atribut-atribut atau fitur-fitur item untuk menentukan kesamaan antara item yang ada dan preferensi pengguna. Tahapan-tahapan yang akan dilakukan yaitu:
1. Data Preparation
   
   Kita sudah menyiapkan data yang telah siap untuk modeling dengan *Content-based filtering*
2. TF-IDF

   Metode Term Frequency-Inverse Document Frequency (TF-IDF) adalah salah satu teknik  yang  digunakan  dalam  pengolahan  teks dan 
   pemodelan bahasa alami. Tujuan utama dari metode  TF-IDF  adalah  untuk  mengevaluasi seberapa penting suatu kata (term) dalam sebuah 
   dokumen dalam konteks koleksi dokumen yang lebih besar. Pada tahap ini, kita akan memanggil fungsi TfidfVectorizer() lalu kita akan 
   fit dengan kolom Category. Lalu kita akan melakukan fit transform dan kita akan menggunakan fungsi todense untuk menghasilkan vektor 
   TF-IDF dalam bentuk matrix. Setelah itu, kita buat dataframe hasil dari TF-IDF. Berikut merupakan hasil TF-IDF yang berhasil kita 
   buat:

   ![21](https://github.com/user-attachments/assets/b9b2e8f9-8755-4ffa-8310-5f6d5c8e1c58)

   Bisa terlihat bahwa Museum Taman Prasasti memiliki nilai 1 pada kolom budaya, sehingga Museum Taman Prasasti termasuk ke dalam 
   kategori budaya, dan sebagainya.
   
3. *Cosinus Similarity*
   
   *Cosinus Similarity* adalah ukuran kesamaan antara dua vektor bukan nol yang banyak digunakan dalam banyak aplikasi pembelajaran 
   mesin dan analisis data. Sebenarnya, ukuran ini mengukur kosinus sudut antara dua vektor. Hasilnya, sebuah ide diberikan tentang 
   seberapa jauh kedua vektor menunjuk ke arah yang sama terlepas dari besarnya. Pada tahap ini, kita akan menghitung derajat kesamaan 
   (similarity degree) antar tempat wisata dengan teknik *cosinus similarity*. Selanjutnya, kita akan melihat matriks kesamaan setiap 
   tempat wisata dengan menampilkan nama tempat wisata dalam 5 sampel kolom (axis = 1) dan 10 sampel baris (axis=0). Berikut ini 
   merupakan hasil dari *Cosinus Similarity*:

   ![22](https://github.com/user-attachments/assets/debade1f-8793-4eee-9e02-c838faf10488)

   Pada contohnya, bisa kita lihat bahwa Curug Malela memiliki angka 1 dengan Situ Patenggang dan Taman Hutan Raya Ir. H. Juanda. Ini 
   berarti bahwa Curug Mamela memiliki kategori yang sama dengan Situ Patenggang dan Taman Hutan Raya Ir. H. Juanda.

5. Membuat fungsi rekomendasi dan melihat hasil rekomendasi

   Setelah itu, kita akan membuat fungsi untuk mendapatkan rekomendasi tempat wisata. Pada fungsi ini, kita akan membuat fungsi untuk 
   mendapatkan 5 rekomendasi tempat wisata dengan nama yang kita inputkan nanti. Setelah itu, kita akan melihat hasil dari rekomendasi 
   yang kita buat. Berikut merupakan input untuk rekomendasi.

   ![23](https://github.com/user-attachments/assets/b2607b11-12ff-426f-b56e-2eb75cf8dbab)

   Berikut merupakan hasil rekomendasi dari input yang telah kita masukkan:

   ![25](https://github.com/user-attachments/assets/2d138277-8653-4e0c-8abe-3c432842ebb9)

   Terlihat bahwa fungsi merekomendasikan tempat wisata dengan category yang sama, yaitu kategori cagar alam.

### Kelebihan dan Kekurangan
   Keuntungan dari content-based filtering adalah kemampuannya untuk memberikan rekomendasi yang personal dan dapat menjelaskan alasan 
   di balik rekomendasi tersebut. Namun, pendekatan ini juga memiliki keterbatasan, seperti kurangnya kemampuan untuk merekomendasikan 
   item yang sangat berbeda dari yang telah disukai oleh pengguna.
   
## *Collaborative Filtering*
Pada teknik *collaborative filtering* memerlukan sekumpulan item yang didasarkan pada pilihan historis pengguna. Sistem ini tidak memerlukan banyak fitur produk untuk bekerja. Penyematan atau vektor fitur mendeskripsikan setiap item dan Pengguna, dan menenggelamkan item dan pengguna di lokasi penyematan serupa. Itu membuat lampiran untuk item dan pengguna sendiri. Tahapan-tahapan yang akan dilakukan yaitu:
1. Data Preparation

   Kita sudah menyiapkan data yang telah siap untuk modeling dengan *Content-based filtering*

2. Acak data

   Pada tahap ini, kita akan menhgacak data supaya distribusinya menjadi random. Kita akan random dari kolom User_Id dan Place_Id. Berikut adalah hasil 5 data pertama dari acak data:

    ![28](https://github.com/user-attachments/assets/58fb2b84-f715-40d3-94b9-1c2e4e7907c3)

3. Membagi data train dan data validation

   Pada tahap ini, kita bagi data train dan validasi dengan komposisi 80:20. Namun sebelumnya, kita perlu memetakan (mapping) data user dan place menjadi satu value terlebih dahulu. Lalu, buatlah rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training.

4. Training
   
   Pada tahap ini, kita membuat class RecommenderNet dengan keras Model class. Setelah itu, kita akan melakukan proses compile terhadap model, dengan menggunakan fungsi loss binary crossentropy, optimizer adam, dan matriks RMSE. Setelah itu, kita akan melakukan training data.

6. Visualisasi Training

   Pada tahap ini, kita akan melakukan visualisasi proses training, kita plot metrik evaluasi dengan matplotlib. Berikut merupakan visualisasinya:

   ![29](https://github.com/user-attachments/assets/eeba095b-f603-4a8c-8bce-2f0c4d4f7e3c)

    
8. Rekomendasi
   
   Sebelum melakukan prediksi sistem rekomendasi, kita akan membuat variabel place_not_visited terlebih dahulu karena daftar place_not_visited inilah yang akan menjadi resto yang kita rekomendasikan. Selanjutnya, kita akan melakukan prediksi untuk memperoleh 10 rekomendasi tempat wisata. Berikut ini merupakan hasil 10 rekomendasi wisata berdasarkan rating:

   ![30](https://github.com/user-attachments/assets/b6e35b80-2683-4ef8-bb33-387e29411f88)


### Kelebihan dan Kekurangan
Dibandingkan dengan *Content Based Filtering*, *Collaborative Filtering* lebih efektif dalam memberikan rekomendasi baru kepada pengguna. Metode berbasis kolaboratif menarik rekomendasi dari kumpulan pengguna yang memiliki minat yang sama dengan satu pengguna target. Kekurangannya, Masalah cold start mungkin merupakan kelemahan yang paling banyak dikutip dari sistem *Collaborative Filtering*. Hal ini terjadi ketika pengguna baru (atau bahkan item baru) memasuki sistem. Kurangnya riwayat interaksi item pada pengguna tersebut mencegah sistem mengevaluasi kesamaan atau keterkaitan pengguna baru tersebut dengan pengguna yang sudah ada.


# Evaluasi
Pada tahap ini, kita akan menguji seberapa efektifnya suatu model sistem rekomendasi. Pada projek ini, kita akan evaluasi model *Content Based Filtering* menggunakan *Precision* dan evaluasi model *Collaborative Filtering* menggunakan RMSE.
## Evaluasi model *Content Based Filtering* menggunakan *Precision*

Sebelum kita membahas ke precision, kita akan membahas Confusion Matrix terlebih dahulu. Confusion Matrix adalah pengukuran performa untuk masalah klasifikasi machine learning dimana keluaran dapat berupa dua kelas atau lebih. Confusion Matrix adalah tabel dengan 4 kombinasi berbeda dari nilai prediksi dan nilai aktual. Ada empat istilah yang merupakan representasi hasil proses klasifikasi pada confusion matrix yaitu True Positif, True Negatif, False Positif, dan False Negatif

- True Positive (TP) :
Interpretasi: Anda memprediksi positif dan itu benar.
- True Negative (TN):
Interpretasi: Anda memprediksi negatif dan itu benar.
- False Positive (FP): (Kesalahan Tipe 1)
Interpretasi: Anda memprediksi positif dan itu salah.
- False Negative (FN): (Kesalahan Tipe 2, kesalahan tipe 2 ini sangat berbahaya)
Interpretasi: Anda memprediksi negatif dan itu salah.

Salah satu nilai yang bisa dihitung dengan Confusion Matrix adalah precision. Precision adalah salah satu metrik penting dalam evaluasi sistem pengambilan informasi yang mengukur tingkat ketepatan atau akurasi sistem dalam menemukan dokumen yang relevan dengan kebutuhan pengguna.  Berikut rumus dari precision di sistem rekomendasi:

![31](https://github.com/user-attachments/assets/ea678bbd-340e-4f71-a9d1-db012085f3c4)

Namun pada sistem rekomendasi, Precision pada K adalah rasio item relevan yang diidentifikasi dengan benar dalam total item yang direkomendasikan dalam daftar sepanjang K. Sederhananya, ini menunjukkan berapa banyak item yang direkomendasikan atau diambil yang benar-benar relevan. Berikut rumus precison di sistem rekomendasi:

![32](https://github.com/user-attachments/assets/ef15d37c-c78a-4030-9850-2458ae220f89)

Dengan menggunakan rumus diatas, kita akan mencari nilai precision pada sistem rekomendasi *Content Based Filtering*. Kita akan menampilkan data input terlebih dahulu:

![23](https://github.com/user-attachments/assets/02e0c154-2fff-4f38-ae98-998e98cbf510)

Pada data input, kita menggunakan data Kebun Binatang Ragunan dengan Category Cagar Alam. Setelah itu kita akan menampilkan hasil 5 rekomendasi yang dihasilkan dari input tersebut:

![25](https://github.com/user-attachments/assets/a861f595-267d-4500-ac66-24e2387a2fa8)

Terlihat diatas bahwa 5 rekomendasi yang dihasilkan memiliki category yang sama, yaitu Cagar Alam. Maka, sesuai dengan rumus diatas:

`precision = number of relevant item in K / total number of items in K`
`precision = 5 / 5`
`precision = 1`

Dari 5 rekomendasi di atas didapatkan nilai precision sebesar 1 dari model *Content Based Learning* yang dikembangkan. Artinya model bekerja dengan sangat baik.

## Evaluasi model *Collaborative Filtering* menggunakan RMSE

Root mean square error (RMSE) adalah simpangan baku residual, atau selisih rata-rata antara nilai proyeksi dan nilai aktual yang dihasilkan oleh model statistik. Mengingat bahwa rumus RMSE pada dasarnya adalah rumus simpangan baku, rumus ini seharusnya dapat dikenali oleh siapa pun yang memiliki pelatihan dalam statistik. Itu masuk akal karena RMSE sama dengan simpangan baku residual. Rumus ini menghitung varians antara nilai yang diamati dan yang diharapkan. Berikut adalah rumus dari RMSE:

![33](https://github.com/user-attachments/assets/b3166cff-c306-49ad-a46d-20104a451f06)

Dengan: 

- yi adalah nilai aktual dari observasi ke-i.
- ŷi adalah nilai prediksi untuk observasi ke-i.
- P adalah jumlah parameter yang diestimasi, termasuk konstanta.
- N adalah jumlah observasi.

RMSE membantu mengevaluasi model dengan melihat error pada saat training. Berikut merupakan visualisasi training pada projek ini:

![29](https://github.com/user-attachments/assets/88a7ab83-6ad8-4eb2-afec-c4eca46be845)

Berdasarkan grafik tersebut, kita bisa mendapatkan bahwa RMSE dari data train adalah 0.3091 dan RMSE dari data validation adalah 0.3658, dimana sistem yang dikembangkan sudah baik untuk model Collaborative Filtering ini.

# Kesimpulan

Projek ini berhasil membuat sistem rekomendasi untuk tempat wisata dengan 2 algoritma sistem rekomendasi, yaitu *Content Based Filtering* dan *Collaborative Filtering*. Pada projek ini, kita berhasil membuat langkah-langkah pengerjaan sistem rekomendasi, seperti Data Understanding, EDA, Data preprocessing, Data Preparation, Modeling, serta evaluasi model. Pada sistem rekomendasi *Content baseed Filtering*, hasil evaluasi yang dihasilkan sangat baik, sehingga kita berhasil membangun sistem rekomendasi yang efektif menggunakan informasi deskripsi, kategori, dan fasilitas destinasi. Begitu pula dengan sistem rekomendasi *Collaborative Filtering*, hasil evaluasi yang dihasilkan cukup baik, sehingga kita berhasil membangun sistem rekomendasi yang efisien dan efektif menggunakan rating destinasi wisata. Namun hasil projek ini belum sempurna karena dataset yang terbatas, sehingga bisa saja model merekomendasikan hal yang kurang cocok dengan input tempat wisata. 

# Reference
- Raysa Puteri Ardhiyani, Herry Mulyono. 2018. ANALISIS DAN PERANCANGAN SISTEM INFORMASI PARIWISATA BERBASIS WEB SEBAGAI MEDIA PROMOSI PADA KABUPATEN TEBO . Jurnal Manajemen Sistem Informasi. Vol.3, No.1, Maret 2018
- Dwi Septiani, Ica Isabela. 2022. ANALISIS TERM FREQUENCY INVERSE DOCUMENT FREQUENCY(TF-IDF) DALAM TEMU KEMBALI INFORMASI PADA DOKUMEN TEKS. SINTESIA: Jurnal Sistem dan Teknologi Informasi Indonesia. Vol. 01, No. 2, Maret 2022.
- geeksforgeeks.org. (2024, 10 Oktober). Cosine Similarity. Diakses pada 15 Januari 2025, dari https://www.geeksforgeeks.org/cosine-similarity/
- Sadesty Rahmadhani, LutfiHakim, GalihHendra Wibowo, Sepyan Purnama Kristanto, Eka Mistiko Rini. 2024. SISTEM REKOMENDASI PENELUSURAN BUKU BERBASIS CONTENT-BASED FILTERINGDENGAN PEMBOBOTAN TF-RF. Volume 10, Edisi 4, Agustus 2024.
- dqlab.id. (2023, 28 November). Content Based Filtering dalam Algoritma Data Science. Diakses pada 15 Januari 2025. dari https://dqlab.id/content-based-filtering-dalam-algoritma-data-science
- dqlab.id. (2022, 16 November). Pendekatan Machine Learning Collaborative Filtering. Diakses pada 15 Januari 2025. dari https://dqlab.id/pendekatan-machine-learning-collaborative-filtering
- ibm.com. (2024, 21 Maret). Apa itu penyaringan kolaboratif?. Diakses pada 15 Januari 2025. dari https://www.ibm.com/id-id/topics/collaborative-filtering
- socs.binus.ac.id. (2020). Confusion Matrix. Diakses pada 15 Januari 2025. dari https://socs.binus.ac.id/2020/11/01/confusion-matrix/
- evidentlyai.com. (2025, 9 Januari). Precision and recall at K in ranking and recommendations. Diakses pada 15 Januari 2025. dari https://www.evidentlyai.com/ranking-metrics/precision-recall-at-k
- arize.com/. (2023, 8 Agustus). Root Mean Square Error (RMSE) In AI: What You Need To Know. Diakses pada 15 Januari 2025. dari https://arize.com/blog-course/root-mean-square-error-rmse-what-you-need-to-know/






   



   
















