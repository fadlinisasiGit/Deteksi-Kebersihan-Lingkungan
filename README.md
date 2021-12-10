# Laporan Proyek Machine Learning - Muhammad Fadli Ramadhan

## Project Overview

Domain proyek yang saya pilih dalam proyek Machine Learning Sistem Rekomendasi ini adalah mengenai Tempat Kuliner dengan judul "Recommend top restaurants based on preference".

Menurut [Wikipedia](https://id.wikipedia.org/wiki/Rumah_makan), **Rumah makan** atau **restoran** adalah istilah umum untuk menyebut usaha gastronomi yang menyajikan hidangan kepada masyarakat dan menyediakan tempat untuk menikmati hidangan tersebut serta menetapkan tarif tertentu untuk makanan dan pelayanannya. Meski pada umumnya rumah makan menyajikan makanan di tempat, tetapi ada juga beberapa yang menyediakan layanan take-out dining dan delivery service sebagai salah satu bentuk pelayanan kepada konsumennya. Rumah makan biasanya memiliki spesialisasi dalam jenis makanan yang dihidangkannya. Sebagai contoh yaitu rumah makan chinese food, rumah makan Padang, rumah makan cepat saji (fast food restaurant) dan sebagainya. Di Indonesia, rumah makan juga biasa disebut dengan istilah restoran. Restoran merupakan kata resapan yang berasal dari bahasa Prancis yang diadaptasi oleh bahasa inggris; "restaurant" yang berasal dari kata "restaurer" yang berarti "memulihkan"

[Sistem Rekomendasi](https://en.wikipedia.org/wiki/Recommender_system)  adalah subkelas sistem penyaringan informasi yang berupaya memprediksi "peringkat" atau "preferensi" yang akan diberikan pengguna pada suatu item.
Sistem pemberi rekomendasi digunakan di berbagai bidang, dengan contoh yang umum dikenal berupa generator daftar putar untuk layanan video dan musik, pemberi rekomendasi produk untuk toko online, atau pemberi rekomendasi konten untuk platform media sosial dan pemberi rekomendasi konten web terbuka.

Proyek ini penting untuk diselesaikan agar Pelanggan atau User mendapatkan rekomendasi restoran dengan penilaian terbaik dan memberikan banyak pilihan untuk memilih restoran dengan ID yang tersedia. Dari pihak restoran, sistem pemberi rekomendasi ini sangat penting untuk mengingkatkan kualitas restoran dan meningkatkan jumlah pelanggan.


## Business Understanding

### Problem Statements

Sebagai data analyst, anda ingin memanfaatkan data tersebut untuk meningkatkan kualitas layanan dan rating perusahaan. Namun, anda memiliki rincian masalah berikut :
- Bagaimana membuat model machine learning untuk merekomendasikan ID restoran berdasarkan rating/penilaian tertinggi User ?
- Bagaimana cara membuat model Machine Learning untuk merekomendasikan ID restoran lain yang mungkin disukai dan belum pernah dikunjungi oleh user?

### Goals

Berdasarkan rincian masalah diatas, berikut adalah tujuan proyek ini:
- Membuat model Machine learning yang dapat merekomendasikan ID restoran berdasarkan penilaian tertinggi user dengan teknik *Popularity based Recomender Model* agar mendapatkan rekomendasi ID restoran dengan popularitas tertinggi.
- Membuat model Machine Learning untuk merekomendasikan ID restoran lain yang mungkin disukai dan belum pernah dikunjungi oleh user dengan teknik Collaborative Filtering : SDV.

### Solution statements

Untuk menyelesaikan masalah ini, saya mengajukan 2 solusi approach (algoritma atau pendekatan sistem rekomendasi). yaitu teknik Popularity based Recommender Model
Collaborative Filtering Model. Berikut adalah penjelasan teknik-teknik yang akan digunakan untuk masalah ini :
- **Popularity based Recommender Model :** Seperti namanya, ini merekomendasikan berdasarkan apa yang sedang tren/populer di seluruh situs. Ini sangat berguna ketika Anda tidak memiliki data masa lalu sebagai referensi untuk merekomendasikan produk kepada pengguna. Ini tidak cocok untuk kelompok penonton atau film tertentu.
- **Collaborative Filtering :** Pada tahap ini, sistem merekomendasikan sejumlah restoran berdasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna, kita akan mengidentifikasi restoran-restoran yang mirip dan belum pernah dikunjungi oleh pengguna untuk direkomendasikan. Teknik ini menggunakan model based collaborative filtering : SVD (Singular Value Decomposition)

## Data Understanding
![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/DataUnderstanding1.png?raw=true)

Dataset ini digunakan untuk studi di mana tugasnya adalah menghasilkan daftar restoran teratas sesuai dengan preferensi konsumen dan menemukan fitur yang signifikan.
Sumber Dataset : [Kaggle Dataset : Recommend top restaurants based on preference](https://www.kaggle.com/uciml/restaurant-data-with-consumer-ratings)

Di dalam dataset ini terdapat 9 file csv dan 1 file readme. Untuk keperluan proyek saya ini, saya hanya menggunakan 1 file csv saja. Yaitu rating_final.csv yang memiliki 5 fitur.
**rating_final.csv**
- Instansces : 1161
- Attributes : 5
- `userID`  Nominal, merupakan ID Pengguna yang memberikan penilaian 
- `placeID` Nominal, merupakan ID Restoran yang akan dinilai 
- `rating`  Numeric 0 - 2, merupakan penilaian restoran menurut user 
- `food_rating`  Numeric 0 - 2, merupakan penilaian makanan restoran menurut user
- `service_rating`  Numeric 0 - 2, merupakan penilaian pelayanan restoran menurut user

Kami menggunakan dataset 'rating_final' untuk merekomendasikan restoran berdasarkan popularitas & berdasarkan Collaborative yaitu peringkat yang diberikan oleh pengguna lain.

Saya juga melakukan eksplorasi data untuk memahami variabel pada data serta korelasi antar variabel,dsb.
**rating_final.csv**
![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/2.png?raw=true)

Berdasarkan output diatas, diketahui bahwa file rating_final.csv memiliki 1161 entri.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/3.png?raw=true)

Berdasarkan output di atas, disimpulkan bahwa nilai maksimum dan minimum untuk seluruh rating adalah 2 dan 0. 

Untuk memahami dataset secara detail, penting untuk melakukan EDA, seperti pada langkah berikut :
* Jumlah pengguna unik, restoran unik, no. rating, food_ratings, service_ratings
* Berapa kali pengguna menilai
* Berapa kali restoran dinilai
* Bagaimana distribusi peringkat untuk makanan, layanan

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/4.png?raw=true)

Berdasarkan output diatas, terlihat bahwa ada sekitar 138 user unik, 130 restaurant unik, Rating yang diberikan sebanyak 1161, rating makanan yang diberikan sebanyak 1161, dan rating layanan yang diberikan sebanyak 1161 kali.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/5.png?raw=true)

