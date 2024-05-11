# PCD_UTS_202231039_ITPLN
## MEMBUAT LIBRARY
```python
import cv2
import matplotlib.pyplot as plt
import numpy as np
```
* Menggunakan library cv2 digunakan untuk memproses gambar dan video.
Library matplotlib.pyplot digunakan untuk menampilkan gambar.
Library numpy digunakan untuk melakukan operasi aritmatika.
```python
img = cv2.imread("Ikhwanul Fatiha.jpeg")
```
* Lalu, kode `img = cv2.imread(“Ikhwanul Fatiha.jpeg”)` membaca gambar dengan nama file “Ikhwanul fatiha.jpeg” menggunakan OpenCV (cv2).
## MEMBUAT BARIS DAN KOLOM
```python
img.shape
```
```python
(baris, kolom) = img.shape[:2]
```
* `img.shape` merupakan atribut dari matriks gambar yang mengembalikan tuple yang berisi tiga elemen yaitu (623, 845, 3). Selanjutnya mengambil dua nilai pertama dari tuple yang dihasilkan yaitu nilai tinggi dan lebar gambar.
```python
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
```python
plt.imshow(img)
```
* Mengkonversi warna gambar dari BGR (Blue, Green, Red) ke warna RGB (Red, Green, Blue) dengan fungsi OpenCV yaitu cv2.cvtColor. setelah dieksekusi, gambar`img` akan memiliki skema warna yang benar untuk ditampilkan dengan `matplotlib.pyplot`.
## MENINGKATKAN KECERAHAN GAMBAR
```python
alpa = 1
beta = 25

citra_gbngn = np.zeros((baris, kolom, 3))
for x in range (baris):
    for y in range (kolom):
        gcx = (img[x, y] * alpa) + beta
        citra_gbngn [x, y] = gcx
        
citra_gbngn = citra_gbngn.astype (np.uint8)

fig, axs = plt.subplots (2, 2, figsize = (15, 5))
axs [0, 0].imshow(img)
axs [0, 1].hist(img.ravel(), 256, [0, 256])
axs [1, 0].imshow(citra_gbngn)
axs [1, 1].hist (citra_gbngn.ravel(), 256, [0, 256])
plt.show()
```
* alpa = 1 dan beta = 25 ini adalah parameter untuk menyesuaikan kontras dan kecerahan gambar. citra_gbngn = np.zeros((baris, kolom, 3)) membuat array Numpy dengan dimensi yang sama dengan gambar awal untuk menyimpan gambar yang akan dihasilkan setelah penyesuaian kontras dan kecerahan. for x in range(baris) dan for y in range(kolom) melakukan iterasi untuk setiap baris dan kolom dalam gambar. gcx = (img[x, y] * alpa) + beta menghitung nilai piksel baru dengan mengalikan nilai piksel asli. Operasi ini dilakukan untuk setiap saluran warna (R, G, B) pada setiap piksel gambar. citra_gbngn[x, y] = gcx menyimpan nilai piksel yang telah disesuaikan ke dalam array citra hasil. citra_gbngn = citra_gbngn.astype(np.uint8) mengonversi array citra hasil ke tipe data unsigned 8-bit integer (uint8).
* plt.subplots() menampilkan gambar asli, histogram gambar asli, gambar yang telah disesuaikan kontras dan kecerahan, dan histogram dari gambar yang telah disesuaikan. axs[0, 0].imshow(img) menampilkan gambar asli pada subplot di posisi baris 0 dan kolom 0. axs[0, 1].hist(img.ravel(), 256, [0, 256]) membuat histogram dari gambar asli dan menampilkannya pada subplot di posisi baris 0 dan kolom 1. axs[1, 0].imshow(citra_gbngn) menampilkan gambar yang telah disesuaikan kontras dan kecerahan pada subplot di posisi baris 1 dan kolom 0. axs[1, 1].hist(citra_gbngn.ravel(), 256, [0, 256]) membuat histogram dari gambar yang telah disesuaikan kontras dan kecerahan dan menampilkannya pada subplot di posisi baris 1 dan kolom 1. plt.show() menampilkan semua subplot yang telah dibuat.

## MENDETEKSI WARNA GAMBAR
```python
plt.subplot(2, 2, 1)
plt.imshow(citra_gbngn)
plt.title('Citra Kontras')

plt.subplot(2, 2, 2)
plt.imshow(citra_gbngn[:,:,0], cmap="gray")
plt.title('RED')

plt.subplot(2, 2, 3)
plt.imshow(citra_gbngn[:,:,1], cmap="gray")
plt.title('GREEN')

plt.subplot(2, 2, 4)
plt.imshow(citra_gbngn[:,:,2], cmap="gray")
plt.title('BLUE')

