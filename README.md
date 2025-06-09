# Analisis Prediksi Kerawanan Banjir Kota Bengkulu

Proyek ini melakukan analisis dan pemetaan spasial prediksi kerawanan banjir di Kecamatan Kota Bengkulu menggunakan data geografis (shapefile) dan data tabular (CSV) hasil prediksi model machine learning.

## Tujuan Proyek

Tujuan dari proyek ini adalah:
1.  Membangun model klasifikasi sederhana untuk memprediksi kerawanan banjir berdasarkan fitur-fitur lahan.
2.  Melakukan geovisualisasi hasil prediksi kerawanan banjir pada peta administrasi Kecamatan Kota Bengkulu.
3.  Menyediakan peta visual yang menunjukkan tingkat kerawanan banjir per kecamatan berdasarkan model.

## Dataset

Proyek ini menggunakan beberapa file data:

1.  **Data Tabular Prediksi:**
    *   `Pembagian_Lahan_Kota_Bengkulu (1) (1).csv`: Berisi data pembagian lahan (terbangun, non-terbangun, sawah/perkebunan) per kecamatan dan data target kerawanan banjir (hasil simulasi atau data aktual jika tersedia). File ini juga akan digunakan untuk menyimpan hasil prediksi.
    *   `prediksi_banjir_kota_bengkulu.csv`: Output dari proses pemodelan, berisi nama kecamatan dan hasil prediksi kerawanan banjir (0 atau 1).

2.  **Data Geografis (Shapefile):**
    *   Sebuah file ZIP yang berisi shapefile administrasi Kecamatan Kota Bengkulu. File ZIP ini harus mengandung file-file standar shapefile (`.shp`, `.shx`, `.dbf`, `.prj`, dll.).

**Catatan:** Nama file di atas mungkin perlu disesuaikan jika Anda menggunakan nama file yang berbeda.

## Struktur File

Pastikan file notebook (`.ipynb`) dan file data yang dibutuhkan berada dalam direktori kerja yang sama, atau sesuaikan path file dalam kode.

## Persyaratan (Requirements)

Proyek ini membutuhkan library Python berikut. Library ini akan diinstal secara otomatis oleh notebook.

*   `geopandas`
*   `rasterio`
*   `contextily`
*   `shapely`
*   `pandas`
*   `numpy`
*   `scikit-learn`
*   `matplotlib`
*   `seaborn`
*   `zipfile`
*   `os`
*   `google.colab` (jika dijalankan di Google Colab)

## Cara Menjalankan Kode

Kode ini dirancang untuk dijalankan di lingkungan Google Colab, meskipun dapat diadaptasi untuk lingkungan Jupyter Notebook lokal.

1.  **Buka Notebook:** Upload atau buka file notebook (`.ipynb`) di Google Colab.
2.  **Jalankan Sel Kode Secara Berurutan:** Jalankan setiap sel kode satu per satu dari atas ke bawah.
3.  **Upload File:** Pada sel yang meminta upload file (`files.upload()`), ikuti instruksi untuk mengupload file CSV data awal (`Pembagian_Lahan_Kota_Bengkulu (1) (1).csv`), file ZIP shapefile administrasi, dan file CSV prediksi yang dihasilkan (`prediksi_banjir_kota_bengkulu.csv`) saat diminta.
4.  **Ikuti Output:** Notebook akan mencetak output untuk menunjukkan proses pemodelan, evaluasi, dan informasi kolom dari data. Peta hasil prediksi akan ditampilkan di akhir proses.
5.  **Download File Hasil:** Notebook akan secara otomatis mengunduh file `prediksi_banjir_kota_bengkulu.csv` yang berisi hasil prediksi untuk setiap kecamatan.

## Penjelasan Kode Singkat

*   **Instalasi & Impor:** Menginstal library yang dibutuhkan dan mengimpornya.
*   **Upload File:** Menggunakan `google.colab.files.upload()` untuk mengunggah data dari lokal.
*   **Data Loading & Preprocessing:** Membaca data CSV, menambahkan kolom 'Curah Hujan' (simulasi), dan menyiapkan data untuk model.
*   **Split Data:** Membagi data menjadi set pelatihan dan pengujian.
*   **Model Training:** Melatih model RandomForestClassifier.
*   **Evaluasi Model:** Menghitung metrik evaluasi untuk model.
*   **Feature Importance:** Menampilkan pentingnya setiap fitur dalam model.
*   **Prediksi & Simpan Hasil:** Melakukan prediksi pada data asli dan menyimpan hasilnya ke CSV.
*   **Proses Shapefile:** Mengunggah dan mengekstrak file ZIP shapefile, kemudian membacanya menggunakan GeoPandas.
*   **Merge Data:** Menggabungkan GeoDataFrame shapefile dengan DataFrame prediksi berdasarkan nama kecamatan yang telah "dibersihkan".
*   **Visualisasi Peta:** Membuat peta visualisasi hasil prediksi kerawanan banjir, dengan warna yang berbeda untuk 'Rawan Banjir', 'Tidak Rawan', dan 'Data Tidak Tersedia'.

## Penanganan Data Tidak Tersedia (Abu-abu pada Peta)

Jika pada peta terlihat area berwarna abu-abu muda ('Data Tidak Tersedia'), ini menandakan adanya ketidakcocokan nama kecamatan antara data shapefile dan data prediksi setelah proses pembersihan. Bagian kode setelah sel yang menyebabkan error sebelumnya sudah dilengkapi dengan langkah-langkah diagnosis untuk mencetak nama-nama unik dari kedua sumber data *setelah* dibersihkan.

Untuk mengurangi area abu-abu:
1.  **Periksa Output Diagnosis:** Analisis output yang mencetak daftar nama kecamatan unik dari CSV dan shapefile, serta daftar area yang tidak cocok (`unmatched_areas`).
2.  **Sesuaikan Fungsi `clean_name`:** Modifikasi fungsi `clean_name` untuk menangani perbedaan penamaan spesifik yang Anda temukan (misalnya, ejaan berbeda, penggunaan singkatan, spasi/tanda hubung).
3.  **Verifikasi Nama Kolom:** Pastikan kolom yang digunakan untuk merge (`'Kecamatan'` di CSV dan `'NAMOBJ'` di shapefile) adalah kolom yang benar-benar berisi nama kecamatan yang relevan.
4.  **Cek Kelengkapan Data:** Konfirmasi apakah data CSV prediksi Anda memang mencakup semua kecamatan yang ada di shapefile.

## Kontribusi

Jika Anda ingin berkontribusi pada proyek ini, silakan buat Fork repositori, lakukan perubahan, dan ajukan Pull Request.


---

*Dibuat dengan ❤️*
