### Clustering Kondisi Ekonomi Provinsi di Indonesia Menggunakan Metode K-Means Clustering

![Python](https://img.shields.io/badge/Python-3.x-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-KMeans-orange) ![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-yellow) ![Status](https://img.shields.io/badge/Status-Selesai-green)

Analisis **unsupervised machine learning** untuk mengelompokkan 38 provinsi di Indonesia berdasarkan indikator kesejahteraan dan kapasitas ekonomi. Menggunakan Elbow Method dan Silhouette Score untuk pemilihan jumlah cluster optimal, serta berbagai visualisasi seperti PCA Biplot, Radar Chart, dan Heatmap Z-Score.

---

## 📋 Daftar Isi
- [Dataset](#dataset)
- [Instalasi](#instalasi)
- [Cara Menjalankan](#cara-menjalankan)
- [Metodologi](#metodologi)
- [Hasil Clustering](#hasil-clustering)
- [Evaluasi Model](#evaluasi-model)
- [Visualisasi yang Dihasilkan](#visualisasi-yang-dihasilkan)
- [Struktur File](#struktur-file)
- [Temuan Kunci](#temuan-kunci)
- [Referensi](#referensi)

---

## 📊 Dataset

**Sumber:** `dataset_ekonomi.xlsx` — Data BPS (Badan Pusat Statistik) Indonesia 2023

| Spesifikasi | Nilai |
|-------------|-------|
| Jumlah Provinsi | 38 |
| Jumlah Variabel | 4 |
| Missing Values | 0 |
| Duplikat | 0 |

### Variabel

| Variabel | Deskripsi | Satuan |
|----------|-----------|--------|
| `IPM` | Indeks Pembangunan Manusia | Skor (0–100) |
| `Kemiskinan` | Persentase penduduk miskin | % |
| `Pengangguran` | Tingkat Pengangguran Terbuka (TPT) | % |
| `PDRB` | Produk Domestik Regional Bruto | Miliar Rupiah |

### Statistik Deskriptif

| Variabel | Min | Max | Mean | Std |
|----------|-----|-----|------|-----|
| IPM | 54.91 | 85.05 | 74.45 | 4.83 |
| Kemiskinan | 3.42 | 29.45 | 9.64 | 6.12 |
| Pengangguran | 1.49 | 6.96 | 4.36 | 1.35 |
| PDRB | 19,111 | 367,687 | 87,154 | 68,941 |

---

## ⚙️ Instalasi

```bash
git clone https://github.com/username/clustering-ekonomi-indonesia
cd clustering-ekonomi-indonesia
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl nbformat scipy
```

---

## 🚀 Cara Menjalankan

```bash
# Pastikan dataset_ekonomi.xlsx ada di folder yang sama
jupyter notebook Clustering_Ekonomi_Provinsi_Indonesia.ipynb
```

Atau buka di **Google Colab** dengan upload kedua file `dataset_ekonomi.xlsx` dan notebook ke sesi yang sama.

---

## 🔬 Metodologi

```
Raw Data (38 Provinsi × 4 Variabel)
         │
         ▼
  Eksplorasi Data (EDA)
  ─ Statistik deskriptif
  ─ Histogram + Boxplot
  ─ Matriks Korelasi
         │
         ▼
  Preprocessing
  ─ Standarisasi Z-Score (StandardScaler)
         │
         ▼
  Penentuan K Optimal
  ─ Elbow Method (WCSS/Inertia)
  ─ Silhouette Score per K
  → K = 4 dipilih
         │
         ▼
  K-Means Clustering (K=4)
  n_init=20, max_iter=500, random_state=42
         │
         ▼
  Visualisasi & Interpretasi
  ─ PCA Biplot, Radar Chart
  ─ Heatmap, Scatter Matrix
  ─ Silhouette Plot
         │
         ▼
  Evaluasi Model
  ─ Silhouette Score
  ─ Davies-Bouldin Index
  ─ Calinski-Harabasz Score
```

---

## 📈 Hasil Clustering (K = 4)

### Distribusi Provinsi

| Cluster | Nama | Jumlah Provinsi | % |
|---------|------|-----------------|---|
| C1 | Ekonomi Sangat Rendah | 9 | 23.7% |
| C2 | Ekonomi Berkembang | 19 | 50.0% |
| C3 | Ekonomi Menengah* | 5 | 13.2% |
| C4 | Ekonomi Maju | 5 | 13.2% |

### Profil Rata-Rata per Cluster

| Cluster | IPM | Kemiskinan (%) | Pengangguran (%) | PDRB (Miliar Rp) |
|---------|-----|----------------|-----------------|------------------|
| C1 – Sangat Rendah | 75.42 | 10.47 | 6.23 | 63,665 |
| C2 – Berkembang | 74.94 | 8.30 | 3.73 | 70,276 |
| C3 – Menengah* | 64.69 | 22.60 | 3.44 | 71,331 |
| C4 – Maju | 79.06 | 5.05 | 5.14 | 226,614 |

### Detail Provinsi per Cluster

**🔴 Cluster 1 — Ekonomi Sangat Rendah (9 provinsi)**
> Pengangguran tertinggi, PDRB rendah, membutuhkan intervensi kebijakan serius.

Aceh · Sumatera Utara · Sumatera Barat · Jawa Barat · Banten · Sulawesi Utara · Maluku · Papua Barat Daya · Papua

---

**🟡 Cluster 2 — Ekonomi Berkembang (19 provinsi)**
> Kluster terbesar, pengangguran moderat, kemiskinan sedang, potensi pertumbuhan tinggi.

Jambi · Sumatera Selatan · Bengkulu · Lampung · Kepulauan Bangka Belitung · Jawa Tengah · DI Yogyakarta · Jawa Timur · Bali · Nusa Tenggara Barat · Kalimantan Barat · Kalimantan Tengah · Kalimantan Selatan · Sulawesi Tengah · Sulawesi Selatan · Sulawesi Tenggara · Gorontalo · Sulawesi Barat · Maluku Utara

---

**🔵 Cluster 3 — Ekonomi Menengah* (5 provinsi)**
> *Catatan: Meskipun PDRB relatif sedang, kemiskinan sangat tinggi (>17%) dan IPM sangat rendah — anomali akibat disparitas distribusi sumber daya alam Papua.*

Nusa Tenggara Timur · Papua Barat · Papua Selatan · Papua Tengah · Papua Pegunungan

---

**🟢 Cluster 4 — Ekonomi Maju (5 provinsi)**
> IPM tertinggi, kemiskinan terendah, PDRB rata-rata 3.5× lebih besar dari kluster lain.

Riau · Kepulauan Riau · DKI Jakarta · Kalimantan Timur · Kalimantan Utara

---

## 📉 Evaluasi Model

| Metrik | Nilai | Interpretasi |
|--------|-------|-------------|
| **Silhouette Score** | 0.3465 | Struktur cluster sedang — valid digunakan |
| **Davies-Bouldin Index** | 0.8904 | ↓ lebih baik; antar cluster cukup terpisah |
| **Calinski-Harabasz Score** | 21.22 | ↑ lebih baik; separasi cluster memadai |
| **Inertia (WCSS)** | 52.92 | Kompak relatif terhadap skala data |

> **Interpretasi Silhouette Score:**
> - `> 0.70` = Struktur sangat kuat
> - `0.50 – 0.70` = Struktur kuat
> - `0.25 – 0.50` = Struktur sedang ✅ *(kasus ini)*
> - `< 0.25` = Struktur lemah

---

## 🖼️ Visualisasi yang Dihasilkan

| File | Deskripsi |
|------|-----------|
| `distribusi_variabel.png` | Histogram + Boxplot keempat variabel |
| `matriks_korelasi.png` | Heatmap korelasi antar variabel |
| `elbow_method.png` | Kurva WCSS untuk pemilihan K |
| `silhouette_score.png` | Bar chart silhouette per nilai K |
| `profil_cluster.png` | Bar chart profil rata-rata per cluster |
| `pca_biplot.png` | Scatter plot PCA 2D dengan loading vector |
| `radar_chart.png` | Radar chart 4-panel profil cluster |
| `heatmap_cluster.png` | Clustermap Z-Score seluruh provinsi |
| `silhouette_plot.png` | Silhouette coefficient per sampel |
| `scatter_matrix.png` | Matriks scatter antar semua variabel |

---

## 📁 Struktur File

```
clustering-ekonomi-indonesia/
│
├── data
│    ├── raw
│    │   ├── Indeks Pembangunan Manusia Menurut Provinsi, 2025.xlsx
│    │   ├── Persentase Penduduk Miskin (P0) Menurut Provinsi dan Daerah, 2025.xlsx
│    │   ├── Produk Domestik Regional Bruto per Kapita Atas Dasar Harga Berlaku Menurut Provinsi (ribu rupiah), 2025.xlsx
│    │   └── Tingkat Pengangguran Terbuka Menurut Provinsi, 2025.xlsx
│    ├── processed
│    │   ├── dataset_ekonomi.xlsx
│    │   └── hasil_clustering.xlsx
├── notebook
│    └── Clustering_Ekonomi_Provinsi_Indonesia.ipynb
│
├── 📄 README.md                                    
│
└── 📁 images/
    ├── distribusi_variabel.png
    ├── matriks_korelasi.png
    ├── elbow_method.png
    ├── silhouette_score.png
    ├── profil_cluster.png
    ├── pca_biplot.png
    ├── radar_chart.png
    ├── heatmap_cluster.png
    ├── silhouette_plot.png
    └── scatter_matrix.png
```

---

## 💡 Temuan Kunci

1. **Kesenjangan geografis signifikan** — Provinsi di Jawa dan Kalimantan Timur jauh melampaui Papua dalam IPM dan PDRB.
2. **Kemiskinan ekstrem di Papua** — Papua Tengah (29.45%) dan Papua Pegunungan (27.21%) memiliki angka kemiskinan tertinggi secara nasional.
3. **Anomali DI Yogyakarta** — IPM tinggi (82.48) namun kemiskinan relatif tinggi (10.08%), mengindikasikan distribusi pendapatan yang tidak merata.
4. **PDRB tinggi ≠ Kesejahteraan tinggi** — Beberapa provinsi kaya SDA memiliki IPM rendah, menunjukkan tantangan dalam distribusi hasil ekonomi.
5. **Dominasi Cluster 4** — Hanya 5 provinsi (13.2%) menguasai rata-rata PDRB 3.5× lebih besar dari provinsi-provinsi di Cluster 1.

### Rekomendasi Kebijakan

| Cluster | Prioritas |
|---------|-----------|
| 🔴 C1 – Sangat Rendah | Intervensi pemerintah pusat intensif: program pengentasan kemiskinan + penyerapan tenaga kerja |
| 🟡 C2 – Berkembang | Stimulus ekonomi daerah, peningkatan kualitas pendidikan dan infrastruktur |
| 🔵 C3 – Menengah | Reformasi distribusi pendapatan SDA, percepatan pembangunan SDM di Papua |
| 🟢 C4 – Maju | Pertahankan momentum, perkuat efek trickle-down ke wilayah sekitar |

---

## 📚 Referensi

- MacQueen, J. (1967). *Some methods for classification and analysis of multivariate observations*. Proceedings of the 5th Berkeley Symposium.
- Rousseeuw, P. J. (1987). *Silhouettes: A graphical aid to the interpretation and validation of cluster analysis*. Journal of Computational and Applied Mathematics.
- Davies, D. L., & Bouldin, D. W. (1979). *A cluster separation measure*. IEEE Transactions on Pattern Analysis and Machine Intelligence.
- **Data:** Badan Pusat Statistik (BPS) Indonesia — [www.bps.go.id](https://www.bps.go.id)

---

> 📌 **Catatan:** Analisis ini bersifat akademis menggunakan data statis. Untuk keperluan kebijakan, disarankan menggunakan data terkini dari BPS dan menggabungkan variabel tambahan seperti akses layanan kesehatan, infrastruktur, dan indikator ketimpangan (Gini Ratio).

---

*Dibuat dengan Python · scikit-learn · Jupyter Notebook*
                                                                                                                                                            
