# Laporan Proyek Machine Learning - Rafi Ardizza Fadhillah Setiadi
## Project Overview
Pada proyek ini, saya mengembangkan sebuah model sistem rekomendasi menggunakan dataset "NetflixOriginals.csv" yang tersedia di repositori GitHub. Dataset ini berisi informasi tentang film-film original Netflix, termasuk judul, genre, bahasa, tanggal rilis, dan skor IMDB. Sistem rekomendasi ini akan membantu pengguna menemukan film-film yang relevan berdasarkan preferensi mereka.

Proyek ini penting karena dengan semakin banyaknya konten yang tersedia di platform streaming seperti Netflix, pengguna sering kali kesulitan menemukan film yang sesuai dengan selera mereka. Sistem rekomendasi yang efektif dapat meningkatkan kepuasan pengguna dan meningkatkan waktu yang dihabiskan pengguna pada platform.

## Business Understanding
### Problem Statements
1. Bagaimana membuat sistem rekomendasi yang dapat memberikan saran film yang relevan berdasarkan genre?
2. Bagaimana menggunakan informasi skor IMDB untuk meningkatkan kualitas rekomendasi?

### Goals
1. Mengembangkan model content-based filtering untuk merekomendasikan film berdasarkan genre.
2. Mengembangkan model collaborative filtering untuk merekomendasikan film berdasarkan skor IMDB dan preferensi pengguna lainnya.

### Solution Approach
1. Content-Based Filtering: Menggunakan teknik TF-IDF untuk mengubah deskripsi genre menjadi fitur numerik dan menghitung kemiripan kosinus antara film untuk memberikan rekomendasi.
2. Collaborative Filtering: Membuat tabel pivot untuk skor IMDB dan menggunakannya untuk menghitung kemiripan antar film, kemudian memberikan rekomendasi berdasarkan kemiripan ini.

