# Customer Segmentation : Airlines Customer

## About the project
Dalam proyek ini, saya melakukan segmentasi pelanggan (customer segmentation) sebuah perusahaan penerbangan. Segmentasi pelanggan adalah praktik memisahkan pelanggan kedalam kelompok-kelompok yang memiliki kesamaan diantara pelanggan disetiap cluster. Saya akan membagi pelanggan menjadi beberapa segmen menggunakan algoritma K-Means Clustering berdasarkan RFM (Recency, Frequency, and Monetary). 

## Business Understanding
* Problem : Maskapai penerbangan 'X' ingin mengetahui bagaimana daya tanggap pelanggan agar dapat merencanakan strategi campaign yang sesuai dengan habit para pelanggan. Namun pihak maskapai kesulitan untuk merencanakan strategi campaign karena habit pelanggan mereka yang beragam
* Goals : Strategi campaign yang tepat sasaran, sesuai dengan habit pelanggan
* Objective : Segmentasi pelanggan (customer segmentation)
* Business Metrics : Segmentasi pelanggan

## Data Understanding
Dataset terdiri berbagai detail informasi dari 62.988 pelanggan maskapai penerbangan ‘X’. Detail tersebut adalah :
* member_no : ID Member
* ffp_date : Frequent Flyer Program Join Date 
* first_flight_date : Tanggal Penerbangan pertama
* gender : Jenis kelamin
* ffp_tier : Tier dari Frequent Flyer Program
* work_city : Kota asal
* work_province : Provinsi asal
* work_country : Negara asal
* age : Umur customer
* load_time : Tanggal data diambil
* flight_count : Jumlah penerbangan customer
* bp_sum : Rencana perjalanan
* sum_yr_1 : Fare revenue
* sum_yr_2 : Votes prices
* seg_km_sum : Total jarak (km) penerbangan yang sudah dilakukan
* last_flight_date : Tanggal penerbangan terakhir
* last_to_end : Jarak waktu penerbangan terakhir ke pesanan penerbangan paling akhir
* avg_interval : Rata-rata jarak waktu
* max_interval : Maksimal jarak waktu
* exchange_count :Jumlah penukaran
* avg_discount : Rata-rata diskon yang didapat customer
* points_sum : Jumlah poin yang didapat customer
point_notflight : Poin yang tidak digunakan oleh members

Sumber dataset : https://www.kaggle.com/c/sa-customer-segmentation/data 

## Data Insights
Insight yang digali dilakukan berdasarkan Recency, Frequency, dan Monetary (RFM). Analisis RFM (Recency, Frequency, Monetary) adalah model pemasaran yang terbukti untuk segmentasi pelanggan berbasis perilaku. Ini mengelompokkan pelanggan berdasarkan riwayat transaksi mereka – seberapa baru, seberapa sering, dan berapa banyak yang mereka beli. RFM membantu membagi pelanggan ke dalam berbagai kategori atau kelompok untuk mengidentifikasi pelanggan yang lebih mungkin merespons promosi dan juga untuk layanan personalisasi di masa mendatang.
Untuk menganalisis RFM dalam proyek ini, dibutuhkan beberapa detail dari setiap pelanggan seperti Recency (R) yaitu kapan terakhir kali pelanggan menggunakan layanan maskapai, 
Frequency (F) yaitu frekuensi pelanggan menggunakan layanan maskapai, dan Monetary (M) yaitu total jarak yang ditempuh pelanggan.

RFM yang berhasil digali dari dataset project ini adalah :
* Monetary dan Frequency memiliki korelasi positif yang kuat (0.85). Artinya semakin besar variabel Monetary maka semakin besar pula variabel Frequency. Sementara itu, Frequency dan Recency memiliki korelasi negatif yang kecil (-0.4), demikian pula dengan Monetary dan Recency yang juga memiliki korelasi negatif yang kecil (-0.37). Artinya tidak terlalu berhubungan antara besar variabel Frequency dan Monetary terhadap besar variabel Recency.
* Recency : Jarak waktu penerbangan terakhir ke pesanan penerbangan paling akhir pelanggan yang paling singkat adalah 1 hari dan paling panjang adalah 73. Kemudian median (titik tengah data yang terletak pada 50% dari keseluruhan data) adalah 108 hari, nilai quartil atas 268, nilai quartil bawah 29, dan jangkauan interquartilnya adalah 239.
* Frequency : Jumlah penerbangan paling sedikit adalah 2, dan jumlah penerbangan paling banyak yang terjadi pada penumpang adalah 213. Kemudian, nilai mediannya adalah 7, nilai quartil atas 15, quartil bawah 3, dan jangkauan interquartilenya adalah 12.
* Monetary (Gambar 4): Jarak paling singkat adalah 368 km, dan paling panjang adalah 580717 km. Lalu, nilai mediannya adalah 9994, quartil atas 21271.25, quartil bawah 4747, dan jangkauan interquartilenya adalah 16524.25.

## Data Cleaning dan Pre-Processing 
* Menghapus null value
* Merubah tipe data object kedalam tipe datatime menggunakan to_datetime
* Mengurangi outlier berdasarkan nilai IQR
* Standarisasi data yang digunakan untuk modeling

## Modeling
Algoritma yang digunakan untuk mensegmentasi pelanggan dalam proyek ini adalah K-Means Clustering. K-Means Clustering adalah algoritma Unsupervised Learning, yang mengelompokkan dataset yang tidak berlabel ke dalam cluster yang berbeda. Cara kerja algoritma ini mula-mula adalah dengan membentuk sejumlah k titik, yang disebut dengan centroid (dimana nilai k merepresentasikan jumlah cluster). Kemudian titik-titik data (data points) yang ada akan membentuk cluster dengan centroid terdekat darinya. Otomatis, titik pusat (centroid) akan berubah seiring dengan pertambahan anggota tiap cluster-nya (yang mana adalah datapoints tadi). Oleh karena itu, tiap-tiap cluster yang telah terbentuk akan ‘mencari’ titik centroid barunya. Proses ini terus menerus dilakukan hingga diperoleh kondisi konvergensi, contohnya jika posisi centroid sudah tidak berubah.

