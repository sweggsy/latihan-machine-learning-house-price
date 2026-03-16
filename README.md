# House Price Prediction API

Proyek ini merupakan implementasi Pembelajaran Mesin (*Machine Learning*) untuk memprediksi harga rumah berdasarkan set data [Ames Housing](https://www.kaggle.com/c/house-prices-advanced-regression-techniques). Proyek ini mencakup proses eksplorasi data, pelatihan model menggunakan *Gradient Boosting Regressor* (GBR), serta penerapan (*deployment*) model sebagai REST API menggunakan Flask.

## Struktur Repositori

Berikut adalah penjelasan mengenai berkas-berkas yang terdapat di dalam repositori ini:

* **`LATIHAN.ipynb`**: *Jupyter Notebook* yang berisi proses *Exploratory Data Analysis* (EDA), pemrosesan data, pelatihan model *Gradient Boosting Regressor*, dan proses penyimpanan model.
* **`testing_deploy.py`**: Skrip aplikasi web berbasis Flask untuk menyajikan model Pembelajaran Mesin sebagai titik akhir (*endpoint*) API.
* **`gbr_model.joblib` / `gbr_model.pkl`**: Model *Gradient Boosting Regressor* yang telah dilatih dan disimpan (keduanya tersedia dalam format `joblib` dan `pickle`). API secara standar (*default*) menggunakan versi `.joblib`.
* **`train.csv` & `test.csv`**: Set data harga rumah yang digunakan untuk melatih dan menguji model.
* **`sample_submission.csv`**: Contoh format penyerahan (*submission*) untuk kompetisi Kaggle.
* **`data_description.txt`**: Dokumentasi lengkap yang menjelaskan arti dari setiap kolom atau fitur di dalam set data.
* **`data.json`**: Berkas yang berisi contoh format data bawaan (*payload*) berupa susunan (*array*) fitur yang digunakan untuk melakukan pengujian permintaan (*testing request*) ke API.

## Syarat

Pastikan Python telah terinstal pada sistem Anda. Anda memerlukan beberapa pustaka (*library*) berikut untuk menjalankan aplikasi ini:

```bash
pip install Flask scikit-learn pandas numpy joblib
```

## Panduan Penggunaan

1. Eksperimen dan Pelatihan Model (Opsional)
Berkas LATIHAN.ipynb disediakan apabila Anda ingin meninjau ulang proses analisis data atau melatih ulang model dengan parameter yang berbeda.

Langkah-langkah eksekusi:

Buka terminal pada direktori repositori.

Jalankan peladen Jupyter Notebook dengan perintah berikut:

```Bash
jupyter notebook LATIHAN.ipynb
```
Eksekusi sel (cell) di dalam notebook secara berurutan untuk melatih ulang dan memperbarui berkas model (`gbr_model.joblib`).

2. Menjalankan Peladen (Server) Flask API
Untuk menjalankan aplikasi web yang akan menyajikan model sebagai API, ikuti langkah-langkah berikut:

Buka terminal dan arahkan ke direktori tempat repositori ini disimpan.

Jalankan skrip peladen menggunakan perintah berikut:

```Bash
python testing_deploy.py
```
Apabila berhasil, peladen akan beroperasi secara lokal pada alamat standar: `http://127.0.0.1:5000/.`

3. Pengujian Titik Akhir (Endpoint) API
Aplikasi ini menyediakan satu titik akhir utama untuk menerima masukan data dan mengembalikan hasil prediksi.

* Titik Akhir URL: `http://127.0.0.1:5000/predict`

* Metode Permintaan: `POST`

* Tipe Konten (Content-Type): `application/json`

Contoh Pengiriman Permintaan menggunakan cURL:
Pastikan peladen Flask sedang berjalan, kemudian buka terminal baru dan jalankan perintah berikut:

```Bash
curl -X POST http://127.0.0.1:5000/predict -H "Content-Type: application/json" -d @data.json
```

Contoh Format Respons:
API akan memproses data dari data.json dan mengembalikan hasil prediksi harga rumah dalam format JSON.

```JSON
{
    "prediction": [150450.25, 210300.75, 185000.0]
}
```
Catatan Tambahan
Pastikan versi `scikit-learn` yang Anda gunakan saat melatih model di dalam `LATIHAN.ipynb` identik dengan versi yang terinstal saat Anda menjalankan `testing_deploy.py`. Ketidaksesuaian versi dapat menyebabkan error kompatibilitas pada modul `joblib`.