Berdasarkan output diatas, terlihat bahwa user U1061 memberikan rating sebanyak 18 kali, user U1106 memberikan rating sebanyak 18 kali, hingga user U1138 memberikan rating sebanyak 3 kali.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/6.png?raw=true)

Berdasarkan output diatas, merupakan banyak ID restoran yang dirating. Untuk ID restoran 135085 dinilai sebanyak 36 kali, ID restoran 132825 dinilai sebanyak 32 kali, hingga ID Restoran 135011 dinilai sebanyak 3 kali. Data ini berguna untuk Modeling teknik Popularity based Recommender Model.

Saya juga membuat visualisai data untuk menampilkan banyaknya data untuk fitur rating, food_rating, dan service_rating.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/7.png?raw=true)

Pada visualisasi data diatas terlihat bahwa banyaknya rating 2 yang diberikan oleh user sebanyak kurang lebih 500 kali, rating 1 sebanyak lebih kurang 400 kali, dan rating 0 lebih kurang 250 kali sehingga bila di totalkan hasilnya adalah 1161 data entri.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/8.png?raw=true)

Pada visualisasi data diatas terlihat bahwa banyaknya rating 2 yang diberikan oleh user sebanyak lebih kurang 500 kali, rating 1 sebanyak kurang lebih 400 kali, dan rating 0 lebih kurang 300 kali sehingga bila di totalkan hasilnya adalah 1161 data entri.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/9.png?raw=true)

