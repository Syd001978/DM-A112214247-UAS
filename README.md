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
- Frekuensi seberapa banyak konsumsi makanan berkalori tinggi (FAVC),
- Frekuensi seberapa banyak konsumsi sayuran(FCVC),
- Jumlah kali makan per hari (NCP),
- Konsumsi makanan di antara waktu makan (CAEC),
- Konsumsi air setiap hari (CH20), 
- Konsumsi alkohol (CALC).

Atribut-atribut yang terkait dengan kondisi fisik
kondisi fisik adalah: 
- Pemantauan konsumsi kalori (SCC),
- Frekuensi aktivitas fisik (FAF),
- Waktu penggunaan perangkat teknologi (TUE),
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
### Input (Processing Data)
Ini adalah tahap persiapan data dimana dataset (obesitas.csv)akan dibersihkan sebelum akhirnya digunakan untuk pembuatan model. atau biasa disebut dengan tahapan Preprocessing.

Seluruh tahapan preprocessing terdapat pada file DM-Pre Processing.ipynb, apa saja yang dilakukan:

- Normalisasi kolom/fitur  yang memiliki value numerik namun, tidak sesuai dengan seharusnya. contoh pada kolom 'Age' terdapat banyak sekali value 'Age' yang memiliki banyak sekali angka dibelakang koma, sehingga value dibulatkan supaya tidak memiliki angka di belakang koma.
- Encoding kolom/fitur yang memiliki value kategorikal yang memiliki banyak jenis value, seperti kolom 'CALC' atau 'MTRANS'.

'CALC' memiliki 4 jenis value, yaitu No, Sometimes, Frequently, Always. jenis value tersebut akan dikonversi menjadi numerik urut dari 0 untuk 'No' hingga 4 untuk 'Always'. begitu pula dengan kolom yang memiliki value serupa. menggunakan fungsi .map() dari library pandas. ini juga berlaku untuk kolom yang bervalue biner

- Normalisasi kolom/fitur yang memiliki value numerik dalam konteks frekuensi. contoh pada kolom 'FAVC', karena fitur tersebut Frekuensi konsumsi makanan berkalori tinggi. atau dengan kata lain seberapa mengkonsumsi makanan berkalori tinggi maka, kolom tersebut menerima input tan berupa frekuensi angka.

untuk kasus 'FAVC', karena banyak ditemukan value yang memuat angka dibelakang koma, maka harus dibulatkan menjadi angka bulat. dengan cara mencari nilai max dan min value untuk menentukan batas atas dan batas bawah. lalu akan dibulatkan ke angka yang terdekat setelah ditentukan batas atas dan bawahnya. begitu pula dengan kolom yang serupa.

hasil akhir berupa file csv (obesitas_preprocessed.csv), yang berisi data yang sudah diubah dan diprocess. dan siap untuk dibuat model

### Proses (Pemodelan)
Ini adalah tahap dimana modelling akan dilakukan. Dengan model data yang memiliki label yang jelas seperti ini, akan sangat cocok bila menggunakan algoritma supervised learning. pada awalnya akan menggunakan algoritma KNN (K-Nearest-Neigbour). Namun mengingat dimensi data yang begitu besar, memiliki banyak fitur dan record, dan memiliki lebih dari 2 jenis label/target. Sedangkan KNN sangat sensitif dan performanya berkurang, ketika dimensi data begitu besar dan akan berpengaruh terhadap performa model. maka dipilihlah, Decision Tree.

Seluruh tahap pemodelan berada pada file DM-Modelling-Decision Tree.ipynb. Lengkap dengan visualisasi tree untuk setiap modelnya.

Modeling akan dilakukan dengan membandingan akurasi yang berbada dari berbagai cara:

- Modeling dengan dataset pure data yang sudah di pre processing
dataset (obesitas_preprocessed.csv), langsung digunakan untuk proses modeling decision tree. tanpa melakukan feature selection maupun tuning hyperparameter.
- Modeling dengan selection Feature menggunakan RFE
didapatkan fitur terbaik setelah rank fitur dihitung  menggunakan RFE, yaitu ['Gender', 'Age', 'Height', 'Weight', 'FAVC', 'NCP', 'CAEC', 'CH2O','FAF','TUE']
- Modeling dengan Selection Feature RFE dikombinasikan dengan Tuning Hyperparameter
modeling masih menggunakan fitur terpilih namun dikombinasikan dengan Hyperparameter terbaik, yaitu {'criterion': 'entropy', 'max_depth': None, 'min_samples_split': 5}.

Pembagian data pelatihan (training) dan data pengujian (testing). untuk semua model sama,  20% dari data akan digunakan sebagai data pengujian, dan  80% sisanya akan digunakan sebagai data pelatihan.

