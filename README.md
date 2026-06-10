# 🌴 Keranjang Pintar — Aplikasi Android Monitoring & Prediksi Hasil Panen Kelapa Sawit

> Aplikasi Android berbasis **Machine Learning** dan **IoT** untuk monitoring hasil penimbangan tandan buah segar (TBS) kelapa sawit secara *real-time* dan prediksi hasil panen berikutnya menggunakan algoritma **Multiple Linear Regression**.

---

## 📌 Latar Belakang

Industri kelapa sawit di Provinsi Riau merupakan sektor strategis dengan luas perkebunan lebih dari **2,86 juta hektar**. Namun, proses penimbangan TBS masih dilakukan secara manual menggunakan timbangan gantung yang berpotensi menimbulkan:

- ❌ Ketidakakuratan pencatatan hasil panen
- ❌ Potensi kecurangan oleh pekerja atau tokeh sawit
- ❌ Kesulitan pengawasan bagi pemilik lahan yang jauh dari kebun
- ❌ Tidak adanya sistem prediksi untuk perencanaan panen

Sistem ini hadir sebagai solusi digital yang mengintegrasikan **IoT + Android + Machine Learning** untuk menjawab permasalahan tersebut.

> 💡 *Penelitian ini terinspirasi dari keterlibatan langsung penulis dalam program penelitian BPDPKS (Badan Pengelola Dana Perkebunan Kelapa Sawit).*

---

## 🎯 Tujuan

1. Merancang dan membangun aplikasi Android terintegrasi sensor timbangan berbasis IoT
2. Mengimplementasikan algoritma **Multiple Linear Regression** untuk prediksi hasil panen
3. Menyediakan monitoring hasil panen secara *real-time* bagi pemilik lahan
4. Meminimalisir potensi kecurangan dan kesalahan penimbangan

---

## 👤 Pengembang

| Nama | NIM |
|------|-----|
| Teguh Al Azizul | 2355301197 |

**Program Studi:** D4 Teknik Informatika — Politeknik Caltex Riau (TA 2026)  
**Jenis:** Proyek Akhir (PA)

> 📌 *Catatan: Pengembangan perangkat keras IoT (keranjang pintar) dikerjakan oleh PA Said Dafa. PA ini berfokus pada pengembangan perangkat lunak (aplikasi Android) dan implementasi Machine Learning.*

---

## ✨ Fitur Aplikasi

| Fitur | Deskripsi |
|-------|-----------|
| 📊 **Data Panen Harian** | Menampilkan berat panen terbaru, total panen hari ini, dan detail tiap penimbangan dari sensor IoT |
| 📈 **Dashboard Analitik** | Ringkasan KPI panen, analisis tren produksi, dan perbandingan produksi per tahun |
| 🔮 **Prediksi Hasil Panen** | Input variabel (waktu, luas lahan, jumlah pohon, frekuensi pemupukan) → prediksi hasil panen berikutnya |
| 📋 **Riwayat Panen** | Seluruh riwayat penimbangan dengan fitur pencarian dan filter data |
| 👤 **Profil** | Manajemen data pengguna / pemilik lahan |

---

## 🏗️ Arsitektur Sistem

```
┌─────────────────────────────────────────────────────┐
│                   KERANJANG PINTAR                  │
│           (Sensor Timbangan Berbasis IoT)           │
└──────────────────────┬──────────────────────────────┘
                       │ Data berat TBS (real-time)
                       ▼
┌─────────────────────────────────────────────────────┐
│                    SUPABASE                         │
│              (Cloud Database / Backend)             │
└──────────────────────┬──────────────────────────────┘
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
┌─────────────────┐       ┌──────────────────────┐
│ Aplikasi Android │       │   Backend ML Server  │
│   (Kotlin)       │◄─────►│ (Multiple Linear     │
│                  │       │  Regression .pkl)    │
└─────────────────┘       └──────────────────────┘
```

---

## 🤖 Machine Learning

### Algoritma: Multiple Linear Regression

Model prediksi hasil panen menggunakan beberapa variabel independen:

```
y = a + b₁x₁ + b₂x₂ + b₃x₃ + b₄x₄
```

| Variabel | Keterangan |
|----------|------------|
| `y` | Hasil panen yang diprediksi (kg) |
| `x₁` | Waktu panen |
| `x₂` | Luas lahan |
| `x₃` | Jumlah pohon |
| `x₄` | Frekuensi pemupukan |
| `a` | Intercept / konstanta |
| `b₁–b₄` | Koefisien regresi |

### Alur ML Pipeline