plt.show()
```
* plt.subplot(2, 2, 1) membuat subplot dengan ukuran 2x2 dan memilih subplot pertama (indeks 1) untuk menampilkan citra yang telah disesuaikan kontras dan kecerahan. Ini akan menempatkan citra kontras di posisi baris 1, kolom 1.
* plt.imshow(citra_gbngn) menampilkan citra yang telah disesuaikan kontras dan kecerahan di subplot yang dipilih sebelumnya.
* plt.title('Citra Kontras') menambahkan judul pada subplot pertama untuk menunjukkan bahwa ini adalah citra yang telah disesuaikan kontras dan kecerahan.
* plt.subplot(2, 2, 2) memilih subplot kedua (indeks 2) untuk menampilkan komponen merah (saluran warna merah) dari citra yang telah disesuaikan kontras dan kecerahan.
* plt.imshow(citra_gbngn[:,:,0], cmap="gray") menampilkan komponen merah dari citra menggunakan plt.imshow(). Argumen cmap="gray" mengatur pemetaan warna menjadi grayscale untuk menampilkan saluran warna merah secara monokromatik.
* plt.title('RED') menambahkan judul pada subplot kedua untuk menunjukkan bahwa ini adalah komponen merah dari citra.
* Langkah-langkah 4-6 di atas diulang untuk menampilkan komponen hijau (plt.subplot(2, 2, 3), plt.imshow(citra_gbngn[:,:,1], cmap="gray"), dan plt.title('GREEN')) dan komponen biru (plt.subplot(2, 2, 4), plt.imshow(citra_gbngn[:,:,2], cmap="gray"), dan plt.title('BLUE')) dari citra yang telah disesuaikan kontras dan kecerahan.
* plt.show() menampilkan semua subplot yang telah dibuat.
## MENAMPILKAN HISTOGRAM SETIAP WARNA
```python
fig, axs = plt.subplots (3, 2, figsize=(15, 15))
# Merah
merah = citra_gbngn[:, :, 0]
hist_merah = cv2.calcHist([merah], [0], None, [256], [0, 256])
axs [0, 0].imshow(merah, cmap='gray')
axs [0, 0].set_title('MERAH')
axs [0, 1].plot(hist_merah, color='r')
axs [0, 1].set_title('MERAH HISTOGRAM')
# Hijau
hijau = citra_gbngn[:,:, 1]
hist_hijau = cv2.calcHist([hijau], [0], None, [256], [0, 256])
axs [1, 0].imshow(hijau, cmap='gray')
axs [1, 0].set_title('HIJAU')
axs [1, 1].plot(hist_hijau, color='g')
axs [1, 1].set_title('HIJAU HISTOGRAM')
#Biru
biru = citra_gbngn[:,:, 2]
hist_biru = cv2.calcHist([biru], [0], None, [256], [0, 256])
axs [2, 0].imshow(biru, cmap='gray')
axs [2, 0].set_title('BIRU')
axs [2, 1].plot(hist_biru, color='b')
axs [2, 1].set_title('BIRU HISTOGRAM')
plt.tight_layout()
plt.show()
```
* fig, axs = plt.subplots(3, 2, figsize=(15, 15)) Membuat subplot dengan ukuran 3x2 (tiga baris dan dua kolom) dengan ukuran keseluruhan 15x15 inci.
* Bagian untuk Saluran Warna Merah :
Mengambil saluran warna merah dari citra yang disesuaikan kontras dan kecerahan.
Menghitung histogram untuk saluran warna merah.
Menampilkan gambar saluran warna merah dalam subplot pada posisi (0, 0).
Menampilkan histogram saluran warna merah dalam subplot pada posisi (0, 1).

* Bagian untuk Saluran Warna Hijau:
Mengambil saluran warna hijau dari citra yang disesuaikan kontras dan kecerahan.
Menghitung histogram untuk saluran warna hijau.
Menampilkan gambar saluran warna hijau dalam subplot pada posisi (1, 0).
Menampilkan histogram saluran warna hijau dalam subplot pada posisi (1, 1).

* Bagian untuk Saluran Warna Biru:
Mengambil saluran warna biru dari citra yang disesuaikan kontras dan kecerahan.
Menghitung histogram untuk saluran warna biru.
Menampilkan gambar saluran warna biru dalam subplot pada posisi (2, 0).
Menampilkan histogram saluran warna biru dalam subplot pada posisi (2, 1).

* plt.tight_layout() mengatur layout subplot agar tidak tumpang tindih.
* plt.show() menampilkan semua subplot yang telah dibuat.
## AMBANG BATAS
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Baca gambar
img = cv2.imread('Ikhwanul Fatiha.jpeg')
# Convert citra ke grayscale
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

# Inisialisasi subplot
fig, axs = plt.subplots(2, 2, figsize=(10,10))

# Ambang batas untuk mendapatkan citra biner (none)
(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

# Convert citra ke HSV
image_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Definisikan range warna biru dalam HSV
blue_lower = np.array([85, 5, 50])
blue_upper = np.array([140, 255, 255])

# Membuat mask untuk warna biru
mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper)
axs[0,1].imshow(mask_blue, cmap='gray')
axs[0,1].set_title('BLUE')

# Ambang batas untuk mendapatkan citra biner (red-blue)
(thresh, binary3) = cv2.threshold(gray, 110, 255, cv2.THRESH_BINARY)
axs[1,0].imshow(binary3, cmap = 'binary')
axs[1,0].set_title('RED-BLUE')

# Ambang batas untuk mendapatkan citra biner (red-green-blue)
(thresh, binary4) = cv2.threshold(gray, 110, 255, cv2.THRESH_BINARY)
axs[1,1].imshow(binary4, cmap = 'binary')
axs[1,1].set_title('RED-GREEN-BLUE')

plt.show()
```
* Mengambil gambar "Ikhwanul Fatiha.jpeg", lalu mengonversinya ke citra skala abu-abu dan ruang warna HSV. Selanjutnya, beberapa citra biner dibuat menggunakan metode ambang batas untuk mendapatkan citra biner standar, memisahkan warna biru, dan mendapatkan kombinasi warna tertentu seperti merah dan kombinasi merah, hijau, dan biru. Subplot digunakan untuk menampilkan citra asli dan citra biner yang dihasilkan, memberikan representasi visual dari proses segmentasi warna yang dilakukan. Ini menunjukkan bagaimana teknik segmentasi warna dapat digunakan untuk mengidentifikasi objek berdasarkan warna tertentu dalam gambar.
