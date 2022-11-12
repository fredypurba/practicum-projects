# Project 1 - Musik di Kota Besar

# Konten <a id='back'></a>

* [Pendahuluan](#intro)
* [Tahap 1. Ikhtisar Data](#data_review)
    * [Kesimpulan](#data_review_conclusions)
* [Tahap 2. Pra-pemrosesan data](#data_preprocessing)
    * [2.1 Gaya Penulisan Judul](#header_style)
    * [2.2 Nilai-Nilai yang Hilang](#missing_values)
    * [2.3 Duplikat](#duplicates)
    * [2.4 Kesimpulan](#data_preprocessing_conclusions)
* [Tahap 3. Menguji Hipotesis](#hypotheses)
    * [3.1 Hipotesis 1: aktivitas pengguna di dua kota](#activity)
    * [3.2 Hipotesis 2: preferensi musik pada hari Senin dan Jumat](#week)
    * [3.3 Hipotesis 3: preferensi genre di kota Springfield dan Shelbyville](#genre)
* [Temuan](#end)

## Pendahuluan <a id='intro'></a>
Setiap kali kita melakukan penelitian, kita perlu merumuskan hipotesis yang kemudian dapat kita uji. Terkadang kita menerima hipotesis ini; tetapi terkadang kita juga menolaknya. Untuk membuat keputusan yang tepat, sebuah bisnis harus dapat memahami apakah asumsi yang dibuatnya benar atau tidak.

Dalam proyek kali ini, Anda akan membandingkan preferensi musik di kota Springfield dan Shelbyville. Anda akan mempelajari data Y.Music yang sebenarnya untuk menguji hipotesis di bawah ini dan membandingkan perilaku pengguna di kedua kota ini.

### Tujuan: 
Menguji tiga hipotesis:
1. Aktivitas pengguna berbeda-beda tergantung pada hari dan kotanya.
2. Pada senin pagi, penduduk Springfield dan Shelbyville mendengarkan genre yang berbeda. Hal ini juga ini juga berlaku untuk Jumat malam.
3. Pendengar di Springfield dan Shelbyville memiliki preferensi yang berbeda. Di Springfield, mereka lebih suka musik pop, sementara Shelbyville, musik rap memiliki lebih banyak penggemar.

### Tahapan
Data tentang perilaku pengguna disimpan dalam berkas `/datasets/music_project_en.csv`. Tidak ada informasi tentang kualitas data, jadi Anda perlu memeriksanya lebih dahulu sebelum menguji hipotesis.

Pertama, Anda akan mengevaluasi kualitas data dan melihat apakah masalahnya signifikan. Kemudian, selama pra-pemrosesan data, Anda akan mencoba memperhitungkan masalah yang paling serius.
 
Proyek ini akan terdiri dari tiga tahap:
 1. Ikhtisar Data
 2. Pra-pemrosesan Data
 3. Menguji Hipotesis

 
[Kembali ke Daftar Isi](#back)

## Tahap 1. Ikhtisar Data <a id='data_review'></a>

Buka data di Y.Music lalu jelajahi data yang ada di sana.

Anda akan membutuhkan `Pandas`, jadi Anda harus mengimpornya.


```python
import pandas as pd
```

Baca file `music_project_en.csv` dari folder `/datasets/` lalu simpan di variabel `df`:


```python
pd.read_csv("/datasets/music_project_en.csv")

df = pd.read_csv("/datasets/music_project_en.csv")

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>userID</th>
      <th>Track</th>
      <th>artist</th>
      <th>genre</th>
      <th>City</th>
      <th>time</th>
      <th>Day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>65074</th>
      <td>729CBB09</td>
      <td>My Name</td>
      <td>McLean</td>
      <td>rnb</td>
      <td>Springfield</td>
      <td>13:32:28</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>65075</th>
      <td>D08D4A55</td>
      <td>Maybe One Day (feat. Black Spade)</td>
      <td>Blu &amp; Exile</td>
      <td>hip</td>
      <td>Shelbyville</td>
      <td>10:00:00</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>65076</th>
      <td>C5E3A0D5</td>
      <td>Jalopiina</td>
      <td>NaN</td>
      <td>industrial</td>
      <td>Springfield</td>
      <td>20:09:26</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65077</th>
      <td>321D0506</td>
      <td>Freight Train</td>
      <td>Chas McDevitt</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>21:43:59</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65078</th>
      <td>3A64EF84</td>
      <td>Tell Me Sweet Little Lies</td>
      <td>Monica Lopez</td>
      <td>country</td>
      <td>Springfield</td>
      <td>21:59:46</td>
      <td>Friday</td>
    </tr>
  </tbody>
</table>
<p>65079 rows × 7 columns</p>
</div>



Tampilkan 10 baris tabel pertama:


```python
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>userID</th>
      <th>Track</th>
      <th>artist</th>
      <th>genre</th>
      <th>City</th>
      <th>time</th>
      <th>Day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>5</th>
      <td>842029A1</td>
      <td>Chains</td>
      <td>Obladaet</td>
      <td>rusrap</td>
      <td>Shelbyville</td>
      <td>13:09:41</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>6</th>
      <td>4CB90AA5</td>
      <td>True</td>
      <td>Roman Messer</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>13:00:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>7</th>
      <td>F03E1C1F</td>
      <td>Feeling This Way</td>
      <td>Polina Griffith</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>20:47:49</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8FA1D3BE</td>
      <td>L’estate</td>
      <td>Julia Dalia</td>
      <td>ruspop</td>
      <td>Springfield</td>
      <td>09:17:40</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>9</th>
      <td>E772D5C0</td>
      <td>Pessimist</td>
      <td>NaN</td>
      <td>dance</td>
      <td>Shelbyville</td>
      <td>21:20:49</td>
      <td>Wednesday</td>
    </tr>
  </tbody>
</table>
</div>



Memperoleh informasi umum tentang tabel dengan satu perintah:


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 65079 entries, 0 to 65078
    Data columns (total 7 columns):
     #   Column    Non-Null Count  Dtype 
    ---  ------    --------------  ----- 
     0     userID  65079 non-null  object
     1   Track     63736 non-null  object
     2   artist    57512 non-null  object
     3   genre     63881 non-null  object
     4     City    65079 non-null  object
     5   time      65079 non-null  object
     6   Day       65079 non-null  object
    dtypes: object(7)
    memory usage: 3.5+ MB


Tabel ini berisi tujuh kolom. Semuanya menyimpan tipe data yang sama, yaitu: `object`.

Berdasarkan dokumentasi:
- `'userID'` — pengenal pengguna
- `'Track'` — judul trek
- `'artist'` — nama artis
- `'genre'`
- `'City'` — kota tempat pengguna berada
- `'time'` — lama waktu lagu tersebut dimainkan
- `'Day'` — nama hari

Kita dapat melihat tiga masalah dengan gaya penulisan nama kolom:
1. Beberapa nama huruf besar, beberapa huruf kecil.
2. Ada penggunaan spasi pada beberapa nama.
3. `Beberapa kata harus dipisahkan satu sama lain dengan simbol garis bawah`.

Jumlah nilai kolom berbeda. Ini berarti data mengandung nilai yang hilang.


### Kesimpulan <a id='data_review_conclusions'></a> 

Setiap baris dalam tabel menyimpan data pada judul trek yang diputar. Beberapa kolom menggambarkan lagu itu sendiri: judul trek, artis, dan genre. Sisanya menyampaikan informasi tentang pengguna: kota asal mereka, waktu mereka memutar lagu.

Jelas bahwa data tersebut cukup untuk menguji hipotesis. Namun, ada nilai-nilai yang hilang.

Selanjutnya, kita perlu melakukan pra-pemrosesan data terlebih dahulu.

[Kembali ke Daftar Isi](#back)

## Tahap 2. Pra-pemrosesan Data <a id='data_preprocessing'></a>
Perbaiki format pada judul kolom dan atasi nilai yang hilang. Kemudian, periksa apakah ada duplikat dalam data.

### Gaya Penulisan Judul <a id='header_style'></a>
Tampilkan judul kolom:



```python
(df.columns)
```




    Index(['  userID', 'Track', 'artist', 'genre', '  City  ', 'time', 'Day'], dtype='object')



Ubah nama kolom sesuai dengan aturan gaya penulisan yang baik:
* Jika nama memiliki beberapa kata, gunakan snake_case
* Semua karakter harus menggunakan huruf kecil
* Hapus spasi


```python
df = df.rename(columns={"  userID": "user_id", "Track": "track", "  City  ": "city", "Day": "day",})

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>track</th>
      <th>artist</th>
      <th>genre</th>
      <th>city</th>
      <th>time</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>65074</th>
      <td>729CBB09</td>
      <td>My Name</td>
      <td>McLean</td>
      <td>rnb</td>
      <td>Springfield</td>
      <td>13:32:28</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>65075</th>
      <td>D08D4A55</td>
      <td>Maybe One Day (feat. Black Spade)</td>
      <td>Blu &amp; Exile</td>
      <td>hip</td>
      <td>Shelbyville</td>
      <td>10:00:00</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>65076</th>
      <td>C5E3A0D5</td>
      <td>Jalopiina</td>
      <td>NaN</td>
      <td>industrial</td>
      <td>Springfield</td>
      <td>20:09:26</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65077</th>
      <td>321D0506</td>
      <td>Freight Train</td>
      <td>Chas McDevitt</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>21:43:59</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65078</th>
      <td>3A64EF84</td>
      <td>Tell Me Sweet Little Lies</td>
      <td>Monica Lopez</td>
      <td>country</td>
      <td>Springfield</td>
      <td>21:59:46</td>
      <td>Friday</td>
    </tr>
  </tbody>
</table>
<p>65079 rows × 7 columns</p>
</div>



Periksa hasilnya. Tampilkan nama kolom sekali lagi:


```python
(df.columns)
```




    Index(['user_id', 'track', 'artist', 'genre', 'city', 'time', 'day'], dtype='object')



[Kembali ke Daftar Isi](#back)

### Nilai-Nilai yang Hilang <a id='missing_values'></a>
Pertama, temukan jumlah nilai yang hilang dalam tabel. Untuk melakukannya, gunakan dua metode `Pandas`:


```python
(df.isna().sum())
```




    user_id       0
    track      1343
    artist     7567
    genre      1198
    city          0
    time          0
    day           0
    dtype: int64



Tidak semua nilai yang hilang berpengaruh terhadap penelitian. Misalnya, nilai yang hilang dalam `track` dan `artist` tidak begitu penting. Anda cukup menggantinya dengan penanda yang jelas.
Namun nilai yang hilang dalam `'genre'` dapat memengaruhi perbandingan preferensi musik di Springfield dan Shelbyville. Dalam kehidupan nyata, sangatlah berguna untuk mempelajari alasan mengapa data tersebut hilang dan mencoba memperbaikinya. Tetapi kita tidak memiliki kesempatan itu dalam proyek ini. Jadi Anda harus:
* Isi nilai yang hilang ini dengan sebuah penanda
* Evaluasi seberapa besar nilai yang hilang dapat memengaruhi perhitungan Anda

Ganti nilai yang hilang pada `'track'`, `'artist'`, dan `'genre'` dengan string `'unknown'`. Untuk melakukannya, buat list `columns_to_replace`, lakukan *loop* dengan `for`, dan ganti nilai yang hilang di setiap kolom:


```python
columns_to_replace = ['track', 'genre', 'artist']
for columns in columns_to_replace:
    df[columns] = df[columns].fillna('unknown')

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>track</th>
      <th>artist</th>
      <th>genre</th>
      <th>city</th>
      <th>time</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>65074</th>
      <td>729CBB09</td>
      <td>My Name</td>
      <td>McLean</td>
      <td>rnb</td>
      <td>Springfield</td>
      <td>13:32:28</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>65075</th>
      <td>D08D4A55</td>
      <td>Maybe One Day (feat. Black Spade)</td>
      <td>Blu &amp; Exile</td>
      <td>hip</td>
      <td>Shelbyville</td>
      <td>10:00:00</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>65076</th>
      <td>C5E3A0D5</td>
      <td>Jalopiina</td>
      <td>unknown</td>
      <td>industrial</td>
      <td>Springfield</td>
      <td>20:09:26</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65077</th>
      <td>321D0506</td>
      <td>Freight Train</td>
      <td>Chas McDevitt</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>21:43:59</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>65078</th>
      <td>3A64EF84</td>
      <td>Tell Me Sweet Little Lies</td>
      <td>Monica Lopez</td>
      <td>country</td>
      <td>Springfield</td>
      <td>21:59:46</td>
      <td>Friday</td>
    </tr>
  </tbody>
</table>
<p>65079 rows × 7 columns</p>
</div>



Pastikan tidak ada tabel lagi yang berisi nilai yang hilang. Hitung kembali nilai yang hilang.


```python
(df.isna().sum())
```




    user_id    0
    track      0
    artist     0
    genre      0
    city       0
    time       0
    day        0
    dtype: int64



[Kembali ke Daftar Isi](#back)

### Duplikat <a id='duplicates'></a>
Temukan jumlah duplikat eksplisit dalam tabel menggunakan satu perintah:


```python
(df.duplicated().sum())
```




    3826



Panggil metode `Pandas` untuk menghapus duplikat eksplisit:


```python
df = df.drop_duplicates().reset_index(drop=True)
```

Hitung duplikat eksplisit sekali lagi untuk memastikan Anda telah menghapus semuanya:


```python
(df.duplicated().sum())
```




    0



Sekarang hapus duplikat implisit di kolom `genre`. Misalnya, nama genre dapat ditulis dengan cara yang berbeda. Kesalahan seperti ini juga akan memengaruhi hasil.

Tampilkan daftar nama genre yang unik, urutkan berdasarkan abjad. Untuk melakukannya:
* Ambil kolom DataFrame yang dimaksud
* Terapkan metode pengurutan untuk itu
* Untuk kolom yang diurutkan, panggil metode yang akan menghasilkan semua nilai kolom yang unik


```python
(sorted(df['genre'].unique()))
```




    ['acid',
     'acoustic',
     'action',
     'adult',
     'africa',
     'afrikaans',
     'alternative',
     'ambient',
     'americana',
     'animated',
     'anime',
     'arabesk',
     'arabic',
     'arena',
     'argentinetango',
     'art',
     'audiobook',
     'avantgarde',
     'axé',
     'baile',
     'balkan',
     'beats',
     'bigroom',
     'black',
     'bluegrass',
     'blues',
     'bollywood',
     'bossa',
     'brazilian',
     'breakbeat',
     'breaks',
     'broadway',
     'cantautori',
     'cantopop',
     'canzone',
     'caribbean',
     'caucasian',
     'celtic',
     'chamber',
     'children',
     'chill',
     'chinese',
     'choral',
     'christian',
     'christmas',
     'classical',
     'classicmetal',
     'club',
     'colombian',
     'comedy',
     'conjazz',
     'contemporary',
     'country',
     'cuban',
     'dance',
     'dancehall',
     'dancepop',
     'dark',
     'death',
     'deep',
     'deutschrock',
     'deutschspr',
     'dirty',
     'disco',
     'dnb',
     'documentary',
     'downbeat',
     'downtempo',
     'drum',
     'dub',
     'dubstep',
     'eastern',
     'easy',
     'electronic',
     'electropop',
     'emo',
     'entehno',
     'epicmetal',
     'estrada',
     'ethnic',
     'eurofolk',
     'european',
     'experimental',
     'extrememetal',
     'fado',
     'film',
     'fitness',
     'flamenco',
     'folk',
     'folklore',
     'folkmetal',
     'folkrock',
     'folktronica',
     'forró',
     'frankreich',
     'französisch',
     'french',
     'funk',
     'future',
     'gangsta',
     'garage',
     'german',
     'ghazal',
     'gitarre',
     'glitch',
     'gospel',
     'gothic',
     'grime',
     'grunge',
     'gypsy',
     'handsup',
     "hard'n'heavy",
     'hardcore',
     'hardstyle',
     'hardtechno',
     'hip',
     'hip-hop',
     'hiphop',
     'historisch',
     'holiday',
     'hop',
     'horror',
     'house',
     'idm',
     'independent',
     'indian',
     'indie',
     'indipop',
     'industrial',
     'inspirational',
     'instrumental',
     'international',
     'irish',
     'jam',
     'japanese',
     'jazz',
     'jewish',
     'jpop',
     'jungle',
     'k-pop',
     'karadeniz',
     'karaoke',
     'kayokyoku',
     'korean',
     'laiko',
     'latin',
     'latino',
     'leftfield',
     'local',
     'lounge',
     'loungeelectronic',
     'lovers',
     'malaysian',
     'mandopop',
     'marschmusik',
     'meditative',
     'mediterranean',
     'melodic',
     'metal',
     'metalcore',
     'mexican',
     'middle',
     'minimal',
     'miscellaneous',
     'modern',
     'mood',
     'mpb',
     'muslim',
     'native',
     'neoklassik',
     'neue',
     'new',
     'newage',
     'newwave',
     'nu',
     'nujazz',
     'numetal',
     'oceania',
     'old',
     'opera',
     'orchestral',
     'other',
     'piano',
     'pop',
     'popelectronic',
     'popeurodance',
     'post',
     'posthardcore',
     'postrock',
     'power',
     'progmetal',
     'progressive',
     'psychedelic',
     'punjabi',
     'punk',
     'quebecois',
     'ragga',
     'ram',
     'rancheras',
     'rap',
     'rave',
     'reggae',
     'reggaeton',
     'regional',
     'relax',
     'religious',
     'retro',
     'rhythm',
     'rnb',
     'rnr',
     'rock',
     'rockabilly',
     'romance',
     'roots',
     'ruspop',
     'rusrap',
     'rusrock',
     'salsa',
     'samba',
     'schlager',
     'self',
     'sertanejo',
     'shoegazing',
     'showtunes',
     'singer',
     'ska',
     'slow',
     'smooth',
     'soul',
     'soulful',
     'sound',
     'soundtrack',
     'southern',
     'specialty',
     'speech',
     'spiritual',
     'sport',
     'stonerrock',
     'surf',
     'swing',
     'synthpop',
     'sängerportrait',
     'tango',
     'tanzorchester',
     'taraftar',
     'tech',
     'techno',
     'thrash',
     'top',
     'traditional',
     'tradjazz',
     'trance',
     'tribal',
     'trip',
     'triphop',
     'tropical',
     'türk',
     'türkçe',
     'unknown',
     'urban',
     'uzbek',
     'variété',
     'vi',
     'videogame',
     'vocal',
     'western',
     'world',
     'worldbeat',
     'ïîï']



Lihat melalui *list* untuk menemukan duplikat implisit dari genre `hiphop`. Ini bisa berupa nama yang ditulis secara salah atau nama alternatif dari genre yang sama.

Anda akan melihat duplikat implisit berikut:
* `hip`
* `hop`
* `hip-hop`

Untuk menghapusnya, gunakan fungsi `replace_wrong_genres()` dengan dua parameter:
* `wrong_genres=` — daftar duplikat
* `correct_genre=` — string dengan nilai yang benar

Fungsi harus mengoreksi nama dalam kolom `'genre'` dari tabel `df`, yaitu mengganti setiap nilai dari daftar `wrong_genres` dengan nilai dalam `correct_genre`.


```python
def replace_wrong_genres(wrong_genres, correct_genre):
    for wrong_genre in wrong_genres:
        df['genre'].replace(wrong_genres, correct_genre)

duplicates = ['hip', 'hop', 'hip-hop']
name = 'hiphop'
```

Panggil `replace_wrong_genres()` dan berikan argumennya sehingga ia menghapus duplikat implisit (`hip`, `hop`, dan `hip-hop`) dan menggantinya dengan `hiphop`:


```python
replace_wrong_genres(duplicates, name)
(df)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>track</th>
      <th>artist</th>
      <th>genre</th>
      <th>city</th>
      <th>time</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>61248</th>
      <td>729CBB09</td>
      <td>My Name</td>
      <td>McLean</td>
      <td>rnb</td>
      <td>Springfield</td>
      <td>13:32:28</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>61249</th>
      <td>D08D4A55</td>
      <td>Maybe One Day (feat. Black Spade)</td>
      <td>Blu &amp; Exile</td>
      <td>hip</td>
      <td>Shelbyville</td>
      <td>10:00:00</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>61250</th>
      <td>C5E3A0D5</td>
      <td>Jalopiina</td>
      <td>unknown</td>
      <td>industrial</td>
      <td>Springfield</td>
      <td>20:09:26</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>61251</th>
      <td>321D0506</td>
      <td>Freight Train</td>
      <td>Chas McDevitt</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>21:43:59</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>61252</th>
      <td>3A64EF84</td>
      <td>Tell Me Sweet Little Lies</td>
      <td>Monica Lopez</td>
      <td>country</td>
      <td>Springfield</td>
      <td>21:59:46</td>
      <td>Friday</td>
    </tr>
  </tbody>
</table>
<p>61253 rows × 7 columns</p>
</div>



Pastikan nama duplikat telah dihapus. Tampilkan daftar nilai unik dari kolom `'genre'`:


```python
(sorted(df['genre'].unique()))
```




    ['acid',
     'acoustic',
     'action',
     'adult',
     'africa',
     'afrikaans',
     'alternative',
     'ambient',
     'americana',
     'animated',
     'anime',
     'arabesk',
     'arabic',
     'arena',
     'argentinetango',
     'art',
     'audiobook',
     'avantgarde',
     'axé',
     'baile',
     'balkan',
     'beats',
     'bigroom',
     'black',
     'bluegrass',
     'blues',
     'bollywood',
     'bossa',
     'brazilian',
     'breakbeat',
     'breaks',
     'broadway',
     'cantautori',
     'cantopop',
     'canzone',
     'caribbean',
     'caucasian',
     'celtic',
     'chamber',
     'children',
     'chill',
     'chinese',
     'choral',
     'christian',
     'christmas',
     'classical',
     'classicmetal',
     'club',
     'colombian',
     'comedy',
     'conjazz',
     'contemporary',
     'country',
     'cuban',
     'dance',
     'dancehall',
     'dancepop',
     'dark',
     'death',
     'deep',
     'deutschrock',
     'deutschspr',
     'dirty',
     'disco',
     'dnb',
     'documentary',
     'downbeat',
     'downtempo',
     'drum',
     'dub',
     'dubstep',
     'eastern',
     'easy',
     'electronic',
     'electropop',
     'emo',
     'entehno',
     'epicmetal',
     'estrada',
     'ethnic',
     'eurofolk',
     'european',
     'experimental',
     'extrememetal',
     'fado',
     'film',
     'fitness',
     'flamenco',
     'folk',
     'folklore',
     'folkmetal',
     'folkrock',
     'folktronica',
     'forró',
     'frankreich',
     'französisch',
     'french',
     'funk',
     'future',
     'gangsta',
     'garage',
     'german',
     'ghazal',
     'gitarre',
     'glitch',
     'gospel',
     'gothic',
     'grime',
     'grunge',
     'gypsy',
     'handsup',
     "hard'n'heavy",
     'hardcore',
     'hardstyle',
     'hardtechno',
     'hip',
     'hip-hop',
     'hiphop',
     'historisch',
     'holiday',
     'hop',
     'horror',
     'house',
     'idm',
     'independent',
     'indian',
     'indie',
     'indipop',
     'industrial',
     'inspirational',
     'instrumental',
     'international',
     'irish',
     'jam',
     'japanese',
     'jazz',
     'jewish',
     'jpop',
     'jungle',
     'k-pop',
     'karadeniz',
     'karaoke',
     'kayokyoku',
     'korean',
     'laiko',
     'latin',
     'latino',
     'leftfield',
     'local',
     'lounge',
     'loungeelectronic',
     'lovers',
     'malaysian',
     'mandopop',
     'marschmusik',
     'meditative',
     'mediterranean',
     'melodic',
     'metal',
     'metalcore',
     'mexican',
     'middle',
     'minimal',
     'miscellaneous',
     'modern',
     'mood',
     'mpb',
     'muslim',
     'native',
     'neoklassik',
     'neue',
     'new',
     'newage',
     'newwave',
     'nu',
     'nujazz',
     'numetal',
     'oceania',
     'old',
     'opera',
     'orchestral',
     'other',
     'piano',
     'pop',
     'popelectronic',
     'popeurodance',
     'post',
     'posthardcore',
     'postrock',
     'power',
     'progmetal',
     'progressive',
     'psychedelic',
     'punjabi',
     'punk',
     'quebecois',
     'ragga',
     'ram',
     'rancheras',
     'rap',
     'rave',
     'reggae',
     'reggaeton',
     'regional',
     'relax',
     'religious',
     'retro',
     'rhythm',
     'rnb',
     'rnr',
     'rock',
     'rockabilly',
     'romance',
     'roots',
     'ruspop',
     'rusrap',
     'rusrock',
     'salsa',
     'samba',
     'schlager',
     'self',
     'sertanejo',
     'shoegazing',
     'showtunes',
     'singer',
     'ska',
     'slow',
     'smooth',
     'soul',
     'soulful',
     'sound',
     'soundtrack',
     'southern',
     'specialty',
     'speech',
     'spiritual',
     'sport',
     'stonerrock',
     'surf',
     'swing',
     'synthpop',
     'sängerportrait',
     'tango',
     'tanzorchester',
     'taraftar',
     'tech',
     'techno',
     'thrash',
     'top',
     'traditional',
     'tradjazz',
     'trance',
     'tribal',
     'trip',
     'triphop',
     'tropical',
     'türk',
     'türkçe',
     'unknown',
     'urban',
     'uzbek',
     'variété',
     'vi',
     'videogame',
     'vocal',
     'western',
     'world',
     'worldbeat',
     'ïîï']



[Kembali ke Daftar Isi](#back)

### Kesimpulan <a id='data_preprocessing_conclusions'></a>
Kita mendeteksi tiga masalah dengan data:

- Gaya penulisan judul yang salah
- Nilai-nilai yang hilang
- Duplikat eksplisit dan implisit

Judulnya pun sekarang telah dibersihkan untuk mempermudah pemrosesan tabel.
Semua nilai yang hilang telah diganti dengan `'unknown'`. Tapi kita masih harus melihat apakah nilai yang hilang dalam `'genre'` akan memengaruhi perhitungan kita.

Tidak adanya duplikat akan membuat hasil lebih tepat dan lebih mudah dipahami.

Sekarang kita dapat melanjutkan ke pengujian hipotesis.

[Kembali ke Daftar Isi](#back)

## Tahap 3. Menguji Hipotesis <a id='hypotheses'></a>

### Hipotesis 1: Membandingkan Perilaku Pengguna di Dua Kota <a id='activity'></a>

Menurut hipotesis pertama, pengguna dari Springfield dan Shelbyville memiliki perbedaan perilaku dalam mendengarkan musik. Pengujian ini menggunakan data pada hari: Senin, Rabu, dan Jumat.

* Pisahkan pengguna ke dalam kelompok berdasarkan kota.
* Bandingkan berapa banyak lagu yang dimainkan setiap kelompok pada hari Senin, Rabu, dan Jumat.

Untuk latihan, lakukan setiap perhitungan secara terpisah.

Evaluasi aktivitas pengguna di setiap kota. Kelompokkan data berdasarkan kota dan temukan jumlah lagu yang diputar di setiap kelompok.




```python
(df.groupby('city')['track'].count())
```




    city
    Shelbyville    18512
    Springfield    42741
    Name: track, dtype: int64



Springfield memiliki lebih banyak lagu yang dimainkan daripada Shelbyville. Namun bukan berarti warga Springfield lebih sering mendengarkan musik. Kota ini lebih besar, dan memiliki lebih banyak pengguna.

Sekarang kelompokkan data menurut hari dan temukan jumlah lagu yang diputar pada hari Senin, Rabu, dan Jumat.


```python
(df.groupby('day')['track'].count())
```




    day
    Friday       21840
    Monday       21354
    Wednesday    18059
    Name: track, dtype: int64



Rabu adalah hari paling tenang secara keseluruhan. Tetapi jika kita mempertimbangkan kedua kota secara terpisah, kita mungkin akan memiliki kesimpulan yang berbeda.

Anda telah melihat cara kerja pengelompokan berdasarkan kota atau hari. Sekarang tulis fungsi yang akan dikelompokkan berdasarkan keduanya.

Buat fungsi `number_tracks()` untuk menghitung jumlah lagu yang diputar untuk hari dan kota tertentu. Ini akan membutuhkan dua parameter:
* nama hari
* nama kota

Dalam fungsi, gunakan variabel untuk menyimpan baris dari tabel asli, di mana:
  *  Nilai kolom `'day'` sama dengan parameter `day`
  * Nilai kolom `'city'` sama dengan parameter `city`

Terapkan pemfilteran berurutan dengan pengindeksan logika.

Kemudian hitung nilai kolom `'user_id'` pada tabel yang dihasilkan. Simpan hasilnya ke variabel baru. Kembalikan variabel ini dari fungsi.


```python
def number_tracks(day,city):
    track_list = df[df['day'] == day]
    track_list = track_list[track_list['city'] == city]
    track_list_count = track_list['user_id'].count()
    return track_list_count
```

Panggil `number_tracks()` enam kali dan ubahlah nilai parameternya, sehingga Anda bisa mengambil data di kedua kota untuk masing-masing hari tersebut.


```python
# jumlah lagu yang diputar di Springfield pada hari Senin

number_tracks('Monday','Springfield')
```




    15740




```python
# jumlah lagu yang diputar di Shelbyville pada hari Senin

number_tracks('Monday','Shelbyville')
```




    5614




```python
#  jumlah lagu yang diputar di Springfield pada hari Rabu

number_tracks('Wednesday','Springfield')
```




    11056




```python
#  jumlah lagu yang diputar di Shelbyville pada hari Rabu

number_tracks('Wednesday','Shelbyville')
```




    7003




```python
# jumlah lagu yang diputar di Springfield pada hari Jumat

number_tracks('Friday','Springfield')
```




    15945




```python
# jumlah lagu yang diputar di Shelbyville pada hari Jumat

number_tracks('Friday','Shelbyville')
```




    5895



Gunakan `pd.DataFrame` untuk membuat tabel, di mana
* Nama kolom adalah: `['city', 'monday', 'wednesday', 'friday']`
* Data adalah hasil yang Anda dapatkan dari `number_tracks()`


```python
name_tracks = [
    {'city':'Springfield', 'monday':15740, 'wednesday':11056, 'friday':15945 },
    {'city':'Shelbyville', 'monday':5614, 'wednesday':7003, 'friday':5895 },
]

df_new = pd.DataFrame(name_tracks)
df_new.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>monday</th>
      <th>wednesday</th>
      <th>friday</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Springfield</td>
      <td>15740</td>
      <td>11056</td>
      <td>15945</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Shelbyville</td>
      <td>5614</td>
      <td>7003</td>
      <td>5895</td>
    </tr>
  </tbody>
</table>
</div>



**Kesimpulan**

Data mengungkapkan perbedaan perilaku pengguna:

- Pada Springfield, jumlah lagu yang diputar mencapai puncaknya pada hari Senin dan Jumat, sedangkan pada hari Rabu terjadi penurunan aktivitas.
- Di Shelbyville, sebaliknya, pengguna lebih banyak mendengarkan musik pada hari Rabu.

Aktivitas pengguna pada hari Senin dan Jumat lebih sedikit.

[Kembali ke Daftar Isi](#back)

### Hipotesis 2: Musik di Awal dan Akhir Minggu <a id='week'></a>

Menurut hipotesis kedua, pada Senin pagi dan Jumat malam, warga Springfield mendengarkan genre yang berbeda dari yang dinikmati warga Shelbyville.

Dapatkan tabel (pastikan nama tabel gabungan Anda cocok dengan DataFrame yang diberikan dalam dua blok kode di bawah):
* Untuk Springfield — `spr_general`
* Untuk Shelbyville — `shel_general`


```python
spr_general = df[df['city']=='Springfield'].reset_index(drop=True)

(spr_general)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>track</th>
      <th>artist</th>
      <th>genre</th>
      <th>city</th>
      <th>time</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>55204538</td>
      <td>Delayed Because of Accident</td>
      <td>Andreas Rönnberg</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>14:07:09</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>E2DC1FAE</td>
      <td>Soul People</td>
      <td>Space Echo</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>08:34:34</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4CB90AA5</td>
      <td>True</td>
      <td>Roman Messer</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>13:00:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>F03E1C1F</td>
      <td>Feeling This Way</td>
      <td>Polina Griffith</td>
      <td>dance</td>
      <td>Springfield</td>
      <td>20:47:49</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8FA1D3BE</td>
      <td>L’estate</td>
      <td>Julia Dalia</td>
      <td>ruspop</td>
      <td>Springfield</td>
      <td>09:17:40</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>42736</th>
      <td>83A474E7</td>
      <td>I Worship Only What You Bleed</td>
      <td>The Black Dahlia Murder</td>
      <td>extrememetal</td>
      <td>Springfield</td>
      <td>21:07:12</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>42737</th>
      <td>729CBB09</td>
      <td>My Name</td>
      <td>McLean</td>
      <td>rnb</td>
      <td>Springfield</td>
      <td>13:32:28</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>42738</th>
      <td>C5E3A0D5</td>
      <td>Jalopiina</td>
      <td>unknown</td>
      <td>industrial</td>
      <td>Springfield</td>
      <td>20:09:26</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>42739</th>
      <td>321D0506</td>
      <td>Freight Train</td>
      <td>Chas McDevitt</td>
      <td>rock</td>
      <td>Springfield</td>
      <td>21:43:59</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>42740</th>
      <td>3A64EF84</td>
      <td>Tell Me Sweet Little Lies</td>
      <td>Monica Lopez</td>
      <td>country</td>
      <td>Springfield</td>
      <td>21:59:46</td>
      <td>Friday</td>
    </tr>
  </tbody>
</table>
<p>42741 rows × 7 columns</p>
</div>




```python
shel_general = df[df['city']=='Shelbyville'].reset_index(drop=True)

(shel_general)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>track</th>
      <th>artist</th>
      <th>genre</th>
      <th>city</th>
      <th>time</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>FFB692EC</td>
      <td>Kamigata To Boots</td>
      <td>The Mass Missile</td>
      <td>rock</td>
      <td>Shelbyville</td>
      <td>20:28:33</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20EC38</td>
      <td>Funiculì funiculà</td>
      <td>Mario Lanza</td>
      <td>pop</td>
      <td>Shelbyville</td>
      <td>20:58:07</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A3DD03C9</td>
      <td>Dragons in the Sunset</td>
      <td>Fire + Ice</td>
      <td>folk</td>
      <td>Shelbyville</td>
      <td>08:37:09</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>842029A1</td>
      <td>Chains</td>
      <td>Obladaet</td>
      <td>rusrap</td>
      <td>Shelbyville</td>
      <td>13:09:41</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E772D5C0</td>
      <td>Pessimist</td>
      <td>unknown</td>
      <td>dance</td>
      <td>Shelbyville</td>
      <td>21:20:49</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18507</th>
      <td>D94F810B</td>
      <td>Theme from the Walking Dead</td>
      <td>Proyecto Halloween</td>
      <td>film</td>
      <td>Shelbyville</td>
      <td>21:14:40</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>18508</th>
      <td>BC8EC5CF</td>
      <td>Red Lips: Gta (Rover Rework)</td>
      <td>Rover</td>
      <td>electronic</td>
      <td>Shelbyville</td>
      <td>21:06:50</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>18509</th>
      <td>29E04611</td>
      <td>Bre Petrunko</td>
      <td>Perunika Trio</td>
      <td>world</td>
      <td>Shelbyville</td>
      <td>13:56:00</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>18510</th>
      <td>1B91C621</td>
      <td>(Hello) Cloud Mountain</td>
      <td>sleepmakeswaves</td>
      <td>postrock</td>
      <td>Shelbyville</td>
      <td>09:22:13</td>
      <td>Monday</td>
    </tr>
    <tr>
      <th>18511</th>
      <td>D08D4A55</td>
      <td>Maybe One Day (feat. Black Spade)</td>
      <td>Blu &amp; Exile</td>
      <td>hip</td>
      <td>Shelbyville</td>
      <td>10:00:00</td>
      <td>Monday</td>
    </tr>
  </tbody>
</table>
<p>18512 rows × 7 columns</p>
</div>



Tulis fungsi `genre_weekday()` dengan empat parameter:
* Sebuah tabel untuk data
* Nama hari
* Tanda waktu pertama, dalam format 'hh:mm'
* Tanda waktu terakhir, dalam format 'hh: mm'

Fungsi tersebut harus menghasilkan info tentang 15 genre paling populer pada hari tertentu dalam periode antara dua tanda waktu.


```python
def genre_weekday(genre_table, day, time1, time2):

    # pemfilteran berturut-turut
    # genre_df hanya akan menyimpan baris df di mana day sama dengan day=
    genre_df = genre_table[genre_table['day'] == day] 

    # genre_df hanya akan menyimpan baris df di mana time lebih kecil dari time2=
    genre_df = genre_df[genre_df['time'] < time2] 
    
    # genre_df hanya akan menyimpan baris df di mana time lebih besar dari time1=
    genre_df = genre_df[genre_df['time'] > time1]

    # kelompokkan DataFrame yang difilter berdasarkan kolom dengan nama genre, ambil kolom genre, dan temukan jumlah baris untuk setiap genre dengan metode count()
    genre_df_grouped = genre_df.groupby('genre')['genre'].count() 

    # kita akan mengurutkan hasilnya dalam urutan menurun (sehingga genre paling populer didahulukan pada objek Series
    genre_df_sorted = genre_df_grouped.sort_values(ascending = False) 

    # kita akan menghasilkan objek Series yang menyimpan 15 genre paling populer pada hari tertentu dalam jangka waktu tertentu
    return genre_df_sorted[:15]
```

Bandingkan hasil fungsi `genre_weekday()` untuk Springfield dan Shelbyville pada Senin pagi (dari pukul 07.00 hingga 11.00) dan pada Jumat malam (dari pukul 17:00 hingga 23:00):


```python
genre_weekday(genre_table=spr_general, day='Monday',time1='07:00',time2='11:00')
```




    genre
    pop            781
    dance          549
    electronic     480
    rock           474
    hip            281
    ruspop         186
    world          181
    rusrap         175
    alternative    164
    unknown        161
    classical      157
    metal          120
    jazz           100
    folk            97
    soundtrack      95
    Name: genre, dtype: int64




```python
genre_weekday(genre_table=shel_general, day='Monday',time1='07:00',time2='11:00')
```




    genre
    pop            218
    dance          182
    rock           162
    electronic     147
    hip             79
    ruspop          64
    alternative     58
    rusrap          55
    jazz            44
    classical       40
    world           36
    rap             32
    soundtrack      31
    rnb             27
    metal           27
    Name: genre, dtype: int64




```python
genre_weekday(genre_table=spr_general, day='Friday',time1='17:00',time2='23:00')
```




    genre
    pop            713
    rock           517
    dance          495
    electronic     482
    hip            267
    world          208
    ruspop         170
    classical      163
    alternative    163
    rusrap         142
    jazz           111
    unknown        110
    soundtrack     105
    rnb             90
    metal           88
    Name: genre, dtype: int64




```python
genre_weekday(genre_table=shel_general, day='Friday',time1='17:00',time2='23:00'
```




    genre
    pop            256
    electronic     216
    rock           216
    dance          210
    hip             94
    alternative     63
    jazz            61
    classical       60
    rusrap          59
    world           54
    unknown         47
    ruspop          47
    soundtrack      40
    metal           39
    rap             36
    Name: genre, dtype: int64



**Kesimpulan**

Setelah membandingkan 15 genre teratas pada Senin pagi, kita dapat menarik kesimpulan berikut:

1. Pengguna dari Springfield dan Shelbyville mendengarkan musik dengan genre yang sama. Lima genre teratas sama, hanya rock dan elektronik yang bertukar tempat.

2. Di Springfield, jumlah nilai yang hilang ternyata sangat besar sehingga nilai `'unknown'` berada di urutan ke-10. Ini berarti bahwa nilai-nilai yang hilang memiliki jumlah data yang cukup besar, yang mungkin menjadi dasar untuk mempertanyakan ketepatan kesimpulan kita.

Untuk Jumat malam, situasinya serupa. Genre individual cukup bervariasi, tetapi secara keseluruhan, 15 besar genre untuk kedua kota sama.

Dengan demikian, hipotesis kedua sebagian terbukti benar:
* Pengguna mendengarkan musik yang sama di awal dan akhir minggu.
* Tidak ada perbedaan yang mencolok antara Springfield dan Shelbyville. Pada kedua kota tersebut, pop adalah genre yang paling populer.

Namun, jumlah nilai yang hilang membuat hasil ini dipertanyakan. Di Springfield, ada begitu banyak yang memengaruhi 15 teratas kita. Jika kita tidak mengabaikan nilai-nilai ini, hasilnya mungkin akan berbeda.

[Kembali ke Daftar Isi](#back)

### Hipotesis 3: Preferensi Genre di Springfield dan Shelbyville <a id='genre'></a>

Hipotesis: Shelbyville menyukai musik rap. Warga Springfield lebih menyukai pop.

Kelompokkan tabel `spr_general` berdasarkan genre dan temukan jumlah lagu yang dimainkan untuk setiap genre dengan metode `count()`. Kemudian urutkan hasilnya dalam urutan menurun dan simpan ke `spr_genres`.


```python
spr_genres = spr_general.groupby('genre')['time'].count().sort_values(ascending=False)

spr_genres
```




    genre
    pop            5892
    dance          4435
    rock           3965
    electronic     3786
    hip            2041
                   ... 
    metalcore         1
    marschmusik       1
    malaysian         1
    lovers            1
    ïîï               1
    Name: time, Length: 253, dtype: int64



Tampilkan 10 baris pertama dari `spr_genres`:


```python
spr_genres.head(10)
```




    genre
    pop            5892
    dance          4435
    rock           3965
    electronic     3786
    hip            2041
    classical      1616
    world          1432
    alternative    1379
    ruspop         1372
    rusrap         1161
    Name: time, dtype: int64



Sekarang lakukan hal yang sama pada data di Shelbyville.

Kelompokkan tabel `shel_general` berdasarkan genre dan temukan jumlah lagu yang dimainkan untuk setiap genre. Kemudian urutkan hasilnya dalam urutan menurun dan simpan ke tabel `shel_genres`:


```python
shel_genres = shel_general.groupby('genre')['time'].count().sort_values(ascending=False)

shel_genres
```




    genre
    pop           2431
    dance         1932
    rock          1879
    electronic    1736
    hip            934
                  ... 
    mandopop         1
    leftfield        1
    laiko            1
    jungle           1
    worldbeat        1
    Name: time, Length: 203, dtype: int64



Tampilkan 10 baris pertama dari `shel_genres`:


```python
shel_genres.head(10)
```




    genre
    pop            2431
    dance          1932
    rock           1879
    electronic     1736
    hip             934
    alternative     649
    classical       646
    rusrap          564
    ruspop          538
    world           515
    Name: time, dtype: int64



**Kesimpulan**

Hipotesis terbukti benar sebagian:
* Musik pop adalah genre paling populer di Springfield, seperti yang diharapkan.
* Namun, musik pop ternyata sama populernya baik di Springfield maupun di Shelbyville, dan musik rap tidak berada di 5 besar untuk kedua kota tersebut.


[Kembali ke Daftar Isi](#back)

# Temuan <a id='end'></a>

Kita telah menguji tiga hipotesis berikut:

1. Aktivitas pengguna berbeda-beda tergantung pada hari dan kotanya.
2. Pada senin pagi, penduduk Springfield dan Shelbyville mendengarkan genre yang berbeda. Hal ini juga ini juga berlaku untuk Jumat malam.
3. Pendengar di Springfield dan Shelbyville memiliki preferensi yang berbeda. Baik Springfield maupun di Shelbyville, mereka lebih suka musik pop.

Setelah menganalisis data, kita dapat menyimpulkan:

1. Aktivitas pengguna di Springfield dan Shelbyville bergantung pada harinya, walaupun kotanya berbeda.

Hipotesis pertama dapat diterima sepenuhnya.

2. Preferensi musik tidak terlalu berbeda selama seminggu di Springfield dan Shelbyville. Kita dapat melihat perbedaan kecil dalam urutan pada hari Senin, tetapi:
* Baik di Springfield maupun di Shelbyville, orang paling banyak mendengarkan musik pop.

Jadi hipotesis ini tidak dapat kita terima. Kita juga harus ingat bahwa hasilnya mungkin saja akan berbeda jika bukan karena nilai yang hilang.
3. Ternyata preferensi musik pengguna dari Springfield dan Shelbyville sangat mirip.

Hipotesis ketiga ditolak. Jika memang ada perbedaan preferensi, ia tidak dapat dilihat dari data ini.
### Catatan
Dalam proyek sesungguhnya, penelitian melibatkan pengujian hipotesis statistik, yang lebih tepat dan lebih kuantitatif. Perhatikan juga bahwa Anda tidak dapat selalu menarik kesimpulan tentang seluruh kota berdasarkan data dari satu sumber saja.

Anda akan mempelajari pengujian hipotesis dalam sprint analisis data statistik.

[Kembali ke Daftar Isi](#back)
