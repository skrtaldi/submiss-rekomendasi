# Laporan Proyek Machine Learning - Moh Aldi Rohmatulloh

## Project Overview
Mahasiswa sebagai bagian dari generasi digital, memiliki akses luas terhadap berbagai bentuk hiburan termasuk anime. Dalam beberapa tahun terakhir, anime telah menjadi salah satu media hiburan terpopuler di kalangan mahasiswa, baik sebagai bentuk pelarian dari tekanan akademik maupun sebagai saran eksplorasi budaya dan nilai nilai sosial. Dengan meningkatnya jumlah konten anime yang tersedia, mahasiswa seringkali kesulitan menemukan anime yang sesuai untuk ditonton kala waktu luang, preferensi genre, dan mood mereka. Banyak dari mereka menghabiskan wkatu cukup lama hanya untuk memilih apa yang akan ditotnon, waktu yang sebenarnya bisa dialokasikan untuk kegiatan produktif lainnya. Mahasiswa membutuhkan hiburan yang efisien dan relevan. Pilihan yang terlalu banyak justru bisa menghambat pengalaman menonton. Sistem rekomendasi yang efektif menjadi semakin penting untuk membantu mahasiswa menemukan konten yang sesuai dengan preferensi mereka. 

Sistem rekomendasi telah menjadi alat penting dalam membantu mahasiswa menavigasi ribuan konten yang tersedia. Dengan menganalisis preferensi mahasiswa dan karakteristik konten, sistem ini dapat memberikan rekomendasi berdasarkan preferensi genre, sehingga dapat meningkatkan kepuasan mahasiswa dan waktu tonton. Dalam konteks anime, sistem rekomendasi dapat membantu mahasiswa menemukan judul-judul yang sesuai dengan selera mereka, bahkan diantara pilihan ribuan yang ada. Sistem rekomendasi terdiri dari beberapa model, termasuk Content-Based Filtering, Collaborative Filtering [^1]. Collaborative filtering memberikan rekomendasi berdasarkan kumpulan dari pendapat, minat dan ketertarikan beberapa user yang biasanya diberikan dalam bentuk rating yang diberikan user kepada suatu item[^2]. Berbeda    dengan Collaborative Filtering, Content-Based Filtering tidak melibatkan pengguna lain dalam menentukan rekomendasi, namun hanya  pengguna itu sendiri. Berdasarkan apa yang dicari user, algoritma ini hanya akan memilih item dengan konten yang mirip untuk direkomendasikan[^3].

## Business Understanding
Setelah memahami latar belakang dan pentingnya permasalahan yang ingin diselesaikan, langkah selanjutnya adalah mengklarifikasi masalah secara lebih terstruktur. Klarifikasi ini bertujuan untuk merumuskan pernyataan masalah yang spesifik, menetapkan tujuan yang ingin dicapai, serta menyusun solusi yang memungkinkan untuk mengatasi permasalahan tersebut

### Problem Statements
- Bagaimana cara memberikan rekomendasi anime yang relevan bagi mahasiswa, dengan mempertimbangkan genre dan pola kesukaan pengguna yang lain?
- Bagaimana dua pendekatan sistem rekomendasi content based dan collaborative filtering dapat dimanfaatkan untuk meningkatkan kualitas rekomendasi?

### Goals
- Menganalisis dataset anime yang tersedia untuk memahami struktut dan karakteristik data
- Membangun model content-based filtering, yang merekemdasikan anime berdasarkan genre dari anime tersebut.
- Membangun model collaborative filtering, yang memanfaatkan data interaksi atau rating pengguna untuk menemukan anime yang disukai pengguna dengan preferensi yang serupa.
- Menguji dan membandingkan performa kedua pendekatan dalam memberikan rekomendasi yang relevan untuk konteks pengguna.
- Menyediakan rekomendasi yang lebih personal dan efisien bagi mahasiswa, agar dapat menemukan tontonan berkualitas tanpa membuang waktu untuk mencari.

