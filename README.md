# PA-PC_202231001_Lily-Fitri-Hasanah_PencitB


Projek ini mengenai pengolahan gambar geometris menggunakan Python dengan menggunakan pustaka seperti OpenCV (cv2) dan Matplotlib. Pemrosesan gambar geometris adalah bagian dari bidang pengolahan gambar komputer yang mencakup transformasi geometris terhadap gambar, seperti rotasi, scaling (resize), cropping, flipping, dan translasi. Berikut adalah beberapa konsep teoritis yang mendukung projek ini:

### 1. Rotasi Gambar

Rotasi gambar adalah salah satu teknik dasar dalam pengolahan citra yang digunakan untuk mengubah orientasi sebuah gambar terhadap suatu titik tertentu. Konsep rotasi pada dasarnya melibatkan transformasi geometris dari titik-titik piksel dalam gambar terhadap pusat rotasi yang ditentukan.

### 2. Resize Gambar

Resize atau redimension adalah proses mengubah ukuran sebuah gambar. Dalam konteks pengolahan citra, resize sering kali diperlukan untuk menyesuaikan ukuran gambar dengan kebutuhan tampilan atau pemrosesan berikutnya.

- **Interpolasi**: Saat meresize gambar, interpolasi digunakan untuk menghitung nilai piksel yang baru di antara piksel-piksel yang ada. Interpolasi seperti bilinear atau bicubic digunakan untuk menjaga kualitas gambar saat meresize.

### 3. Cropping Gambar

Cropping atau pemotongan adalah proses mengambil sebagian dari gambar asli dengan cara menghilangkan bagian yang tidak diperlukan. Pemotongan digunakan untuk memfokuskan perhatian pada area tertentu dalam gambar.

- **Operasi Slicing**: Dalam pemrograman pengolahan citra, pemotongan gambar dapat dicapai dengan operasi slicing pada array atau matriks gambar, yaitu dengan menentukan rentang piksel yang ingin dipertahankan.

### 4. Flipping Gambar

Flipping atau flipping gambar adalah proses membalik gambar secara horizontal atau vertikal. Ini sering digunakan untuk tujuan visualisasi atau analisis lebih lanjut dari sudut pandang yang berbeda.

- **Matriks Transformasi**: Flipping horizontal dan vertikal menggunakan matriks transformasi khusus yang mengubah koordinat piksel sesuai dengan arah flipping yang diinginkan.

### 5. Translasi Gambar

Translasi adalah proses menggeser seluruh gambar dari satu lokasi ke lokasi lain dalam koordinat gambar. Translasi digunakan untuk memindahkan gambar ke posisi yang diinginkan dalam analisis atau visualisasi.

- **Matriks Translasi**: Dalam pengolahan citra, translasi dilakukan dengan menggunakan matriks translasi yang menggeser koordinat piksel gambar sesuai dengan vektor translasi yang diberikan.

Berikut adalah penjelasan rinci mengenai implementasi geometrix citra dalam python 

### Mengimpor Library

```python
import numpy as np
import cv2 as cv
import matplotlib.pyplot as plt
```

- `import numpy as np`: Mengimpor library NumPy dengan alias `np`. NumPy digunakan untuk operasi numerik dan manipulasi array, yang sangat berguna dalam pengolahan citra.
  
- `import cv2 as cv`: Mengimpor library OpenCV dengan alias `cv`. OpenCV adalah library yang kuat untuk pengolahan citra dan komputer vision.
  
- `import matplotlib.pyplot as plt`: Mengimpor modul `pyplot` dari library Matplotlib dengan alias `plt`. Matplotlib digunakan untuk membuat plot dan visualisasi, termasuk menampilkan gambar hasil pengolahan.

### Membaca dan Mengubah Warna Gambar

```python
# Membaca gambar
img = cv.imread('lifina.jpg')
# Mengubah warna dari BGR ke RGB
img_rgb = cv.cvtColor(img, cv.COLOR_BGR2RGB)
```

- `img = cv.imread('lifina.jpg')`: Membaca gambar dengan nama file 'lifina.jpg' menggunakan fungsi `cv.imread()` dari OpenCV. Gambar dibaca dalam format BGR (Blue-Green-Red).
  
- `img_rgb = cv.cvtColor(img, cv.COLOR_BGR2RGB)`: Mengubah format warna gambar dari BGR ke RGB menggunakan fungsi `cv.cvtColor()` dari OpenCV. Ini diperlukan karena Matplotlib menggunakan urutan warna RGB untuk menampilkan gambar.

### Rotasi Gambar

```python
# Rotasi 45 derajat
rows, cols = img_rgb.shape[:2]
M_rotation = cv.getRotationMatrix2D(((cols-1)/2.0, (rows-1)/2.0), 45, 1)
img_rotated = cv.warpAffine(img_rgb, M_rotation, (cols, rows))
```

- `rows, cols = img_rgb.shape[:2]`: Mengambil dimensi tinggi (`rows`) dan lebar (`cols`) gambar setelah dikonversi ke RGB. Ini digunakan untuk menentukan pusat rotasi.
  
