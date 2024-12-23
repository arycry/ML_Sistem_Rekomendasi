# Sistem Rekomendasi Wisata Indonesia - Dita Ary Crystian

# Domain Projek

Perkembangan teknologi membawa perubahan pesat sehingga semua informasi dapat diakses dengan mudah. Salah satu sektor yang terdampak perkembangan teknologi yaitu sektor pariwisata. Indonesia memiliki potensi pariwisata yang sangat besar, dengan beragam destinasi menarik. Namun, banyaknya pilihan destinasi terkadang membuat wisatawan kesulitan menentukan tempat yang tepat untuk dikunjungi. Oleh karena itu, dibutuhkan sebuah sistem rekomendasi yang dapat membantu wisatawan menemukan destinasi yang sesuai dengan preferensi mereka. Proyek ini bertujuan membangun sistem rekomendasi destinasi wisata di Indonesia menggunakan dataset yang berisi informasi detail mengenai berbagai tempat wisata di Indonesia. 

Referensi: [Jurnal Prediksi rekomendasi wisata](https://ejournal.unama.ac.id/index.php/jurnalmsi/article/download/1262/1071).

# Business Understanding

## Problem Statement

Berdasarkan latar belakang yang dijelaskan di atas, kita mendapatkan rumusan masalah sebagai berikut:
1. Bagaimana sistem dapat merekomendasikan destinasi wisata di Indonesia berdasarkan deskripsi, kategori, dan fasilitas yang tersedia di dataset?
2. Bagaimana sistem dapat menyederhanakan proses pencarian informasi dan memberikan rekomendasi yang relevan secara efisien?

## Goals
Berdasarkan rumusan masalah yang dijelaskan di atas, kita mendapatkan tujuan sebagai berikut:
1. Membangun sistem rekomendasi yang efektif menggunakan informasi deskripsi, kategori, dan fasilitas destinasi.
2. Mengembangkan sistem rekomendasi yang efisien dan efektif dalam memberikan informasi dan rekomendasi destinasi wisata.

## Solution 
Berdasarkan tujuan di atas, ada beberapa solusi yang bisa dilakukan, yaitu:
1. Membuat sistem menggunakan Content-Based Filtering. Metode ini merekomendasikan destinasi yang serupa dengan destinasi yang sebelumnya disukai oleh pengguna, berdasarkan deskripsi dan fitur destinasi tersebut (misalnya, kategori, fasilitas).
2. Membuat sistem menggunakan Collaborative Filtering. Metode ini merekomendasikan destinasi berdasarkan preferensi pengguna lain yang memiliki selera yang mirip. Dalam konteks ini, kita bisa menggunakan user-item interaction untuk memprediksi rating yang mungkin diberikan user ke suatu destinasi.


# Data Understanding
Dataset pada projek ini diambil dari kaggle, yaitu [Sistem Rekomendasi Wisata](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination?select=tourism_with_id.csv). Pada dataset ini berisi 4 *file* dengan nama `package_tourism`, `tourism_rating`, `tourism_with_id`, dan `user` dengan ekstensi `csv` `(*Comma Separated Values*)`.

Berikut merupakan deskripsi variabel dari dataset Sistem rekomendasi wisata:
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/14.jpg" width="75%">
## Univariate EDA
Berikut merupakan variabel-variabel yang ada di dataset sistem rekomendasi wisata:
- Package: ID paket wisata
- City: Kota destinasi wisata
- Place_Tourism1: destinasi paket wisata pertama 
- Place_Tourism2: destinasi paket wisata kedua
- Place_Tourism3: destinasi paket wisata ketiga 
- Place_Tourism4: destinasi paket wisata keempat 
- Place_Tourism5: destinasi paket wisata kelima
- User_Id: ID pengguna/pemberi rating
- Place_Id: ID destinasi wisata
- Place_Ratings: rating destinasi wisata
- Place_Name: nama destinasi wisata
- Description: deskripsi destinasi wisata
- Category: kategori destinasi wisata
- Price: tiket masuk destinasi wisata
- Time_minutes: Waktu tempuh menuju destinasi wisata
- Coordinate: Koordinat dari destinasi wisata
- Long: Longitude
- Lat: Latitute
- Location: Kota dan provinsi destinasi wisata
- Age: Usia pengguna

Selanjutnya, kita membaca untuk beberapa data di atas. 
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/15.png" width="75%">

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/16.png" width="40%">

Dari gambar tersebut, dapat diketahui bahwa:
- Banyaknya tempat wisata yaitu 437 tempat dengan 6 kategori.
- Banyaknya *user* sebanyak 300 orang dengan sebaran 28 kota di Indonesia.

Setelah itu, kita ingin mengetahui berapa interval dari rating.
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/17.png" width="40%">
Sehingga rating pada sistem ini adalah 1-5.

## Data Preprocessing

Pada tahap ini, kita ingin melihat total *user* dari menggabungkan `User_Id` dari tabel *rating_df* dan *user_df*
####visualisasi
Terlihat pada gambar, banyaknya *user* yang ada yaitu 300 *user*

Setelah itu, kita akan melihat total tempat wisata dari menggabungkan `Place_Id` dari tabel *location_df* dan *rating_df*
####visualisasi
Terlihat pada gambar, banyaknya tempat wisata yang ada yaitu 437 tempat.

Setelah itu, kita akan membuat dataframe baru, yaitu `place` dengan menggabungkan *location_df* dan *rating_df* dengan kunci yaitu `Place_Id`. Kita akan mengecek missing value dan jumlah rating dari dataframe yang baru kita buat. 
####visualisasi
####visualisasi

Setelah itu, kita akan membuat dataframe untuk pembuatan sistem dengan metode *Content Based Filtering*. Langkah pertama, kita akan membuat dataframe bernama `all_place_name` dengan data dari `rating_df`. Setelah itu, kita gabungkan dataframe ini dengan kolom `place_name`, `category`, dan `city` dari tabel *location_df* dengan kunci `Place_Id`. Setelah itu kita akan menggabungkan lagi dengan kolom `age` dari tabel *user_df* dengan kunci `User_Id`. Hasil akhir 4 data pertama dataframe ini yaitu:

####visualisasi

## Data Preparation

Pada tahap ini, kita akan mengecek nilai null, menghapus data duplikat, dan membuat dataframe yang siap untuk *content based filtering*. Hal ini penting dilakukan karena untuk memastikan data bersih, terhindar dari *error*, dan memastikan model bekerja lebih efektif. 

Lebih detail, kita akan mengecek nilai null, deskriptif analisis untuk data numerik dan mengecek banyaknya data dari kolom `Place_Id`,`Place_Name`, dan `Category` di dataframe yang telah kita buat sebelumnya.

####visualisasi

Karena data sudah bersih, kita akan melakukan persiapan data. kita akan menghapus data duplikat di kolom `Place_Id`. Setelah itu, kita mengecek banyaknya data setelah drop duplikat. 

Lalu, kita membuat dataframe `place_new`, yang terdiri dari kolom `place_id` yang diubah menjadi 'id', `place_name` yang diubah menjadi 'name', dan `place_cat` yang diubah menjadi 'category'.

Dataframe ini telah siap untuk dibuat sistem dengan model *content based filtering*. 

# Modeling
## *Content *







## Missing Value
Jika dilihat dari gambar deskripsi variabel, terlihat ada beberapa kolom yang memiliki data kurang dari kolom `name` sampai `owner`. Sehingga akan dilakukan penghapusan missing value sehingga dataset terbebas dari missing value.

```sh
car_df = car_df.dropna()
```

## Duplicate Data
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/2.png" width="50%">
Terlihat di gambar bahwa dataset memiliki 1189 data duplikat, sehingga kita perlu menghapus data duplikat tersebut.

```sh
car_df = car_df.drop_duplicates()
```

## Change data type and column name
Terlihat di deskripsi dataset bahwa pada kolom `max power` perlu kita ubah tipe data nya dari `object` menjadi `float` karena nilai `max power` yang memiliki nilai desimal pada dataset. 

```sh
car_df['max_power'] = car_df['max_power'].astype('float')

```
Setelah itu, kita mengubah nama kolom `mileage(km/ltr/kg)` menjadi `mileage` supaya lebih mudah dalam proses data preparation. 

```sh
car_df.rename(columns={'mileage(km/ltr/kg)':'mileage'}, inplace = True)
```

## Outliers
Outlier dapat didefenisikan sebagai amatan yang menyimpang sedemikian jauh dari pengamatan lainnya. Adanya data outlier ini dapat mempunyai efek bagi pengambilan suatu kesimpulan atau keputusan pada penelitian. Oleh karena itu,  kita perlu menghapus outlier supaya tidak merusak hasil analisis data. Pada tahap ini, kita akan melakukan visualisasi  outlier menggunakan `Boxplot` dengan metode IQR(*Interquartile range*). 

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/3.jpg" width="75%">

Pada metode IQR, kita perlu mencari nilai IQR dengan
$IQR = Q3 - Q1$.
Setelah itu, kita mencari batas bawah dan batas atas dengan 

$Batas Bawah = Q1 - 1.5*IQR$ 

dan

$Batas Atas = Q3 + 1.5*IQR$.

Setelah itu, kita akan menghapus data di luar rentang Batas Atas dan Batas bawah. 

## Univariate Analysis
Univariate Analysis melibatkan pemeriksaan satu variabel pada satu waktu untuk meringkas dan menemukan pola. Pada proses ini, data dibagi menjadi 2 bagian, yaitu `number features` dan `categorical features`. Lalu akan ditunjukkan visualisasi menggunakan `barplot` dari kedua *features* tersebut. 

### Categorical Features

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/4.jpg" width="90%">

Dari Gambar diatas, kita bisa mengetahui bahwa:
- Mobil terbanyak yang tersedia yaitu Maruti Swift Dzire VDI dengan 118 data.
- Mobil dengan bahan bakar Petrol dan Diesel mendominasi data dengan masing-masing berjumlah 2848 dan 2458 data.
- Mobil dengan tipe penjual mandiri memiliki data paling banyak, yaitu 4877 data.
- Mobil dengan transmisi manual memiliki data paling banyak, yaitu 5099 data.
- Mobil dengan penjual tangan pertama memiliki data paling banya, yaitu 3404 data.
- Mobil yang memiliki 5 kursi memiliki data paling banyak, yaitu 4906 data.

### Numenical Features

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/5.png" width="90%"> 
Dari gambar diatas, kita bisa mengetahui bahwa:

- Mobil paling banyak dijual yaitu mobil tahun penjualan 2017.
- Kebanyakan mobil bekas yang dijual telah digunakan sepanjang 2500 sampai 12500 km.
- Kebanyakan mobil bekas yang dijual menempuh jarah 15-25 km per liter bahan bakarnya.
- Kebanyakan mobil bekas yang dijual memiliki mesin sebesar 1200 cc.

## Multivariate Analysis
Multivariate Analysis mengeksplorasi hubungan antara dua variabel atau lebih secara bersamaan. Pada proses ini, data dibagi menjadi 2 bagian, yaitu `number features` dan `categorical features`. Lalu akan ditunjukkan visualisasi menggunakan `catplot` pada *categorical features* dan `pairplot` dari *numerical features*.

### Categorical Features

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/6.jpg" width="90%">

### Numercial Features

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/7.png" width="90%">

## Correlation Matrix

Matriks korelasi adalah sebuah matriks yang menunjukkan koefisien korelasi antar variabel. Jika nilai dari matriks mendekati -1, maka korelasi negatif antar variabel semakin kuat. Jika nilai dari matriks mendekati , maka korelasi antar variabel semakin minim. Jika nilai dari matriks mendekati 1, maka korelasi positif antar variabel semakin kuat.

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/8.png" width="75%">

# Data Preparation
Data Preparation merupakan tahap transformasi data kita. Data preparation penting dilakukan supaya data kita bisa melakukan modeling data dengan baik. Berikut merupakan tahap Data Preparation:
1. Encoding fitur kategori

Pada tahap ini, kita menggunakan 2 metode untuk encoding, yaitu Target Encoder pada kolom `name` dan Label Encoder pada kolom kategori lainnya. Target encoder dipilih pada kolom `name` karena Encoder ini mengurangi dimensionalitas dan mempertahankan hubungan antara fitur kategoris dan variabel target. Terget Encoder membutuhkan kolom y(`selling price`) untuk menghitung rata-rata target per kategori. Proses yang dilakukan yaitu mengubah isi kolom `selling price` terlebih dahulu ke bentuk logaritma nya karena  target dari kolom y memiliki nilai yang cukup besar, sehingga berimbas ke Target Encoding yang tidak efektif. Setelah itu dilakukan proses Target Encoding. Setelah itu, kolom `selling price log` akan dihapus.
Setelah itu dilakukan proses Label Encoding. Label Encoding dipilih karena lebih efisien dalam memori dan komputasi. Label Encoding dilakukan di kolom kategori selain `name`.  
```sh
car_df['selling_price_log'] = np.log1p(car_df['selling_price'])
car_df['name']= target_encoder.fit_transform(car_df[['name']], car_df['selling_price_log'])
```
```sh
car_df['fuel']= label_encoder.fit_transform(car_df['fuel'])
```
2. Train Test Split

Train test split adalah proses membagi data menjadi data latih dan data uji. Pada proses ini, kita membagi data dengan rasio 80:20. Kemudian didapat hasil pembagian data latih dan data uji.
```sh
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.2, random_state = 123)
```
Hasil dari train test split adalahe seperti dibawah

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/9.png" width="40%">

3. Standarisasi pada kolom numerik

Standarisasi fitur numerik memiliki tujuan untuk memastikan bahwa semua fitur berkontribusi secara proporsional terhadap model. Standarisasi dilakukan dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi. StandardScaler menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. 
Hasil dari Standarisasi sebagai berikut

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/10.png" width="40%">

# Modeling
Modeling adalah tahapan di mana kita menggunakan algoritma machine learning untuk menjawab problem statement dari tahap business understanding. Ada 3 algoritma machine learning yang akan digunakan dalam projek ini, yaitu:
1. Random Forest Regressor

Random Forest merupakan teknik pembelajaran ensemble yang fleksibel dan canggih yang khususnya berguna untuk masalah regresi. Selama fase pelatihan, ia membangun sejumlah besar pohon keputusan dan menghasilkan prediksi rata-rata dari setiap pohon individu. Random Forest merupakan pilihan yang menarik untuk banyak aplikasi dunia nyata karena ia tahan terhadap gangguan dan outlier, mengelola kumpulan data berdimensi tinggi secara efektif, dan menghasilkan estimasi relevansi fitur. Random Forest beroperasi dengan membangun beberapa pohon keputusan selama pelatihan dan menghasilkan prediksi rata-rata (regresi) dari pohon individu. Prinsip yang mendasarinya melibatkan pembuatan serangkaian pohon yang beragam dan menggabungkan prediksi mereka untuk meningkatkan akurasi dan ketahanan secara keseluruhan. Adapun kelebihan dari Random Forest sebagai berikut:
- Akurasi Tinggi
- Ketahanan terhadap Noise
- Menaksir Pentingnya Fitur
- Menangani Data yang Hilang dan Outlier
- Menangani Data Numerik dan Kategoris

Sedangkan kekurangan dari Random Forest sebagai berikut:
- Kompleksitas Komputasi
- Penggunaan Memori yang lebih banyak
- Waktu Prediksi yang lebih lama
- Dapat mengalami Overfitting

berikut kode untuk model Random Forest Regressor

```sh
rf = RandomForestRegressor(n_estimators=100, random_state=123)
```

2. XGBoost

XGBoost, atau *Extreme Gradient Boosting* adalah algoritma pembelajaran mesin yang populer dan canggih yang termasuk dalam kategori teknik peningkatan gradien. Algoritma ini banyak digunakan untuk tugas klasifikasi dan regresi. XGBoost menyempurnakan pendekatan peningkatan gradien tradisional dengan menggabungkan berbagai teknik pengoptimalan dan regularisasi, sehingga menghasilkan peningkatan akurasi dan efisiensi. XGBoost menggabungkan prediksi beberapa algoritma tradisional, biasanya pohon keputusan, untuk membuat model prediktif yang kuat. Intuisi di balik XGBoost melibatkan pengoptimalan melalui penurunan gradien dan peningkatan. Berikut Kelebihan XGBoost:
- Akurasi Tinggi
- Penanganan data Nonlinier
- Penanganan Data yang Hilang
- Pemrosesan Paralel
- XGBoost dioptimalkan untuk performa dan penggunaan memori
 
Berikut kekurangan XGBoost:
- Kompleksitas
- Risiko Overfitting

berikut kode untuk model XGBoost:

```sh
xgb_r = xgb.XGBRegressor(objective ='reg:squarederror', random_state=123)
```

3. Gradient Boosting

Gradien Boosting adalah teknik pembelajaran mesin yang digunakan untuk tugas regresi dan klasifikasi. Teknik ini membangun model secara berurutan, setiap model mencoba memperbaiki kesalahan model sebelumnya. Tidak seperti algoritme lain yang berfokus pada satu model tunggal, Peningkatan Gradien menggabungkan beberapa model tradisional (biasanya pohon keputusan) untuk membentuk model prediktif yang kuat. Gradient Boosting bekerja dengan inisialisasi model dengan prediksi sederhana terlebih dahulu, lalu hitung residual untuk setiap titik data dengan menemukan perbedaan antara nilai aktual dan prediksi. Setelah itu, pasangkan model tradisional (biasanya pohon keputusan) ke residual ini. Lalu perbarui prediksi dengan menambahkan prediksi model baru, yang diskalakan berdasarkan laju pembelajaran, ke prediksi yang ada. Ulangi langkah 2–4 untuk sejumlah iterasi yang ditetapkan atau hingga residual diminimalkan secara memadai. Berikut kelebihan Gradient Boosting:
- Akurasi Tinggi
- Fleksibel
- Dapat menangani data non linear

Berikut kekurangan Gradient Boosting
- Gradient Boosting memakan banyak waktu pelatihan
- Dapat Overfitting
- Memerlukan penyetelan(Tuning)

berikut kode untuk model Gradient Boosting:

```sh
gbr = GradientBoostingRegressor(n_estimators=200, learning_rate=0.1, random_state=123)
```

Setelah dilakukan modeling, maka dilakukan evaluasi model mana yang memiliki kinerja paling baik. 

# Evaluasi 

Pada tahap ini, kita akan menguji seberapa efektifnya suatu model dan membandingkan 3 model mana yang memiliki kinerja paling baik. Sebelum melakukan evaluasi, fitur numerik pada data uji harus distandarisasi terlebih dahulu. supaya didapat mean = 0 dan standar deviasi = 1.  Pada tahap evaluasi ini, kita akan menggunakan MSE(*Mean Square Error*). MAE mencari selisih kuadrat antara nilai aktual dan nilai prediksi. Semakin kecil nilai MAE, maka semakin bagus juga modelnya. Berikut formula dari MSE

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/rumus.jpeg" width="40%">

dengan $N$ adalah jumlah dataset, $y_i$ adalah nilai sebenarnya, $y_{\text{pred}}$ adalah nilai prediksi. Setelah dicoba proses evaluasi, berikut adalah hasil dari evaluasi antara 3 model:

<img src="https://github.com/arycry/GambarMLTerapan/blob/main/11.png" width="40%">
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/12.png" width="60%">

Bisa terlihat bahwa

- Random Forest Regressor memiliki error di data latih paling kecil, dengan nilai 767694.8, dengan error pada data uji sebesar 5178709.2
- XGBoost memiliki error di data uji paling kecil 4972300.3, dengan error di data latih sebesar 1122749.5
- Gradient Boosting memiliki error paling besar dari kedua algoritma lain, baik di data latih maupun data uji, dengan masing-masing nilai 4029683.6 dan 5366731.6, sehingga model ini kurang efektif dengan dataset ini.

Selanjutnya, kita akan melihat beberapa prediksi model dari data actualnya. 
<img src="https://github.com/arycry/GambarMLTerapan/blob/main/13.png" width="60%">

Bisa dilihat bahwa prediksi dari XGBoost lebih akurat daripada Random Forest Regressor karena hasil prediksi XGBoost lebih mendekati nilai data aktual. 
Sehingga bisa disimpulkan bahwa model yang cocok dengan projek prediksi penjualan harga mobil bekas ini adalah model XGBoost karena memiliki error yang lebih rendah dan nilai prediksi yang mendekati nilai sebenarnya.

---

# Referensi
- Pardomuan Robinson Sihombing, Suryadiningrat, Deden Achmad Sunarjo, Yoshep Paulus, Apri Caraka Yuda, "Identifikasi Data Outlier (Pencilan) dan Kenormalan Data Pada Data Univariat serta Alternatif Penyelesaiannya", BPS-Statistics Indonesia, 2022, Retrieved from: https://jurnaljesi.com/index.php/jurnaljesi/article/view/112
- NORTH DAKOTA STATE UNIVERSITY, "MULTIVARIATE ANALYSES", Retrieved from: https://www.ndsu.edu/faculty/horsley/Introduction_and_describing_variables.pdf
- w3schools, "Data Science - Statistics Correlation Matrix", Retrieved from: https://www.w3schools.com/datascience/ds_stat_correlation_matrix.asp
- geeksforgeeks, "What are the Advantages and Disadvantages of Random Forest?", 2024, Retrieved from: https://www.geeksforgeeks.org/what-are-the-advantages-and-disadvantages-of-random-forest/
- Ambika, "XGBoost Algorithm in Machine Learning", 2023, Retrieved from: https://medium.com/@ambika199820/xgboost-algorithm-in-machine-learning-2391edb101ce
- Piyush Kashyap, "A Comprehensive Guide to Gradient Boosting and Regression in Machine Learning: Step-by-Step Intuition and Example", 2024, Retrieved From: https://medium.com/@piyushkashyap045/a-comprehensive-guide-to-gradient-boosting-and-regression-in-machine-learning-step-by-step-faa17fbd0e2c#:~:text=Pros%20and%20Cons%20of%20Gradient%20Boosting,-Pros%3A&text=High%20accuracy%3A%20Often%20outperforms%20other,Boosting%20can%20model%20complex%20relationships.
- Raghav Agrawal, "Know The Best Evaluation Metrics for Your Regression Model !", 2024, Retrieved from: https://www.analyticsvidhya.com/blog/2021/05/know-the-best-evaluation-metrics-for-your-regression-model/#h-mean-squared-error-mse