Pada visualisasi data diatas terlihat bahwa banyaknya rating 2 yang diberikan oleh user sebanyak lebih kurang 400 kali, rating 1 sebanyak lebih kurang 400 kali, dan rating 0 lebih kurang 300 kali sehingga bila di totalkan hasilnya adalah 1161 data entri.

**Dengan EDA ini, kita dapat menyimpulkan :**
- Semua 130 restoran dinilai minimal 3 kali dalam skala 0 hingga 2
- Semua 138 pengguna telah memberi peringkat minimal 3 kali
- Untuk distribusi rating, pengguna cukup puas dengan restoran karena tidak signifikan. pengguna telah memberi peringkat 1,2

Jumlah no. dari peringkat adalah 1161, namun jika masing-masing pengguna akan menilai semua restoran itu akan menjadi total 138 * 130 = 17940 peringkat

Untuk model sistem rekomendasi untuk merekomendasikan restoran pilihan teratas, kita harus meminta setiap pengguna memberi peringkat semua restoran. Karena ini tidak mungkin, kami harus memprediksi peringkat yang akan diberikan pengguna ke restoran.


## Data Preparation

Untuk data preparation, saya menggunakan beberapa teknik yang diperlukan dalam tahapan data preparation, yaitu :

- Mengubah bentuk data menjadi bentuk matriks : hal ini diperlukan untuk mempermudah model colab dalam teknik modeling Collaborative filtering : SVD. Untuk mengubah bentuk data menjadi bentuk matriks, jalankan perintah .pivot()
- Mengatasi missing values : missing value ini adalah hilangnya beberapa data yang telah diperoleh dalam arti data yang tidak berguna dan harus di hilangkan. Untuk memeriksa missing values, ketik perintah berikut. sal.isnull().sum()



## Modeling

Untuk tahap modeling ini, saya akan menggunakan teknik sederhana dari content based recommendation yaitu popularity based, dan teknik Singular Value Decomposition untuk Model Collaborative filtering

- **Popularity based Recommender Model :** Seperti namanya, ini merekomendasikan berdasarkan apa yang sedang tren/populer di seluruh situs. Teknik ini sangat cocok untuk merekomendasikan suatu produk berdasarkan rating tertinggi agar pelanggan lebih mudah dalam menilai suatu produk. Hasil dari teknik ini adalah pemeringkatan dari nilai rating restoran tertinggi  sehingga menandakan bahwa restoran tersebut sangat populer. Dari pemeringkatan ini bisa jadi rekomendasi pelanggan untuk memilih restoran sesuai ID. Karena ini adalah rekomendasi berdasarkan popularitas, ini tidak dipersonalisasi sehingga rekomendasi tetap sama untuk semua pengguna.

Kelebihan dari teknik ini, seperti sangat berguna ketika Anda tidak memiliki data masa lalu sebagai referensi untuk merekomendasikan produk kepada pengguna. 
Kekurangan dari teknik ini, seperti tidak cocok untuk kelompok penonton atau film tertentu, lalu tidak cocok untuk dataset yang besar dan kotor.

Hal yang harus dilakukan menggunakan teknik ini adalah:

- Jumlah pengguna yang telah memberi peringkat resto
- Beri peringkat berdasarkan skor
- Rekomendasikan tempat paling populer