- `M_rotation = cv.getRotationMatrix2D(((cols-1)/2.0, (rows-1)/2.0), 45, 1)`: Menghitung matriks transformasi rotasi menggunakan `cv.getRotationMatrix2D()`. Pusat rotasi diatur di tengah gambar dengan sudut rotasi 45 derajat dan faktor skala 1.
  
- `img_rotated = cv.warpAffine(img_rgb, M_rotation, (cols, rows))`: Menerapkan rotasi ke gambar menggunakan `cv.warpAffine()`, dengan menggunakan matriks rotasi `M_rotation` yang sudah dihitung sebelumnya.

### Resize Gambar

```python
# Resize dengan faktor 0.5
resized_height, resized_width = int(rows * 1), int(cols * 0.5)
img_resized = cv.resize(img_rgb, (resized_width, resized_height), interpolation=cv.INTER_CUBIC)
```

- `resized_height, resized_width = int(rows * 1), int(cols * 0.5)`: Menghitung tinggi dan lebar baru gambar setelah diresize dengan faktor 0.5 dari lebar asli.
  
- `img_resized = cv.resize(img_rgb, (resized_width, resized_height), interpolation=cv.INTER_CUBIC)`: Meresize gambar menggunakan `cv.resize()`. Parameter `interpolation=cv.INTER_CUBIC` digunakan untuk metode interpolasi Cubic yang memberikan hasil yang lebih halus.

### Cropping Gambar

```python
# Posisi crop
start_row, start_col = int(rows * 0.1), int(cols * 0.1)
end_row, end_col = int(rows * 0.9), int(cols * 0.9)
img_cropped = img_rgb[start_row:end_row, start_col:end_col]
```

- `start_row, start_col = int(rows * 0.1), int(cols * 0.1)`: Menghitung titik awal untuk cropping pada 10% dari tinggi dan lebar gambar.
  
- `end_row, end_col = int(rows * 0.9), int(cols * 0.9)`: Menghitung titik akhir untuk cropping pada 90% dari tinggi dan lebar gambar.
  
- `img_cropped = img_rgb[start_row:end_row, start_col:end_col]`: Melakukan cropping gambar menggunakan operasi slicing pada array `img_rgb`, dengan membatasi area gambar dari `start_row` sampai `end_row` dan dari `start_col` sampai `end_col`.

### Flipping Horizontal

```python
# Flipping horizontal
img_flipped = cv.flip(img_rgb, 1)
```

- `img_flipped = cv.flip(img_rgb, 1)`: Melakukan flipping horizontal terhadap gambar menggunakan `cv.flip()` dengan parameter `1`, yang menunjukkan flipping horizontal. Hasilnya disimpan dalam variabel `img_flipped`.

### Translasi Gambar

```python
# Translasi gambar
M_translation = np.float32([[1, 0, 50], [0, 1, 50]])
img_translated = cv.warpAffine(img_rgb, M_translation, (cols, rows))
```

- `M_translation = np.float32([[1, 0, 50], [0, 1, 50]])`: Mendefinisikan matriks transformasi translasi `M_translation` menggunakan NumPy. Matriks ini akan menggeser gambar sebesar 50 piksel ke kanan dan 50 piksel ke bawah.
  
- `img_translated = cv.warpAffine(img_rgb, M_translation, (cols, rows))`: Menerapkan translasi ke gambar menggunakan `cv.warpAffine()`, dengan menggunakan matriks translasi `M_translation` yang sudah dihitung sebelumnya.

### Menampilkan Hasil Secara Bersamaan

```python
# Menampilkan hasil secara bersamaan
fig, axs = plt.subplots(2, 3, figsize=(15, 10))

axs[0, 0].imshow(img_rgb)
axs[0, 0].set_title('Citra Asli')
axs[0, 0].axis('on')

axs[0, 1].imshow(img_rotated)
axs[0, 1].set_title('Setelah Rotasi')
axs[0, 1].axis('on')

axs[0, 2].imshow(img_resized)
axs[0, 2].set_title('Setelah Resize')
axs[0, 2].axis('on')

axs[1, 0].imshow(img_cropped)
axs[1, 0].set_title('Setelah Cropped')
axs[1, 0].axis('on')

axs[1, 1].imshow(img_flipped)
axs[1, 1].set_title('Setelah Flipped')
axs[1, 1].axis('on')

axs[1, 2].imshow(img_translated)
axs[1, 2].set_title('Setelah Translasi')
axs[1, 2].axis('on')

plt.tight_layout()
plt.show()
```

- `fig, axs = plt.subplots(2, 3, figsize=(15, 10))`: Membuat subplot grid 2x3 dengan ukuran gambar keseluruhan 15x10 inci.
  
- Setiap gambar hasil transformasi ditampilkan dalam subplot yang sesuai menggunakan `imshow()` dan diberi judul dengan `set_title()`.

- `plt.tight_layout()`: Mengatur tata letak plot agar lebih rapi sebelum menampilkan dengan `plt.show()`.
