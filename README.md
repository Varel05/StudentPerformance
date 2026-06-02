# 📊 Student Performance Analyse
> *Analisis faktor-faktor penentu performa akademik murid untuk menghasilkan insight bisnis strategis menggunakan AI pipeline Langflow*

**Dibuat oleh:** Varel Deva Dewangga — Universitas Duta Bangsa Surakarta  
**Versi Langflow:** 1.9.2  
**Model AI:** Google Gemini 2.5 Flash  
**Tag:** `classification` | `education-analytics` | `business-insight`

---

## 🎯 Tentang Project

Project ini adalah **pipeline analisis data pendidikan berbasis AI** yang dibangun di Langflow. Tujuannya adalah menganalisis hubungan antara berbagai faktor penentu performa murid dengan hasil ujian akhir (`Exam_Score`), lalu mengubah temuan tersebut menjadi **rekomendasi bisnis yang actionable** bagi institusi pendidikan.

Pipeline ini bekerja dalam dua tahap:

1. **Analisis Data** — AI membaca dataset performa murid dan melakukan analisis statistik, korelasi, segmentasi, serta identifikasi faktor risiko secara otomatis.
2. **Business Intelligence** — Hasil analisis diolah menjadi laporan bisnis lengkap berisi rekomendasi program, roadmap, dan proyeksi ROI pendidikan.

### 🎓 Pengguna Target Laporan

| Peran | Manfaat |
|-------|---------|
| Kepala Sekolah / Manajemen | Dasar pengambilan keputusan strategis |
| Tim Konselor & Guru | Identifikasi murid yang membutuhkan intervensi |
| Dinas Pendidikan / Policy Maker | Dasar kebijakan peningkatan kualitas pendidikan |
| Orang Tua Murid | Pemahaman faktor yang memengaruhi nilai anak |

---

## 📁 Dataset

| Atribut | Detail |
|---------|--------|
| **Nama File** | `StudentPerformanceFactors.csv` |
| **Jumlah Data** | 6.607 baris (murid) |
| **Jumlah Variabel** | 20 kolom |
| **Target Variabel** | `Exam_Score` (skala 55–101, rata-rata 67.2) |

### Variabel dalam Dataset

**Numerik:**
- `Hours_Studied` — Jam belajar per minggu (range: 1–44)
- `Attendance` — Persentase kehadiran (range: 60–100%)
- `Sleep_Hours` — Jam tidur per malam
- `Previous_Scores` — Nilai ujian sebelumnya
- `Tutoring_Sessions` — Jumlah sesi les per bulan
- `Physical_Activity` — Jam aktivitas fisik per minggu
- `Exam_Score` — ⭐ **[TARGET]** Nilai ujian akhir

**Kategoris:**
- `Parental_Involvement` — Low / Medium / High
- `Access_to_Resources` — Low / Medium / High
- `Motivation_Level` — Low / Medium / High
- `Extracurricular_Activities` — Yes / No
- `Internet_Access` — Yes / No
- `Family_Income` — Low / Medium / High
- `Teacher_Quality` — Low / Medium / High *(ada missing values)*
- `School_Type` — Public / Private
- `Peer_Influence` — Positive / Negative / Neutral
- `Learning_Disabilities` — Yes / No
- `Parental_Education_Level` — High School / College / Postgraduate *(ada missing values)*
- `Distance_from_Home` — Near / Moderate / Far *(ada missing values)*
- `Gender` — Male / Female

> ⚠️ **Catatan:** Kolom `Teacher_Quality`, `Parental_Education_Level`, dan `Distance_from_Home` memiliki nilai kosong (NaN). Pipeline ini secara otomatis merekomendasikan strategi imputasi yang tepat.

---

## 🔁 Arsitektur Pipeline

Pipeline terdiri dari **5 komponen aktif** yang terhubung secara berurutan:

```
[Read File] 
    │  (konten CSV)
    ▼
[Prompt Template 1 — Analisis Data]
    │  (instruksi analisis + data)
    ▼
[Language Model 1 — Gemini 2.5 Flash]
    │  (summary statistik & insight)
    ▼
[Prompt Template 2 — Business Intelligence]
    │  (instruksi rekomendasi + summary)
    ▼
[Language Model 2 — Gemini 2.5 Flash]
    │  (laporan bisnis final)
    ▼
[Chat Output]
```

### Penjelasan Setiap Komponen

| No | Komponen | Fungsi |
|----|----------|--------|
| 1 | **Read File** | Membaca dan memuat file CSV dataset performa murid |
| 2 | **Prompt Template 1** | Menyusun instruksi analisis data komprehensif (statistik deskriptif, korelasi, segmentasi, faktor risiko) |
| 3 | **Language Model 1** | Menjalankan analisis dengan Gemini 2.5 Flash (temperature: 0.3) |
| 4 | **Prompt Template 2** | Menerima hasil analisis dan menyusun instruksi untuk pembuatan laporan bisnis |
| 5 | **Language Model 2** | Menghasilkan rekomendasi bisnis final dengan Gemini 2.5 Flash (temperature: 0.6) |
| 6 | **Chat Output** | Menampilkan hasil akhir di Playground Langflow |

---

## 📤 Output yang Dihasilkan

### Tahap 1 — Ringkasan Analisis Data
Analisis mendalam mencakup:
- **Statistik Deskriptif** — Distribusi Exam_Score (min, max, mean, median, std)
- **Analisis Korelasi** — Ranking variabel numerik berdasarkan kekuatan korelasi dengan nilai ujian
- **Analisis Komparatif** — Perbandingan rata-rata Exam_Score antar grup (9 variabel kategoris)
- **Segmentasi Murid** — Profil murid berdasarkan kelompok nilai (rendah/sedang/tinggi)
- **Faktor Risiko & Protektif** — Top 3 faktor yang paling memengaruhi nilai (positif & negatif)
- **Kualitas Data** — Rekomendasi penanganan missing values

### Tahap 2 — Laporan Bisnis Strategis
Dokumen lengkap berisi:
- **Executive Summary** — Ringkasan temuan untuk manajemen (maks. 150 kata)
- **Matriks Prioritas Intervensi** — Kuadran Quick Win / Strategis / Tambahan / Tunda
- **Top 5 Rekomendasi Program** — Lengkap dengan KPI, timeline, dan estimasi dampak
- **Roadmap 3 Fase** — Rencana implementasi 12 bulan (Quick Wins → Penguatan → Transformasi)
- **Analisis Risiko** — 3 risiko utama beserta mitigasinya
- **Segmen Prioritas Murid** — 🔴 High / 🟡 Medium / 🟢 Enhancement
- **Proyeksi ROI Pendidikan** — Estimasi kenaikan rata-rata nilai jika rekomendasi dijalankan

**Target bisnis:** Meningkatkan rata-rata Exam Score dari **67.2** menjadi **≥ 75** dalam 1 tahun akademik.

---

## 🚀 Cara Menggunakan di Langflow

### Prasyarat
- Langflow versi **1.9.2** atau lebih baru
- Akun Google AI Studio dengan **Google Gemini API Key** yang aktif
- File dataset: `StudentPerformanceFactors.csv`

### Langkah 1 — Import Flow

1. Buka Langflow di browser (`http://localhost:7860` atau instance cloud kamu)
2. Klik tombol **"New Flow"** di halaman utama
3. Pilih **"Import"** atau klik ikon upload
4. Upload file `Student_Performance_Analyse.json`
5. Flow akan terbuka otomatis di canvas

### Langkah 2 — Konfigurasi API Key

> ⚠️ API Key yang ada di file JSON adalah contoh dan mungkin sudah tidak aktif. Kamu harus menggantinya dengan API Key milikmu sendiri.

