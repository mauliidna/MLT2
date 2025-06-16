# Movie Recommendation System
**Sistem Rekomendasi Film Berbasis Content-Based Filtering**
Nama: Maulidina Rahmawati
ID : MC009D5X2352

---

## 🧩 1. Project Overview (Ulasan Proyek)

### Latar Belakang
Dalam era digital saat ini, jumlah konten film yang tersedia di platform streaming terus meningkat exponentially. Pengguna seringkali menghadapi kesulitan dalam menemukan film yang sesuai dengan preferensi mereka dari ribuan pilihan yang tersedia. Fenomena ini dikenal sebagai "information overload" atau kelebihan informasi.

Sistem rekomendasi menjadi solusi yang sangat penting untuk membantu pengguna menemukan konten yang relevan dengan efisien. Netflix, misalnya, melaporkan bahwa 80% konten yang ditonton pengguna berasal dari sistem rekomendasi mereka.

### Pentingnya Proyek
Project ini penting karena:

1. **Meningkatkan User Experience**: Membantu pengguna menemukan film yang sesuai dengan selera mereka tanpa harus mencari secara manual
2. **Efisiensi Waktu**: Menghemat waktu pengguna dalam proses pencarian film
3. **Personalisasi**: Memberikan pengalaman yang dipersonalisasi berdasarkan konten film
4. **Aplikasi Bisnis**: Dapat diimplementasikan pada platform streaming untuk meningkatkan engagement pengguna

### Riset Pendukung
Berdasarkan riset dari McKinsey & Company (2021), sistem rekomendasi dapat meningkatkan engagement pengguna hingga 35% dan meningkatkan revenue hingga 15% pada platform digital entertainment.

---

## 🧠 2. Business Understanding

### Problem Statement
Bagaimana membuat sistem rekomendasi film yang dapat memberikan saran film yang relevan berdasarkan kesamaan konten (genre, overview, dan karakteristik film) dengan akurasi yang tinggi?

### Goals/Tujuan
1. **Membangun sistem rekomendasi** yang dapat memberikan rekomendasi film berdasarkan content similarity
2. **Mencapai precision minimal 90%** dalam memberikan rekomendasi berdasarkan kesamaan genre
3. **Mengoptimalkan diversity** rekomendasi untuk menghindari monotonitas
4. **Mengembangkan interface** yang user-friendly untuk sistem rekomendasi

### Solution Approach

#### 1. Content-Based Filtering (Implementasi Utama)
- **Prinsip**: Merekomendasikan film berdasarkan kesamaan karakteristik/fitur film
- **Fitur yang digunakan**: Genre, overview/sinopsis film
- **Algoritma**: TF-IDF Vectorization + Cosine Similarity
- **Kelebihan**: Tidak memerlukan data rating pengguna, dapat memberikan rekomendasi untuk film baru
- **Kekurangan**: Terbatas pada fitur yang tersedia, sulit untuk memberikan surprise recommendations

#### 2. Collaborative Filtering (Approach Alternatif)
- **Prinsip**: Merekomendasikan berdasarkan preferensi pengguna serupa
- **Kelebihan**: Dapat menemukan pola tersembunyi dalam preferensi pengguna
- **Kekurangan**: Memerlukan data rating/interaksi pengguna yang tidak tersedia dalam dataset ini

**Pilihan Implementasi**: Content-Based Filtering dipilih karena sesuai dengan karakteristik dataset yang tersedia.

---

## 📊 3. Data Understanding

### Informasi Umum Dataset
- **Sumber Data**: [The Movies Dataset - Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset)
- **Lisensi**: CC0-1.0 (Public Domain)

### Variabel/Fitur dalam Dataset

Dataset ini memiliki **24 fitur** yang mendeskripsikan berbagai aspek dari film. Berikut adalah penjelasan lengkap untuk setiap variabel:

