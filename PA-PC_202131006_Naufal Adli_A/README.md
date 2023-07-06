
# Deteksi Bentuk Gambar menggunakan Contour

Kontur adalah garis yang menggambarkan batas-batas atau bentuk dari objek dalam gambar. Dalam konteks pengolahan citra dan pengenalan pola, kontur sering digunakan untuk memisahkan objek dari latar belakang atau mengidentifikasi fitur-fitur penting dari objek tersebut. Kontur ditemukan dengan menganalisis perbedaan intensitas piksel di sekitar area objek dalam gambar.

Deskripsi Program : Program sistem deteksi bentuk gambar menggunakan kontur adalah program yang dapat mengidentifikasi dan membedakan berbagai bentuk geometris dalam sebuah gambar menggunakan teknik kontur.

Kontur biasanya terbentuk oleh perubahan tajam dalam intensitas piksel di sekitar objek. Misalnya, dalam gambar biner (hitam-putih), kontur seringkali merupakan garis yang memisahkan piksel bernilai putih (objek) dengan piksel bernilai hitam (latar belakang).

Ada beberapa fitur yang mendukung penggunaan kontur dalam proyek deteksi bentuk gambar,

Contohnya :
Segmentasi Objek
Kontur juga dapat digunakan untuk memisahkan objek dari latar belakang atau mengidentifikasi bagian-bagian objek dalam gambar. Dengan menganalisis kontur, kita dapat mengidentifikasi garis dan lengkungan yang menggambarkan batas objek, yang memungkinkan segmentasi objek yang lebih akurat. Ini dapat digunakan dalam berbagai aplikasi seperti deteksi wajah, deteksi kendaraan, atau deteksi citra medis

pada project ini saya mengaitkan teori dengan jurnal mengenai deteksi citra medis menggunakan contour dengan refrensi jurnal dari Institut Teknologi Sepuluh November, namun untuk membuat project ini saya mengambil poto sisir dari kamera hp saya

# Teori Pengolahan Citra
1. Pra-pemrosesan: Sebelum deteksi kontur dilakukan, gambar sering kali harus diproses terlebih dahulu. Proses pra-pemrosesan ini dapat meliputi konversi gambar ke skala abu-abu (grayscale), pemulusan (smoothing) untuk mengurangi derau (noise) dalam gambar, dan segmentasi (thresholding) untuk memisahkan objek dari latar belakang. Pra-pemrosesan ini bertujuan untuk meningkatkan kualitas dan kejelasan kontur yang akan dideteksi.

2. Deteksi tepi: Deteksi tepi adalah langkah awal dalam deteksi kontur. Tepi atau garis yang terdapat pada gambar adalah tanda dari perubahan yang tajam dalam intensitas piksel. Metode deteksi tepi seperti operator Sobel, Prewitt, atau Canny Edge Detection dapat digunakan untuk menemukan tepi dalam gambar. Metode ini akan menandai piksel-piksel yang memiliki perbedaan intensitas yang signifikan dengan piksel sekitarnya.

3. Penyempurnaan kontur: Setelah tepi terdeteksi, kontur seringkali memiliki ketidaksempurnaan seperti piksel yang tidak terhubung, piksel yang terisolasi, atau garis-garis yang terputus. Untuk memperbaiki kontur tersebut, dilakukan langkah-langkah seperti operasi morfologi (erosi dan dilasi) atau pemisahan komponen yang terhubung untuk menyatukan tepi yang terputus.

4. Segmentasi objek: Setelah kontur ditemukan, langkah berikutnya adalah memisahkan objek dari latar belakang. Ini dapat dilakukan dengan menggunakan teknik segmentasi seperti thresholding atau metode berbasis region yang membagi gambar menjadi wilayah-wilayah dengan karakteristik yang sama.

5. Analisis bentuk: Setelah kontur dan objek terisolasi, analisis lanjutan dapat dilakukan untuk mengidentifikasi bentuk-bentuk spesifik. Ini melibatkan pengukuran dan perbandingan fitur-fitur geometris seperti jumlah sisi, panjang dan lebar, luas, atau perbandingan aspek untuk mengklasifikasikan objek menjadi bentuk-bentuk tertentu.

# Tahapan pembuatan Objek
1. Menentukan Citra (gambar yang akan dideteksi)
2. Menentukan Library yang akan digunakan
   - CV2 : Library utama untuk pengolahan gambar
   - numpy : Library untuk operasi matematika
   - matplotlib.pyplot : Library untuk visualisasi gambar
3. Melakukan Pra-pemrosesan
  -Konversi Gambar ke grayscale
  -Melakukan Tresholding gambar
4. Melakukan Penyempurnaan kontur pada gambar asli
   
# Penjelasan Program
```bash
import cv2 
import numpy as np 
import matplotlib.pyplot as adli
```
- CV2 : Library utama untuk pengolahan gambar menggunakan OpenCV
- numpy : Library untuk operasi matematika
- matplotlib.pyplot : Library untuk visualisasi gambar

```bash
image = cv2.imread('sisir.jpg')
```
membaca gambar menggunakan cv2.imread

```bash
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
Mengubah gambar menjadi abu abu menggunakan cv2.cvtColor, hasilnya disimpan pada variable gray

```bash
ret, thresh = cv2.threshold(gray, 127, 255, 0)
```
Melakukan Treshholding pada gambar, menggunakan threshold dari library OpenCV untuk melakukan segmentasi pada citra grayscale yang disimpan di variable gray

```bash
contours, hierarchy = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
```
Menggunakan fungsi findContours untuk menemukan kontur pada citra threshold

```bash
contour_image = cv2.drawContours(image.copy(), contours, -1, (0, 0, 255), 3)
```
Menggunakan fungsi drawContours pada openCV untuk menggambar kontur pada citra asli

```bash
white_bg = np.ones_like(image) * 255
contour_white_bg = cv2.drawContours(white_bg.copy(), contours, -1, (0, 0, 0), 3)
```
Menggunakan Numpy untuk membuat latar belakang Putih

```bash
adli.subplot(131)
adli.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
adli.title('Original Image')
adli.axis('on') #jika tidak ingin ada koordinat di off kan
```
Menampilkan Citra Asli

```bash
adli.subplot(132)
adli.imshow(cv2.cvtColor(contour_white_bg, cv2.COLOR_BGR2RGB))
adli.title('Contour Image')
adli.axis('on') #jika tidak ingin ada koordinat di off kan
```
Menampilkan Gambar dengan kontur pada background putih

```bash
adli.subplot(133)
adli.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
adli.axis('on') #jika tidak ingin ada koordinat di off kan
```
Menampilkan gambar dengan kontur pada background gambar aslinya
adli.tight_layout()
adli.show()