### Solution statements
Untuk mencapai tujuan proyek dalam menyediakan sistem rekomdasi anime yang relevan bagi mahasiswa, dua pendekatan algoritma digunakan yaitu, conten based filtering dan collaborative filtering.
- Content Based Filtering, pendekatan ini merekomendasikan anime berdasarkan kemiripan konten, seperti genre, tipe dan nama anime. Sistem ini mengasumsikan bahwa pengguna akan menyukai anime yang memiliki karakteristik serupa dengan yang sebelumnya disukai.
- Collaborative Filtering, pendekayan ini memanfaatkan data rating pengguna untuk merekomendasikan anime. Dalam proyek ini digunakan collaborative filtering berbasis kemiripan anyat anime, jika penguna menyukai anime A, maka sistem akan mencari anime B yang disukai oleh pengguna lain dengan pola yang mirip.
- Menggunakan metrik Root Mean Squared Error (RMSE) yang mengukur seberapa besar perbedaan antara rating yang diprediksi oleh sistem dengan rating aktual dari pengguna.
- Dengan mengeimplementasikan kedua pendekatan ini, sistem dapat dibandingkan dari segi relevansi hasil, performa, dan keterbatasannya masing-masing.

## Data Understanding
Proyek ini menggunakan dua dataset utama yang berkaitan dnegan anime dan interaksi pengguna yaitu anime dan rating yang berkestensi csv. Dataset anime memiliki total 12293 entri dan 7 kolom yang berisi informasi metadata anime seperti anime_id, nama, genre, tipe, episodes, rating, dan members, digunakan untuk content based filtering. Pada dataset anime kolom genre memiliki 62 missing values, kolom type memiliki 25 missing values dan kolom rating memiliki total 230 missing. Sedangkan kolom anime_id, name, episodes dan members memiliki 0 missing values. Dataset rating memiliki total 7813736 entri dan 3 kolom yaitu user_id, anime_id dan rating, digunakan untun collaborative filtering. Pada dataset rating kolom user_id, anime_id dan rating memiliki 0 missing values. Akan tetapi pada kolom rating pada dataset ini terdapat sebuah outlier -1 yang menandakan bahwa anime dengan id tersebut tidak memiliki rating oleh user. Dataset ini dapat diunduh dan dieksplorasi lebih lanjut melalui tautan [Kaggle](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database/data).

### Variabel-variabel anime.csv adalah sebagai berikut:
- anime_id : merupakan id unik untuk setiap judul anime yang dimiliki oleh myanimelist.net
- name : merupakan nama atau judul lengkap dari setiap anime
- genre : merupakan genre dari anime tersebut, genre bisa lebih dari satu dan dipisahkan oleh koma.
- type : merupakan tipe dari anime seperti TV, Movie, OVA, Special, Music.
- episodes : merupakan jumlah episode dari anime, data unknown menandakan bahwa anime tersebut masing on-going.
- rating : merupakan rata-rata rating yang diberikan oleh pengguna
- members : merupakan total pengguna yang menandai anime sebagai sudah ditonton, sedang ditonton, atau akan ditonton.


### Variabel-variabel rating.csv adalah sebagai berikut:
- user_id : merupakan id pengguna yang dibuat secara acak dan tidak dapat teridentifikasi.
- anime_id : merupakan id dari anime yang diberikan rating oleh pengguna.
- rating : merupakan nilai rating yang diberikan user dari 1 sampai dengan 10. Data -1 menandakan bahwa user menonton tapi tidak memberikan rating 

Melakukan tahapan Exploratory Data Analysis(EDA) untuk memahami dataset. Berikut hasil EDA yang sudah dilakukan:
### Distribusi Tipe Anime 
Tahapan ini dilakukan untuk mengetahui distribusi tipe anime. Jumlah total anime dalam dataset tersebut adalah 12294 anime. Setiap anime memiliki tipe. Total dari tipe anime adalah 6 tipe yaitu TV, Movie, Special, Music, OVA dan ONA. Akan tetapi terdapat beberapa anime yang memiliki tipe NaN. Berdasarkan hasil grafik visualisasi, diketahui bahwa:
- TV memiliki total lebih dari 3500 anime
- Movie memiliki total lebih dari 2000 anime 
- OVA memiliki total lebih dari 3000 anime
- Special memiliki total lebih dari 1500 anime
- Music memiliki total kurang dari 500 anime 
- ONA memiliki total lebih dari 500 anime
### Genre Anime
Dari tahapan ini dapat diketahui bahwa jumlah kombinasi genre adalah sebanyak 3265, dan masing masing anime bisa memiliki lebih dari satu genre(multilabel). Kombinasi genre ini dpaat membentuk sebuah identitas unik yang bisa digunakan dalam sistem Content-Based Filtering.
### Members Anime 
Berdasarkan analisis pada kolom members, ditemukan bahwa jumlah anggota (pengguna yang menandai anime sebagai sudah ditonton, sedang ditonton, atau akan ditonton) sangat bervariasi. Anime dengan jumlah member terbanyak memiliki 1.013.917 anggota, yang menunjukkan tingkat popularitas dan jangkauan yang sangat tinggi di kalangan penonton. Di sisi lain, terdapat anime dengan jumlah paling sedikit, yaitu 5 anggota, menandakan bahwa anime tersebut kemungkinan kurang dikenal atau tidak banyak diminati. Variasi yang sangat signifikan ini menunjukkan adanya perbedaan popularitas antar anime, yang dapat dijadikan sebagai indikator tambahan dalam sistem rekomendasi, terutama unutk memahami tren dan preferensi pengguna terhadap anime yang populer.
### Rating 
Berdasarkan analisis pada dataset rating, ditemukan bahwa rating terdiri atas rating 1 sampai dengan 10. Dalam dataset tersebut terdapat data -1 yang menandakan bahwa user dalam data tersebut tidak memberikan rating terhadap anime. Dataset ini mencakup 73.515 pengguna yang memberikan interaksi terhadap 11.200 judul anime yang tersedia. Secara keseluruhan terdapat sebanyak 7.813.737 data rating yang terekam, emnunjukkan volume interaksi yang besar antara pengguna dan konten. Berdasarkan hal tersebut, dataset ini menyediakan fondasi yang kuat untuk membangun sistem rekomendasi berbasis collaborative filtering, yang sangat bergantung pada pola interaksi pengguna.