## Data Understanding
Dataset yang digunakan adalah dari Kaggle dengan link [Netflix Dataset](https://www.kaggle.com/datasets/data855/heart-disease) Dataset ini berisi 1025 sampel dan 6 atribut.

### Kondisi Dataset
Setelah dilakukan pemeriksaan, tidak ditemukan adanya nilai null atau missing values pada dataset ini. Hal ini menunjukkan bahwa dataset sudah lengkap dan tidak perlu dilakukan imputasi data.

### Variabel pada Netflix Dataset adalah sebagai berikut:
1. Title: Judul film Netflix Original.
2. Genre: Genre atau kategori film.
3. Premiere: Tanggal perilisan film.
4. Runtime: Durasi film dalam menit.
5. Language: Bahasa film.
6. IMDB Score: Skor atau rating film di IMDB.

Dataset ini memberikan informasi yang cukup lengkap mengenai atribut-atribut yang relevan dalam membuat sistem rekomendasi berdasarkan preferensi pengguna terhadap film. Dengan tidak adanya nilai null, dataset ini siap digunakan untuk tahap selanjutnya dalam proses pengembangan model rekomendasi.

### Exploratory Data Analysis (EDA):
1. Informasi Dataset: Menampilkan informasi mengenai tipe data dari masing-masing kolom serta jumlah nilai non-null di setiap kolom.

2. Statistik Deskriptif: Menampilkan statistik deskriptif dari dataset seperti mean, standar deviasi, nilai minimum dan maksimum, serta kuartil.

3. Visualisasi Data: Menampilkan visualisasi data untuk memberikan gambaran lebih jelas tentang distribusi data dan hubungan antar variabel.

## Data Preparation
1. Data Cleaning: Langkah ini memastikan bahwa dataset bersih dan siap untuk digunakan dalam analisis. Dalam kasus ini, tidak ada nilai yang hilang (missing values) pada dataset, sehingga tidak diperlukan penanganan lebih lanjut untuk nilai yang hilang.

2. Data Transformation: 
    * Mengubah kolom 'Premiere' menjadi format datetime dan kemudian menjadi numerik menggunakan encoding ordinal.
    * Mengubah kolom 'Language' menjadi format numerik menggunakan LabelEncoder.

3. Normalisasi Data: Normalisasi adalah proses penskalaan fitur-fitur sehingga mereka berada dalam skala yang sama. Ini penting karena banyak algoritma pembelajaran mesin bekerja lebih baik ketika fitur-fitur memiliki rentang nilai yang serupa.

4. Memisahkan Fitur dan Label: Memisahkan fitur dan label adalah langkah di mana kita memisahkan atribut input (fitur) dari target output (label) yang ingin diprediksi oleh model.

5. Split Data Menjadi Training dan Testing Set: Membagi data menjadi training dan testing set adalah langkah untuk memastikan model dapat dievaluasi secara objektif. Data training digunakan untuk melatih model, sedangkan data testing digunakan untuk menguji performa model pada data yang belum pernah dilihat sebelumnya.

## Modeling and Result
### Content-Based Filtering
Content-Based Filtering adalah pendekatan dalam sistem rekomendasi yang menggunakan informasi atau konten dari item yang direkomendasikan untuk membuat rekomendasi kepada pengguna. Dalam konteks ini, content-based filtering digunakan untuk merekomendasikan film berdasarkan kesamaan genre mereka.

#### Tahapan Pembuatan Model
1. TF-IDF Vectorizer : Menggunakan TF-IDF untuk mengubah deskripsi genre film menjadi representasi numerik dengan menggunakan skema Term Frequency-Inverse Document Frequency (TF-IDF). Stop words bahasa Inggris dihapus untuk meningkatkan kualitas vektorisasi.
2. Cosine Similarity: Untuk menghitung seberapa mirip satu film dengan film lain berdasarkan vektor representasi TF-IDF mereka.
3. Get Recommendations: Fungsi get_recommendations digunakan untuk memberikan rekomendasi film yang mirip berdasarkan film yang dipilih oleh pengguna.
4. Example Recommendations: Memberikan contoh rekomendasi

#### Kelebihan dan Kekurangan Content-Based Filtering
Kelebihan:
* Tidak memerlukan data pengguna lain untuk memberikan rekomendasi.
* Mudah diimplementasikan.
Kekurangan:
* Hanya dapat merekomendasikan film yang serupa dengan yang sudah pernah dilihat oleh pengguna.
* Tidak dapat menangkap preferensi pengguna secara dinamis.

### Collaborative Filtering
Collaborative Filtering adalah pendekatan yang berfokus pada penggunaan informasi dari pengguna lain untuk memberikan rekomendasi. Dalam kasus ini, collaborative filtering digunakan untuk merekomendasikan film berdasarkan preferensi pengguna lain yang memiliki kesamaan dalam skor IMDB.

#### Tahapan Pembuatan Model
1. Pivot Table: Pivot table dibuat dengan film sebagai indeks, genre sebagai kolom, dan skor IMDB sebagai nilai untuk memfasilitasi perhitungan kemiripan.
2. Cosine Similarity: Matriks kemiripan kosinus digunakan untuk menghitung seberapa mirip satu film dengan film lain berdasarkan skor IMDB mereka dalam pivot table.
3. Get Recommendations: Fungsi get_recommendations digunakan untuk memberikan rekomendasi film yang mirip berdasarkan film yang dipilih oleh pengguna.
4. Example Recommendations: Memberikan contoh rekomendasi

#### Kelebihan dan Kekurangan Collaborative Filtering
Kelebihan:
* Dapat menangkap preferensi pengguna secara dinamis.
* Dapat merekomendasikan film yang berbeda dari yang sudah pernah dilihat pengguna.
Kekurangan:
* Memerlukan data dari banyak pengguna untuk memberikan rekomendasi yang akurat.
* Sulit diimplementasikan untuk pengguna baru yang belum memiliki riwayat interaksi.

## Evaluation
Pada bagian ini, kita menggunakan beberapa metrik evaluasi untuk menilai performa model yang dikembangkan, yaitu MAE dan RMSE. Berikut penjelasan mengenai metrik yang digunakan dan hasil proyek berdasarkan metrik tersebut:

### Metrik Evaluasi yang Digunakan
Metode evaluasi yang digunakan dalam proyek ini adalah Mean Absolute Error (MAE) dan Root Mean Squared Error (RMSE):
* Mean Absolute Error (MAE): Mean Absolute Error mengukur rata-rata absolut dari selisih antara nilai prediksi dan nilai aktual. Semakin kecil nilai MAE, semakin baik performa model.
  $$MAE=\frac{1}{n}\sum_{i=1}^{n}\left| y_i-\hat{y}_i \right|$$
* Root Mean Squared Error (RMSE): Root Mean Squared Error mengukur akar kuadrat dari rata-rata kuadrat selisih antara nilai prediksi dan nilai aktual. Nilai RMSE yang lebih kecil menunjukkan performa model yang lebih baik.
  $$RMSE=\sqrt{\frac{1}{n}\sum_{i=1}^{n}\left(y_i-\hat{y}_i \right)^{2}}$$

### Hasil Evaluasi Model
* MAE: Mean Absolute Error adalah 0.317
* RMSE: Root Mean Squared Error adalah 0.391

### Kesimpulan
Metrik evaluasi yang digunakan dalam laporan ini, yaitu Mean Absolute Error (MAE) dan Root Mean Squared Error (RMSE), sesuai dengan konteks penggunaan dalam sistem rekomendasi ini. MAE digunakan untuk mengukur rata-rata absolut dari selisih antara nilai prediksi dan nilai aktual, memberikan informasi tentang rata-rata kesalahan prediksi yang dapat diharapkan dari model. Di sisi lain, RMSE memberikan gambaran tentang seberapa besar kesalahan prediksi dalam skala yang lebih besar, dengan memberikan bobot lebih besar pada kesalahan yang lebih besar.

Penggunaan kedua metrik ini penting karena membantu mengevaluasi seberapa baik model dapat memprediksi skor film berdasarkan preferensi pengguna, sesuai dengan tujuan proyek untuk meningkatkan kualitas rekomendasi film kepada pengguna.

Hasil evaluasi model menunjukkan bahwa model memiliki performa yang baik dalam memprediksi skor film berdasarkan preferensi pengguna. MAE yang diperoleh sebesar 0.317 menunjukkan bahwa rata-rata kesalahan prediksi model relatif kecil. Selain itu, RMSE sebesar 0.391 mengindikasikan bahwa model memiliki kemampuan untuk membuat prediksi yang presisi dan mendekati nilai sebenarnya dengan akurat.

Performa model yang solid ini memberikan keyakinan bahwa rekomendasi yang diberikan kepada pengguna dapat diandalkan dan akurat sesuai dengan preferensi mereka terhadap film. Evaluasi ini juga menunjukkan bahwa model telah berhasil menginterpretasikan pola dari data yang tersedia dengan baik, sehingga mampu memberikan nilai prediksi yang mendekati nilai sebenarnya dengan tingkat kesalahan yang minim.
