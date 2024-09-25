<!-- Cover Makalah dengan Logo -->

<div align="center">

# **PEMROSESAN CITRA DIGITAL**

## **(Halftoning: Patterning & Dithering)**
<!-- Menambahkan Logo -->
<img src="https://ulm.ac.id/id/wp-content/uploads/2023/03/lambangULM2021warna.png" width="200"/>
---

### Disusun Oleh:

**Siti Rahmatul Maulidiah**  
**2310131220013**

### Dosen Pembimbing:
**Dr. Harja Santana Purba, M.KOM**
**Novan Alkaf Bahraini Saputra, S.Kom., M.T**
**Ihdalhubbi Maulida, M.Kom**

**UNIVERSITAS LAMBUNG MANGKURAT**  
**FAKULTAS KEGURUAN DAN ILMU PENDIDIKAN**  
**PROGRAM STUDI PENDIDIKAN KOMPUTER**
**2024**

</div>

---

# Daftar Isi
1. Daftar Isi
2. BAB I Pendahuluan
3. BAB II Pembahasan
    2.1 Patterning
    2.2 Dithering
4. BAB III Penutup
5. Daftar Pustaka

---

# BAB I  Pendahuluan

Halftoning adalah sebuah teknik dalam pencetakan dan pemrosesan citra yang memungkinkan gambar dengan variasi gradasi warna atau tingkat keabuan diubah menjadi gambar biner—yakni gambar yang hanya memiliki dua nilai, seperti hitam dan putih—tanpa kehilangan detail visual yang signifikan. Walaupun gambar hasil halftoning secara teknis hanya terdiri dari dua warna, teknik ini menciptakan ilusi visual yang membuat gambar tampak seolah memiliki banyak gradasi warna. Hal ini dimungkinkan dengan penggunaan pola titik atau piksel yang diatur sedemikian rupa sehingga mata manusia menangkapnya sebagai percampuran warna yang halus. Oleh karena itu, meskipun hanya menggunakan piksel biner, citra yang dihasilkan tetap mampu merepresentasikan gradasi warna dan bayangan secara efektif.
Dalam implementasinya, terdapat dua pendekatan utama dalam teknik halftoning, yaitu patterning dan dithering. Kedua teknik ini berbeda dalam menciptakan ilusi gradasi warna. Keduanya memiliki keunggulan masing-masing dan dapat disesuaikan dengan berbagai kondisi teknis dan preferensi visual.

---

# BAB II  Pembahasan

### 2.1 Patterning
Pattering melibatkan penggunaan pola tertentu (pattern) untuk menentukan warna atau tingkat keabuan pada setiap piksel. Pola ini dapat berupa matriks biner atau matriks nilai abu-abu. Setiap elemen dalam matriks ini dibandingkan dengan nilai piksel asli. Jika nilai piksel lebih besar dari nilai elemen matriks, maka piksel tersebut diberi warna atau tingkat keabuan maksimum yang tersedia. Jika tidak, maka piksel tersebut diberi warna atau tingkat keabuan minimum.

**Cara Kerja:**
Buat matriks pola: Tentukan ukuran dan jenis pola yang akan digunakan.
Normalisasi nilai piksel: Skala nilai piksel agar sesuai dengan rentang nilai pada matriks pola.
Bandingkan nilai piksel dengan nilai matriks: Untuk setiap piksel, bandingkan nilai piksel yang telah dinormalisasi dengan nilai elemen matriks yang sesuai.
Tentukan warna atau tingkat keabuan: Jika nilai piksel lebih besar dari nilai matriks, gunakan warna atau tingkat keabuan maksimum; jika tidak, gunakan minimum.

Membagi citra menjadi grid kecil, di mana setiap grid mewakili satu warna keabuan.
Menggunakan pola dot (titik), setiap grid diisi dengan titik hitam sesuai dengan intensitas keabuan pada grid tersebut.
Jumlah titik hitam dalam setiap grid diatur sesuai dengan level keabuan: semakin terang (putih), semakin sedikit titik hitam, dan semakin gelap (hitam), semakin banyak titik hitam.

Tentukan grid (misalnya 4x4 atau 8x8).
Nilai keabuan (0–255) dikonversi ke persentase.
Sesuaikan jumlah titik hitam dalam grid sesuai dengan nilai persentase keabuan tersebut.