## Data Preparation
Proses Data preparation yang dilakukan untuk membangun dua buah model untuk membangun sistem rekomendasi ini antara lain:
# Menggabungkan keseluruhan data
Pada tahapan ini dataset rating dan anime digabungkan menggunakan fungsi pd.merge dalam library pandas. Kolom anime_id digunakan sebagai kolom kunci untuk menggabungkan kedua dataset ini yang artinya baris-baris akan dicocokkan berdasarkan nilai dari kolom anime_id yang berada didalam kedua dataset rating dan anime. Jenis join yang digunakan adalah ***left join***, yang berarti data anime akan ditambahkan dengan dataset rating jika nilai anime_id nya sesuai. Tujuan dari dilakukan merge ini adalah untuk menggabungkan data rating dengan informasi anime seperti, judul, genre, type, episodes, rating, dan members. Hasil dari teknik merge ini adalah sebuah dataframe dengan 7813737 entri dan memiliki 9 kolom hasil merge berdasarkan kunci kolom anime_id.
# Menggabungkan Dataset Rating Dengan Nama dan Genre Anime
Pada tahapan ini dataset rating digabungkan dengan nama dan genre anime menggunakan teknik merge. Dataset rating yang berisi informasi rating dari anime berdasarkan anime_id. Dataset tersebut dilakukan proses merge dengan dataset anime yang memiliki informasi terkait metadata anime seperti ***judul, genre, type, episodes, rating dan members***. Dalam case ini, informasi yang dibutuhkan untuk content-based filtering adalah data name yang merupakan judul dan data genre yang merupakan genre anime. Kedua data ini ditambahkan agar dataset rating memiliki informasi tambahan terkait judul dan genre anime. Proses merge ini menggunakan kolom ***anime_id*** sebagai kolom kunci yang berarti data genre dan judul akan ditambahkan dalam dataset rating jika kolom anime_id nya sesuai. Proses ini menggunakan ***left join*** dimana dataset sebelah kiri(rating) akan dipertahankan dan dataset anime dalam case ini judul dan genre akan ditambahkan berdasarkan kolom ***anime_id*** dan jika tidak cocok data akan menjadi NaN. Hasil dari proses ini adalah sebuah dataframe dengan total 7813737 entri dengan 5 kolom yaitu ***user_id, anime_id, rating, judul, dan genre***.
### Mengatasi nilai -1 pada kolom rating
Pada dataset rating.csv, terdapat sebanyak 1.476.596 baris data dengan nilai rating -1 yang menandakan bahwa pengguna belum memberikan penilaian terhadap anime dihapus agar model hanya dilatih pada data yang benar-benar merepresantikan preferensi pengguna. Penghapusan ini dilakukan untuk menjaga kualitas input pada model collaborative filtering, yang sangat bergantung pada data rating eksplisit. Hasil setelah pembersihan terdapat total 6.337.241 rating yang valid dengan jumlah rating 10 dengan distribusi 10, 9, 8, 7, 6, 5, 4, 3, 2, 1. Langkah ini penting untuk memastikan model yang dibangun tidak  dipengaruhi oleh noise atau data yang tidak mewakili preferensi aktual pengguna. Setelah pembersihan, dataset siap digunakan untuk pendekatan collaborative filtering dan dapat digabung dengan metadata anime untuk pendekatan content-based-filtering.
### Menangani Missing Values
Beberapa entri pada kolom name dan genre pada dataframe memiliki nilai kosong. Untuk keperluan cntent-based filtering nilai kosong tersebut dihapus karena jumlahnya tidak terlalu banyak. Proses ini dilakukan untuk menjaminkualitas data sebelum dilakukan tahap modelling.
### Menangani Koma dalam kolom Genre
Kolom genre berisi beberapa genre yang digabung dalam satu string dan dipisahkan dengan koma. Tanda koma dI replace dengan spasi kosong. Hal ini perlu dilakukan dalam pendekatan content-based filtering, informasi genre digunakan untuk mengukur kemiripan antar anime. Oleh karena itu, kolom genre perlu dipersiapkan agar bisa diubah menjadi representasi numerik melalui teknik vektorisasi seperti TF-IDF. Sehingga nantinya, dapat digunakan untuk menyusun sistem rekomendasi berdasarkan kemiripan genre.
### Pembersihan String Unik Kolom Name
Beberapa judul anime mengandung karakter khusus, non alfabetik, atau spasi berlebih. Langkah pembersihan ini dilakukan untuk menghapus atau menormalisasi karakter-karakter tersebut agar tidak mempengaruhi hasil permodelan. TRansformasi yang dilakukan antara lain:
- Menghapus karakter seperti !,? atau tanda berlebihan
- Menghapus spasi berlebih diawal dan diakhir string.
### Menangani Duplikasi Data
Tujuan dilakukan proses ini adalah untuk menghindari dupliaksi output rekomendasi yang sama dan mempersiapkan data agar seragam untuk model berbasis teks atau pencocokan nama. Langkah ini berkontribusi penting dalam menjaga kualitas data dan memastikan sistem rekomendasi bekerja secara optimal, terutama dalam pendekatan content-based yang sangat senditif terhadap pencocokan teks dan fitur deskriptif
### Membuat dataframe untuk content-based
Setelah melakukan pembersihan dan transformasi data pada tahap sebelumnya, dilakukan proses penyusunan ulang dataframe untuk mempersiapkan data yang akan digunakan dalam permodelan sistem rekomendasi content-based. Dataframe baru dibuat untuk menyimpan informasi dari setiap anime yaitu:
- id : ID unik dari setiap anime
- name : Nama judul anime yang telah dibersihkan
- genre : Kumpulan genre yang telah diproses agar dapat diubah menjadi vektor fitur
Dataframe ini menjadi dasar utama dalam pengembangan sistem content-based, karena berisi seluruh informasi dari anime yang akan dibandingkan satu sama lain berdasarkan genrenya.
### Encode User_id
Langkah-langkah yang dilakukan antara lain:
- Membuat daftar unik user_id, dengan mengambil seluruh nilai unik dari kolom user_id dan menyusunnya dalam bentuk list. Hal ini dilakukan untuk memastikan tidak ada duplikasi saat melakukan mapping
- Membuat Dictionary user_to_user_encoded yang memetakan setiap user_id ke angka unik yang dimulai dari 0
-Membuat Reverse Mapping untuk mengembalikan angka hasil encoding ke  user_id aslinya.
Langkah ini dilakukan merupakan bagian penting dalam pengembangan sistem rekomendasi berbasis collaborative filtering. Setiap pengguna perlu direpresentasikan dalam bentuk numerik agar bisa dimasukkan kedalam struktur data seperti user-item matrix atau embedding layer. Oleh karena itu dilakukan proses manual encoding terhadap user_id
### Encode anime_id
Sama seperti user_id, kolom anime_id juga perlu dipresentasikan dalam bentuk numerik agar bisa digunakan dalam proses modeling sistem rekomendasi berbasis collaborative filtering.
- Mengambil nilai unik dari anime_id dan disimpankedalam bentuk list untuk memastikan tidak ada duplikasi. 
- Membuat dictionary untuk mapping. Dictionary anime_to_anime_encoded digunakan untuk mengubah anime_id menjadi angka dari 0 hingga jumlah anime unik. Dictionary anime_encoded_to_anime berfungsi sebagai reverse mapping yaitu untuk mengembalikan angka ke anime_id.
### Mapping dan Encoding 
Tahap ini merupakan bagian penting dalam preparation data untuk sistem rekomendasi, dimana dilakukan transformasi identitas pengguna dan item menjadi format yang dapat diproses oleh model machine learning
- **Mapping User ID ke Format Encoded**, pada tahap ini dilakukan mapping dari user_id ke dalam format encoded yang berupa indeks numerik berurutan, proses ini perlu dilakukan karena dapat menjaga konsistensi format, efisiensi memori dan kompatibilitas model yang dapat memudahkan proses training dan inference pada model collaborative filtering.
- **Mapping Anime ID ke Format Encoded**, sama seperti user id, anime id juga perlu dilakan mapping kedalam format encoded, proses ini bertujuan untuk standarisasi id yang dapat mengoptimalkan proses dan juga menjaga konsistensi dataset dengan memastikan semua anime memeliki representasi numerik yang valid.
- **Analisis dimensi dataset**, proses ini menghitung jumlah pengguna dan anime dalam dataset dan memberikan informasi penting tentang, ukuran matrix yang menentukan dimensi matrix user-anime yang akan dibentuk(num_users*num_anime). Proses ini dapat membantu untuk menjaga kompleksitas model dan dapat memperkirakan kebutuhan memori yang sesuai.
- **Normalisasi Data Rating**, proses ini meliputi konversi tipe data untuk mengubah rating menjadi float 32 supaya memiliki kompatibilitas dengan library deep learning. Selain itu, tipe float 32 juga lebih memiliki efisiensi memori dibandingkan float64 dan memiliki presisi yang cukup untuk perhitungan numerik. Proses selanjutnya adalah analisis range rating untuk menentukan nilai minimum dan maksimum rating yang berguna untuk memvalidasi konsistensi skala rating dan dapat dijadikan referensi dalam interpretasi hasil prediksi dan memudahkan proses normalisasi data jika diperlukan.
- **Summary Statistik Dataset**, proses ini memberikan ringkasan tentang karakteristik dataset yang telah diproses seperti, jumlah pengguna unik yang menunjukkan skala user dalam sistem, jumlah anime unik menunjukkan variasia nime yang tersedia untuk rekomendasi dan range rating yang memberikan informasi terkait skala penilaian yang digunakan.
### Mengatasi nilai -1 pada kolom rating
Pada dataset rating.csv, terdapat sebanyak 1.476.596 baris data dengan nilai rating -1 yang menandakan bahwa pengguna belum memberikan penilaian terhadap anime dihapus agar model hanya dilatih pada data yang benar-benar merepresantikan preferensi pengguna. Penghapusan ini dilakukan untuk menjaga kualitas input pada model collaborative filtering, yang sangat bergantung pada data rating eksplisit.
### Randomisasi Dataset
Tahap ini dilakukan menggunakan parameter ***frac=1*** yang berarti seluruh dataset akan diacak urutannya tanpa mengurangi jumlah data dan parameter ***random_state=42** digunakan untuk memastikan hasil randomisasi yang konsisten setoap kali kode djalankan. Tujuan dilakukan tahapan ini adalah untuk menghilangkan bias urutan yang dapat terjadi karena dataset asli yang memiliki pola tertentu dalam urutannya, sehingga pengacakan diperlukan untuk menghindari bias dalam proses training. Selain itu juga untuk memastikan data traing dan validasi memiliki karakteristik yang serupa dan representatif. 
### Data splitting
Tahap ini bertujuan untuk mempersiapkan data sebelum digunakan dalam pelatihan model sistem rekomendasi. Langkah-langkah yang dilkukan antara lain:
- Menggabungkan data dari kolom user dan anime menjadi sebuah array dua dimensi yang mewakili pasangan antara pengguna dan item yang dinilai.
- Selanjutnya, dilakukan normalisasi pada nilai rating agar seluruh nilai berada dalam rentang 0 hingga 1.
- Setelah itu, dataset dibagi menjadi dua bagian, yaitu 80% untuk data pelatihann dan 20% data validasi.
- Terakhir data input dan hasil normalisasi ditampilkan untuk memastikan bahwa proses transformasi data dilakukan dengan benar.
### Content Based Featur Engineering dengan TF-IDF
TF-IDF(Term Frequency-Inverse Document Frequency) merupakan teknik untuk mengubah teks menjadi representasi numerik dengan mempertimbangkan, ***Term Frequency(TF)*** yang merupakn seberapa sering suatu genre muncul dalam anime tertentu dan ***Inverse Document Frequency*** yaitu seberapa unik suatu genre dalam keseluruhan dataset. Pendekatan ini menggunakan informasi deskriptif dari setiap anime seperti genre untuk merekomendasikan anime yang memiliki kesamaan dengan apa yang pernah disukai oleh pengguna. Dalam implementasinya teknik TF-IDF(Term Frequency-Inverse Document Frequency) diterapkan pada fitur genre untuk mengubah data teks menjadi vektor numerik yang dapat dihitung kesamaaannya menggunakan cosine similarity. 
Tahapan ini diawali dengan menginisialisasi TF-IDF Vectorizer dan menggunakan proses fit() pada kolom genre yang bertujuan untuk:
- Membangun kosakata dari semua genre unik yang ada.
- Menghitung Nilai IDF untuk setiap genre berdasarkan distribusinya dalam dataset
- Melakukan tokenisasi dan normalisasi teks genre.
Tahapan selanjutnya adalah mengekstraksi featur names menggunakan fungsi ***get_feature_names_out()***, fungsi ini mengembalikan daftar semua genre unik yang telah diidentifikasi oleh TF-IDF vectorizer. Tujuan dari tahapan ini adalah untuk:
- Memahami genre apa saja yang menjadi fitur dakam model.
- Mengetahui jumlah dimensi yang akan dihasilkan.
- Memastikan genre yang diekstrak sesuai dengan ekspektasi.
Tahapan selanjutnya adalah transformasi kedalam TF-IDF Matrix menggunakan fungsi ***fit_transform()***. Tujuan dari proses ini adalah untuk menghasilkan matrik dalam format sparse untuk efisiensi memori dimana setiap cell berisi nilai TF-IDF yang mempresentasikan bobot genre setiap anime tertentu. Genre yang awalnya berupa teks kini menjadi vektor numerik. Hasil dari kode ***tf_idf_matrix.shape adalah baris yang merupakan jumlah anime dalam dataset dan kolom merupakan jumlah genre unik yang teridentifikasi.
Tahapan terakhir dalam data proses data ini adalah visualisasi TF-IDF Matrix. Fungsi ***todense()*** digunakan untuk mengkonversi ke dense matrix untuk kemudahan visualisasi. Tahapan ini membuat sebuah dataframe dengan menggunakan nama genre sebagai kolom dan nama anime sebagai index baris sehingga memudahkan interpretasi hubungan anime-genre. Kode ***sample(20, axis=1)*** yang mengambil 20 genre secara random sebagai kolom dan  ***sample(10, axis=0)*** mengambil 10 anime secara random sebagai baris.
### Perhitungan Cosine-Similarity
Setelah mendapatkan representasi TF-IDF dari genre anime, langkah selanjutnya adalah menghitung similarity antar anime untuk mendukung content-based recomendation menggunakan cosine similarity. Cosine Similarity mengukur kesamaan antara dua vektor berdasarkan sudut yang dibentuk antar keduanya. Range nilai dari proses ini adalah antara 0 hingga 1 dengan interpretasi nilai mendekati 1 berarti anime memiliki genre yang mirip. Proses ini diawali dengan inisialisasi variabel cosine_sim. Kemudian hasil perhitungan di konversi menjadi dataframe ***cosine_sim_df*** dengan output yang menunjukkan baris dan kolom yang merupakan jumlah anime dalam dataset dan total cells yang merupakan kombinasi pasangan anime. Langkah selanjutnya adalah menggunakan sampling dengan tujuan memilih 5 anime secara random sebagai pembanding dan memilih 10 anime secara random sebagai analiss. Hasil dari proses ini dapat memberikan gambaran distribusi similarity tanpa overwhelm. 

