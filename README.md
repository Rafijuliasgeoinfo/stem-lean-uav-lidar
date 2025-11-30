# STEM LEAN FROM UAV LiDAR
### Measuring Tree Stem Lean Angle and Azimuth from Point Cloud

Repository ini berisi notebook dan data contoh untuk menghitung **kemiringan batang pohon (stem lean angle dan azimuth)** dari data LiDAR berbasis UAV. Analisis dilakukan dengan **Python di Google Colab**, sehingga dapat dijalankan tanpa instalasi khusus di komputer lokal.

Notebook utama: `STEM_LEAN_LIDAR.ipynb`.

---

## 🎯 Tujuan

Repo ini disusun untuk:

- Menyediakan workflow lengkap perhitungan **stem lean** dari point cloud LiDAR.
- Menunjukkan bagaimana kemiringan batang pohon dapat digunakan sebagai **biosensor deformasi** tanah dan indikasi zona reaktivasi longsor.
- Menjadi bahan ajar / tutorial untuk topik **longsor, stabilitas lereng, dan deformasi vegetasi**.

---

## 📂 Struktur Repository

Struktur folder yang disarankan:

```text
.
├── STEM_LEAN_LIDAR.ipynb          # notebook utama (Google Colab)
├── data/
│   └── sample_tree_pointcloud.csv # data contoh point cloud (format CSV)
└── README.md                      # file ini
```

---

## 🌲 Data Input: Point Cloud CSV

Notebook menggunakan data point cloud dalam format **CSV** dengan kolom:

- `X`  : koordinat X (mis. UTM / koordinat lokal)
- `Y`  : koordinat Y
- `Z`  : elevasi titik (di atas permukaan laut atau datum tertentu)
- `tree_id` : ID pohon, digunakan untuk membedakan tiap pohon / cluster titik
- `HeightAboveGround` : tinggi titik dari permukaan tanah (height above ground)

Contoh baris data:

| X         | Y          | Z       | tree_id | HeightAboveGround |
|----------:|-----------:|--------:|--------:|------------------:|
| 456782.12 | 9123450.55 | 103.55  | 1       | 5.23              |
| 456782.35 | 9123450.60 | 104.10  | 1       | 5.78              |
| 456783.00 | 9123451.10 | 110.20  | 2       | 10.45             |

File CSV contoh disarankan diberi nama:

```text
data/sample_tree_pointcloud.csv
```

Dengan adanya kolom `tree_id`, notebook dapat memproses **setiap pohon** secara terpisah (per-tree processing), menghitung sumbu batang, lean angle, dan azimuth untuk masing-masing pohon.

---

## 🌲 Konsep: Stem Lean (Kemiringan Batang)

Notebook berfokus pada dua parameter utama:

- **Lean angle (°)**  
  Sudut kemiringan batang terhadap garis vertikal (0° = tegak, nilai lebih besar = lebih miring).

- **Lean azimuth (°)**  
  Arah kemiringan batang pada bidang horizontal (0–360°).  
  Secara konvensi:
  - 0°   → Utara  
  - 90°  → Timur  
  - 180° → Selatan  
  - 270° → Barat  

Pola spasial lean angle dan azimuth dapat digunakan untuk:

- Mengidentifikasi **zona reaktivasi longsor**  
- Menginferensikan **arah pergerakan massa tanah**  
- Menghubungkan ciri vegetasi dengan **struktur bawah permukaan** (misalnya dari ERT)

---

## ⚙️ Dependensi & Lingkungan

Notebook ditulis untuk dijalankan di **Google Colab**.

Pustaka Python yang umum digunakan (bisa disesuaikan dengan isi notebook):

- `numpy`
- `pandas`
- `matplotlib`
- `mpl_toolkits.mplot3d`
- (opsional) `scipy` untuk analisis PCA / fitting vektor batang
- (opsional) pustaka geospasial lain (`geopandas`, dll.)

Instalasi pustaka tambahan di Colab dapat dilakukan, misalnya:

```python
!pip install numpy pandas matplotlib
```

(atau sesuai kebutuhan aktual notebook).

---

## ▶️ Cara Menjalankan Notebook di Google Colab

1. **Buka Colab dan upload notebook**

   - Buka: https://colab.research.google.com  
   - Klik **Upload** lalu pilih `STEM_LEAN_LIDAR.ipynb`.

2. **Upload data point cloud**

   - Buka panel **Files** (ikon folder di kiri Colab).
   - Buat folder `data` (untuk kerapian).
   - Upload file CSV (mis. `sample_tree_pointcloud.csv`) ke dalam folder tersebut.
   - Sesuaikan path di notebook, misalnya:
     ```python
     data_path = "/content/data/sample_tree_pointcloud.csv"
     ```

3. **Jalankan sel-sel notebook**

   Urutan umum:
   - Import pustaka
   - Load data CSV
   - Grouping berdasarkan `tree_id`
   - Estimasi sumbu batang per pohon
   - Perhitungan lean angle & azimuth
   - Visualisasi 2D/3D dan analisis grafik

---

## 📈 Output

Notebook dapat menghasilkan:

- Tabel / DataFrame berisi:
  - `tree_id`
  - Lean angle (°)
  - Lean azimuth (°)
  - Koordinat / vektor sumbu batang

- Visualisasi:
  - Plot 3D point cloud dan model batang
  - Histogram sudut kemiringan
  - Scatter plot atau diagram arah kemiringan

Output ini dapat digunakan untuk:

- Analisis deformasi vegetasi
- Identifikasi zona kritis pada lereng
- Integrasi dengan data geospasial lain (DEM, ERT, peta morfologi, dll.)

---

## 🧩 Pengembangan Lanjutan

Notebook ini dapat dikembangkan lebih lanjut, misalnya untuk:

- Menghubungkan pola kemiringan pohon dengan:
  - Zona retakan tanah
  - Alur akumulasi aliran
  - Zona resistivitas rendah (ERT)
- Membuat:
  - Peta stem lean skala lereng
  - Statistik per zona (kepala, tubuh, kaki longsor)
  - Indikator gabungan morfologi–vegetasi–bawah permukaan

---

## 📜 Lisensi

Script dan struktur repo ini dapat digunakan untuk:

- Penelitian
- Tugas akhir / tesis
- Edukasi dan pelatihan

Mohon cantumkan kredit atau referensi yang sesuai jika metode atau script ini digunakan dalam publikasi ilmiah.

---
