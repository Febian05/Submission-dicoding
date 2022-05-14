# Laporan Proyek Machine Learning - Eko Febian Wijaksana
## Domain Proyek

Domain proyek yang dipilih dalam proyek _machine learning_ ini adalah mengenai Penjualan mobil bekas dengan judul proyek _"Cars used price Predictive Analytics"_.

### Latar Belakang
  
Mobil bekas adalah mobil yang dijual belikan setelah digunakan oleh orang lain atau mobil yang bukan baru atapun merupakan mobil yang telah digunakan sebagai simulasi pada calon pembeli atau yang lebih dikenal sebagai test drive. Harga mobil bekas di pasaran sendiri bukan hahnya bergantung pada merek brand tertentu namun faktor lain yang paling krusial adalah seberapa lama mobil itu digunakan. Hal tersebut diketahui dengan berapa kali mobil tersebut diperjual belikan ke pembeli berikutnya sehingga dapat diketahui dengan melihat seberapa besar angka kilo meter pada dashborad mobil. Fitur lain seperti jenis transmisi, bahan bakar juga mempengaruhi besar kecilnya harga penjualan mobil bekas. Dalam proses transaksi mobil bekas juga bisa membuat harga semakin mahal atau murah, Semakin tempat pembelian mobil itu terpercaya maka harga mobil juga mahal berbeda jika membeli mobil bekas dengan melakukan transaksi antar individu yang akan menjual mobilnya sendiri. Di masa yang akan datang perkembangan mobil keluaran baru terus mengalami peningkatn dan tentunya jumlah mobil bekas yang dijual di pasaran akan semakin banyak. Tentu hal tersebut bisa menjadi alternatif bagi calon pembeli mobil yang ingin mendapatkan mobil dengan harga yang lebih murah ketimbang beli yang baru.

Berdasarkan permasalahan di atas, maka pada proyek ini akan dibangun suatu model _machine learning_ untuk memprediksi harga pasar mobil bekas dengan berbagai pertimbangan sperti yang telah disebutkan di atas. Dengan adanya model machine learning ini, di harapkan dapat membantu dan memudahkan calon pembeli mobil untuk memberikan estimasi harga yang perlu disiapkan sebelum mebeli mobil bekas dengan berbagai pertimbangan informasi fitur mobil tersebut dan juga riwayat penggunaan mobil tersebut.


## Business Understanding

### Problem Statements
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

-   Bagaimana cara melakukan pra-pemrosesan data pada informasi harga mobil bekas dan juga fitur pendukungnya hingga didapatkan model yang baik?
-   Bagaimana cara membangun model prediksi _machine learning_ dengan menerapkan beberapa model sehingga dapat dipertimbangan salah satu model yang paling baik?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:

-   Melakukan pra-pemrosesan data informasi harga mobil bekas supaya dapat diproses ke dalam  model.
-   Membangun beberapa model perdiksi _machine learning_ untuk memprediksi harga mobil bekas dengan pertimbangan beberapa fitur pada data.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini di antaranya:

- **Pra-pemrosesan Data**. Pada pra-pemrosesan data dapat dilakukan beberapa tahapan, antara lain:
  
    -   Melakukan visualisasi pada data
    -   Mengatasi data outlier dengan Metode IQR.
    -   Melakukan split dataset.
    -   Encoding Fitur Kategori
    -   Mencari korelasi yang kuat antara fitur dan target.
    -   Melakukan standardisasi data fitur numerik pada dataset.
  
- **Pembangunan Model**. Pada pembangunan model terdapat beberapa algoritma yang digunakan, antara lain:
  - **K-Nearest Neighbor** 
  - **Random Forest**
  - **Boosting Algorithm**
  
- **Evaluasi Model**. Metrik yang digunakan untuk evaluasi model yaitu:
   - **MSE atau Mean Squared Error**
    