## Modeling
### Content-Based Filtering
Content-Based Filtering adalah pendekatan sistem rekomendasi yang memberikan rekomendasi berdasarkan karakteristik atau fitur dari item itu sendiri. Dalam konteks rekomendasi anime, sistem ini menganalisis atribut anime seperti genre dan judul untuk mencari kesamaan antar anime. Pendekatan ini bekerja dengan asumsi bahwa jika seorang pengguna menyukai anime dengan karakteristik tertentu, maka pengguna tersebut kemungkinan besar akan menyukai anime lain yang memiliki karakteristik serupa. Kelebihan dari content-based filtering adalah kemampuannya dalam memberikan rekomendasi yang sangat personal dan tidak memerlukan data dari pengguna lain, sehingga tetap efektif meskipun jumlah penggunanya terbatas. Selain itu, metode ini dapat merekomendasikan item baru selama informasi kontennya tersedia, serta kemampuannya menangani cold-start pada pengguna baru. Namun pendekatan ini juga memiliki kekurangan, seperti kecenderungan hanya merekomendasikan anime yang mirip dengan yang sudah pernah disukai, yang berpotensi dapat membatasi keberagama rekomendasi. Metode ini juga sangat bergantung pada kelengkapan dan kualitas fitur dari item.

Fungsi anime_recommendations() dirancang untuk menghasilkan Top-K rekomendasi anime berdasarkan kemiripan konten. Fungsi ini menggunakan nilai kemiripan antar anime yang telah dihitung sebelumnya dan disimpan dalam sebuah dataframe similarity_data, yang umumnya diperoleh melalui perhitungan cosine similarity terhadap fitur genre. Parameter nama_anime digunakan sebagai input untuk menentukan item referensi, sedangkan parameter k menentukan jumlah rekomendasi yang ingin ditampilkan. Proses pencarian dilakukan dengan mengambil indeks dari K item terdekat berdasarkan nilai kemiripan tertinggi, kemudian hasilnya disaring agar tidak menyertakan anime yang sama dengan input. Daftar anime yang paling mirip kemudian digabungkan dengan data asli (items) untuk menampilkan informasi tambahan seperti nama dan genre. Fungsi ini mengembalikan hasil dalam bentuk dataframe yang berisi rekomendasi anime yang secara konten paling mirip dengan anime yang diberikan oleh pengguna.