1. Klik komponen **Language Model 1** (node pertama dari kiri)
2. Di panel kanan, buka bagian **Advanced**
3. Masukkan Google Gemini API Key kamu di field **"API Key"**
4. Ulangi langkah yang sama untuk **Language Model 2**

> 💡 Untuk mendapatkan API Key Google Gemini, kunjungi [Google AI Studio](https://aistudio.google.com/app/apikey)

### Langkah 3 — Upload Dataset

1. Klik komponen **Read File** di canvas
2. Di panel kanan, klik tombol upload
3. Upload file `StudentPerformanceFactors.csv`
4. Pastikan file berhasil ter-load (akan muncul nama file)

### Langkah 4 — Jalankan Pipeline

1. Klik tombol **"Playground"** di pojok kanan atas
2. Klik tombol **"Run"** atau tekan Enter
3. Tunggu proses analisis selesai (estimasi: 30–90 detik tergantung kecepatan API)
4. Hasil laporan bisnis akan muncul di jendela chat

### Langkah 5 — Melihat Hasil (Opsional)

- Klik kanan pada node **Language Model 1** → **"Preview Output"** untuk melihat hasil analisis data tahap pertama
- Hasil akhir di Chat Output adalah laporan bisnis lengkap dari tahap kedua

---

## ⚙️ Konfigurasi Teknis

| Parameter | Language Model 1 | Language Model 2 |
|-----------|-----------------|-----------------|
| Model | Gemini 2.5 Flash | Gemini 2.5 Flash |
| Provider | Google Generative AI | Google Generative AI |
| Temperature | 0.3 (lebih konsisten) | 0.6 (lebih kreatif) |
| Fungsi | Analisis data | Rekomendasi bisnis |

> **Mengapa temperature berbeda?** LM pertama menggunakan temperature rendah (0.3) agar analisis data lebih deterministik dan akurat. LM kedua menggunakan temperature lebih tinggi (0.6) agar rekomendasi bisnis lebih variatif dan kreatif.

---

## 🔧 Kustomisasi

### Mengganti Model AI
Di setiap node Language Model, kamu bisa mengganti provider dan model:
- **OpenAI** — GPT-4o, GPT-4 Turbo
- **Anthropic** — Claude 3.5 Sonnet, Claude 3 Haiku
- **Google** — Gemini 2.5 Pro (untuk analisis lebih dalam)
- **Ollama** — Model lokal (LLaMA, Mistral, dst.)

### Menyesuaikan Prompt
Klik komponen **Prompt Template** untuk mengedit instruksi analisis sesuai kebutuhan institusimu, misalnya:
- Menambah/menghapus variabel yang dianalisis
- Mengubah target Exam Score yang ingin dicapai
- Menyesuaikan format output laporan

### Menggunakan Dataset Berbeda
Flow ini dapat digunakan untuk dataset performa murid lain selama memiliki kolom `Exam_Score` sebagai target. Sesuaikan deskripsi variabel di Prompt Template 1.

---

## 🗂️ Struktur File Project

```
📦 Student Performance Analyse
├── Student_Performance_Analyse.json   # File flow Langflow (import ini)
├── StudentPerformanceFactors.csv      # Dataset (upload ke komponen Read File)
└── README.md                          # Dokumentasi ini
```

---

## ❓ Troubleshooting

| Masalah | Solusi |
|---------|--------|
| Error "Invalid API Key" | Ganti API Key di kedua Language Model node |
| File CSV tidak terbaca | Pastikan format CSV benar dan encoding UTF-8 |
| Output kosong / error | Periksa koneksi internet dan kuota API |
| Flow tidak mau di-import | Pastikan versi Langflow ≥ 1.9.2 |
| Analisis terpotong | Naikkan nilai `Max Tokens` di node Language Model |

---

## 📜 Lisensi

Project ini dibuat untuk keperluan akademik.  
**© 2025 Varel Deva Dewangga — Universitas Duta Bangsa Surakarta**