| No | Kolom                  | Deskripsi                                                                 | Tipe Data | Missing Values (Count & %)      |
|----|------------------------|---------------------------------------------------------------------------|-----------|----------------------------------|
| 1  | `adult`                | Indikator apakah film untuk dewasa                          | Object    | 0 (0.000%)                       |
| 2  | `belongs_to_collection`| Informasi koleksi/franchise film dalam format JSON                        | Object    | 40,972 (90.116%)                 |
| 3  | `budget`               | Anggaran produksi film dalam USD                                          | Object    | 0 (0.000%)                       |
| 4  | `genres`               | Genre film dalam format JSON                                              | Object    | 0 (0.000%)                       |
| 5  | `homepage`             | URL website resmi film                                                    | Object    | 37,684 (82.884%)                 |
| 6  | `id`                   | ID unik film                                                              | Object    | 0 (0.000%)                       |
| 7  | `imdb_id`              | ID film di IMDb                                                           | Object    | 17 (0.037%)                      |
| 8  | `original_language`    | Bahasa asli film (kode ISO)                                               | Object    | 11 (0.024%)                      |
| 9  | `original_title`       | Judul asli film                                                           | Object    | 0 (0.000%)                       |
| 10 | `overview`             | Sinopsis/ringkasan film                                                   | Object    | 954 (2.098%)                     |
| 11 | `popularity`           | Skor popularitas film                                                     | Object    | 5 (0.011%)                       |
| 12 | `poster_path`          | Path poster film                                                          | Object    | 386 (0.849%)                     |
| 13 | `production_companies` | Perusahaan produksi dalam format JSON                                     | Object    | 3 (0.007%)                       |
| 14 | `production_countries` | Negara produksi dalam format JSON                                         | Object    | 3 (0.007%)                       |
| 15 | `release_date`         | Tanggal rilis film                                                        | Object    | 87 (0.191%)                      |
| 16 | `revenue`              | Pendapatan film dalam USD                                                 | Float64   | 6 (0.013%)                       |
| 17 | `runtime`              | Durasi film dalam menit                                                   | Float64   | 263 (0.578%)                     |
| 18 | `spoken_languages`     | Bahasa yang digunakan dalam format JSON                                   | Object    | 6 (0.013%)                       |
| 19 | `status`               | Status film (Released, Post Production, dll)                              | Object    | 87 (0.191%)                      |
| 20 | `tagline`              | Tagline/slogan film                                                       | Object    | 25,054 (55.105%)                 |
| 21 | `title`                | Judul film                                                                | Object    | 6 (0.013%)                       |
| 22 | `video`                | Indikator apakah ada video trailer                                        | Object    | 6 (0.013%)                       |
| 23 | `vote_average`         | Rating rata-rata film                                                     | Float64   | 6 (0.013%)                       |
| 24 | `vote_count`           | Jumlah votes yang diterima                                                | Float64   | 6 (0.013%)                       |

### Statistik Deskriptif Kolom Numerik:

| Statistik | `revenue`       | `runtime`     | `vote_average` | `vote_count`  |
|-----------|------------------|----------------|-----------------|----------------|
| Count     | 45,460           | 45,203         | 45,460          | 45,460         |
| Mean      | 11,209,350       | 94.13          | 5.62            | 109.90         |
| Std Dev   | 64,332,250       | 38.41          | 1.92            | 491.31         |
| Min       | 0                | 0              | 0.0             | 0              |
| 25%       | 0                | 85             | 5.0             | 3              |
| 50%       | 0                | 95             | 6.0             | 10             |
| 75%       | 0                | 107            | 6.8             | 34             |
| Max       | 2,787,965,000    | 1,256          | 10.0            | 14,075         |

### Fitur Utama untuk Content-Based Filtering
Untuk sistem rekomendasi ini, fitur yang paling relevan adalah:
- **`title`**: Identifikasi film
- **`overview`**: Sinopsis untuk analisis konten
- **`genres`**: Genre untuk kategori film
- **`release_date`**: Informasi temporal
- **`vote_average`**: Kualitas film berdasarkan rating
- **`popularity`**: Tingkat popularitas film

