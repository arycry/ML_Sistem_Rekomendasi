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
Pada tahap ini, akan lakukan hal- hal berikut:
1. Mendeskripsikan dataset
2. Mengecek masing-masing variabel dari semua dataset
3. Melakukan EDA dari masing-masing dataset


Berikut adalah masing-masing penjelasan nya:

## Deskripsi Dataset

![1](https://github.com/user-attachments/assets/c4a2a976-13e3-40b4-b4da-ffd3c52fa220)


Dataset pada projek ini diambil dari kaggle, yaitu [Sistem Rekomendasi Wisata](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=tourism_with_id.csv). Pada dataset ini berisi 4 *file* dengan nama `package_tourism`, `tourism_rating`, `tourism_with_id`, dan `user` dengan ekstensi `csv` `(*Comma Separated Values*)`, dengan masing-masing banyaknya data yaitu 100 data dan 7 variabel untuk `package_tourism(package)`, 1000 data dan 3 variabel untuk `tourism_rating(rating)`, 437 data dan 13 variabel untuk `tourism_with_id(location)`, serta 300 data dan 3 variabel untuk `user`.
Berikut adalah penjelasan variabel dari masing-masing dataset:
### package_tourism(package)
Berikut merupakan deskripsi variabel dari dataset `package_tourism(package)`:
- Package: ID unik untuk setiap paket wisata.
- City: Kota di mana tempat wisata berada.
- Place_Tourism1 : Destinasi wisata pertama yang termasuk dalam paket
- Place_Tourism2 : Destinasi wisata kedua yang termasuk dalam paket
- Place_Tourism3 : Destinasi wisata ketiga yang termasuk dalam paket
- Place_Tourism4 : Destinasi wisata keempat yang termasuk dalam paket
- Place_Tourism5 : Destinasi wisata kelima yang termasuk dalam paket
### tourism_rating(rating)
Berikut merupakan deskripsi variabel dari dataset `tourism_rating(rating)`:
- User_Id       : ID unik untuk setiap user.
- Place_Id      : ID unik untuk setiap tempat wisata.
- Place_Ratings : Rating untuk setiap tempat wisata dari user.
### tourism_with_id(location)
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
### user
- User_Id       : ID unik untuk setiap pengguna.
- Location      : Kota atau lokasi asal pengguna.
- Age           : Usia pengguna.
## EDA
Pada tahap ini akan diketahui banyaknya data dan mengecek beberapa kolom di semua dataset tersebut. Pengecekan akan dilakukan terhadap 4 dataset terlebih dahulu.
### package

![2](https://github.com/user-attachments/assets/ba8aedbb-485f-4503-908c-cdd9304e5b78)


![3](https://github.com/user-attachments/assets/bc5bbd71-0687-457d-a472-0b028bd07afc)


Terlihat bahwa dataset package memiliki 100 data dan 7 variabel, dengan ada nya nilai null pada variabel Place_tourism4 dan Place_tourism5. Selain itu, pada dataset ini memiliki 5 data unik untuk variabel City, yaitu Jakarta, Yogyakarta, Bandung, Semarang, Surabaya, dengan banyaknya data di tiap kota adalah 20 paket.
### rating

![4](https://github.com/user-attachments/assets/93dc1a4e-2d5a-4e24-8f51-d83b238f9e12)


![5](https://github.com/user-attachments/assets/db9d93d0-61a0-4302-ae34-ba735ade11cc)


Terlihat bahwa dataset rating memiliki 10000 data dan 3 variabel. Pada dataset ini juga memiliki 300 nilai unik pada variabel User_Id dan 5 nilai unik pada Place_Ratings, dengan nilai 1,2,3,4,5, dengan rating 4 memiliki data paling banyak daripada rating lainnya dengan selisih yang tipis.

### location


![6](https://github.com/user-attachments/assets/8aa5627d-9bf4-402b-9b5e-9720c2c1a24f)


![7](https://github.com/user-attachments/assets/ccf509af-02d4-4f28-a106-a0b4ac85efe5)


Terlihat bahwa dataset location memiliki 437 data dan 13 variabel, dimana merupakan banyak nya data unik dari tempat wisata, dan adanya nilai null pada kolom Time_Minutes dan Unnamed: 11. Pada dataset ini juga memiliki 6 nilai unik pada kolom Category, yaitu Budaya, Taman Hiburan, Cagar Alam, Bahari, Pusat Perbelanjaan, Tempat Ibadah dan Taman hiburan memiliki data paling banyak dibandingkan kategori lain dengan 135 data.

### user


![8](https://github.com/user-attachments/assets/caf937fd-21a0-45dd-9e95-4bdf63999c3a)


![9](https://github.com/user-attachments/assets/1b69ae84-95e4-4926-a4a1-39e5b3cfee86)


![10](https://github.com/user-attachments/assets/c565c7d2-acfb-4c29-9d3b-34970b807dee)


Terlihat bahwa dataset user memiliki 300 data dan 3 variabel, yang merupakan banyaknya nilai unik pada user. Pada dataset ini juga memiliki 28 nilai unik untuk asal daerah user, yaitu kolom Location. Selain itu, dataset user memiliki data di kolom Age, yaitu usia user, dengan rentang 24 sampai dengan 40 tahun. Serta 5 user pemberi rating terbanyak berada di Bekasi, Semarang, Yogyakarta, Lampung, dan Bogor.
# Data Preparation
Pada tahap ini akan dibuat dataframe yang siap untuk EDA lanjutan, *content based filtering* dan *Collaborative Filtering*. Hal ini penting dilakukan karena untuk memastikan data bersih, terhindar dari *error*, dan memastikan model bekerja lebih efektif. 
## Data Preprocessing untuk EDA
Pada tahap ini akan dilakukan langkah-langkah berikut:
1. Mengetahui jumlah *user* dan *location*
2. Mengetahui jumlah rating

Berikut merupakan penjelasan dari masing-masing tahap:
### melihat total user dan location
Pada tahap ini dataset akan dibagi menjadi 2 bagian, yaitu user dan location(tempat wisata). Kemudian gabungkan dataset rating_df dan user_df untuk mengetahui total dari user, gabungkan dataset location_df dan rating_df untuk mengetahui total dari location.

Pada tahap pertama akan dilihat total *user* dari menggabungkan `User_Id` dari tabel *rating_df* dan *user_df*

![11](https://github.com/user-attachments/assets/8240f18d-df27-4410-9158-1fbdcfe1e437)



Terlihat pada gambar, banyaknya *user* yang ada yaitu 300 *user*

Setelah itu, akan dilihat total tempat wisata dari menggabungkan `Place_Id` dari tabel *location_df* dan *rating_df*

![12](https://github.com/user-attachments/assets/0e29745f-ac64-4272-9a91-944942a24b2b)



Terlihat pada gambar, banyaknya tempat wisata yang ada yaitu 437 tempat.
### melihat total rating
Selanjutnya, akan dibuat variabel baru, yaitu place, dengan menggabungkan data rating dan place untuk melihat banyaknya rating dari gabungan data yang ada, pada kasus ini data rating_df dan location_df. Setelah itu, akan dicoba mengecek variabel setelah penggabungan data. Terlihat bahwa variabel memiliki 10000 data rating dari gabungan dataset rating_df dan location_df, serta data ini memiliki nilai null pada kolom time_minutes dan Unnamed: 11. Setelah itu  akan diambil fitur numerik terlebih dahulu, kemudian akan dicari jumlah dari fitur numerik tersebut berdasarkan Place-Id. Berikut adalah hasil dari proses ini, yaitu melihat total rating:

![13](https://github.com/user-attachments/assets/ce7f27aa-15f1-4b6d-a4ab-ed3a63e0e567)


## Data Preprocessing untuk *Content Based Filtering*
Pada tahap ini akan dilakukan langkah-langkah berikut:
1. Membuat dataframe untuk Modeling *Content Based Filtering* 
2. Mengecek nilai null
3. Mengecek nilai duplikat
4. Mengecek deskripsi analisis dan banyaknya data unik
5. Mengecek kembali data untuk *Content Based Filtering*
6. Mengecek nilai unik dari kolom Category
7. Menghapus duplikat pada Place_Id
8. Membuat data dictionary untuk modeling
9. TF-IDF

Berikut merupakan penjelasan dari masing-masing tahap:
### Membuat dataframe untuk Modeling *Content Based Filtering*
Pada tahap ini, kita akan membuat dataframe untuk pembuatan sistem dengan metode *Content Based Filtering*. Langkah pertama, kita akan membuat dataframe bernama `all_place_name` dengan data dari `rating_df`. Setelah itu, kita gabungkan dataframe ini dengan kolom `place_name`, `category`, dan `city` dari tabel *location_df* dengan kunci `Place_Id`. Setelah itu kita akan menggabungkan lagi dengan kolom `age` dari tabel *user_df* dengan kunci `User_Id`. Hasil akhir 4 data pertama dataframe ini yaitu:

![14](https://github.com/user-attachments/assets/553ff0c4-af94-443e-94fe-a36a41dfb571)


### Mengecek nilai null
Pada tahap ini, kita akan mengecek nilai null dari dataset yang telah dibuat tadi, berikut merupakan hasil pengecekan nilai null:

![15](https://github.com/user-attachments/assets/959ec073-a901-4298-ba07-f3d4f9c9e578)


Terlihat bahwa data kita tidak memiliki nilai null, sehingga kita bisa lanjut ke tahap berikutnya. 

### Mengecek data duplikat
Pada tahap ini, kita akan mengecek nilai duplikat dari dataset yang telah dibuat. Berikut merupakan hasil pengecekan nilai null:

![24](https://github.com/user-attachments/assets/2aea2842-1f1d-4cf3-9dbf-850792fe6e39)


Terlihat bahwa data kita tidak memiliki nilai null, sehingga kita perlu untuk menghapus ni[lai duplikat tersebut dengan fungsi `drop_duplicated()`

### Mengecek deskripsi analisis dan banyaknya data unik
Pada tahap ini, kita akan mengecek deskripsi analisis dan kita akan mengecek banyaknya data unik pada kolom Place_Id, Place_Name, dan Location.
Berikut merupakan deskripsi analisis dari data numerik ini:

![16](https://github.com/user-attachments/assets/b2fb733d-830b-43cc-ad6f-1e2f7003a8ae)



Berikut merupakan deskripsi analisis dari data numerik ini:

![17](https://github.com/user-attachments/assets/1cf6958e-973e-4166-a7ad-16e20247ab59)


Berdasarkan data diatas, terlihat bahwa banyaknya data unik pada kolom Place_Id sebanyak 437 data unik, Place_Name sebanyak 437 data unik, dan Location sebanyak 6 data unik. Sehingga dataset sudah siap untuk langkah selanjutnya.
### mengecek kembali data untuk *Content Based Filtering*
Pada tahap ini akan dicek kembali data yang telah dipreprocessing di langkah sebelumnya. Data akan diurutkan terlebih dahulu berdasarkan Place_Id. Berikut adalah 5 data pertama data tersebut:

![18](https://github.com/user-attachments/assets/c5cee268-6fb9-4f5d-811d-4dfdb39dee3e)



### mengecek nilai unik dari kolom Category
Pada tahap ini akan diecek nilai unik dari kolom Category untuk mengecek apakah ada kategori tempat wisata. 

![19](https://github.com/user-attachments/assets/003f995b-a83a-4599-a00e-def9a2734711)


Terlihat bahwa data mempunyai kategori tempat wisata yaitu Budaya, Taman Hiburan, Cagar Alam, Pusat Perbelanjaan, dan Tempat Ibadah.

### Menghapus duplikat pada Place_Id
Pada tahap ini akan dibuat variabel preparation yang berisi data all_place_name. Lalu data akan diurutkan berdasarkan Place_Id. Kemudian  nilai duplikat akan dihapus dari Place_Id karena hanya menggunakan data unik dari data yang ada.
### Membuat data dictionary untuk modeling
Pada tahap ini akan dikonversi data series menjadi list, sehingga akan menggunakan fungsi tolist untuk konversi data. Setelah itu membuat data dictionary untuk data place_id, place_name, dan place_cat(place_category). Lalu akan dicek data yang telah dibuat. Berikut merupakan 5 data pertama untuk modeling. 

![20](https://github.com/user-attachments/assets/c282a5df-07ec-45cc-9f97-79372d1186e7)


Dataframe ini telah siap untuk Langkah selanjutnya. 
### TF-IDF

Metode Term Frequency-Inverse Document Frequency (TF-IDF) adalah salah satu teknik  yang  digunakan  dalam  pengolahan  teks dan 
pemodelan bahasa alami. Tujuan utama dari metode  TF-IDF  adalah  untuk  mengevaluasi seberapa penting suatu kata (term) dalam sebuah 
dokumen dalam konteks koleksi dokumen yang lebih besar. Pada tahap ini, kita akan memanggil fungsi TfidfVectorizer() lalu kita akan 
fit dengan kolom Category. Lalu kita akan melakukan fit transform dan kita akan menggunakan fungsi todense untuk menghasilkan vektor TF-IDF dalam bentuk matrix. Setelah itu, kita buat dataframe hasil dari TF-IDF. Berikut merupakan hasil TF-IDF yang berhasil kita buat:

![21](https://github.com/user-attachments/assets/3c4b7500-0c90-4899-8f5e-79c80b0c8b99)



Bisa terlihat bahwa Museum Perangko memiliki nilai 1 pada kolom budaya, sehingga Museum Perangko termasuk ke dalam 
kategori budaya, dan sebagainya.

## Data Preprocessing untuk *Collaborative Filtering*
Pada tahap ini akan dilakukan langkah-langkah berikut:
1. Membuat dataframe untuk Modeling *Collaborative Filtering* 
2. Acak data
3. Membagi data menjadi data train dan data test

### Membuat dataframe untuk Modeling *Collaborative Filtering*

Pada tahap ini akan dibuat dataframe untuk pembuatan sistem dengan metode *Collaborative Filtering*. Pada tahap pertama dilakukan persiapan data untuk menyandikan (encode) fitur User_Id ke dalam indeks integer. Berikut merupakan hasil encode User_Id:

![26](https://github.com/user-attachments/assets/2e41f7c4-f2c4-41a0-b163-fcc85065928f)


Setelah itu, dilakukan persiapan data untuk menyandikan (encode) fitur Place_Id ke dalam indeks integer. Berikutnya dilakukan pemetaan userID dan placeID ke dataframe yang berkaitan. Setelah itu mengecek beberapa hal dalam data seperti jumlah user, jumlah tempat wisata, dan mengubah nilai rating menjadi float. Berikut merupakan hasil pengecekan banyaknya *user* dan *place*:

![27](https://github.com/user-attachments/assets/6f342526-9328-44cc-8f3c-e9f3a63d57ef)


Terlihat bahwa dataframe memiliki data *user* sebanyak 300 data, data *place* sebanyak 437 data, serta data rating dari 1.0 sampai 5.0.

### Acak data
Pada tahap ini dilakukan acak data supaya distribusinya menjadi random. Acak dataframe dari kolom User_Id dan Place_Id. Berikut adalah hasil 5 data pertama dari acak data:

![28](https://github.com/user-attachments/assets/b7662354-18f0-4d82-aafc-a585a0f1efca)


### Membagi data train dan data validation
Pada tahap ini  bagi data train dan validasi dengan komposisi 80:20. Namun sebelumnya  perlu dipetakan (mapping) data user dan place menjadi satu value terlebih dahulu. Lalu, buatlah rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training.

# Data Modeling
Pada tahap ini akan digunakan metode *Content Based Filtering* dan *Collaborative Filtering* untuk menjawab problem statement dari tahap business understanding
## *Content Based Filtering*
*Content-based filtering* adalah metode yang digunakan dalam sistem rekomendasi dan analisis data yang berfokus pada karakteristik atau konten dari item-item yang ingin direkomendasikan atau dianalisis. Pendekatan ini menggunakan atribut-atribut atau fitur-fitur item untuk menentukan kesamaan antara item yang ada dan preferensi pengguna. Tahapan-tahapan yang akan dilakukan yaitu:

1. *Cosinus Similarity*
   
   *Cosinus Similarity* adalah ukuran kesamaan antara dua vektor bukan nol yang banyak digunakan dalam banyak aplikasi pembelajaran 
   mesin dan analisis data. Sebenarnya, ukuran ini mengukur kosinus sudut antara dua vektor. Hasilnya, sebuah ide diberikan tentang 
   seberapa jauh kedua vektor menunjuk ke arah yang sama terlepas dari besarnya. Pada tahap ini akan dihitung derajat kesamaan 
   (similarity degree) antar tempat wisata dengan teknik *cosinus similarity*. Selanjutnya akan dilihat matriks kesamaan setiap 
   tempat wisata dengan menampilkan nama tempat wisata dalam 5 sampel kolom (axis = 1) dan 10 sampel baris (axis=0). Berikut ini 
   merupakan hasil dari *Cosinus Similarity*:

   ![22](https://github.com/user-attachments/assets/dac23e8d-6de6-46b9-997c-9256a635b86a)



   Pada contohnya, bisa terlihat bahwa Curug Cipanas memiliki angka 1 dengan Bumi Perkemahan Batu Kuda dan Umbul Sidomukti. Ini 
   berarti bahwa Curug Cipanas memiliki kategori yang sama dengan Bumi Perkemahan Batu Kuda dan Umbul Sidomukti.

2. Membuat fungsi rekomendasi dan melihat hasil rekomendasi

   Setelah itu akan dibuat fungsi untuk mendapatkan rekomendasi tempat wisata. Pada fungsi ini  akan dibuat fungsi untuk 
   mendapatkan 5 rekomendasi tempat wisata dengan nama yang kita inputkan nanti. Setelah itu akan dilihat hasil dari rekomendasi 
   yang telah dibuat. Berikut merupakan input untuk rekomendasi.

   ![23](https://github.com/user-attachments/assets/ee88c333-cbb9-44df-8695-d05d9ed0b206)



   Berikut merupakan hasil rekomendasi dari input yang telah dimasukkan:

   ![25](https://github.com/user-attachments/assets/e7b65e82-8352-41a9-b582-710f90dad51f)


   Terlihat bahwa fungsi merekomendasikan tempat wisata dengan category yang sama, yaitu kategori cagar alam.

### Kelebihan dan Kekurangan
   Keuntungan dari content-based filtering adalah kemampuannya untuk memberikan rekomendasi yang personal dan dapat menjelaskan alasan 
   di balik rekomendasi tersebut. Namun, pendekatan ini juga memiliki keterbatasan, seperti kurangnya kemampuan untuk merekomendasikan 
   item yang sangat berbeda dari yang telah disukai oleh pengguna.
   
## *Collaborative Filtering*
Pada teknik *collaborative filtering* memerlukan sekumpulan item yang didasarkan pada pilihan historis pengguna. Sistem ini tidak memerlukan banyak fitur produk untuk bekerja. Penyematan atau vektor fitur mendeskripsikan setiap item dan Pengguna, dan menenggelamkan item dan pengguna di lokasi penyematan serupa. Itu membuat lampiran untuk item dan pengguna sendiri. Tahapan-tahapan yang akan dilakukan yaitu:
1. Training
   
   Pada tahap ini akan dibuat class RecommenderNet dengan keras Model class. Setelah itu akan dilakukan proses compile terhadap model, dengan menggunakan fungsi loss binary crossentropy, optimizer adam, dan matriks RMSE. Setelah itu akan dilakukan training data.

2. Visualisasi Training

   Pada tahap ini akan dilakukan visualisasi proses training, plot metrik evaluasi dengan matplotlib. Berikut merupakan visualisasinya:

   ![29](https://github.com/user-attachments/assets/34e013e6-cf8b-4102-8ebb-7e94608c87e9)



    
3. Rekomendasi
   
   Sebelum melakukan prediksi sistem rekomendasi akan dibuat variabel place_not_visited terlebih dahulu karena daftar place_not_visited inilah yang akan menjadi resto yang direkomendasikan. Selanjutnya akan dilakukan prediksi untuk memperoleh 10 rekomendasi tempat wisata. Berikut ini merupakan hasil 10 rekomendasi wisata berdasarkan rating:

   ![30](https://github.com/user-attachments/assets/d8bf51a0-0975-43e2-af85-5ba7df27a51e)




### Kelebihan dan Kekurangan
Dibandingkan dengan *Content Based Filtering*, *Collaborative Filtering* lebih efektif dalam memberikan rekomendasi baru kepada pengguna. Metode berbasis kolaboratif menarik rekomendasi dari kumpulan pengguna yang memiliki minat yang sama dengan satu pengguna target. Kekurangannya, Masalah cold start mungkin merupakan kelemahan yang paling banyak dikutip dari sistem *Collaborative Filtering*. Hal ini terjadi ketika pengguna baru (atau bahkan item baru) memasuki sistem. Kurangnya riwayat interaksi item pada pengguna tersebut mencegah sistem mengevaluasi kesamaan atau keterkaitan pengguna baru tersebut dengan pengguna yang sudah ada.


# Evaluasi
Pada tahap ini akan diuji seberapa efektifnya suatu model sistem rekomendasi. Pada projek ini akan dievaluasi model *Content Based Filtering* menggunakan *Precision* dan evaluasi model *Collaborative Filtering* menggunakan RMSE.
## Evaluasi model *Content Based Filtering* menggunakan *Precision*

Sebelum membahas ke precision, terlebih dahulu membahas tentang Confusion Matrix. Confusion Matrix adalah pengukuran performa untuk masalah klasifikasi machine learning dimana keluaran dapat berupa dua kelas atau lebih. Confusion Matrix adalah tabel dengan 4 kombinasi berbeda dari nilai prediksi dan nilai aktual. Ada empat istilah yang merupakan representasi hasil proses klasifikasi pada confusion matrix yaitu True Positif, True Negatif, False Positif, dan False Negatif

- True Positive (TP) :
Interpretasi: Prediksi positif dan itu benar.
- True Negative (TN):
Interpretasi: Prediksi negatif dan itu benar.
- False Positive (FP): (Kesalahan Tipe 1)
Interpretasi: Prediksi positif dan itu salah.
- False Negative (FN): (Kesalahan Tipe 2, kesalahan tipe 2 ini sangat berbahaya)
Interpretasi: Prediksi negatif dan itu salah.

Salah satu nilai yang bisa dihitung dengan Confusion Matrix adalah precision. Precision adalah salah satu metrik penting dalam evaluasi sistem pengambilan informasi yang mengukur tingkat ketepatan atau akurasi sistem dalam menemukan dokumen yang relevan dengan kebutuhan pengguna.  Berikut rumus dari precision di sistem rekomendasi:

![31](https://github.com/user-attachments/assets/214489d6-57a7-452e-96ad-4871ed34ce65)


Namun pada sistem rekomendasi, Precision pada K adalah rasio item relevan yang diidentifikasi dengan benar dalam total item yang direkomendasikan dalam daftar sepanjang K. Sederhananya, ini menunjukkan berapa banyak item yang direkomendasikan atau diambil yang benar-benar relevan. Berikut rumus precison di sistem rekomendasi:

![32](https://github.com/user-attachments/assets/efcc7cd7-fc98-4924-9b54-df25942497af)


Dengan menggunakan rumus diatas, akan dicari nilai precision pada sistem rekomendasi *Content Based Filtering*. Tampilkan data input terlebih dahulu:

![23](https://github.com/user-attachments/assets/ff86dce3-735d-4fb3-8bb2-50923e79cb21)



Pada data input digunakan data Kebun Binatang Ragunan dengan Category Cagar Alam. Setelah itu akan ditampilkan hasil 5 rekomendasi yang dihasilkan dari input tersebut:

![25](https://github.com/user-attachments/assets/ffecaf87-f085-474a-a61a-3b50d7dc4928)



Terlihat diatas bahwa 5 rekomendasi yang dihasilkan memiliki category yang sama, yaitu Cagar Alam. Maka, sesuai dengan rumus diatas:

`precision = number of relevant item in K / total number of items in K`
`precision = 5 / 5`
`precision = 1`

Dari 5 rekomendasi di atas didapatkan nilai precision sebesar 1 dari model *Content Based Filtering* yang dikembangkan. Artinya model bekerja dengan sangat baik.

## Evaluasi model *Collaborative Filtering* menggunakan RMSE

Root mean square error (RMSE) adalah simpangan baku residual, atau selisih rata-rata antara nilai proyeksi dan nilai aktual yang dihasilkan oleh model statistik. Mengingat bahwa rumus RMSE pada dasarnya adalah rumus simpangan baku, rumus ini seharusnya dapat dikenali oleh siapa pun yang memiliki pelatihan dalam statistik. Itu masuk akal karena RMSE sama dengan simpangan baku residual. Rumus ini menghitung varians antara nilai yang diamati dan yang diharapkan. Berikut adalah rumus dari RMSE:

![33](https://github.com/user-attachments/assets/9e171645-010d-4e31-beda-a9d6fc99f864)


Dengan: 

- yi adalah nilai aktual dari observasi ke-i.
- ŷi adalah nilai prediksi untuk observasi ke-i.
- P adalah jumlah parameter yang diestimasi, termasuk konstanta.
- N adalah jumlah observasi.

RMSE membantu mengevaluasi model dengan melihat error pada saat training. Berikut merupakan visualisasi training pada projek ini:

![29](https://github.com/user-attachments/assets/5a6ed488-dfcf-4a78-be49-0d63490473c9)



Berdasarkan grafik tersebut, didapatkan bahwa RMSE dari data train adalah 0.3144 dan RMSE dari data validation adalah 0.3661, dimana sistem yang dikembangkan sudah baik untuk model Collaborative Filtering ini.

# Kesimpulan

Projek ini berhasil membuat sistem rekomendasi untuk tempat wisata dengan 2 algoritma sistem rekomendasi, yaitu *Content Based Filtering* dan *Collaborative Filtering*. Pada projek ini, kita berhasil membuat langkah-langkah pengerjaan sistem rekomendasi, seperti Data Understanding, Data Preparation, Modeling, serta evaluasi model. Pada sistem rekomendasi *Content Based Filtering*, hasil evaluasi yang dihasilkan sangat baik, sehingga kita berhasil membangun sistem rekomendasi yang efektif menggunakan informasi deskripsi, kategori, dan fasilitas destinasi. Begitu pula dengan sistem rekomendasi *Collaborative Filtering*, hasil evaluasi yang dihasilkan cukup baik, sehingga kita berhasil membangun sistem rekomendasi yang efisien dan efektif menggunakan rating destinasi wisata. Namun hasil projek ini belum sempurna karena dataset yang terbatas, sehingga bisa saja model merekomendasikan hal yang kurang cocok dengan input tempat wisata. 

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






   



   
















