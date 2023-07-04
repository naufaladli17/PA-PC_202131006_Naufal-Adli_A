
# Deteksi Bentuk Gambar menggunakan Contour

Kontur adalah garis yang menggambarkan batas-batas atau bentuk dari objek dalam gambar. Dalam konteks pengolahan citra dan pengenalan pola, kontur sering digunakan untuk memisahkan objek dari latar belakang atau mengidentifikasi fitur-fitur penting dari objek tersebut. Kontur ditemukan dengan menganalisis perbedaan intensitas piksel di sekitar area objek dalam gambar.

Kontur biasanya terbentuk oleh perubahan tajam dalam intensitas piksel di sekitar objek. Misalnya, dalam gambar biner (hitam-putih), kontur seringkali merupakan garis yang memisahkan piksel bernilai putih (objek) dengan piksel bernilai hitam (latar belakang).

Ada beberapa fitur yang mendukung penggunaan kontur dalam proyek deteksi bentuk gambar,

Contohnya :
Segmentasi Objek
Kontur juga dapat digunakan untuk memisahkan objek dari latar belakang atau mengidentifikasi bagian-bagian objek dalam gambar. Dengan menganalisis kontur, kita dapat mengidentifikasi garis dan lengkungan yang menggambarkan batas objek, yang memungkinkan segmentasi objek yang lebih akurat. Ini dapat digunakan dalam berbagai aplikasi seperti deteksi wajah, deteksi kendaraan, atau deteksi citra medis

pada project ini saya mengaitkan teori dengan jurnal mengenai deteksi citra medis menggunakan contour dengan refrensi jurnal dari Institut Teknologi Sepuluh November, namun untuk membuat project ini saya mengambil poto sisir dari kamera hp saya




# Source Code

import cv2 
import numpy as np 
import matplotlib.pyplot as adli
# Baca gambar
image = cv2.imread('sisir.jpg')
# Konversi gambar ke grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
# Melakukan Thresholding gambar
ret, thresh = cv2.threshold(gray, 127, 255, 0)
# Cari kontur pada gambar
contours, hierarchy = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
# Gambar kontur pada gambar asli
contour_image = cv2.drawContours(image.copy(), contours, -1, (0, 0, 255), 3)
# Buat gambar dengan background putih
white_bg = np.ones_like(image) * 255
contour_white_bg = cv2.drawContours(white_bg.copy(), contours, -1, (0, 0, 0), 3)
# Tampilkan gambar asli
adli.subplot(131)
adli.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
adli.title('Original Image')
adli.axis('on') #jika tidak ingin ada koordinat di off kan

# Tampilkan gambar dengan contour pada background putih
adli.subplot(132)
adli.imshow(cv2.cvtColor(contour_white_bg, cv2.COLOR_BGR2RGB))
adli.title('Contour Image')
adli.axis('on') #jika tidak ingin ada koordinat di off kan

# Tampilkan gambar dengan contour pada background seperti aslinya
adli.subplot(133)
adli.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
adli.axis('on') #jika tidak ingin ada koordinat di off kan

adli.tight_layout()
adli.show()



