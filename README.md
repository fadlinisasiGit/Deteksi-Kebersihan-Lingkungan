# Laporan Proyek Machine Learning - Sistem Deteksi Kebersihan Lingkungan (Capstone Project)

## Project Overview

Semakin hari semakin berkurangnya kesadaran manusia akan kebersihan. Hal ini ditandai dengan banyaknya tempat berisi tumpukan sampah yang membuat lingkungan tidak enak dilihat. Sudah seharusnya masyarakat memiliki kesadaran untuk membersihkan lingkungan sekitarnya. Maka dari itu, dengan memanfaatkan machine learning kami membuat mesin pendeteksi kebersihan lingkungan dengan mengidentifikasi gambar masukan guna mengingatkan masyarakat pentingnya menjaga kebersihan lingkungan sekitar. 
Dalam proyek ini kami memilih tema “Sampah dan Polusi” dengan judul “Website Pendeteksi Kebersihan Lingkungan”. Kami membuat model machine learning untuk image classification yang dapat mendeteksi sebuah gambar masukan apakah termasuk ke dalam kategori lingkungan bersih atau kotor. Kemudian dikembangkan dalam sebuah website guna memudahkan user dalam penggunaannya di dunia nyata.
User akan mengakses website kemudian telah menyiapkan sebuah gambar yang akan di upload untuk di deteksi bagaimana keadaan lingkungan nya. Hasil dari proses deteksi tersebut adalah sebuah pernyataan dan beberapa saran. Jika gambar yang dimasukan memiliki hasil “Bersih” maka akan muncul pop up tips menjaga kebersihan lingkungan. Sementara jika gambar yang dimasukan memiliki hasil “Kotor” maka akan muncul pop up cara dan motivasi untuk membersihkan lingkungan tersebut.


## Business Understanding

### Problem Statements

Berikut adalah problem statement dari proyek ini :

- Bagaimana user dapat mengidentifikasi kebersihan lingkungan mereka ?
- Bagaimana cara agar potret lingkungan yang diunggah user dapat diidentifikasi sehingga user dapat mengetahui kondisi kebersihan lingkungan mereka ? 


### Goals

Berdasarkan problem statement diatas, berikut adalah tujuan proyek ini:
- Membuat model machine learning yang dapat mengklasifikasi gambar.
- Membuat model machine learning yang bisa memprediksi hasil identifikasi gambar yang diunggah user.

### Solution statements

Untuk menyelesaikan masalah ini, saya menggunakan teknik penyelesaian masalah klasifikasi, yaitu Binary Classification. Berikut adalah penjelasan teknik-teknik yang akan digunakan untuk masalah ini :
- **Binary Classification :** Klasifikasi biner mengacu pada memprediksi satu dari dua kelas dan klasifikasi multi-kelas melibatkan memprediksi satu dari lebih dari dua kelas. Tugas klasifikasi biner untuk mengklasifikasikan elemen-elemen himpunan menjadi dua kelompok berdasarkan aturan klasifikasi.

## Data Understanding
![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/dataset1.png?raw=true)