### Insight dari EDA
- **Cakupan Data**: Dataset terdiri dari 45.466 film dengan 24 fitur yang mencakup informasi genre, sinopsis, popularitas, pendapatan, dan lainnya.
- **Missing Value**: Kolom `belongs_to_collection` (90%), `homepage` (83%), dan `tagline` (55%) memiliki banyak data kosong, perlu perlakuan khusus.
- **Fitur Penting untuk Rekomendasi**:
  - `title`: Nama film sebagai identitas
  - `overview`: Sinopsis untuk analisis konten
  - `genres`: Untuk kategorisasi dan kemiripan film
  - `release_date`: Informasi waktu
  - `vote_average`: Kualitas berdasarkan rating
  - `popularity`: Indikator ketertarikan audiens

---
## 🧹 4. DATA PREPARATION

### Tahapan Data Preparation

#### 1. Data Cleaning & Filtering
```python
# Hapus baris dengan missing values pada kolom penting
movies_clean = movies_df.dropna(subset=['title', 'overview'])
```
**Alasan**: Kolom `title` dan `overview` adalah fitur kunci untuk content-based filtering.
**Result**: 
- **Ukuran dataset awal**: 45,466 film
- **Ukuran dataset setelah cleaning**: 44,506 film
- **Data yang dihapus**: 960 film (2.1%)

#### 2. Filter Tahun Rilis
```python
# Filter film dengan tahun rilis yang valid (1900-2024)
movies_clean = movies_clean[(movies_clean['release_year'] >= 1900) & (movies_clean['release_year'] <= 2024)]
```
**Alasan**: Menghilangkan data anomali tahun rilis yang tidak valid atau di luar rentang yang masuk akal.

#### 3. Konversi Tipe Data dan Ekstraksi Tahun
```python
# Konversi release_date ke datetime dan ekstrak tahun
movies_df['release_date'] = pd.to_datetime(movies_df['release_date'], errors='coerce')
movies_df['release_year'] = movies_df['release_date'].dt.year
```
**Alasan**: 
- Mengkonversi string tanggal menjadi format datetime untuk analisis temporal
- Ekstraksi tahun memudahkan analisis distribusi film per tahun dan filtering
- Parameter `errors='coerce'` menangani format tanggal yang tidak valid dengan mengubahnya menjadi NaT

**Result**:
**Ukuran dataset setelah filter tahun**: 44,355 film

**Statistik Deskriptif Kolom Popularitas Film**
- **Jumlah Data (count)**: 45.460
- **Rata-rata (mean)**: 2.92
- **Standar Deviasi (std)**: 6.01
- **Minimum (min)**: 0.00
- **Kuartil 1 (25%)**: 0.39
- **Median (50%)**: 1.13
- **Kuartil 3 (75%)**: 3.68
- **Maksimum (max)**: 547.49

📌 *Insight*: Mayoritas film memiliki skor popularitas rendah (median hanya 1.13), namun ada beberapa outlier dengan popularitas sangat tinggi hingga 547.

