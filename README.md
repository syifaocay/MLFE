# Laporan Proyek Machine Learning - Ahmad Syifaul Umam
## Domain Proyek

Dalam proyek _machine learning_ ini domain yang saya pilih adalah mengenai keuangan (_cryptocurrency_) dengan judul  _"Etherium Price Predictive Analytics"_.

### Dataset
https://www.kaggle.com/datasets/sudalairajkumar/cryptocurrencypricehistory?select=coin_Ethereum.csv

### Latar Belakang
  
  Dalam beberapa tahun ini anda pasti sudah sering mendengar perihal cryptocurrency bukan? Secara sederhana, cryptocurrency ialah sebuah mata uang digital. Cryptocurrency tidak tersedia dalam bentuk fisik seperti koin atau uang tunai yang digunakan secara umum di seluruh dunia. Dalam cryptocurrency, seluruhnya benar-benar virtual. Meskipun demikian, uang digital tersebut memiliki nilai yang cukup tinggi.
  
  Cryptocurrency dapat disimpan dalam ‘dompet digital’ yang tersedia dalam telepon genggam atau perangkat komputer lainnya. Selain itu, pemilik cryptocurrency juga dapat menggunakan mata uang digital untuk keperluan transaksi jual-beli.
  
  salah satu mata uang kripto yang pupuler adalah Etherium (ETH), Ethereum adalah platform perangkat lunak terdesentralisasi yang memungkinkan Smart Contracts and Distributed Applications (DApps) dibangun dan dijalankan tanpa waktu henti (downtime), penipuan, kontrol, atau gangguan dari pihak ketiga. Definisi ini tercantum dalam buku Ekonomi dan Bisnis Digital.
  
  Mengutip Dasar Investasi dan Trading Cryptocurrency, Ethereum sendiri membangun sebuah jaringan blockchain yang berfokus pada koin Ethereum. Para developer koin bisa membuat koinnya masing-masing di atas jaringan Ethereum.
  
  karena populernya koin Etherium dalam dunia Cryptocurrency Tersebut juga banyak orang yang mempertimbangkan dan menganalisa untuk membeli koin tersebut, maka dengan adanya model machine learning ini diharapkan bisa membantu memudahkan analisa serta dapat mengambil keputusan yang tepat agar bisa bermanfaat bagi banyak orang dimasa depan, aamiin.


## Business Understanding

### Problem Statements
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

-   Bagaimana cara membangun model _machine learning_ untuk memprediksi data harga Etherium di masa mendatang?
-   bagaimana cara membuat pra pemrosesan data?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:
-   membuat pra pemrosesan data
-   Membangun model _machine learning_ untuk memprediksi data harga di masa mendatang dengan tingkat akurasi > 70%.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini di antaranya:

- **Pra-pemrosesan Data**. Pada pra-pemrosesan data dapat dilakukan beberapa tahapan, antara lain:
  
    -   Melakukan perhitungan rerata berdasarkan data _Open, Close, High dan Low_.
    -   Melakukan pembagian dataset.
    -   Mengatasi data pencilan (_outliers_) dengan Metode IQR.
    -   Standardisasi data fitur numerik pada dataset.
  
- **Pembangunan Model**. Pada pembangunan model terdapat beberapa algoritma yang digunakan, antara lain:
  - **K-Nearest Neighbor** 
  - **Random Forest**
  - **Boosting Algorithm**
    
## Data Understanding
- **Informasi Dataset**
  Dataset yang digunakan pada proyek ini yaitu dataset lengkap dengan riwayat harga Etherium yang saya temukan di kaggle dengan lik dihalaman atas laporan ini.

  Setelah melakukan observasi pada dataset yang diunduh melalui _link_ Kaggle yaitu `coin_Etherium.csv`, didapatkan informasi sebagai berikut :
  
  - Terdapat  2160 baris (_records_ atau jumlah pengamatan) yang berisi informasi mengenai data riwayat harga Etherium.
  - Terdapat 10 kolom yaitu `SNo, Name, Symbol, Date, High, Low, Open, Close, Volume, Marketcap` yang merupakan variabel - variabel pada data
  - Dari kolom-kolom tersebut terdapat 6 kolom numerik dengan tipe data float64, yaitu `High, Low, Open, Close, Volume, Marketcap` dan terdapat 1 kolom numerik dengan tipe data int64 yaitu `SNo` yang merupakan fitur numerik. 
  - Terdapat 2 kolom dengan tipe object yaitu `Name, Symbol`
  - Tidak terdapat _missing value_ pada dataset. 
  
  Untuk penjelasan mengenai variabel-variabel pada dataset dapat dilihat pada poin-poin berikut ini:

    *   Date : Tanggal pencatatan data
    *   Open : harga ketika dibuka yang dihitung perhari
    *   Close : harga ketika ditutup yang dihitung perhari
    *   Low : harga terendah perhari
    *   High : harga tertinggi perhari
    *   Volume : volume transaksi perhari
    *   Market Cap : Kapitalisasi Pasar berdasarkan USD

