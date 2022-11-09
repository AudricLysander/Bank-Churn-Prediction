# Laporan Proyek Machine Learning - Audric Lysander

## Domain Proyek
Bank adalah salah satu badan usaha lembaga keuangan yang memiliki tujuan untuk memberikan jasa serta kredit [Sumber](https://repository.unpar.ac.id/bitstream/handle/123456789/1553/Sentosa_138949-p.pdf?sequence=1&isAllowed=y). 

Churn adalah kata dari bahasa Inggris yang memiliki arti beralih, dimana nasabah atau customer akan beralih ke perusahaan lainnya karena beberapa faktor, seperti faktor harga yang kurang tepat dikantong nasabah, kualitas jasa atau produk yang diberikan kurang sesuai dengan harapan, atau kurangnya fitur yang tidak sesuai dengan yang ditawarkan [Sumber](https://repository.uinjkt.ac.id/dspace/bitstream/123456789/18656/1/DELFIA%20ZANNA-FSH.pdf).

Bank dapat beroperasi ketika mereka memiliki nasabah yang menggunakan jasa mereka, ketika banyak nasabah yang beralih, maka kegiatan pemberian jasa, kredit, meredarkan alat pembayaran baru, dan lain-lain akan terhambat. Sehingga bank harus memastikan bahwa hal ini dapat di minimalisir, bisa saja dengan memperbaiki kualitas jasa, memberikan fitur yang sesuai, dan lain sebagainya. Selain itu, bank juga dapat melakukan prediksi untuk mengetahui apakah seorang nasabah akan beralih atau tidak, sehingga sebelum nasabah tersebut beralih, mungkin pihak bank dapat memberikan penawaran lain yang sesuai dengan nasabah, sehingga nasabah tidak jadi untuk beralih.

## Business Understanding

### Problem Statements
- Apakah kita dapat memprediksi nasabah akan keluar atau tidak?
- Model (Logistic Regression, KNN, Random Forest, dan Adaboosting) manakah yang paling baik dalam melakukan prediksi studi kasus ini>

## Goals
- Dapat melakukan prediksi nasabah akan tetap menggunakan jasa bank atau tidak
- Dapat mengetahui model paling baik dalam melakukan prediksi

## Data Understanding
Data yang akan digunakan dalam proyek ini adalah dataset Bank Data - Churn Classification, dimana data ini dapat digunakan untuk melakukan klasifikasi untuk nasabah yang akan melakukan Churn ataupun tidak, untuk dataset yang dipakai dapat dibuka pada tautan [ini](https://www.kaggle.com/datasets/parisanahmadi/bank-data-churn-classification).
### Variabel-variabel pada Bank Data - Churn Classification:
- RowNumber: Nomor urut baris data
- CustomerId: Nomor identifikasi unik yang diberikan oleh Bank kepada setiap nasabah
- CreditScore: Angka dari 300 hingga 850 yang menggambarkan kelayakan kredit nasabah
- Geography: Lokasi pelanggan dapat mempengaruhi keputusan mereka untuk meninggalkan bank
- Gender: Jenis kelamin nasabah (Female / Male)
- Age: Umur nasabah dalam tahun
- Tenure: Jumlah tahun nasabah telah menjadi nasabah bank
- Balance: akumulasi dari transaksi utang sebelumnya
- NumOfProducts: Jenis produk keuangan yang dipakai oleh nasabah
- HasCrCard: Status kepemilikan credit card nasabah
- IsActiveMember: Status ke-aktivan nasabah
- EstimatedSalary: Estimasi pendapatan nasabah
- Exited: Status keluarnya nasabah

## Data Preparation
- Pertama dilakukan pembuangan pada kolom yang tidak akan dipakai
- Kedua dilakukan outlier handling untuk menghilangkan outlier, karena akan menggangu saat melakukan permodelan, namun disini hanya akan dilihat banyaknya outlier, untuk penanganannya akan dilakukan pada saat scaling.
- Ketiga dilakukan encoding yang bertujuan untuk mengubah data kategorik yang memiliki tipe data string, menjadi data kategorik yang memiliki tipe data numerik, sehingga data tersebut dapat dipakai untuk model machine learning.
- Keempat dilakukan split untuk data train dan test
- Kelima dilakukan scaling agar data setiap kolom memiliki skala data yang serupa, namun hanya akan dilakukan scaling pada pada train, sehingga tidak ada kebocoran data test.

## Modeling
Pada tahap ini dilakukan modeling menggunakan Logistic Regression, KNN, Random Forest, dan Adaboost Algorithm.
- Pertama akan dibuat variabel untuk memanggil model
- Kedua akan dilakukan fit untuk memasukkan data train kedalam model
- Ketiga akan dicari MSE (Mean Squared Error) untuk mendapatkan besaran error pada model tersebut

## Evaluation
1. Model Logistic Regression memiliki tingkat akurasi prediksi secara keseluruhan sebesar 81%, namun akurasi recall hanya sebesar 23%. Hal tersebut sangatlah rendah, karena akan sangat fatal jika model memprediksi nasabah tidak akan keluar, namun pada kenyataannya nasabah tersebut akan keluar. Hal ini mungkin terjadi karena perbedaan jumlah data nasabah yang keluar dan tidak keluar.

2. Model Random Forest memiliki tingkat akurasi train yang sangat rendah, namun memiliki akurasi test yang tinggi, hal ini dapat disebut dengan underfitting.

3. Model AdaBoosting adalah model yang memiliki tingkat akurasi paling baik dari antara model lainnya, dimana model ini memiliki akurasi train dan test yang serupa.

4. Model KNN adalah model paling bagus ke-dua setelah adaboosting, dimana memiliki nilai akurasi train dan test yang hampir serupa dan bisa memprediksi dengan baik.