Semua Modeling decision tree menggunakan kriteria entropy, untuk mengukur ketidakpastian dalam dataset. Semakin tinggi entropi, semakin tidak teratur data tersebut. Tujuannya adalah untuk meminimalkan entropi setelah pemisahan. dengan acuan atau pedoman pada materi decision tree pertemuan 7.

Cara Kerja nya seperti berikut : Pertama, decision tree menghitung entropy untuk seluruh data. Kemudian, untuk setiap fitur, decision tree menghitung entropy setelah membagi data berdasarkan nilai fitur tersebut. decision tree mencari tahu seberapa banyak ketidakpastian berkurang setelah pemisahan ini, yang disebut information gain. Fitur yang memberikan information gain tertinggi dipilih untuk menjadi cabang pada tree. Proses ini diulang sampai kita mendapatkan keputusan akhir, sehingga decision tree dapat memprediksi kelas berdasarkan fitur yang paling membantu.

Juga dilakukan uji coba untuk memprediksi dataframe baru, dengan inputan yang disesuaikan dengan value dataset yang telah dipreprocess atau dataset yang digunakan untuk training model saat ini, yakni numerik.


### Output
Output yang dihasilkan adalah suatu model decision tree yang dapat mengklasifikasi tiap kelas obesitas yang ada. termasuk dengan visualisasi tree secara keseluruhan dari model yang ada. model yang dihasilkan ada 3, yakni dt_1, dt_2, dan best_model.

Visualisasi tree memuat, Nama fitur, nilai entropy, hingga class yang berhasil di klasifikasi/prediksi. keluaran yang didapat juga berupa evaluasi model, mulai dari confussion matrix hingga akurasi model secara keseluruhan.


### Evaluation
Evaluasi model menggunakan metode metode berikut:

- Confusion Matrix, Tabel yang menunjukkan jumlah prediksi benar dan salah dari model. Terdiri dari True Positives (TP), True Negatives (TN), False Positives (FP), dan False Negatives (FN), memberikan gambaran jelas tentang kesalahan model.
- Precision, Mengukur seberapa banyak prediksi positif yang benar-benar positif. Dihitung dari TP dibagi dengan total prediksi positif (TP + FP). Penting ketika kesalahan dalam prediksi positif memiliki konsekuensi serius.
- Recall (Sensitivity), Mengukur seberapa banyak kasus positif yang berhasil diidentifikasi. Dihitung dari TP dibagi dengan total kasus positif yang sebenarnya (TP + FN). Krusial ketika tidak mendeteksi kasus positif dapat berakibat fatal.
- F1-Score, Rata-rata harmonis dari precision dan recall. Memberikan keseimbangan antara keduanya dan berguna saat ada ketidakseimbangan kelas dalam dataset.
- Support, Jumlah aktual dari setiap kelas dalam dataset. Memberikan konteks untuk metrik lainnya, membantu memahami seberapa relevan hasil evaluasi untuk setiap kelas.

Dan menghitung nilai akurasi model, berikut sekilas nilai akurasi yang didapat untuk tiap model:

- dt_1       : 93,22% (pure dari dataset setelah preprocess)
- dt_2       : 94.80% (dengan feature selection)
- best_model : 93.85% (feature selection dikombinasikan dengan Tuning hyperparameter)

hasil yang lebih detail terdapat pada file DM-Modelling-Decision Tree.ipynb


### Kesimpulan 
Modeling decision tree untuk Klasifikasi Status Obesitas, berhasil dilakukan dengan mendapatkan nilai akurasi tertinggi yakni 94.80%. model tersebut adalah model yang dilakukan feature selection sebelumnya, karena mungkin kompleksitas fitur sangat berpengaruh terhadap akurasi model dalam memprediksi kelas obesitas. jika dilihat dari kasat mata pengguna dari ke-16 fitur yang ada sangat mungkin digunakan untuk mengklasifikasi(mengidentifikasi), apakah seseorang


### Referensi 
Berikut beberapa refrensi yang digunakan:

- Materi Pertemuan 2 Preprocessing Data
- Materi Pertemuan 7 Decision Tree
- https://ejournal.mediaantartika.id/index.php/jka/article/view/341 "Penerapan Algoritma C4.5 Untuk Prediksi Faktor Risiko Obesitas Pada Penduduk Dewasa"
- https://www.semanticscholar.org/paper/35b40bacd2ffa9370885b7a3004d88995fd1d011 'Dataset for estimation of obesity levels based on eating habits and physical condition in individuals from Colombia, Peru and Mexico' 