- **Sebaran atau Distribusi Data pada Setiap Fitur**
  <br> sebelum masuk ke tahap distribusi data, persiapan yang dilakukan yaitu perlu membuat dua variabel baru yaitu variabel OHLC_Average untuk menampung rata-rata harga dan Price_After_Month untuk harga setelah sebulan.
  <br> Berikut merupakan visualisasi data yang menunjukkan sebaran/distribusi data pada setiap fitur-fitur numerik (`High, Low, Open, Close, OHLC_Average, Price_After_Month`) :
  
  - Mengidentifikasi Missing Value dan Outlier
    <br>
    <image src='https://raw.githubusercontent.com/AzharRizky/Predictive-Anlaytics/main/images/boxplot_outlier.png' width= 500/>
    <br> Terlihat jika di atas banyak terdapat outlier pada setiap variabel, lalu untuk mengatasinya nantinya penulis akan menerapkan batas bawah dan batas atas menggunakan metode IQR
    
  - Univariate Analysis
    <br>
    <image src='https://raw.githubusercontent.com/AzharRizky/Predictive-Anlaytics/main/images/distribusi_data(right-skewed).png' width= 500/>
    <br> Terlihat pada grafik bahwa semua data cenderung distribusi nilainya miring ke kanan (right-skewed). Hal ini akan berimplikasi pada model nantinya.
    
  - Multivariate Analysis
    <br>
    <image src='https://raw.githubusercontent.com/AzharRizky/Predictive-Anlaytics/main/images/korelasi_antar_variabel.png' width= 500/>
    <br> Terlihat bahwa pada grafik kebanyakan bernilai positif karena kebanyakan grafik pada sumbu y dan x mengalami peningkatan yang cukup signifikan membentuk sebuah garis lurus.
    
    <br>
    <image src='https://raw.githubusercontent.com/AzharRizky/Predictive-Anlaytics/main/images/corelation_matrix.png' width= 500/>
    <br> Terlihat pada matriks korelasi di atas dapat disimpulkan bahwa semua variabel memiliki keterikatan dan korelasi yang kuat antar variabel lainnya, dimana nilai korelasi antar variabel bernilai lebih dari 0.9 atau mendekati 1.
  
## Data Preparation
Berikut ini merupakan tahapan-tahapan dalam melakukan pra-pemrosesan data:
  - **Melakukan Penanganan Missing Value dan Outlier**
    <br> Penanganan yang penulis lakukan pada Missing Value yaitu dengan melakukan drop data, tetapi karena dataset yang digunakan cukup bersih, missing value hanya terdapat pada variabel yang penulis buat pada model untuk membandingkan harga setelah perbulan (Price_After_Month) sebanyak 30 missing value. Dan untuk mengatasi outlier pada proyek, penulis menggunakan penentuan batas atas dan bawah nilai kuartil pada data dengan menggunakan metode IQR.

  - **Melakukan pembagian dataset**
    <br> Membagi dataset menjadi data latih (train) dan data uji (test) merupakan hal yang harus kita lakukan sebelum membuat model. Kita perlu mempertahankan sebagian data yang ada untuk menguji seberapa baik generalisasi model terhadap data baru. Ketahuilah bahwa setiap transformasi yang kita lakukan pada data juga merupakan bagian dari model. Karena data uji (test set) berperan sebagai data baru, kita perlu melakukan semua proses transformasi dalam data latih. Inilah alasan mengapa langkah awal adalah membagi dataset sebelum melakukan transformasi apa pun [25]. Tujuannya adalah agar kita tidak mengotori data uji dengan informasi yang kita dapat dari data latih. Pada proyek ini dataset dibagi menjadi data latih dan data uji dengan rasio 80% untuk data latih dan 20% untuk data uji.
    
  - **Standardisasi data pada semua fitur numerik pada dataset**
  <br> Standardisasi adalah teknik transformasi yang paling umum digunakan dalam tahap persiapan pemodelan. Untuk fitur numerik, kita tidak akan melakukan transformasi dengan one-hot-encoding seperti pada fitur kategori. Kita akan menggunakan teknik StandarScaler dari library Scikitlearn,
  
## Modeling
Pada proyek ini, Proses modeling dalam proyek ini menggunakan 3 algoritma _machine learning_ yaitu `K-Nearest Neighbor`, `Random Forest` dan `Boosting Algorithm` kemudian membandingkan performanya.