```
Data Historis TBS
      │
      ▼
Data Gathering
(catatan manual + data IoT)
      │
      ▼
Data Preparation
├── Data Cleaning (hapus null & duplikat)
├── Normalisasi data
└── Pengurutan kronologis (time series)
      │
      ▼
Exploratory Data Analysis (EDA)
(distribusi, tren, outlier)
      │
      ▼
Feature Engineering
(waktu, luas lahan, jumlah pohon, pemupukan)
      │
      ▼
Train/Test Split
├── Training data: ±80%
└── Testing data: ±20%
      │
      ▼
Modeling Multiple Linear Regression
      │
      ▼
Evaluasi Model
(MAE, MSE, RMSE, R²)
      │
      ▼
Simpan Model (.pkl)
      │
      ▼
Integrasi ke Backend → Android App
```

### Metrik Evaluasi

| Metrik | Keterangan |
|--------|------------|
| **MAE** | Mean Absolute Error — rata-rata kesalahan absolut (kg) |
| **MSE** | Mean Squared Error — rata-rata kuadrat kesalahan |
| **RMSE** | Root Mean Squared Error — kesalahan dalam satuan kg |
| **R²** | Koefisien determinasi — semakin mendekati 1 semakin baik |

### Kriteria Keberhasilan
- Nilai MAE, MSE, RMSE dalam batas toleransi yang dapat diterima
- Nilai R² mendekati 1
- Prediksi mengikuti tren data historis
- Model stabil dan tidak menghasilkan nilai ekstrem
- Model dapat diintegrasikan dengan aplikasi Android

---

## 🛠️ Teknologi yang Digunakan

| Layer | Teknologi |
|-------|-----------|
| **Mobile App** | Kotlin, Android Studio |
| **Database** | Supabase (PostgreSQL) |
| **Machine Learning** | Python, Multiple Linear Regression, Pickle (.pkl) |
| **IoT Integration** | Sensor timbangan berbasis IoT (hardware oleh PA lain) |
| **Backend ML** | Python (Flask/FastAPI) |

---

## 📱 Tampilan Aplikasi

### Halaman Data Panen Harian
Menampilkan berat panen terbaru yang diterima dari sensor IoT, total panen hari ini, dan detail per penimbangan.
<img width="289" height="555" alt="Screenshot 2026-05-24 190431" src="https://github.com/user-attachments/assets/05181c22-16b2-4c4f-b937-71662bc72590" />


### Halaman Dashboard Analitik
Ringkasan KPI performa panen, grafik tren produksi, dan perbandingan produksi antar tahun.
<img width="576" height="1280" alt="WhatsApp Image 2026-06-10 at 22 34 05" src="https://github.com/user-attachments/assets/1dfc6228-467f-4ef4-b1e0-c8b156861dad" />


### Halaman Prediksi Panen
Input variabel panen → sistem memproses melalui model Multiple Linear Regression → menampilkan estimasi hasil panen berikutnya.

### Halaman Riwayat Panen
Seluruh riwayat penimbangan TBS dengan fitur pencarian dan filter berdasarkan periode waktu.
<img width="576" height="1280" alt="WhatsApp Image 2026-06-10 at 22 34 06" src="https://github.com/user-attachments/assets/c7c9b01a-f988-42af-81d8-69673a30ce06" />


---

## 🗄️ Struktur Database (Supabase)

### Tabel Utama

```sql
-- Tabel data penimbangan
CREATE TABLE penimbangan (
  id          BIGINT PRIMARY KEY,
  total_panen VARCHAR,       -- Berat TBS (kg)
  waktu       TIMESTAMPTZ,   -- Waktu penimbangan
  created_at  TIMESTAMPTZ
);

-- Tabel data lahan (untuk prediksi)
CREATE TABLE lahan (
  id                BIGINT PRIMARY KEY,
  luas_lahan        DECIMAL,   -- Hektar
  jumlah_pohon      INTEGER,
  frekuensi_pemupukan INTEGER, -- Per bulan
  pemilik_id        BIGINT
);
```

---

---

## 🧪 Pengujian

Pengujian dilakukan menggunakan metode **Black Box Testing** mencakup:

| Kelas Uji | Butir Uji |
|-----------|-----------|
| Data Panen Harian | Menampilkan berat panen terbaru, total panen hari ini, data tiap timbangan |
| Dashboard Analitik | Ringkasan KPI, analisis tren, perbandingan produksi per tahun |
| Prediksi Hasil Panen | Input tanggal prediksi, tampilkan hasil prediksi Linear Regression |
| Riwayat Panen | Tampilkan seluruh riwayat, pencarian/filter data |

---

## 📄 Lisensi

Proyek ini merupakan Proyek Akhir (PA) untuk keperluan akademis di Politeknik Caltex Riau. Semua hak cipta milik penulis.