### Top 10 Tahun dengan Film Terbanyak
![5b529780-6304-4473-9775-bc1102407493](https://github.com/user-attachments/assets/e8af62ae-6aff-489e-b2ee-e72b6fcc5752)

1. **2015** – 1.905 film  
2. **2014** – 1.974 film  
3. **2013** – 1.889 film  
4. **2012** – 1.722 film  
5. **2011** – 1.667 film  
6. **2016** – 1.604 film  
7. **2009** – 1.586 film  
8. **2010** – 1.501 film  
9. **2008** – 1.473 film  
10. **2007** – 1.320 film  

📌 *Insight*: Produksi film mencapai puncaknya pada tahun 2014–2015.


#### 4. Preprocessing Genre
```python
def extract_genres(genres_str):
    try:
        genres_list = ast.literal_eval(genres_str)
        return [genre['name'] for genre in genres_list]
    except:
        return []
```
**Alasan**: 
- Genre disimpan dalam format JSON string yang perlu dikonversi menjadi list Python
- Ekstraksi nama genre saja (tanpa ID) untuk kemudahan pemrosesan
- Error handling untuk data genre yang tidak valid
**Output**: 
**Top 10 Genre Paling Populer:**
- **Drama**: 20,010 film (45.1%)
- **Comedy**: 12,795 film (28.8%)
- **Thriller**: 7,581 film (17.1%)
- **Romance**: 6,670 film (15.0%)
- **Action**: 6,559 film (14.8%)
- **Horror**: 4,651 film (10.5%)
- **Crime**: 4,268 film (9.6%)
- **Documentary**: 3,843 film (8.7%)
- **Adventure**: 3,468 film (7.8%)
- **Science Fiction**: 3,020 film (6.8%)

![f51ed44c-cc84-4acf-bc87-fcaa36f711ad](https://github.com/user-attachments/assets/b050fe38-3b1c-4537-85e8-0ac618f37ade)

#### 5. Text Preprocessing
```python
def clean_text(text):
    text = re.sub(r'[^a-zA-Z\s]', '', str(text))
    text = text.lower()
    text = ' '.join(text.split())

```
**Alasan**: 
- Menghilangkan noise dalam teks (karakter khusus, angka)
- Standardisasi ke lowercase untuk konsistensi
- Normalisasi spasi untuk menghindari duplikasi token
**Output**: 
- `overview_clean` dan `content_features` (gabungan genre + overview).
- Rata-rata panjang overview: 313 karakter

#### 6. Feature Engineering
**TF-IDF Vectorization**: Mengkonversi teks menjadi vektor numerik
**Representasi Konten Film**

   * Setiap film direpresentasikan dalam bentuk vektor menggunakan **TF-IDF**.
   * TF-IDF (*Term Frequency-Inverse Document Frequency*) mengubah teks (misalnya sinopsis film) menjadi angka sehingga bisa dihitung kemiripannya.

```python
tfidf = TfidfVectorizer(
    max_features=5000,
    stop_words='english',
    ngram_range=(1, 2),
    min_df=2,
    max_df=0.8
)
```
**Alasan**: 
- `max_features=5000`: Membatasi fitur untuk efisiensi komputasi
- `stop_words='english'`: Menghilangkan kata-kata umum yang tidak informatif
- `ngram_range=(1,2)`: Menggunakan unigram dan bigram untuk capture konteks
- `min_df=2`: Menghilangkan kata yang muncul terlalu jarang
- `max_df=0.8`: Menghilangkan kata yang muncul terlalu sering
**Output**: TF-IDF matrix dengan dimensi (44,355, 5,000).

---

## ⚙️ 5. Modeling and Result

### Sistem Rekomendasi Content-Based Filtering

#### Algoritma yang Digunakan
1. **Cosine Similarity**: Mengukur kesamaan antar film
2. **On-Demand Calculation**: Menghitung similarity saat diperlukan untuk efisiensi memori

### Implementasi Model
Dalam sistem rekomendasi film berbasis konten ini, cosine similarity digunakan untuk mengukur tingkat kemiripan antar film berdasarkan informasi yang terkandung di dalamnya. Ketika seorang pengguna memilih sebuah film sebagai referensi, sistem akan membandingkan film tersebut dengan seluruh film lain yang tersedia dalam basis data.

Cosine similarity bekerja dengan menghitung seberapa sejajar arah representasi dua film dalam bentuk vektor. Nilai kemiripan yang dihasilkan berada dalam rentang antara 0 hingga 1, di mana nilai 1 menunjukkan bahwa dua film memiliki tingkat kemiripan yang sangat tinggi, sedangkan nilai 0 menunjukkan bahwa keduanya tidak memiliki kemiripan.

Setelah seluruh skor kemiripan dihitung, sistem akan mengurutkan daftar film dari yang paling mirip hingga yang paling tidak mirip. Beberapa film teratas dengan nilai kemiripan tertinggi kemudian disajikan sebagai rekomendasi kepada pengguna. Pendekatan ini memungkinkan sistem memberikan rekomendasi film yang relevan berdasarkan kesamaan konten, tanpa bergantung pada popularitas atau penilaian pengguna lainnya.

### Testing Sistem Rekomendasi
```python
# Contoh Penggunaan Sistem Rekomendasi Berdasarkan Konten

test_movies = ['Toy Story', 'The Dark Knight', 'Forrest Gump', 'The Matrix']

for movie_title in test_movies:
    if movie_title in movies_clean['title'].values:
        print(f"\n🎬 REKOMENDASI UNTUK: {movie_title}")

        recommendations = get_content_recommendations_ondemand(
            movie_title,
            tfidf_matrix=tfidf_matrix,
            df=movies_clean
        )

        for idx, (_, row) in enumerate(recommendations.head().iterrows(), 1):
            print(f"{idx}. {row['title']} ({row['release_year']:.0f}) - {row['genres_str']}")
```

### 🎬 REKOMENDASI UNTUK: Toy Story
==================================================
📝 Genre: Animation Comedy Family
⭐ Rating: 7.7
📅 Tahun: 1995

🔝 Top 10 Rekomendasi:
1. Banana (2010)
   Genre: Animation Comedy Family
   Rating: 7.2 | Similarity: 0.255

2. Toy Story 2 (1999)
   Genre: Animation Comedy Family
   Rating: 7.3 | Similarity: 0.237

3. Hawaiian Vacation (2011)
   Genre: Animation Family
   Rating: 6.9 | Similarity: 0.231

4. Botsman i Popugay (1982)
   Genre: Animation Comedy Family
   Rating: 7.0 | Similarity: 0.229

5. Mr. Bug Goes to Town (1941)
   Genre: Animation Comedy Family
   Rating: 5.7 | Similarity: 0.223


### 🎬 REKOMENDASI UNTUK: The Dark Knight
==================================================
📝 Genre: Drama Action Crime Thriller
⭐ Rating: 8.3
📅 Tahun: 2008

🔝 Top 10 Rekomendasi:
1. The Dark Knight Rises (2012)
   Genre: Action Crime Drama Thriller
   Rating: 7.6 | Similarity: 0.318

2. Batman Forever (1995)
   Genre: Action Crime Fantasy
   Rating: 5.2 | Similarity: 0.278

3. Batman: The Dark Knight Returns, Part 2 (2013)
   Genre: Action Animation
   Rating: 7.9 | Similarity: 0.270

4. Batman Returns (1992)
   Genre: Action Fantasy
   Rating: 6.6 | Similarity: 0.261

5. Ricochet (1991)
   Genre: Action Crime Thriller
   Rating: 5.9 | Similarity: 0.258


### 🎬 REKOMENDASI UNTUK: Forrest Gump
==================================================
📝 Genre: Comedy Drama Romance
⭐ Rating: 8.2
📅 Tahun: 1994

🔝 Top 10 Rekomendasi:
1. Nigdy w życiu! (2004)
   Genre: Comedy
   Rating: 5.7 | Similarity: 0.292

2. Breaking Up (1997)
   Genre: Comedy Drama Romance
   Rating: 4.0 | Similarity: 0.268

3. Bed of Roses (1933)
   Genre: Comedy Drama Romance
   Rating: 0.0 | Similarity: 0.260

4. For a Handful of Kisses (2014)
   Genre: Drama Romance
   Rating: 5.4 | Similarity: 0.258

5. Night and Fog (2009)
   Genre: Drama
   Rating: 7.6 | Similarity: 0.253


### 🎬 REKOMENDASI UNTUK: The Matrix
==================================================
📝 Genre: Action Science Fiction
⭐ Rating: 7.9
📅 Tahun: 1999

🔝 Top 10 Rekomendasi:
1. Fallout (1998)
   Genre: Action Science Fiction
   Rating: 0.0 | Similarity: 0.329

2. Prince of Space (1959)
   Genre: Action Science Fiction
   Rating: 1.9 | Similarity: 0.293

3. Rollerball (1975)
   Genre: Adventure Action Science Fiction
   Rating: 6.0 | Similarity: 0.275

4. Hooked on the Game 2. The Next Level (2010)
   Genre: Action Science Fiction
   Rating: 5.1 | Similarity: 0.270

5. Battle of the Stars (1978)
   Genre: Science Fiction Action
   Rating: 0.0 | Similarity: 0.270

### Kelebihan dan Kekurangan Pendekatan

#### Kelebihan Content-Based Filtering:
1. **Tidak memerlukan data user**: Dapat bekerja tanpa history pengguna
2. **Explainable**: Mudah dijelaskan mengapa suatu film direkomendasikan
3. **Tidak ada cold start problem**: Dapat merekomendasikan film baru
4. **Konsisten**: Hasil rekomendasi stabil dan dapat diprediksi

#### Kekurangan Content-Based Filtering:
1. **Limited diversity**: Cenderung merekomendasikan film sejenis
2. **Feature dependency**: Kualitas bergantung pada fitur yang tersedia
3. **No serendipity**: Sulit memberikan surprise recommendations
4. **Over-specialization**: Dapat terjebak dalam genre yang sama

---

## 📈 6. Evaluation

### Metrik Evaluasi yang Digunakan

#### 1. Genre Precision
**Definisi**: Proporsi film yang direkomendasikan memiliki setidaknya satu genre yang sama dengan film referensi.

**Formula**:
```
Genre Precision = (Jumlah rekomendasi dengan genre yang sama) / (Total rekomendasi)
```

**Alasan Pemilihan**: Relevan untuk content-based filtering karena genre adalah indikator utama kesamaan konten film.

#### 2. Diversity Score
**Definisi**: Mengukur variasi genre dalam rekomendasi untuk menghindari monotonitas.

**Formula**:
```
Diversity Score = (Jumlah unique genres) / (Total genres dalam rekomendasi)
```

**Alasan Pemilihan**: Penting untuk memastikan rekomendasi tidak terlalu homogen.

### Hasil Evaluasi

#### Performance Metrics
| Metrik | Toy Story | The Dark Knight | Forrest Gump | **Average** |
|--------|-----------|-----------------|--------------|-------------|
| **Genre Precision** | 1.000 | 0.900 | 0.900 | **0.933** |
| **Diversity Score** | 0.148 | 0.357 | 0.273 | **0.259** |
Dataset Coverage: 44,355 film

#### Interpretasi Hasil

**Genre Precision (93.3%)**:
- **Excellent Performance**: Melampaui target 90%
- **Konsistensi Tinggi**: Semua film test mencapai precision ≥ 90%
- **Indikasi**: Sistem berhasil merekomendasikan film dengan genre relevan

**Diversity Score (25.9%)**:
- **Moderate Performance**: Nilai sedang yang menunjukkan trade-off antara relevance dan diversity
- **Interpretasi**: Rekomendasi cukup fokus namun masih memiliki variasi genre
- **Area Improvement**: Dapat ditingkatkan dengan tuning parameter atau hybrid approach

#### Dataset Coverage
- **Total Film**: 44,355 film dalam database
- **Coverage**: Sistem dapat memberikan rekomendasi untuk seluruh film dalam dataset

### Validasi Kualitas
Sistem menunjukkan performa yang sangat baik dalam memberikan rekomendasi yang relevan berdasarkan genre, dengan precision 93.3% yang melampaui target. Meskipun diversity score masih dapat ditingkatkan, hasil ini menunjukkan sistem bekerja sesuai dengan tujuan content-based filtering yang memprioritaskan relevance.

---

## 🗂️ 7. Kesimpulan dan Rekomendasi

### Kesimpulan
1. **Sistem berhasil dibangun** dengan architecture content-based filtering menggunakan TF-IDF dan cosine similarity
2. **Target precision tercapai** dengan skor 93.3% (target: ≥90%)
3. **Efisiensi computational** tercapai dengan on-demand similarity calculation
4. **Interface user-friendly** tersedia dengan fitur pencarian partial matching

### Rekomendasi Pengembangan
1. **Hybrid Approach**: Kombinasi content-based dengan collaborative filtering jika data rating tersedia
2. **Deep Learning**: Implementasi neural collaborative filtering untuk meningkatkan akurasi
3. **Real-time Updates**: Sistem update otomatis saat ada film baru
4. **A/B Testing**: Evaluasi dengan user feedback untuk validasi praktis

### Implementasi Bisnis
Sistem ini siap untuk diimplementasikan pada:
- Platform streaming film
- Website review film
- Aplikasi mobile entertainment
- Sistem internal content management