Pada teknik ini menggunakan cara yang sederhana yaitu mengelompokkan fitur, meng-agregatkan banyaknya data, lalu mereset index. Setelah itu memilah nilai agregat dan fitur yanng dikelompokkan. 

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/13.png?raw=true)

Berdasarkan output diatas, terlihat bahwa fitur yang akan digunakan yaitu placeID dan userID. Fitur score merupakan count dari userID yang berarti banyaknya user memilih placeID atau ID restoran.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/14.png?raw=true)

Setelah itu, saya buatkan sistem pemeringkatan dari yang terbesar hingga seterusnya. Pemeringkatan tersebut seperti pada output diatas. 

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/15.png?raw=true)

Dari output diatas dapat disimpulkan bahwa ID Restoran yang mendapat peringkat 1 dengan nilai atau penilaian dari user yaitu ID restoran 135085 dengan nilai 36 dari para user, dsb. Sistem telah merekomendasikan restoran terpopuler berdasarkan preferensi user.

- **Collaborative Filtering :** Pada tahap ini, sistem merekomendasikan sejumlah restoran berdasarkan rating yang telah diberikan sebelumnya. Dari data rating pengguna, kita akan mengidentifikasi restoran-restoran yang mirip dan belum pernah dikunjungi oleh pengguna untuk direkomendasikan. Teknik ini menggunakan model based collaborative filtering : SVD (Singular Value Decomposition) 

 Algoritma SVD digunakan untuk mendekomposis matrik yang bertujuan agar meningkatkan scalability dari sistem.
Algoritma SVD dapat dikolaborasikan dengan algoritma item-based untuk menghasilkan prediksi dan algoritma SVD menghasilkan nilai prediksi dengan nilai error yang lebih kecil dibanding dengan algoritma plain item-based.

Hal yang harus dilakukan dengan menggunakan teknik ini adalah :
- Ubah data menjadi tabel pivot 
- Buat kolom user_index untuk menghitung no. pengguna -> Ubah konvensi penamaan pengguna dengan menggunakan penghitung
- Terapkan metode SVD pada matriks sparse besar -> Untuk memprediksi peringkat untuk semua resto yang tidak diberi peringkat oleh pengguna
- Prediksi peringkat untuk semua restoran yang tidak dinilai oleh pengguna menggunakan SVD
- Bungkus semuanya menjadi sebuah fungsi

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/16.png?raw=true)

Kita mengubah data yang kita pakai menjadi bentuk pivot table, karena format ini dibutuhkan untuk model colab.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/17.png?raw=true)

Selanjutnya adalah buat kolom user_index untuk menghitung no. pengguna. Ubah konvensi penamaan pengguna dengan menggunakan penghitung.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/18.png?raw=true)

Output diatas adalah tampilan data yang telah berbentuk pivot table.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/19.png?raw=true)

Setelah itu menerapkan metode SVD pada matrikse sparse besar, ini digunakan untuk memprediksi peringkat untuk semua resto yang tidak diberi peringkat oleh pengguna. Output diatas adalah hasil penerapan SVD dengan 3 parameter, yaitu matriks ortogonal, nilai tunggal dan transpose dari matriks ortogonal.

Perhatikan bahwa untuk matriks sparse, Anda dapat menggunakan fungsi sparse.linalg.svds() untuk melakukan dekomposisi. SVD berguna dalam banyak tugas, seperti kompresi data, pengurangan kebisingan mirip dengan Analisis Komponen Utama dan Pengindeksan Semantik Laten (LSI), digunakan dalam pengambilan dokumen dan kesamaan kata dalam penambangan teks.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/20.png?raw=true)

Selanjutnya memprediksi peringkat untuk semua restoran yang tidak dinilai oleh pengguna menggunaakn SVD, hasil dari prediksi rating terlihat di output diatas.