Berikut hasil untuk Top-5 Rekomendasi Anime Berdasarkan 'Ohisama to Kaeru'

| No | Nama Anime               | Genre   |
|----|--------------------------|---------|
| 1  | Forestry                 | Comedy  |
| 2  | Marie amp Gali Special   | Comedy  |
| 3  | Neko Ramen              | Comedy  |
| 4  | Barakamon Mijikamon     | Comedy  |
| 5  | Ketsuekigatakun         | Comedy  |

### Collaborative Filtering
Model sistem rekomendasi tahap ini dibangun menggunakan pendekatan deep learning dengan memanfaatkan arsitektur berbasis embedding layer, yang diimplementasikan dalam kelas RecommenderNet. Model ini dinisialisasi dengan parameter num_users, num_anime, dan dimensi embedding sebanyak 50. Untuk proses training, model dicompile menggunakan fungsi loss Binnary Crossentropy yang umum digunakan ketika target output telah dinormalisasi dalam rentang 0 hingga 1. Optimizer yang digunakan Adam dengan learning rate 0.001. Sebagai metrik evaluasi, digunakan Root Mean Squared Error (RMSE) untuk mengukur sejauh mana prediksi model mendekati nilai target dalam skala aslinya. Model kemudian dilatih menggunakan data latih x_train dan y_train dengan batch size 8 selama 1 epoch, dan divalidasi menggunakan data x_val dan y_val. Meskipun hanya dilakukan pelatihan selama satu epoch untuk tahap awal, proses ini bertujuan untuk mengevaluasi kinerja awal model dan memastikan bahwa arsitektur dan pipeline pelatihan telah berjalan dengan benar sebelum melakukan pelatihan lebih lanjut.

