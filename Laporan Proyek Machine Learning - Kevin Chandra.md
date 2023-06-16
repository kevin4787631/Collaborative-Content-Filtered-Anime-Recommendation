# Laporan Membuat Model Sistem Rekomendasi - Kevin Chandra

## Project Overview
Berdasarkan salah satu website berjudul [9 Benefits of Watching Anime That Makes You Smarter](https://animemotivation.com/benefits-of-watching-anime/), menonton anime dapat memberikan banyak keuntungan. Salah satunya adalah kita dapat mendapatkan pelajaran hidup dan mempelajari budaya Jepang.

Karena semankin banyaknya peminat anime, tak sedikit pengguna ingin mencari anime yang cocok dengan preferensi pengguna. Ketika pengguna selesai menonton satu seri anime terkenal, banyak yang ingin menonton seri lain karena pengguna sangat menyukai anime tersebut. Oleh sebab itu sistem rekomendasi sangat diperlukan agar pengguna dapat lebih mudah mencari anime kesukaannya.

Studio juga mempunyai peran penting dalam anime. Tak hanya pengguna yang mencari anime kesukaan berdasarkan rekomendasi teman, namun juga memperhatikan studio sebelum menonton sebuah anime. Hal ini disebabkan banyak pengguna yang ingin menonton anime dengan grafik yang bagus dan nyaman untuk ditonton, sehingga tak sedikit pengguna ingin mencari rekomendasi berdasarkan studio kesukaan mereka.

Saya akan menyelesaikan masalah ini dengan *content filtered based* dari rating yang diberikan oleh para pengguna dan *content filtered based recommendation system* yang berasal dari studio anime yang sama. 

## Business Understanding

### Problem Statement
- Bagaimana cara membuat sistem yang dapat merekomendasikan anime dari anime yang pernah ditonton oleh pengguna sebelumnya?
- Bagaimana cara mendapatkan rekomendasi anime yang memiliki studio yang sama?

### Goals
- Dapat merekomendasikan anime dari anime yang pernah ditonton oleh pengguna sebelumnya.
- Dapat merekomendasikan anime yang memiliki studio yang sama.


### Solution Approach
Dalam melaksanakan proyek ini, saya menggunakan dua teknik yaitu:
- **Content Based Filtering**
  Sebelum melanjutkan, saya akan mendefinisikan beberapa istilah:
  - Item merujuk pada konten yang atributnya digunakan dalam model rekomendasi. Contohnya seperti film, dokumen, buku, dan lainnya. Dalam proyek ini saya menggunakan anime.
  - Atribut merujuk pada ciri-ciri sebuah item. Contohnya adalah kalimat dalam dokumen.
  
  *Content-based recommender* bekerja dengan data yang disediakan oleh pengguna, baik secara eksplisit (rating) atau secara implisit (klik pada sebuah link). Berdasarkan data tersebut, sebuah profil pengguna dibuat yang nanti digunakan untuk membuat rekomendasi kepada pengguna. Saat pengguna memberikan lebih banyak masukan atau mengambil tindakan berdasarkan rekomendasi, mesin menjadi lebih dan lebih akurat.

  Rangkuman dari pernyataan di atas dapat dilihat pada gambar berikut:
  ![Rangkuman 1](https://user-images.githubusercontent.com/92379646/140357072-3f4cbe8f-4995-43ce-9710-7fd587ee551a.png)

- **Collaborative Filtering**
  Collaborative Filtering menyaring informasi dengan menggunakan interaksi dan data yang dikumpulkan oleh sistem dari pengguna lain. Hal ini didasarkan pada gagasan bahwa orang-orang yang setuju dalam evaluasi mereka terhadap item tertentu, maka mereka kemungkinan akan setuju lagi di masa depan. Ketika kita ingin mencari film baru untuk ditonton, kita akan sering meminta rekomendasi teman. Tentu saja, kami lebih percaya pada rekomendasi dari teman-teman yang memiliki selera yang sama dengan kami.

  Rangkuman dari pernyataan di atas dapat dilihat pada gambar berikut:
  ![Rangkuman 2](https://user-images.githubusercontent.com/92379646/140371049-bf6d29e0-5a2e-470e-88cd-154daed3a9df.png)

Pada gambar berikut kita dapat melihat perbedaan dari *content-based filtering* dan *collaborative filtering*:
![Perbandingan](https://user-images.githubusercontent.com/92379646/140362739-2aa2fb10-51e0-4c73-a23a-d05d6d69cbdb.png)

## Data Understanding
Dataset untuk proyek ini dapat diunduh pada [Anime Recommendation Database 2020](https://www.kaggle.com/hernan4444/anime-recommendation-database-2020?select=animelist.csv)
Pada dataset kali ini, saya hanya akan menggunakan 2 buah dataset:
**anime.csv**:
- MAL_ID: MyAnimelist ID dari sebuah anime. (contoh: 1)
- Name: nama lengkap dari sebuah anime. (contoh: Cowboy Bebop)
- Score: skor rata-rata dari anime yang diberikan pengguna di MyAnimeList. (contoh: 8.78)
- Genres: Genre dari anime. (contoh: Action, Adventure, Comedy, Drama, Sci-Fi, Space)
- English name: nama lengkap anime dalam Bahasa Inggris. (contoh: Cowboy Bebop)
- Japanese name: nama lengkap anime dalam Bahasa Jepang. (contoh: カウボーイビバップ)
- Type: jenis dari anime. (contoh: TV)
- Episodes: jumlah episode anime. (contoh: 26)
- Aired: tanggal pengumuman. (contoh: Apr 3, 1998 to Apr 24, 1999)
- Premiered: musim ditayangkannya anime. (contoh: Spring 1998)
- Producers: produser dari anime (contoh: Bandai Visual)
- Licensors: pemberi lisensi dari anime (contoh: Funimation, Bandai Entertainment)
- Studios: nama studio dari anime (contoh: Sunrise)
- Source: sumber cerita anime. (e.g Original)
- Duration: durasi anime setiap episode (e.g 24 min. per ep.)
- Rating: tingkat umur (contoh: R - 17+ (violence & profanity))
- Ranked: posisi anime berdasarkan rating pengguna. (e.g 28)
- Popularity: posisi anime berdasarkan jumlah pengguna yang memasukkan anime ke dalam daftar mereka. (e.g 39)
- Members: jumlah anggota komunitas yang terdapat dalam grup anime ini. (contoh: 1251960)
- Favorites: jumlah pengguna yang memberi tanda anime sebagai favorit. (contoh: 61,971)
- Watching: jumlah pengguna yang masih menonton anime. (contoh: 105808)
- Completed: jumlah pengguna yang telah menyelesaikan menonton anime. (contoh: 718161)
- On-Hold: jumlah pengguna yang memberi tanda *on-hold* pada anime. (contoh: 71513)
- Dropped: jumlah pengguna yang berhenti menonton anime sebelum tamat. (contoh: 26678)
- Plan to Watch': jumlah pengguna yang berencana menonton anime. (contoh: 329800)
- Score-10': jumlah pengguna yang memberi skor 10. (contoh: 229170)
- Score-9': jumlah pengguna yang memberi skor 9. (contoh: 182126)
- Score-8': jumlah pengguna yang memberi skor 8. (contoh: 131625)
- Score-7': jumlah pengguna yang memberi skor 7. (contoh: 62330)
- Score-6': jumlah pengguna yang memberi skor 6. (contoh: 20688)
- Score-5': jumlah pengguna yang memberi skor 5. (contoh: 8904)
- Score-4': jumlah pengguna yang memberi skor 4. (contoh: 3184)
- Score-3': jumlah pengguna yang memberi skor 3. (contoh: 1357)
- Score-2': jumlah pengguna yang memberi skor 2. (contoh: 741)
- Score-1': jumlah pengguna yang memberi skor 1. (contoh: 1580)

**Ratings.csv**
- user_id: id pengguna.
- anime_id: - MyAnimelist ID dari anime yang memberikan rating.
- rating: rating yang telah diberikan oleh pengguna.

Berikut adalah visualisasi data yang berasal dari kedua dataset tersebut:
Diagram-diagram di bawah ini merupakan sebagian kecil dari dataset keseluruhan karena jumlah datasetnya sangat banyak.
**Univariate Data Analysis**
- Pie chart 1
  ![Pie chart 1](https://user-images.githubusercontent.com/92379646/140381848-60ebb1c7-421c-4e50-8477-83b23dff18d1.png)

- Pie chart 2
  ![Pie chart 2](https://user-images.githubusercontent.com/92379646/140382336-0b03f7cd-d841-43de-b263-c5400ab58b4c.png)
  Dikarenakan banyaknya nilai unknown dalam dataset tersebut, maka saya melakukan visualisasi lagi setelah data-data unknown dibersihkan. Berikut adalah diagram setelah dibersihkan:
  ![Pie chart 2 clean](https://user-images.githubusercontent.com/92379646/140382576-ad658f5d-6cf0-49ab-b7ee-6d77b6502875.png)

**Multivariate Data Analysis**
![Pair plot](https://user-images.githubusercontent.com/92379646/140382769-c35ec4d0-ec69-4ab6-8c7b-577ddc14c34e.png)

## Data Preparation
Pada tahap ini, saya melakukan dua teknik yaitu:
- **dropna**
  Fungsi dropna digunakan untuk menghilangkan nilai yang kosong atau *null* dan mempastikan apakah baris atau kolom yang mempunyai nilai kosong telah dihapus. Saya menggunakan teknik ini dikarenakan dataset yang saya gunakan kemungkinan mempunyai nilai kosong dan dapat menyebabkan bias.
- **Drop Duplicates**
  Drop dulicates digunakan untuk menghapus data duplikat dalam dataset. Saya menggunakan teknik ini untuk mencegah redundansi pada dataset.

**Content Based Filtering**
Data preparation yang saya gunakan pada *content-based filtering* ada 2, yaitu:
- **Memasukkan data-data yang signifikan ke dalam list**
  Saya menggunakan teknik ini dikarenakan banyaknya kolom data yang tidak diperlukan dalam pengerjaan proyek ini. Jadi saya hanya mengambil beberapa kolom data yang penting dan memasukkannya ke dalam list yang kemudian akan dibuat menjadi dataframe kembali.
- **Membuat dataframe baru dari list sebelumnya**
  Setelah saya membuat list yang menampung kolom-kolom data, saya membuat kembali dataframe menggunakan list tersebut. Saya menggunakan teknik ini karena teknik ini memudahkan saya dibandingkan dengan teknik drop satu persatu, dikarenakan kolom data yang penting hanya berjumlah 4 kolom.

**Collaborative Based Filtering**
- **Enumeration**
  Fungsi enumerate memungkinkan untuk melakukan *loop* terhadap objek iterasi dan memantai berapa banyak iterasi yang telah terjadi. Saya menggunakan teknik ini karena dataset yang saya gunakan kemungkinan mempunyai nilai string, sehingga lebih aman jika saya menggunakan fungsi enumerate untuk mencegah error.
- **Data Splitting**
  Teknik ini digunakan untuk mengevaluasi performa dari algoritma machine learning. Saya menggunakan teknik ini untuk membagi data menjadi training dan testing set. Data yang lebih banyak akan digunakan untuk training set dan data yang lebih sedikit akan digunakan untuk testing set.

## Modeling
**Content Based Filtering**
Modeling pada *content-based filtering*, saya pertama-tama menggunakan TfidfVectorizer untuk mengevaluasi apakah sebuah kata relevan pada sebuah data dalam dataset. Saya melakukan fit pada kolom studio untuk mendapatkan kata-kata yang penting untuk digunakan pada sistem rekomendasi nantinya. Kata-kata ini disebut dengan token. 

Setelah saya mendapatkan token-token tersebut, saya akan menggunakan metode *cosine similarity* untuk mengidentifikasi derajat kesamaan pada token tersebut. 

Kemudian saya akan membuat contoh sistem rekomendasi dengan judul anime terkenal, yaitu Naruto: Shippuuden. Setelah saya mengolah data-data tersebut saya akan mendapatkan hasil rekomendasi sebanyak 5 buah seperti gambar berikut.
![Rekomendasi 1](https://user-images.githubusercontent.com/92379646/140513146-c6aa5eb9-9467-4283-b84f-43f69cd44d38.png)

Kelebihan:
- Model tidak membutuhkan data dari pengguna lain, karena rekomendasinya spesifik kepada penggunanya saja. Hal ini membuat lebih mudah untuk skala jumlah pengguna yang besar.
- Model dapat menangkap minat spesifik penggunam dan dapat merekomendasikan item khusus yang sangat tidak diminati pengguna lain.

Kekurangan:
- Karena representasi fitur dari item direkayasa dengan tangan sampai batas tertentu, teknik ini membutuhkan banyak pengetahuan domain. Oleh karena itu, modelnya hanya bisa sebagus fitur rekayasa tangan.
- Model hanya dapat membuat rekomendasi berdasarkan minat pengguna yang ada. Dengan kata lain, model memiliki kemampuan terbatas untuk memperluas minat pengguna yang ada.

**Collaborative Filtering**
Dalam pembuatan model dalam *collaborative filtering*, saya menggunakan RecommenderNet. Saya melakukan *embed* antara pengguna dan anime ke dalam vektor 50 dimensi.
Model akan menghitung skor kecocokan antara pengguna dan *embedding* anime melalui *dot product*, dan menambahkan bias setiap anime dan setiap pengguna. Skor pertandingan diskalakan ke interval [0, 1] melalui sigmoid.

Setelah selesai membuat fungsi untuk modelnya, saya melakukan *compile* pada model sebanyak 20 *epoch* dan *batch size* sebesar 5. *Compile* ini berfungsi untuk melakukan training pada model dari data setelah dilakukan *data splitting*.

Setelah melakukan training, saya melakukan visualisasi dari *compile* model tersebut dalam bentuk grafik. Gambarnya sebagai berikut:
![Visualisasi](https://user-images.githubusercontent.com/92379646/140517282-bd19aba4-f294-4679-983c-0b16643491ab.png)

Setelah tahap-tahap di atas dilakukan, saya mengambil salah satu user id secara acak dari dataset dan memberikan rekomendasi 10 judul anime dengan rating tertinggi.
Hasil dari rekomendasi tersebut adalah sebagai berikut:
![Rekomendasi 2](https://user-images.githubusercontent.com/92379646/140517645-1e9c5337-748e-4423-96e0-349d97ffb6f0.png)

Kelebihan:
- Model tidak memerlukan pengetahuan domain karena embeddings dipelajari secara otomatis. 
- Model ini dapat membantu pengguna menemukan minat baru. Secara terpisah, sistem ML mungkin tidak mengetahui bahwa pengguna tertarik pada item tertentu, tetapi model mungkin masih merekomendasikannya karena pengguna serupa tertarik pada item tersebut.
- Sistem hanya membutuhkan matriks umpan balik untuk melatih model faktorisasi matriks. Sistem tidak memerlukan fitur kontekstual. Dalam praktiknya, hal ini dapat digunakan sebagai salah satu dari beberapa kandidat generator.

Kekurangan:
- Prediksi model untuk pasangan tertentu (pengguna, item) adalah *dot product* dari *embedding* yang sesuai. Jadi, jika item tidak terlihat selama pelatihan, sistem tidak dapat membuat *embedding* untuk item tersebut dan tidak dapat mengkueri model dengan item ini.
- Sulit untuk menyertakan *side feature* untuk kueri/item. *Side feature* adalah fitur apa pun di luar kueri atau ID item. Sebagai contoh untuk rekomendasi film, *side feature* mungkin menyertakan negara atau usia.

## Evaluation

**Content Based Filtering**
Pada *content-based filtering*, saya menggunakan metrik *precision* sebagai evaluasi model.

Saya akan menjelaskan tahap-tahap yang saya lakukan untuk menghitung presisi tersebut. 

Pertama saya akan mengidentifikasi studio dari anime yang sebelumnya saya sudah ambil sebagai contoh, yaitu *Naruto: Shippuuden*, dan memasukkannya ke dalam variabel *anime_that_have_been_watched_studio*. Kemudian saya akan memasukkan list nama-nama studio dari 5 rekomendasi yang sudah saya dapatkan sebelumnya ke dalam *anime_recommendation_studio*. Setelah itu saya akan membandingkan variabel *anime_that_have_been_watched_studio* dengan *sanime_recommendation_studio* dengan menggunakan for loop. Setiap kesamaan nama studio akan menambahkan variabel real_studio dengan 1. 

Setelah tahap di atas saya lakukan, saya menghitung presisi dari model dengan real_studio/(jumlah rekomendasi)*100. Dari persamaan tersebut saya dapat mendapatkan hasil presisi dari model yang telah saya buat, yaitu 5/5 * 100.  Dengan begitu model yang saya buat mempunyai presisi 100%.

Hasil dari evaluasinya adalah sebagai berikut:
![Evaluasi 1](https://user-images.githubusercontent.com/92379646/140679241-ee557717-8eb7-4cd6-a812-fe9d937b8405.png)

**Collaborative Based Filtering**
Pada *collaborative filtering*, saya akan menggunakan RMSE (Root Mean Squared Error) dalam evaluasi model. RMSE adalah  penilaian kuadrat yang mengukur besarnya rata-rata *error*. Persamaan untuk RMSE diberikan di kedua referensi. Perbedaan antara perkiraan dan nilai yang diamati terkait masing-masing dikuadratkan dan kemudian dirata-ratakan pada sampel. Akhirnya, akar kuadrat dari rata-rata diambil. Karena *error* dikuadratkan sebelum dirata-ratakan, RMSE memberikan bobot yang relatif tinggi untuk *error*. Hal ini berarti RMSE paling berguna ketika *error* yang besar sangat tidak diinginkan.

Sebelum saya memberikan hasil evaluasi, saya akan membahas rumus dari RMSE.
Berdasarkan kalimat sebelumnya, rumus dari RMSE dapat dirangkum pada gambar berikut: 
![Formula](https://user-images.githubusercontent.com/92379646/140523299-1968c5e9-b89d-42fe-8cc3-1c40b86cca9d.png)

Berikut adalah hasil dari evaluasi model menggunakan RMSE dalam bentuk grafik:
![Evaluasi 2](https://user-images.githubusercontent.com/92379646/140523543-8fc972c1-1f5c-4334-8008-3c59fb0397e2.png)