**Algoritma:**
1. Input Gambar Grayscale: Ambil gambar grayscale yang akan diproses. Setiap piksel pada gambar memiliki nilai intensitas antara 0 (hitam) hingga 255 (putih).
2. Tentukan Ukuran Pola: Pilih ukuran pola yang akan digunakan untuk membagi gambar (misalnya, 2x2 atau 4x4).
3. Hitung Kecerahan Rata-rata: Untuk setiap blok/pola:
* Hitung kecerahan rata-rata dari piksel dalam blok tersebut.
* Jika ukuran pola adalah 4x4, maka ambil 16 piksel dan hitung rata-ratanya.
4. Tentukan Nilai Biner Berdasarkan Kecerahan: Bandingkan kecerahan rata-rata dengan nilai ambang batas (biasanya 128).
* Jika rata-rata kecerahan lebih besar atau sama dengan ambang batas, semua piksel dalam pola diubah menjadi putih (255).
* Jika rata-rata kecerahan kurang dari ambang batas, semua piksel dalam pola diubah menjadi hitam (0).
5. Ulangi untuk Seluruh Gambar: Proses ini dilakukan untuk setiap blok dalam gambar hingga seluruh gambar diproses.

**Contoh Perhitungan:**
Misalkan kita memiliki blok 2x2 dengan piksel-piksel berikut:
Piksel:
| 100 | 150 |
| 200 | 255 |

Cara hitung:
1. Hitung Kecerahan Rata-rata:
\text{average_brightness} = \frac{100 + 150 + 200 + 255}{4} = 176.25
2. Tentukan Nilai Biner:
Karena 176.25 ≥ 128, set semua piksel dalam blok menjadi putih (255).

**Pseudocode:**
1. Input: Gambar grayscale
2. Output: Gambar biner hasil patterning
3. Tentukan ukuran pola (block_size)
4. For y = 1 to height of image with step = block_size:
      For x = 1 to width of image with step = block_size:
          a. Inisialisasi sum = 0
          b. Untuk setiap piksel dalam pola (i, j) di (x, y):
              sum += image[x+i, y+j]
          c. Hitung kecerahan rata-rata:
              average_brightness = sum / (block_size * block_size)
          d. Tentukan nilai biner berdasarkan ambang batas:
              if average_brightness >= 128:
                  Set all pixels in the block to 255 (white)
              else:
                  Set all pixels in the block to 0 (black)


### 2.2 Dithering
Dithering adalah proses yang lebih kompleks, di mana nilai piksel dibandingkan dengan nilai ambang (threshold) yang ditentukan oleh pola dithering. Pola dithering dapat berupa matriks biner atau matriks nilai abu-abu yang lebih kompleks daripada pola patterning. Nilai ambang bervariasi untuk setiap piksel, sehingga menghasilkan transisi warna yang lebih halus.

**Cara Kerja:**
Buat matriks pola dithering: Tentukan ukuran dan jenis pola dithering yang akan digunakan.
Normalisasi nilai piksel: Sama seperti pada patterning.
Hitung nilai ambang: Untuk setiap piksel, hitung nilai ambang berdasarkan nilai elemen matriks dithering yang sesuai dan nilai piksel yang telah dinormalisasi.
Bandingkan nilai piksel dengan nilai ambang: Jika nilai piksel lebih besar dari nilai ambang, gunakan warna atau tingkat keabuan maksimum; jika tidak, gunakan minimum.

Konversi nilai keabuan dari gambar ke nilai biner.
Menambahkan noise atau pengacakan untuk mendistribusikan titik-titik hitam dan putih, sehingga nilai intensitas terlihat lebih halus secara visual.
Menggunakan algoritma tertentu (misalnya Floyd-Steinberg dithering) untuk menghitung distribusi titik-titik.

Setiap piksel dibandingkan dengan nilai ambang batas (misalnya, 128).
Jika lebih besar, jadikan putih; jika lebih kecil, jadikan hitam.
Hitung kesalahan dari proses tersebut dan distribusikan ke tetangga (menggunakan bobot tertentu).