Sistem ini memanfaatkan data interaksi pengguna dan anime dalam bentuk rating, kemudian menghitung kemiripan antar pengguna untuk memberikan rekomendasi berdasarkan pola perilaku yang serupa. Top-N anime yang ditampilkan merupakan hasil dari prediksi preferensi pengguna berdasarkan kesamaan dengan pengguna atau anime lain. Kelebihan pendekatn ini adalah kemampuannya menemukan rekomendasia yang lebih bergam dan tidak terbatas pada konten serupa. Namun kelemhan utam metode ini adalah ketergantungannya pada data interaksi yang cukup besar. Jika terdapat pengguna atau item baru yang belum memiliki riwayat interaksi, sistem ini akan mengalami kesulitan memberikan rekomendasi yang akurat(cold-start).

## Showing Recommendations for User: 8643

## Anime with High Ratings from User
Berikut adalah daftar anime yang mendapatkan rating tinggi dari pengguna:

- **Naruto**  
  *Genres:* Action, Comedy, Martial Arts, Shounen, Super Power

- **Steins;Gate Movie: Fuka Ryouiki no Déjà vu**  
  *Genres:* Sci-Fi, Thriller

- **Mirai Nikki (TV)**  
  *Genres:* Action, Mystery, Psychological, Shounen, Supernatural, Thriller