Sementara itu, untuk menentukan jumlah cluster paling optimal dapat ditentukan dengan Elbow Method. Elbow Method merupakan salah satu metode paling populer yang digunakan untuk mencari jumlah cluster paling optimal. Elbow method ini bisa dilakukan menggunakan distorsi atau inersia. Distorsi merupakan rata-rata jarak kuadrat dari pusat cluster dari masing-masing cluster. Sedangkan inersia merupakan jumlah kuadrat jarak sampel ke pusat cluster terdekat mereka. Keduanya menggunakan metrik jarak Euclidean.
Untuk menentukan jumlah cluster yang optimal, kita harus memilih nilai k pada “elbow” yaitu titik dimana distorsi atau inersia mulai menurun secara linier.
Bedasarkan analisa elbow method, jumlah cluster paling optimal dalam kasus data ini adalah 4.

## Model Insights
* Cluster yang paling banyak memiliki pelanggan adalah cluster 1, sedangkan cluster dengan jumlah pelanggan paling sedikit adalah cluster 0.
* Distribusi recency setiap cluster : Pelanggan di cluster 0, 1, dan 2 memiliki nilai recency yang sedikit. Artinya mereka baru-baru ini menggunakan layanan maskapai. Pelanggan yang memiliki rata-rata recency paling sedikit adalah cluster 0, diikuti oleh cluster 2, kemudian cluster 1. Sementara itu, cluster 3 merupakan pelanggan dengan recency yang tinggi. Dengan kata lain, mereka sudah lama tidak menggunakan layanan maskapai ini. Selain itu, pada cluster 0, 1, dan 2 terdapat beberapa pelanggan yang memiliki nilai recency extrem yang jauh dari nilai umumnya pada masing-masing cluster.
* Distribusi frekuensi setiap cluster : Cluster 0 memiliki rata-rata frekuensi paling tinggi dibandingkan cluster lainnya. Cluster 1 dan cluster 3 memiliki rata-rata frekuensi yang tidak berbeda jauh satu sama lain. Sedangkan Cluster 2 memiliki rata-rata frekuensi dibawah cluster 0 dan diatas cluster 1 dan 3. Selain itu, pada cluster 1, 2, dan 3 terdapat beberapa pelanggan yang memiliki nilai frekuensi extrem jika dibandingkan nilai-nilai umum yang ada pada setiap cluster mereka.
* Distribusi monetary setiap cluster : Cluster 0 memiliki nilai rata-rata monetary paling tinggi dibandingkan cluster lainnya, namun terdapat beberapa pelanggan yang memiliki nilai monetary extrem yang jauh dari nilai umum di cluster tersebut. Sementara itu, cluster 2 memiliki rata-rata jauh dibawah cluster 0 namun lebih tinggi dibandingkan cluster 1 dan 3, selain itu, terdapat beberapa pelanggan yang memiliki nilai monetary yang extrem tinggi dan ada pula beberapa pelanggan yang memiliki nilai monetary extrem yang rendah dibandingkan nilai umum pada cluster 2. Rata-rata monetary pada cluster 1 dan 3 tidak berbeda jauh, namun pada cluster 3 terdapat beberapa pelanggan yang memiliki nilai monetary extrem yang tinggi.

## Customer Segment Profile
Kluster yang terbentuk berdasarkan hasil model adalah :
* Champions : Profil untuk cluster 0 yang berisi pelanggan dengan detail informasi : (R) Baru, (M) Banyak, (F) Tinggi
* Promising : Profil untuk cluster 1 yang berisi pelanggan dengan detail informasi : (R) Baru, (M) Sedikit, (F) Rendah
* Potential Loyalist : Profil untuk cluster 2 yang berisi pelanggan dengan detail informasi: (R) Baru, (M) Sedang, (F) Sedang
* Hibernating : Profil untuk cluster 3 yang berisi pelanggan dengan detail informasi : (R) Lama, (M) Sedikit, (F) Rendah

## Actionable Tip
Berikut adalah strategi campaign untuk masing-masing profil pelanggan :
* Champions : Hadiahi pelanggan dicluster ini karena telah menjadi pelanggan utama dan supaya mereka tetap menjadi pelanggan utama dimasa yang akan datang. Jika ada produk atau layanan baru, kelompok ini dapat menjadi pengadopsi awal. Cluster ini juga bisa menjadi orang-orang yang akan mempromosikan layanan penerbangan maskapai 'X' secara tidak langsung kepada orang lain.
* Promising : Cluster ini merupakan cluster yang paling banyak jumlah pelanggannya, oleh karena itu penting untuk memberikan perhatian lebih kepada mereka supaya mereka dapat terus menjadi pelanggan di maskapai ini. Oleh karena itu, penting untuk membangun Brand Awareness untuk pelanggan di cluster ini. Contoh brand awareness yang bisa diterapkan bisa dengan memberikan free trials layanan dengan batas waktu tertentu.
* Potential Loyalist : Pelanggan dicluster ini dapat diberikan treatment berupa penawaran membership/loyalty program dengan berbagai benefit. Diharapkan dengan diberikan treatment tersebut bisa meningkatkan nilai RFM mereka.
* Hibernating : Untuk menarik pelanggan dicluster ini supaya kembali menggunakan layanan maskapai, salah satu caranya adalah dengan memberikan diskon khusus.
