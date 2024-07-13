# Laporan Proyek Machine Learning - Rafi Ardizza Fadhillah Setiadi
## Project Overview
### Latar Belakang
Dengan semakin banyaknya konten yang tersedia di platform streaming seperti Netflix, pengguna sering kali kesulitan menemukan film yang sesuai dengan selera mereka. Hal ini dapat mengakibatkan pengalaman pengguna yang kurang memuaskan dan waktu yang terbuang dalam mencari film yang diinginkan. Salah satu cara untuk membantu pengguna menemukan film yang sesuai adalah dengan memberikan rekomendasi berdasarkan genre yang mereka sukai. Genre adalah salah satu atribut utama yang digunakan oleh pengguna untuk memilih film, sehingga sistem rekomendasi berbasis genre dapat lebih efektif dalam menyajikan film-film yang relevan.

### Tujuan Proyek
Proyek ini bertujuan untuk mengembangkan sebuah model sistem rekomendasi yang dapat membantu pengguna menemukan film-film yang relevan berdasarkan preferensi mereka. Model ini menggunakan dataset "NetflixOriginals.csv" yang tersedia di repositori GitHub, yang berisi informasi tentang film-film original Netflix, termasuk judul, genre, bahasa, tanggal rilis, dan skor IMDB. Sistem rekomendasi ini akan membantu pengguna menemukan film-film yang relevan berdasarkan preferensi mereka.

## Business Understanding
### Problem Statements
1. Bagaimana membuat sistem rekomendasi yang dapat memberikan saran film yang relevan berdasarkan genre?
2. Bagaimana meningkatkan kualitas rekomendasi dengan memanfaatkan informasi skor IMDB dan preferensi pengguna lainnya?

### Goals
1. Mengembangkan model content-based filtering untuk merekomendasikan film berdasarkan genre.
2. Meningkatkan kualitas rekomendasi dengan mengembangkan model collaborative filtering yang memanfaatkan skor IMDB dan preferensi pengguna lainnya.

### Solution Approach
1. Content-Based Filtering: Menggunakan teknik TF-IDF untuk mengubah deskripsi genre menjadi fitur numerik dan menghitung kemiripan kosinus antara film untuk memberikan rekomendasi.
2. Collaborative Filtering: Membuat tabel pivot untuk skor IMDB dan menggunakannya untuk menghitung kemiripan antar film, kemudian memberikan rekomendasi berdasarkan kemiripan ini.