- **Bakemonogatari**  
  *Genres:* Mystery, Romance, Supernatural, Vampire

- **Suzumiya Haruhi no Shoushitsu**  
  *Genres:* Comedy, Mystery, Romance, School, Sci-Fi, Supernatural

---

## Top 10 Anime Recommendations
Berikut adalah rekomendasi anime terbaik untuk pengguna:

1. **Fullmetal Alchemist: Brotherhood**  
   *Genres:* Action, Adventure, Drama, Fantasy, Magic, Military, Shounen

2. **Gintama**  
   *Genres:* Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen

3. **Gintama°**  
   *Genres:* Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen

4. **Gintama Movie: Kanketsu-hen - Yorozuya yo Eien Nare**  
   *Genres:* Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen

5. **Gintama°: Enchousen**  
   *Genres:* Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen

6. **Hunter x Hunter (2011)**  
   *Genres:* Action, Adventure, Shounen, Super Power

7. **Rurouni Kenshin: Meiji Kenkaku Romantan - Tsuiokuhen**  
   *Genres:* Action, Drama, Historical, Martial Arts, Romance, Samurai

8. **Haikyuu!!: Karasuno Koukou VS Shiratorizawa Gakuen Koukou**  
   *Genres:* Comedy, Drama, School, Shounen, Sports