Selanjutnya adalah membungkuskan semua menjadi fungsi.
Hal yang harus dilakukan adalah :
- Buat fungsi untuk merekomendasikan tempat dengan peringkat prediksi tertinggi
- Gunakan fungsi untuk merekomendasikan tempat berdasarkan ID pengguna, peringkat sebelumnya, peringkat yang diprediksi, dan jumlah tempat yang direkomendasikan.

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/21.png?raw=true)

Seperti pada output diatas, terlihat bahwa ada 10 ID tempat restoran yang direkomendasikan untuk pelanggan atau user id 26. Sistem akan merekomendasikan ID restoran pada user dengan prediksi yang telah diperhitungkan sehingga pelanggan telah mendapatkan 10 rekomendasi tempat restoran.


## Evaluation
Pada tahap ini, saya menggunakan metrik evaluasi Akurasi, Presisi, dan RMSE (Root Mean Squared Error) yang dihitung menggunakan perhitungan matematis.

- `Akurasi` adalah salah satu metrik untuk mengevaluasi model klasifikasi. Secara informal, akurasi adalah sebagian kecil dari prediksi model kami yang benar. Secara formal, akurasi memiliki definisi sebagai berikut:

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20accuracy.png?raw=true)

Untuk klasifikasi biner, akurasi juga dapat dihitung dalam hal positif dan negatif sebagai berikut:

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20akurasi.png?raw=true)

Dimana TP = Positif Benar, TN = Negatif Benar, FP = Positif Palsu, dan FN = Negatif Palsu.

Dalam proyek ini, pada model Popularity Based Recommender System, nilai akurasi menggunakan data dari variabel data_sort['score']. Berikut adalah nilai metrik evaluasi akurasi pada model popularity based recommender system :

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/hasil%20akurasi.png?raw=true)


- `Presisi` adalah rasio prediksi benar positif dibandingkan dengan keseluruhan hasil yang diprediksi positf. 

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20precision.png?raw=true)

Berikut adalah nilai metrik evaluasi presisi pada model popularity based recommender system :


![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/hasil%20presisi.png?raw=true)


- ` root-mean-square deviation (RMSD) atau root-mean-square error (RMSE) ` adalah aturan penilaian kuadrat yang juga mengukur besarnya rata-rata kesalahan. Sama seperti MAE, semakin rendahnya nilai root mean square error juga menandakan semakin baik model tersebut dalam melakukan prediksi. RMSE adalah aturan penilaian kuadrat yang juga mengukur besarnya rata-rata kesalahan. Sama seperti MAE, semakin rendahnya nilai root mean square error juga menandakan semakin baik model tersebut dalam melakukan prediksi.

Rumus RMSE :

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20rmse.png?raw=true)


![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/nilai%20RMSE%20svd.png?raw=true)

Nilai RMSE SVD model diatas merupakan hasil perhitungan dari 
<code> RMSE = round((((rmse_data.Avg_actual_rating - rmse_data.Avg_predicted_ratings) ** 2).mean() ** 0.5),5) </code>

 Berikut adalah hasil visualisasi rate error rmse pada variabel rmse_data :
 
![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/plot%20rmse%201.png?raw=true)
 
![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/plot%20rmse%202.png?raw=true)
 
## Conclusion
Sistem pemberi rekomendasi berbasis popularitas tidak dipersonalisasi dan rekomendasi didasarkan pada jumlah frekuensi, yang mungkin tidak sesuai untuk pengguna. Model berbasis popularitas akan merekomendasikan 5 tempat yang sama untuk semua pengguna tetapi model berbasis Collaborative Filtering telah merekomendasikan seluruh daftar yang berbeda berdasarkan peringkat pengguna.

Collaborative Filtering Berbasis Model adalah sistem rekomendasi yang dipersonalisasi, rekomendasi didasarkan pada perilaku / interaksi pengguna di masa lalu dan tidak bergantung pada informasi tambahan apa pun. Dalam hal ini kami memiliki peringkat yang menunjukkan interaksi.
  
**---Ini adalah bagian akhir laporan---**