## Data Understanding
Dataset yang digunakan adalah dari Kaggle dengan link [Netflix Dataset](https://www.kaggle.com/datasets/luiscorter/netflix-original-films-imdb-scores) Dataset ini berisi 584 sampel dan 6 atribut.

### Kondisi Dataset
* Nilai Null: Dataset ini tidak memiliki nilai null, sehingga tidak diperlukan penanganan missing values.
* Sebaran Data: Dataset ini terdiri dari 6 atribut yang memiliki sebaran nilai yang bervariasi, seperti Title, Genre, IMDB Score, dan lain-lain.

### Variabel pada Netflix Dataset adalah sebagai berikut:
1. Title: Judul film Netflix Original.
2. Genre: Genre atau kategori film.
3. Premiere: Tanggal perilisan film.
4. Runtime: Durasi film dalam menit.
5. Language: Bahasa film.
6. IMDB Score: Skor atau rating film di IMDB.

Dataset ini memberikan informasi yang cukup lengkap mengenai atribut-atribut yang relevan dalam membuat sistem rekomendasi berdasarkan preferensi pengguna terhadap film. Dengan tidak adanya nilai null, dataset ini siap digunakan untuk tahap selanjutnya dalam proses pengembangan model rekomendasi.

### Exploratory Data Analysis (EDA):
1. 5 baris pertama dari dataset : Menampilkan lima baris pertama dari dataset

2. Informasi Dataset: Menampilkan informasi mengenai tipe data dari masing-masing kolom serta jumlah nilai non-null di setiap kolom.

3. Statistik Deskriptif: Menampilkan statistik deskriptif dari dataset seperti mean, standar deviasi, nilai minimum dan maksimum, serta kuartil.
   
4. Mengecek Jumlah Null: Langkah ini memastikan bahwa dataset bersih dan siap untuk digunakan dalam analisis. Dalam kasus ini, tidak ada nilai yang hilang (missing values) pada dataset, sehingga tidak diperlukan penanganan lebih lanjut untuk nilai yang hilang.
  
5. Visualisasi Data: Menampilkan visualisasi data untuk memberikan gambaran lebih jelas tentang distribusi data dan hubungan antar variabel.

## Data Preparation
1. Data Transformation: 
    * Mengubah kolom 'Premiere' menjadi format datetime dan kemudian menjadi numerik menggunakan encoding ordinal.
    * Mengubah kolom 'Language' menjadi format numerik menggunakan LabelEncoder.

2. Normalisasi Data: Normalisasi adalah proses penskalaan fitur-fitur sehingga mereka berada dalam skala yang sama. Ini penting karena banyak algoritma pembelajaran mesin bekerja lebih baik ketika fitur-fitur memiliki rentang nilai yang serupa.

3. TF-IDF Vectorizer : Menggunakan TF-IDF untuk mengubah deskripsi genre film menjadi representasi numerik dengan menggunakan skema Term Frequency-Inverse Document Frequency (TF-IDF). Stop words bahasa Inggris dihapus untuk meningkatkan kualitas vektorisasi.

4. Memisahkan Fitur dan Label: Memisahkan fitur dan label adalah langkah di mana kita memisahkan atribut input (fitur) dari target output (label) yang ingin diprediksi oleh model.
    * Dalam proyek ini:
        * Fitur (X): Semua kolom yang telah dinormalisasi.
        * Label (y): Kolom 'IMDB Score'.

5. Split Data Menjadi Training dan Testing Set: Membagi data menjadi training dan testing set adalah langkah untuk memastikan model dapat dievaluasi secara objektif. Data training digunakan untuk melatih model, sedangkan data testing digunakan untuk menguji performa model pada data yang belum pernah dilihat sebelumnya.
    * Dalam proyek ini, konfigurasi split data menggunakan skala 80:20, artinya 80% data digunakan untuk training dan 20% data digunakan untuk testing. Penggunaan random_state=42 memastikan bahwa pembagian data dilakukan secara konsisten setiap kali kode dijalankan, memungkinkan reproduksibilitas hasil.

## Modeling and Result
### Content-Based Filtering
Content-Based Filtering adalah pendekatan dalam sistem rekomendasi yang menggunakan informasi atau konten dari item yang direkomendasikan untuk membuat rekomendasi kepada pengguna. Dalam konteks ini, content-based filtering digunakan untuk merekomendasikan film berdasarkan kesamaan genre mereka.

#### Tahapan Pembuatan Model
1. Cosine Similarity: Untuk menghitung seberapa mirip satu film dengan film lain berdasarkan vektor representasi TF-IDF mereka.
2. Get Recommendations: Fungsi get_recommendations digunakan untuk memberikan rekomendasi film yang mirip berdasarkan film yang dipilih oleh pengguna.
3. Example Recommendations: Memberikan contoh rekomendasi

#### Kelebihan dan Kekurangan Content-Based Filtering
* Kelebihan:
    * Tidak memerlukan data pengguna lain untuk memberikan rekomendasi.
    * Mudah diimplementasikan.
* Kekurangan:
    * Hanya dapat merekomendasikan film yang serupa dengan yang sudah pernah dilihat oleh pengguna.
    * Tidak dapat menangkap preferensi pengguna secara dinamis.

### Collaborative Filtering
Collaborative Filtering adalah pendekatan yang berfokus pada penggunaan informasi dari pengguna lain untuk memberikan rekomendasi. Dalam kasus ini, collaborative filtering digunakan untuk merekomendasikan film berdasarkan preferensi pengguna lain yang memiliki kesamaan dalam preferensi film atau interaksi sebelumnya.

#### Tahapan Pembuatan Model
1. Pivot Table: Pivot table dibuat dengan film sebagai indeks, genre sebagai kolom, dan skor IMDB sebagai nilai untuk memfasilitasi perhitungan kemiripan.
2. Cosine Similarity: Matriks kemiripan kosinus digunakan untuk menghitung seberapa mirip satu film dengan film lain berdasarkan skor IMDB mereka dalam pivot table.
3. Get Recommendations: Fungsi get_recommendations digunakan untuk memberikan rekomendasi film yang mirip berdasarkan film yang dipilih oleh pengguna.
4. Example Recommendations: Memberikan contoh rekomendasi

#### Kelebihan dan Kekurangan Collaborative Filtering
* Kelebihan:
    * Dapat menangkap preferensi pengguna secara dinamis.
    * Dapat merekomendasikan film yang berbeda dari yang sudah pernah dilihat pengguna.
* Kekurangan:
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
* MAE: Mean Absolute Error adalah 0.0507
* RMSE: Root Mean Squared Error adalah 0.1620

### Kesimpulan
Metrik evaluasi yang digunakan dalam laporan ini, yaitu Mean Absolute Error (MAE) dan Root Mean Squared Error (RMSE), sesuai dengan konteks penggunaan dalam sistem rekomendasi ini. MAE digunakan untuk mengukur rata-rata absolut dari selisih antara nilai prediksi dan nilai aktual, memberikan informasi tentang rata-rata kesalahan prediksi yang dapat diharapkan dari model. Di sisi lain, RMSE memberikan gambaran tentang seberapa besar kesalahan prediksi dalam skala yang lebih besar, dengan memberikan bobot lebih besar pada kesalahan yang lebih besar.

Dari hasil evaluasi model sistem rekomendasi film berdasarkan preferensi pengguna, diperoleh nilai Mean Absolute Error (MAE) sebesar 0.051 dan Root Mean Squared Error (RMSE) sebesar 0.162.

MAE yang rendah, sebesar 0.051, menunjukkan bahwa rata-rata kesalahan prediksi model relatif kecil. Artinya, model cenderung memberikan rekomendasi yang sangat dekat dengan preferensi pengguna dalam menyarankan film. Sementara RMSE yang juga rendah, yaitu 0.162, mengindikasikan bahwa model memiliki kemampuan untuk membuat prediksi yang stabil dan akurat dalam menentukan skor film yang direkomendasikan.

Hasil evaluasi ini menegaskan bahwa model sistem rekomendasi yang dikembangkan telah berhasil dalam memberikan rekomendasi film yang sesuai dengan preferensi pengguna dengan tingkat kesalahan yang sangat rendah. Kedua metrik evaluasi ini memberikan keyakinan bahwa rekomendasi yang diberikan kepada pengguna dapat diandalkan dan akurat, meningkatkan kepuasan pengguna dalam menemukan film yang mereka nikmati.

Dengan demikian, model ini telah berhasil mencapai tujuan untuk meningkatkan kualitas rekomendasi film kepada pengguna, serta memberikan dasar yang solid untuk pengembangan dan perbaikan lebih lanjut di masa mendatang.