**Algoritma:**
Salah satu algoritma yang menggunakan pendekatan Dithering adalah algoritma Floyd-Steinberg sebagai berikut:
1. Ambil Nilai Intensitas Grayscale Piksel: Setiap piksel pada gambar grayscale memiliki nilai intensitas antara 0 (hitam) hingga 255 (putih). Nilai ini akan dikonversi menjadi biner, yaitu 0 (hitam) atau 255 (putih).
2. Tentukan Nilai Threshold (Ambang Batas): Tentukan nilai ambang batas (biasanya 128). Jika intensitas piksel lebih besar atau sama dengan threshold, piksel tersebut akan diubah menjadi putih (255), dan jika kurang dari threshold, diubah menjadi hitam (0).
3. Hitung Kesalahan Kuantisasi: Kesalahan kuantisasi adalah selisih antara nilai intensitas asli dan nilai biner hasil konversi (hitam atau putih).
Kesalahan kuantisasi = nilai intensitas asli − nilai biner baru
4. Sebarkan Kesalahan Kuantisasi ke Piksel Tetangga: Kesalahan kuantisasi ini didistribusikan ke piksel-piksel tetangga yang belum diproses dengan bobot tertentu.
5. Ulangi Langkah untuk Semua Piksel: Proses ini dilakukan untuk setiap piksel pada gambar sampai seluruh gambar diproses

**Contoh Perhitungan**
Misalkan kita memiliki piksel dengan nilai intensitas asli 150, dan threshold yang digunakan adalah 128.
1. Nilai Piksel Asli: 150
2. Threshold: 128 → Karena 150 > 128, piksel akan diubah menjadi putih (255).
3. Hitung Kesalahan Kuantisasi:
quant_error=150−255=−105
4. Distribusi Kesalahan: Kesalahan ini akan didistribusikan ke piksel-piksel tetangga dengan bobot 7/16, 3/16, 5/16, dan 1/16.

**Pseudocode:**
1. Input: Gambar grayscale
2. Output: Gambar biner hasil dithering
3. For each pixel (x, y) in the image:
    a. Ambil nilai intensitas asli: old_pixel = image[x, y]
    b. Tentukan nilai ambang batas:
        if old_pixel >= threshold:
            new_pixel = 255  # Putih
        else:
            new_pixel = 0    # Hitam
    c. Hitung kesalahan kuantisasi:
        quant_error = old_pixel - new_pixel
    d. Tetapkan nilai baru untuk piksel:
        image[x, y] = new_pixel
    e. Sebarkan kesalahan kuantisasi ke piksel tetangga yang belum diproses:
        image[x+1, y]   += quant_error * (7 / 16)  # Piksel kanan
        image[x-1, y+1] += quant_error * (3 / 16)  # Piksel bawah kiri
        image[x, y+1]   += quant_error * (5 / 16)  # Piksel bawah
        image[x+1, y+1] += quant_error * (1 / 16)  # Piksel bawah kanan

---

# BAB III  Penutup
Halftoning merupakan teknik penting dalam pencetakan dan pemrosesan citra yang memungkinkan representasi gambar dengan gradasi warna dalam format biner. Dengan menggunakan pendekatan seperti patterning dan dithering, halftoning dapat menciptakan ilusi warna yang halus meskipun hanya menggunakan dua nilai piksel, yaitu hitam dan putih. Patterning memanfaatkan pola tetap untuk menentukan tingkat keabuan, sementara dithering menawarkan metode yang lebih dinamis dengan menyesuaikan nilai ambang berdasarkan piksel dan menambahkan noise untuk memperhalus transisi warna. Keduanya memiliki cara yang berbeda dan keunggulan masing-masing, memungkinkan pengguna untuk memilih metode yang paling sesuai dengan kebutuhan. Dengan pemahaman yang baik tentang kedua teknik ini, proses halftoning dapat diterapkan secara efektif untuk menghasilkan citra berkualitas tinggi yang mempertahankan detail visual yang penting.

---

# Daftar Pustaka
Ques10. (n.d.). Write short notes on half toning and dithering. Diakses pada 23 September 2024, dari https://www.ques10.com/p/11455/write-short-notes-on-half-tonning-and-dithering--1/#google_vignette
Swardika, I. K. (2017). Analisa teknik kompresi data satelit dengan metode error diffusion dithering. Matrix: Jurnal Manajemen Teknologi dan Informatika, 5(1), 51. Diakses pada 24 September 2024, dari https://ojs.pnb.ac.id/index.php/matrix/article/view/81