9. **Gintama**  
   *Genres:* Action, Comedy, Historical, Parody, Samurai, Sci-Fi, Shounen

10. **Ginga Eiyuu Densetsu**  
    *Genres:* Drama, Military, Sci-Fi, Space

## Evaluation

Sebagai metrik evaluasi, digunakan Root Mean Squared Error (RMSE) untuk mengukur sejauh mana prediksi model mendekati nilai target dalam skala aslinya. Model kemudian dilatih menggunakan data latih x_train dan y_train dengan batch size 8 selama 1 epoch, dan divalidasi menggunakan data x_val dan y_val. Meskipun hanya dilakukan pelatihan selama satu epoch untuk tahap awal, proses ini bertujuan untuk mengevaluasi kinerja awal model dan memastikan bahwa arsitektur dan pipeline pelatihan telah berjalan dengan benar sebelum melakukan pelatihan lebih lanjut. **Root Mean Squared Error (RMSE)** mengukur seberapa besar rata-rata kesalahan antara nilai yang diprediksi oleh model dan nilai aktual. RMSE memberikan penalti lebih besar untuk kesalahan prediksi yang besar karena penggunaan kuadrat dari selisih.

### Formula
$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} \left( y_i - \hat{y}_i \right)^2}
$$

**Keterangan:**
- \( y_i \): rating aktual dari pengguna  
- \( \hat{y}_i \): rating yang diprediksi oleh model  
- \( n \): jumlah total prediksi

Semakin kecil nilai RMSE, maka semakin dekat prediksi model dengan nilai aktual. Model dilatih menggunakan `BinaryCrossentropy` sebagai fungsi loss, namun untuk evaluasi, digunakan **RMSE** sebagai metrik tambahan untuk mengetahui seberapa akurat model memprediksi rating terhadap data validasi.

Epoch | Loss (Train) | RMSE (Train) | Val Loss | RMSE (Val) |
|-------|--------------|--------------|----------|------------|
| 1     | 0.4849       | 0.1229       | 0.4758   | 0.1116     |

Training RMSE sebesar 0.1229 menunjukkan bahwa model mampu mempelajari pola data dengan cukup baik dalam 1 epoch pelatihan. Validation RMSE sebesar 0.1116 menunjukkan generalisasi model terhadap data yang belum pernah dilihat cukup baik, dengan error prediksi yang relatif rendah.

## Referensi
- [^1] Ardiansyah, R., Ari Bianto, M., & Saputra, B. D. (2023). Sistem Rekomendasi Buku Perpustakaan Sekolah menggunakan Metode Content-Based Filtering. Jurnal CoSciTech (Computer Science and Information Technology), 4(2), 510-518.
- [^2] AE Wijaya, D Alfian - Jurnal Computech & Bisnis, 2018 - academia.edu
- [^3]Larasati, F. B. A., & Februariyanti, H. (2021). SISTEM REKOMENDASI PRODUCT EMINA COSMETICS DENGAN MENGGUNAKAN METODE CONTENT - BASED FILTERING. Jurnal Manajemen Informatika Dan Sistem Informasi, 4(1), 45–54.