## Data Understanding
- **Informasi Dataset**
  <br> Dataset yang digunakan pada proyek ini yaitu informasi harga mobil bekas **Vehicle dataset**, informasi lebih lanjut mengenai dataset tersebut dapat lihat pada tabel berikut:

  | Jenis                   | Keterangan                                                                              |
  | ----------------------- | --------------------------------------------------------------------------------------- |
  | Sumber                  | Dataset: [Kaggle](https://www.kaggle.com/datasets/nehalbirla/vehicle-dataset-from-cardekho) |
  | Dataset Owner           | NEHAL BIRLA                                                                           |
  | Lisensi                 | (DbCL) v1.0                                                                        |
  | Kategori                | Automobiles and Vechiles                                                                   |
  | Usability               | 10.00                                                                                      |
  | Jenis dan Ukuran Berkas | CSV (354.64 kB)                                                                           |

  Setelah melakukan observasi pada dataset yang diunduh melalui _link_ Kaggle yaitu `coin_Bitcoin.csv`, didapatkan informasi sebagai berikut :
  
  - Terdapat  4340 baris yang berisi informasi mengenai informasi harga mobil bekas, fitur dan riwayat pembelian.
  - Terdapat 8 kolom yaitu `name, year, selling_price, km_driven, fuel, seller_type, transmission`, Volume dan `owner`
  - Dari kolom-kolom tersebut terdapat 3 kolom numerik dengan tipe data int64, yaitu `year, selling_price` dan `km_driven
  - Terdapat 5 kolom dengan tipe object yaitu `name, fuel, seller_type, transmission`, dan `owner`
  - Tidak terdapat _missing value_ pada dataset. 

- **Distribusi Data pada Setiap Fitur**
  <br>Pada kasus ini yang perlu diperhatikan adalah menganalisa apakah terdapat outlier pada data kemudian jika ya maka harus diatasi. Tujuannya adalah untuk menghindari distorsi pada data
  <br> Berikut ini merupakan visualisasi distribusi data pada tiap-tiap fitur numerik (`year, km_driven`) :
  
  - Mengidentifikasi Outlier pada data
    <br>
   ![outlier](https://user-images.githubusercontent.com/61940572/168427644-900d6cb5-f496-4bce-9b89-34b25ef745f2.PNG)
    <br> pada visualisasi di atas nilai outlier dapat dilihat sebagai titik-titik di luar batas minimum dan maksimum. Untuk mengatasi permasalahan ini kama penulis menggunakan metode IQR dengan tujuan untuk menyaring data-data yang ada pada rentang batas bawah - batas atas sehingga outlier yang berada di luar batas bawah - batas atas tidak disertakan.
    
  - Univariate Analysis
    <br>
   ![Capture22](https://user-images.githubusercontent.com/61940572/168427808-b7cd6e4c-a49f-49a6-a20e-b821803ea167.PNG)
    <br> Terlihat pada grafik bahwa semua data cenderung distribusi nilainya miring ke kanan (right-skewed). Hal ini akan berimplikasi pada model nantinya.
     -  Mobil bekas yang paling banyak dijual yaitu mobil pada keluaran tahun 2018,2016, 2012. Kemudian yang paling sedikit yaitu mobil keluaran 2020 dan 2004.
     -  Peningkatan harga mobil bekas sebanding dengan jumlah mobil yang ada walaupun terdapat kenaikan sedikit.
     -  Mobil bekas yang dijual paling banyak yaitu mobil yang sudah dipakai dengan kilometer 50000.
  - Multivariate Analysis
    <br>
    ![image6](https://user-images.githubusercontent.com/61940572/168428022-409285c8-b018-4a3e-bc1d-51bc463a43fb.png)
    <br>
    Untuk memahami data lebih lanjut dapat dilihat pada grafik matriks korelasi di bawah ini:
    ![image 7](https://user-images.githubusercontent.com/61940572/168428164-246031eb-9445-49cd-b59e-286d080eeab5.png)
    <br> Dari visualisasi di atas dapat disimpulkan bahwa Pada grafik korelasi matrix di atas antara fitur (year dan km_driven) terhadap target (selling_price) terlihat bahwa tidak terdapat nilai korelasi yang mendekati 0 terhadap target. Nilai korelasi antara fitur year terhadap selling_price yaitu 0.63, dan fitur km_driven terhadap selling_price yaitu -0.28. Jadi tidak perlu ada yang didrop.
  
## Data Preparation
Berikut ini merupakan tahapan-tahapan dalam melakukan pra-pemrosesan data:

  - **Melakukan Penanganan Missing Value dan Outlier**
    <br> Dengan menggunakan interquartil, nilai pencilan yang melebihi nilai Quartil 1 (Q1) akan diubah menjadi nilai Q1. Sementara itu, nilai pencilan yang kurang dari nilai Quartil 3 (Q3) akan diubah nilainya menjadi nilai Q3. kemudian membuat variabel batas atas dan batas bawah karena outlier berada diluar jangkauan itu. Kemudian yang terakhir menyaring data-data yang ada pada rentang batas bawah - batas atas sehingga outlier yang berada di luar batas bawah - batas atas tidak disertakan.

  - **Melakukan pembagian dataset**
    <br> Untuk mengetahui kinerja model ketika dihadapkan pada data yang belum pernah dilihat sebelumnya, maka perlu dilakukan pembagian dataset. Pada proyek ini Pada proses split dataset yaitu menggunakan proporsi 0.2 engan fungsi train_test_split dari sklearn. Split dataset menjadi data train dan data test sebelum transformasi dilakukan supaya transformasi diterapkan hanya pada data latih.
    
 - **Encoding Fitur Kategori**
   <br> Karena data yang bisa diproses oleh model adalah data berupa angka maka perlu melakukan proses one-hot encoding yaitu merubahnya menjadi numerik dengan memanfaatkan library Library scikit-learn.
    
  - **Standardisasi data pada semua fitur numerik pada dataset**
  <br> StandardScaler yaitu proses standarisasi fitur dengan mengurangkan mean (nilai rata-rata) kemudian membaginya dengan standar deviasi untuk menggeser distribusi. Kemudian menghasilkan distribusi dengan standar deviasi sama dengan 1 dan mean sama dengan 0. Untuk pertama kali yang akan dilakukan standarisasi yaitu pada data latih, Tujuannya adalah menghindari kebocoran informasi pada data uji.
  
## Modeling
Pada proyek ini, Proses modeling dalam proyek ini menggunakan 3 algoritma _machine learning_ yaitu `K-Nearest Neighbor`, `Random Forest` dan `Boosting Algorithm` kemudian membandingkan performanya.

- **K-Nearest Neighbor**
  <br> cara kerja algoritma KNN yaitu memprediksi nilai dari setiap data yang baru menggunakan pendekatan "kesamaan fitur". Dengan kata lain, setiap data baru diberi nilai berdasarkan seberapa mirip titik tersebut dalam set pelatihan.

- **Random Forest**
  <br> Algoritma ini disusun dari banyak algoritma pohon (decision tree) yang pembagian data dan fiturnya dipilih secara acak. Random forest merupakan model prediksi yang terdiri dari beberapa model dan bekerja secara bersama-sama. 

- **Boosting Algorithm**
  <br> Boosting Algorithm yaitu model bekerja dengan membangun model dari data latih kemudian ia membuat model kedua yang bertugas memperbaiki kesalahan dari model pertama. Model ditambahkan sampai data latih terprediksi dengan baik atau telah mencapai jumlah maksimum model untuk ditambahkan
 
 
## Evaluation
Pada proyek ini, metrik evaluasi yang digunakan untuk mengukur kinerja model yaitu menggunakan metrik **MSE**. 
<br> Berikut ini perbandingan grafik metrik MSE pada ketiga model:
<br> 
![evaluasi1](https://user-images.githubusercontent.com/61940572/168428554-3eca0d1a-c5f7-473f-b9be-e1b0e2520eb2.png)
<br>Berdasarkan gambar di atas, terlihat model Random Boosting Algorithm memberikan nilai eror yang paling kecil. Dan model dengan Random Forest juga memiliki eror tidak jauh berbeda namun berpotensi mengalami over fitting. Sedangkan model KNN memiliki nilai error yang paling besar.

Hasil pengujian ketiga model yang telah dibuat 
<br> 
![evaluasi2](https://user-images.githubusercontent.com/61940572/168428846-6cbaff19-0c02-4500-9c1c-2b20ac9acd2d.PNG)
<br> Hasil prediksi yang paling mendekati nilai asli yaitu dengan menggunakan algoritma Bossting.
