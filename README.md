# LAPORAN PROJECT AKHIR UAS PRAKTIKUM PCD

Teori Deteksi Tepi Pola Objek

Deteksi tepi pola objek adalah teknik untuk mengidentifikasi titik-titik dalam citra di mana intensitas berubah tajam. Ini membantu dalam menemukan batas-batas objek dan fitur-fitur penting dalam citra. Algoritma deteksi tepi biasanya mengandalkan kalkulasi gradien intensitas piksel dalam citra.

Fungsi Deteksi Tepi
- Segmentasi Objek: Membantu dalam memisahkan objek dari latar belakang.
- Pengenalan Bentuk: Identifikasi bentuk dan struktur objek dalam citra.
- Pelacakan Objek: Mengikuti pergerakan objek dari satu frame ke frame berikutnya dalam video.
- Analisis Medis: Mengidentifikasi tepi organ atau tumor dalam citra medis.



Canny Edge Detection
Canny Edge Detection adalah algoritma yang bertujuan untuk mendeteksi tepi yang efisien dan andal. Algoritma ini terdiri dari beberapa langkah untuk memastikan bahwa hanya tepi yang relevan dan akurat yang dideteksi.

* Langkah-langkah dalam Canny Edge Detection
1. Penghalusan (Smoothing):
- Menggunakan filter Gaussian untuk menghaluskan citra dan mengurangi noise. Noise dapat mengganggu deteksi tepi yang akurat.
- Fungsi: cv2.GaussianBlur()
python blurred = cv2.GaussianBlur(image, (5, 5), 1.4)
   
2. Gradien Intensitas:
- Menggunakan operator Sobel untuk menghitung gradien intensitas citra. Gradien ini menunjukkan perubahan intensitas yang tajam.
- Fungsi: cv2.Sobel()
python
grad_x = cv2.Sobel(blurred, cv2.CV_64F, 1, 0, ksize=3)
grad_y = cv2.Sobel(blurred, cv2.CV_64F, 0, 1, ksize=3)
magnitude = cv2.magnitude(grad_x, grad_y)
   
3. Non-maximum Suppression:
- Memastikan bahwa hanya piksel yang merupakan puncak lokal dalam arah gradien yang dipertahankan sebagai tepi.
- Fungsi: Bagian dari cv2.Canny()

4. Double Thresholding:
- Menerapkan dua ambang batas untuk mendeteksi tepi yang kuat dan lemah.
- Fungsi: Bagian dari cv2.Canny()
python
edges = cv2.Canny(blurred, 100, 200)

5. Edge Tracking by Hysteresis:
- Menghubungkan tepi yang lemah ke tepi yang kuat untuk membentuk tepi yang lengkap.
- Fungsi: Bagian dari cv2.Canny()


Fungsi Canny Edge Detection
- Keakuratan Tinggi: Menghasilkan tepi yang sangat akurat dan tajam.
- Reduksi Noise: Mengurangi efek noise yang dapat mengganggu deteksi tepi.
- Deteksi Tepi yang Kuat dan Lemah: Memastikan bahwa tepi penting tidak terlewatkan.


2. Deteksi Kontur
Kontur adalah kurva yang menghubungkan semua titik kontinu dengan warna atau intensitas yang sama. Deteksi kontur digunakan untuk menemukan batas-batas objek dalam citra biner.

* Langkah-langkah dalam Deteksi Kontur
1. Pra-pemrosesan:
- Mengubah citra menjadi biner dengan thresholding atau deteksi tepi.
- Fungsi: cv2.threshold() atau cv2.Canny()
python
ret, binary = cv2.threshold(image, 127, 255, cv2.THRESH_BINARY)
   
