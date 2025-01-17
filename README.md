# Klasifikasi Status Obesitas Menggunakan Decision Tree
##### Muhammad Sholahuddin Rasyid
##### A11.2022.14247
##### DM-4504

## Deskripsi Singkat Projek
Projek ini ditujukan untuk memenuhi tugas UAS mata kuliah Data-Mining, projek Klasifikasi Status Obesitas Menggunakan Decision Tree ini dimulai dari tahap preprocessing data - hingga evaluasi model Decision Tree yang yang dibuat. 
Ketertarikan pada topik  dimulai ketika saya hendak mencari dataset yang berhubungan dengan gaya hidup manusia. Kemudian munculah beberapa hasil pencarian yang salah satu nya adalah ‘Estimation of Obesity Levels Based On Eating Habits and Physical Condition’. Sebuah dataset dari archive.ics.uci.edu, yang membicarakan Tingkat Obesitas berdasarkan gaya makan dan kondisi fisik seseorang. Terdiri dari 17 atribut yang tentunya berkaitan dengan Kebiasaan makan dan kondisi fisik seperti pola makan, kegiatan sehari-hari seseorang. Yang nantinya berdasarkan data dari atribut tersebut, dapat diidentifikasi Tingkat Obesitas dari seseorang.

## Permasalahan dan Harapan
Mengingat obesitas dapat menyebabkan berbagai masalah kesehatan dan dapat mempengaruhi keseharian. Project kali ini mencoba mengatasi permasalahan tersebut dengan membuat model klasifikasi berdasarkan data kebiasaan makan dan kondisi fisik seseorang. Dengan tujuan model dapat mengklasifikasi tingkat obesitas seseorang secara akurat, dengan harapan dapat memberikan informasi berharga yang dapat mendorong seseorang untuk melakukan perubahan gaya hidup, dan pada akhirnya, mendukung upaya pencegahan obesitas yang lebih efektif.

## Dataset
Data diambil dari UC Irvine Repository yang dimana data ini digunakan untuk mengestimasi tingkat obesitas pada individu dari negara Meksiko, Peru dan Kolombia, berdasarkan kebiasaan makan dan kondisi fisik mereka.
- link : https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition

Dataset memiliki 17 Atribut dan 2111 record data, dimana 16 atribut sebagai fitur, dan 1 Atribut lainnya sebagai kelas/label. Dengan Penjelasan detail atribut sebagai berikut:

Atribut-atribut yang terkait dengan kebiasaan makan kebiasaan makan adalah: 
- Frekuensi konsumsi makanan berkalori tinggi (FAVC),
- Frekuensi konsumsi sayuran(FCVC),
- Jumlah makanan utama (NCP),
- Konsumsi makanan di antara waktu makan (CAEC),
- Konsumsi air setiap hari (CH20), 
- Konsumsi alkohol (CALC).

Atribut-atribut yang terkait dengan kondisi fisik
kondisi fisik adalah: 
- Pemantauan konsumsi kalori (SCC),
- Frekuensi aktivitas fisik (FAF),
- Waktu penggunaan menggunakan perangkat teknologi (TUE),
- Transportasi yang digunakan (MTRANS)
- Merokook atau tidak (SMOKE)

variabel lain yang diperoleh adalah: 
- Jenis Kelamin(Gender),
- Usia(AGE),
- Tinggi(Height), 
- Berat Badan(Weight),
- Riwayat obesitas keluarga (family_history_with_overweight).

Dan yang terakhir adalah atribut 'NoBayesdad', sebagai label yang mengindikasi kelas kelas obesitas yakni, Insufficient Weight, Normal Weight, Overweight Level I, Overweight Level II, Obesity Type I, Obesity Type II, and Obesity Type III

Terdapat 3 tipikal value pada fitur-fitur tersebut:
- Kolom (fitur) dengan value numerik, numerical_cols = ['Age', 'Height', 'Weight', 'FCVC', 'NCP', 'CH2O', 'FAF']
- Kolom (fitur) dengan value kategorikal, yang memiliki beberapa jenis value, categorical_cols = ['NCP', 'CAEC', 'FAF', 'TUE', 'CALC', 'MTRANS']
- Kolom (fitur) dengan value kategorikal, yang hanya memiliki 2 jenis value 'ya' atau 'tidak' || 'Male' or 'Female', binary_cols = ['Gender', 'fam_history', 'FAVC', 'SMOKE', 'SCC']

Penjelasan Lebih lengkap mengenai atribut dapat diakses di (https://doi.org/10.1016/j.dib.2019.104344)

## Alur/Tahapan
### Input