[Dataset](https://www.kaggle.com/mfadliramadhan/cleandirtygarbage) yang saya gunakan merupakan dataset yang saya upload sendiri dengan memodifikasi dataset dari [Sumber dataset](https://www.kaggle.com/rodrigolaguna/clean-dirty-containers-in-montevideo)

Di dalam dataset ini terdapat 2 direktori yaitu train dan test. Disetiap direktori tersebut terdapat 2 direktori, yaitu clean dan dirty. Bentuk dataset pada direktori ini merupakan gambar dan terdapat 3426 files pada dataset ini.

Saya juga melakukan eksplorasi data untuk memahami variabel pada jumlah data dari dataset.

![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/EDA.png?raw=true)

Berdasarkan output diatas, diketahui bahwa dataset memiliki 4 direktori dan berjumlah 3426 files.


## Data Preparation

Untuk data preparation, saya menggunakan beberapa teknik yang diperlukan dalam tahapan data preparation, yaitu :

- Training data split : Membagi dataset menjadi training dan validation dengan skala 4:1 atau 20 % validation.
- Rescale : digunakan untuk mengubah skala nilai citra. Jadi ketika citra itu di load, citra direpresentasikan sebagai array 3D (atau kadang disebut Tensor) dengan nilai rentangan antara 0..255


## Modeling

Untuk tahap modeling ini, saya membuat model sequential CNN.

Berikut adalah Summary dari model Machine Learning yang digunakan.

![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/model%20ML.png?raw=true)

























Model yang telah dibuat akan compile dan dilatih agar mendapatkan akurasi prediksi yang bagus.

Berikut adalah hasil prediksi dari file dataset
![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/predict%20dataset1.png?raw=true)

Dari hasil prediksi diatas, terlihat bahwa gambar yang terlihat kotor dapat diprediksi sistem sebagai kotor.

![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/predict%20dataset%202.png?raw=true)

Dari hasil prediksi diatas, terlihat bahwa gambar yang terlihat bersih dapat diprediksi sistem sebagai bersih.

Berikut adalah hasil prediksi dari file diluar dataset
![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/predict%20outside%201.png?raw=true)

Dari output diatas, gambar yang terlihat bersih akan diprediksi sistem sebagai bersih.

![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/predict%20outside%202.png?raw=true)

Dari output diatas, gambar yang terlihat kotor akan diprediksi sistem sebagai kotor. Ini membuktikan bahwa gambar yang diprediksi tidak tergantung pada data dataset, namun bisa juga digunakan untuk data gambar lainnya sehingga berlaku untuk data gambar.


## Evaluation
Pada tahap ini, saya menggunakan metrik evaluasi Akurasi yang dihitung menggunakan perhitungan matematis.

- `Akurasi` adalah salah satu metrik untuk mengevaluasi model klasifikasi. Secara informal, akurasi adalah sebagian kecil dari prediksi model kami yang benar. Secara formal, akurasi memiliki definisi sebagai berikut:

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20accuracy.png?raw=true)

Untuk klasifikasi biner, akurasi juga dapat dihitung dalam hal positif dan negatif sebagai berikut:

![image](https://github.com/fadlinisasiGit/Laporan-Proyek-Machine-Learning-2/blob/main/rumus%20akurasi.png?raw=true)

Dimana TP = Positif Benar, TN = Negatif Benar, FP = Positif Palsu, dan FN = Negatif Palsu.

Dalam proyek ini, pada model CNN yang dibuat dan dilatih akan menghasilkan nilai akurasi. Berikut adalah nilai metrik evaluasi akurasi pada model CNN sistem pendeteksi kebersihan lingkungan :

![image](https://github.com/fadlinisasiGit/data-deteksi-kebersihan/blob/main/evaluation1.png?raw=true)

Terlihat pada visualisasi data diatas, nilai akurasi dan validasi nya mencapai 1.000 yang berarti akurasi dari pelatihan model akan sangat akurat pada hasil prediksi. Sehingga model machine learning ini sangat baik untuk mengklasifikasi kebersihan lingkungan.
 
## Conclusion
Sistem Deteksi Kebersihan Lingkungan ini mengatasi masalah klasifikasi yang merupakan bagian dari supervised learning. Dengan sistem ini, kita dapat mengidentifikasi suatu lingkungan yang bersih dan kotor, sehingga dapat memberikan edukasi kepada masyarakat untuk menjaga kebersihan di lingkungan sekitar mereka khususnya pada kebersihan sampah. Model ini akan di simpan dalam format file tflite, json, dan h5 agar dapat mendukung proses web deployment sehingga nantinya bisa diimplementasikan di sebuah website.
  
**---Ini adalah bagian akhir laporan---**