2. Deteksi Kontur:
- Menggunakan cv2.findContours() untuk mendeteksi kontur dalam citra biner.
- Fungsi: cv2.findContours()
python
contours, hierarchy = cv2.findContours(binary, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
   
3. Gambar Kontur:
- Menggambar kontur yang terdeteksi pada citra asli atau citra kosong.
- Fungsi: cv2.drawContours()
python
image_contours = cv2.drawContours(cv2.cvtColor(image, cv2.COLOR_GRAY2BGR), contours, -1, (0, 255, 0), 2)

Fungsi Deteksi Kontur
- Segmentasi Objek: Memisahkan dan mengekstrak objek dari latar belakang.
- Pengenalan Pola: Mengidentifikasi bentuk dan pola dalam citra.
- Pengukuran Bentuk: Mengukur parameter bentuk seperti luas, keliling, dan momen.
- Analisis Struktural: Menentukan struktur dan hubungan hierarkis antar objek dalam citra.

// Tahapan cara menyelesaikan projek diatas:

1. Mengimpor Modul yang Diperlukan
   ```python
   import cv2
   import numpy as np
   import matplotlib.pyplot as plt
   ```
   Langkah pertama adalah mengimpor modul OpenCV (cv2), NumPy (numpy), dan Matplotlib (matplotlib.pyplot) yang akan digunakan.

2. Membaca Gambar dari File
   ```python
   img = cv2.imread('maurinn.jpg')
   ```
   Selanjutnya, Menggunakan fungsi cv2.imread untuk membaca gambar dari file dengan nama `maurinn.jpg`. Gambar akan disimpan dalam variabel img sebagai array NumPy.

3. Mengubah Ukuran Gambar
   ```python
   height = 1400
   aspect_ratio = height / img.shape[0]
   new_width = int(img.shape[1] * aspect_ratio)
   img_resized = cv2.resize(img, (new_width, height))
   ```
   - height ditetapkan menjadi 1400 piksel.
   - Menghitung rasio aspek (aspect_ratio) berdasarkan tinggi gambar yang baru dengan tinggi gambar yang asli.
   - Menghitung lebar baru berdasarkan rasio aspek.
   - Mengubah ukuran gambar menggunakan cv2.resize dengan dimensi baru.

4. Konversi Gambar ke Warna RGB
   ```python
   img_rgb = cv2.cvtColor(img_resized, cv2.COLOR_BGR2RGB)
   ```
   OpenCV membaca gambar dalam format BGR. Langkah ini mengonversi gambar dari BGR ke RGB menggunakan `cv2.cvtColor`.

5. Deteksi Tepi Menggunakan Canny Edge Detection
   ```python
   edges = cv2.Canny(img_resized, 100, 150)
   ```
   Menggunakan metode Canny untuk mendeteksi tepi pada gambar. Nilai threshold yang digunakan adalah 100 dan 150.

6. Menampilkan Gambar Asli dan Hasil Deteksi Tepi
   ```python
   fig, axs = plt.subplots(1, 2, figsize=(15, 5))
   ax = axs.ravel()
   ax[0].imshow(img_rgb)
   ax[0].set_title("Original Image")
   ax[1].imshow(edges, cmap='gray')
   ax[1].set_title("Canny Edge Detection")
   plt.show()
   ```
   - Membuat dua subplot menggunakan `plt.subplots` untuk menampilkan gambar asli dan hasil deteksi tepi.
   - Menampilkan gambar asli pada subplot pertama (ax[0]).
   - Menampilkan hasil deteksi tepi pada subplot kedua (ax[1]).
   - Mengatur judul untuk masing-masing subplot dan menampilkan plot menggunakan `plt.show()`.

7. Menemukan dan Menggambar Kontur
   ```python
   contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
   contour_image = img_resized.copy()
   cv2.drawContours(contour_image, contours, -1, (0, 255, 0), 2)
   ```
   - Menggunakan `cv2.findContours` untuk menemukan kontur pada peta tepi. `cv2.RETR_EXTERNAL` hanya mengembalikan kontur luar, dan `cv2.CHAIN_APPROX_SIMPLE` menghapus semua titik redundan dan hanya menyimpan
     titik yang diperlukan untuk menggambarkan kontur.
   - Membuat salinan gambar asli untuk menggambar kontur.
   - Menggambar kontur pada gambar salinan menggunakan `cv2.drawContours`. Kontur akan digambar dengan warna hijau `(0, 255, 0)` dan ketebalan garis 2 piksel.

8. Menampilkan Gambar Asli, Hasil Deteksi Tepi, dan Deteksi Kontur
   ```python
   fig, axs = plt.subplots(1, 3, figsize=(15, 5))
   ax = axs.ravel()
   ax[0].imshow(img_rgb)
   ax[0].set_title("Original Image")
   ax[0].axis('off')
   ax[1].imshow(edges, cmap='gray')
   ax[1].set_title("Canny Edge Detection")
   ax[1].axis('off')
   ax[2].imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
   ax[2].set_title("Contours Detection")
   ax[2].axis('off')
   plt.show()
   ```
   - Membuat tiga subplot untuk menampilkan gambar asli, hasil deteksi tepi, dan hasil deteksi kontur.
   - Menampilkan gambar asli, hasil deteksi tepi, dan gambar dengan kontur yang telah dideteksi pada subplot masing-masing.
   - Mengatur judul dan mematikan sumbu untuk setiap subplot.
   - Menampilkan plot menggunakan `plt.show()`.
