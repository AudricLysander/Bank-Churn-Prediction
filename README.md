# Laporan Proyek Machine Learning - Audric Lysander

## Domain Proyek
Bank adalah salah satu badan usaha lembaga keuangan yang memiliki tujuan untuk memberikan jasa serta kredit [Sumber](https://repository.unpar.ac.id/bitstream/handle/123456789/1553/Sentosa_138949-p.pdf?sequence=1&isAllowed=y). 

*Churn* adalah kata dari bahasa Inggris yang memiliki arti beralih, dimana nasabah atau customer akan beralih ke perusahaan lainnya karena beberapa faktor, seperti faktor harga yang kurang tepat dikantong nasabah, kualitas jasa atau produk yang diberikan kurang sesuai dengan harapan, atau kurangnya fitur yang tidak sesuai dengan yang ditawarkan [Sumber](https://repository.uinjkt.ac.id/dspace/bitstream/123456789/18656/1/DELFIA%20ZANNA-FSH.pdf).

Bank dapat beroperasi ketika mereka memiliki nasabah yang menggunakan jasa mereka, ketika banyak nasabah yang beralih, maka kegiatan pemberian jasa, kredit, meredarkan alat pembayaran baru, dan lain-lain akan terhambat. Sehingga bank harus memastikan bahwa hal ini dapat di minimalisir, bisa saja dengan memperbaiki kualitas jasa, memberikan fitur yang sesuai, dan lain sebagainya. Selain itu, bank juga dapat melakukan prediksi untuk mengetahui apakah seorang nasabah akan beralih atau tidak, sehingga sebelum nasabah tersebut beralih, mungkin pihak bank dapat memberikan penawaran lain yang sesuai dengan nasabah, sehingga nasabah tidak jadi untuk beralih.

## Business Understanding

### Problem Statements
- Apakah model dapat memprediksi nasabah akan beralih atau tidak dengan baik?

### Goals
- Mengetahui model yang terbaik untuk melakukan prediksi nasabah akan berlatih ke bank lain atau tidak.
- 
### Solution Statements
- Melakukan Exploratory Data Analysis untuk melihat korelasi antar fitur dan hubungannya dengan tingkat *Churn*
- Menggunakan model *Machine Learning* yang sesuai dengan tujuan dan dataset yang digunakan, yaitu model regresi. Beberapa model regresi yang dapat digunakan adalah *K-Neighbors Regressor*, *Random Forest Regressor*, dan *AdaBoost Regresor*.

## Data Understanding
Data yang akan digunakan dalam proyek ini adalah dataset Bank Data - Churn Classification, dimana data ini dapat digunakan untuk melakukan klasifikasi untuk nasabah yang akan melakukan Churn ataupun tidak, untuk dataset yang dipakai dapat dibuka pada [tautan ini](https://www.kaggle.com/datasets/parisanahmadi/bank-data-churn-classification). Pada dataset ini diberikan file *.xlsx* yang memiliki 14 kolom serta 10000 baris, dimana 80000 baris merupakan data nasabah yang tidak beralih, sedangkan 20000 baris merupakan data nasabah yang beralih.
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

Dilakukan proses *Exploratory Data Analysis* (EDA) untuk menghilangkan outliers dan hubungan antar kolom.

1. *Churn*

![Persentase *Churn*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/churn.png)

Dapat dilihat dari diagram pie diatas churn rate pada data bank ini ada sebesar 20% atau sebanyak 2037 nasabah dari total 10000 nasabah.

2. *Credit Score*

![Distribusi *Churn* berdasarkan *Credit Score*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_CreditScore.png)

Dari distplot diatas dapat dilihat bahwa *credit score* tidak menentukan nasabah keluar atau tidak.
![*Outliers* pada kolom *CreditScore*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/outliers_CreditScore.png)

Pada data *Credit Score* terdapat *outliers* dibawah quantile 1, hal ini nanti akan diperbaiki pada saat melakukan *scaling* menggunakan robust scaler. Robust scaler digunakan untuk melakukan *scaling* data yang distribusinya bukan distribusi normal, serta belum dilakukan *outliers handling*.

3. *Age*

![Distribusi *Churn* berdasarkan umur](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_Age.png)

Dari data diatas dapat dilihat bahwa nasabah yang banyak keluar adalah nasabah yang memiliki berumur diantara 40 - 50 tahun.

![*Outliers* pada kolom *Age*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/outliers_Age.png)

Pada data *Age* terdapat *outliers* dibawah quantile 1, hal ini nanti akan diperbaiki pada saat melakukan *scaling* menggunakan robust scaler. Robust scaler digunakan untuk melakukan *scaling* data yang distribusinya bukan distribusi normal, serta belum dilakukan *outliers handling*.

4. *Tenure*

![Distribusi *Churn* berdasarkan *Tenure*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_Tenure.png)

Dari distplot diatas dapat dilihat bahwa *Tenure* tidak menentukan nasabah keluar atau tidak.

5. *Balance*

![Distribusi *Churn* berdasarkan *Balance*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_Balance.png)

*Chart* tersebut menunjukan nasabah yang banyak keluar adalah nasabah yang memiliki *Balance* sekitar 100000 - 150000, sedangkan yang banyak keluar adalah nasabah yang memiliki *Balance* sebesar 0.

5. *Number of Products*

![Distribusi *Churn* berdasarkan *NumOfProducts*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_NumOfProducts.png)

Plot diatas dapat disimpulkan bahwa jika nasabah memiliki jenis produk 1, 3, dan 4 kemungkinan besar akan keluar, sedangkan nasabah yang memilih jenis produk 2 hanya memiliki kemungkinan kecil untuk keluar.

6. *Has Credit Card*

![Distribusi *Churn* berdasarkan *HasCrCard*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_HasCrCard.png)

Nasabah yang memiliki ataupun tidak memiliki kartu kredit tidak mempengaruhi seorang nasabah keluar.

6. *Is Active Member*

![Distribusi *Churn* berdasarkan *IsActiveMember*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_IsActiveMember.png)

Nasabah yang aktif memiliki kemungkinan lebih kecil untuk keluar.

6. *Estimated Salary*

![Distribusi *Churn* berdasarkan *IsActiveMember*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_EstimatedSalary.png)

Estimasi pendapatan nasabah tidak mempengaruhi nasabah tersebut keluar atau tidak.

7. *Geography*

![Distribusi *Churn* berdasarkan *Geography*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_Geography.png)

Nasabah yang berasal dari Prancis adalah nasabah dengan tingkat keluar paling tinggi sebesar 42%, sedangkan tingkat keluar yang paling tinggi adalah nasabah yang berasal dari Jerman dan Prancis sebesar 0.81%.

8. *Gender*

![Distribusi *Churn* berdasarkan *Gender*](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/distribusi_Gender.png)

Nasabah laki-laki lebih banyak yang tidak keluar dibandingkan dengan nasabah perempuan.

Dari data diatas dapat disimpulkan bahwa
- Dataset ini memiliki 10000 baris data dengan 20% data *churn* dan 80% data *not churn*.
- Tidak ditemukan pola nasabah akan beralih pada kolom *Credit Score*, *Tenure*, *Has Credit Card*, *Estimated Salary*
- Pada kolom *Age* ditemukan pola nasabah yang berumur diantara 40-50 tahun banyak yang beralih.
- Pada kolom *Balance* ditemukan pola nasabah yang memiliki *Balance* sekitar 100000 - 150000 adalah nasabah yang kemungkinan besar akan beralih, sedangkan nasabah yang memiliki *Balance* 0 akan cenderung tidak akan beralih.
- Pada kolom *Number of Products* ditemukan pola nasabah yang menggunakan produk jenis 1, 3, dan 4 kemungkinan besar akan beralih, sedangkan nasabah yang menggunakan produk jenis 2 hanya memiliki kemungkinan kecil untuk beralih.
- Pada kolom *Is Active Member* menunjukan pola nasabah yang tidak aktif akan lebih cenderung untuk beralih dibandingkan nasabah yang aktif.
- Nasabah yang berasal dari Prancis memilki tingkat *not Churn* paling tinggi sebesar 42%, sedangkan nasabah yang berasal dari Jerman dan Prancis adalah nasabah yang paling besar tingkat *Churn*-nya.
- Nasabah yang bergender laki-laki cenderung akan bertahan dibandingkan nasabah yang bergender perempuan.

## Data Preparation
- Melakukan drop pada kolom yang tidak dapat dipakai dalam melakukan prediksi.
- Melakukan *one hot encoding* pada data kategorikal dengan menggunakan fungsi *get_dummies* yang tersedia di *library* Pandas. Data kategorikal tersebut akan di konversi menjadi bilangan biner.
- Melakukan *Train Test Split* untuk memisahkan data *train* sebesar 80% dan *test* sebesar 20%.
- Melakukan *scaling* untuk menyamakan skala pada data. Pada tahap ini digunakan robust scaler, karena data tidak berdistribusi normal dan memiliki banyak outliers.

## Modeling
Pada tahap ini, akan digunakan beberapa algoritma regresi yang akan membantu dalam pembuatan model, yaitu
- *K-Neightbor Regressor* adalah algoritma yang berasal dari algoritma *K-Nearest Neighbors*. Algoritma ini baik dalam memproses data yang non-linear, namun kurang baik dalam memproses data yang memiliki null values atau outliers. 
- *Random Forest* adalah algoritma yang berasal dari *decision tree*, dimana algoritma ini populer karena memiliki stabilitas yang baik.
- *AdaBoost* adalah algoritma yang memberikan bobot lebih pada observasi yang tidak tepat.

Berikutnya adalah tahapan yang dilakukan untuk membuat pemodelan machine learning, yaitu dibuat dataframe yang berisikan hasil perhitungan MSE pada setiap algoritma yang dipakai, untuk parameter setiap algortma akan dijelaskan dibawah ini.
1. KNeighborsRegressor, menggunakan 10 data neighbors terdekat sebagai data pembanding.
2. Random Forest, memiliki estimator sebanyak 35, maksimal kedalaman sebanyak 10, dan random_state = 55.
3. AdaBoost, menggunakan learning rate sebesar 0.05 dan random_state = 55.

## Evaluation
Evaluasi yang dipakai untuk melihat error model yang telah dibuat adalah menggunakan metoe Mean Squared Error (MSE). MSE akan menghitung rata-rata jumlah dari selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi.

![](https://pbs.twimg.com/media/Etuc3lBXcAEH7wO.png)

MSE	= mean squared error

n	= jumlah dataset

Yi	= nilai sebenarnya

Ŷi	= nilai prediksi

## Kesimpulan

![](https://github.com/AudricLysander/Bank-Churn-Prediction/blob/main/result.png)

Didapatkan kesimpulan dari proyek predictive analysis ini, yaitu berdasarkan prediksi *Churn* nasabah bank dengan menggunakan tiga model regresi Machine Learning, yaitu K-Neighbors Regressor, Random Forest, dan AdaBoost, yaitu algortima AdaBoosting adalah algoritma yang paling baik dalam memprediksi *Churn* dibandingkan dua algoritma lainnya. Hal ini dapat dilihat pada diagram diatas, dimana akurasi prediksi data *train* dan *test* memiliki akurasi yang tinggi, dan perbedaan antara kedua akurasi tersebut tidak terlalu besar.
