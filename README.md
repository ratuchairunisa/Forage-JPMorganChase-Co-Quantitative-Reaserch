# JPMorgan Chase & Co. Quantitative Reasearch (Forage) Job Simulation
JPMorgan Chase &amp; Co. Quantitative Research (Forage) — natural gas storage contract pricing model &amp; FICO-based credit risk rating using Python

> Quantitative finance & risk analytics case studies — from raw data to a decision-ready spreadsheet dashboard & stakeholder report

---

## 🔥 Case Study 1 — Natural Gas Storage Contract Pricing Model

**Business problem:** Sebuah trading desk ingin menawarkan kontrak penyimpanan gas alam kepada klien — membeli gas saat harga rendah (musim panas), menyimpannya, lalu menjualnya saat harga tinggi (musim dingin). Dibutuhkan model penetapan harga kontrak yang general, dapat menangani banyak siklus injeksi/penarikan, dan memperhitungkan seluruh biaya operasional.

**Pendekatan:**
1. **Estimasi harga** — Interpolasi linear untuk tanggal di dalam rentang data historis; ekstrapolasi tren + musiman (seasonal decomposition) untuk tanggal di masa depan.
2. **Penetapan harga kontrak** — Fungsi general yang menerima jadwal injeksi/penarikan (tanggal & volume), lalu menghitung:
   - Pendapatan penjualan − Biaya pembelian
   - Biaya sewa storage (pro-rata per bulan)
   - Biaya injeksi/penarikan (per MMBtu)
   - Biaya transportasi (per event)
3. Validasi otomatis terhadap batas kecepatan operasi (rate limit) dan kapasitas maksimum storage.

**Hasil kunci:**
| Skenario | Nilai Kontrak Bersih |
|---|---|
| A — Ilustratif (1x beli-jual) | **$490.000** |
| B — Klien nyata (multi-siklus, proyeksi musim dingin 2026/2027) | **~$502.500** |

**Insight:** Strategi arbitrase (strategi investasi atau perdagangan yang memanfaatkan selisih harga suatu aset atau komoditas antara musim sepi (off-season) dan musim puncak (peak season). Konsep utamanya adalah membeli saat harga murah di luar musim dan menjualnya dengan harga tinggi saat permintaan melonjak) musiman tetap profitable setelah memperhitungkan seluruh biaya operasional, bahkan pada skenario multi-siklus dengan volume dan biaya lebih kompleks.

---

## 💳 Case Study 2 — FICO-Based Probability of Default (PD) Rating Model

**Business problem:** Tim risiko bank ingin memprediksi probabilitas gagal bayar (PD) hipotek menggunakan skor FICO. Model ML yang akan dipakai membutuhkan data kategorikal, sehingga skor FICO (variabel kontinu, 300–850) perlu dikuantisasi menjadi sejumlah kecil rating — dengan rating lebih rendah = kualitas kredit lebih baik.

**Pendekatan:**
- Mengimplementasikan **kuantisasi optimal 1-dimensi** via **dynamic programming**, dengan dua kriteria:
  - **MSE** — meminimalkan kesalahan kuadrat saat setiap skor didekati oleh rata-rata bucket.
  - **Log-likelihood** — memaksimalkan log-likelihood binomial berdasarkan tingkat gagal bayar tiap bucket (kriteria yang dipilih sebagai model final karena langsung mengoptimalkan pemisahan risiko).
- Kompleksitas O(U²×k) dengan agregasi data ke level skor FICO unik (374 titik dari 10.000 baris data) — dijamin optimal, bukan heuristik seperti equal-width binning.

**Hasil kunci (5 rating) untuk Pendekatan Log-Likelihood:**
| Rating | Rentang FICO | Jumlah Peminjam | PD |
|---|---|---|---|
| 1 (terbaik) | 697–850 | 1.657 | 4,65% |
| 2 | 641–696 | 3.197 | 10,51% |
| 3 | 581–640 | 3.438 | 20,45% |
| 4 | 521–580 | 1.407 | 38,10% |
| 5 (terburuk) | 408–520 | 301 | 66,11% |

**Insight:** gagal bayar naik secara signifikan dan tajam seiring rating memburuk, mengonfirmasi bahwa skor FICO sebagai prediktor kuat untuk memprediksi risiko gagal bayar. Lebar bucket yang tidak seragam (rating 5 jauh lebih sempit dari rating 1) menunjukkan keunggulan kuantisasi berbasis log-likelihood dibanding binning naif — wilayah skor rendah jauh lebih sensitif terhadap perubahan PD.

---

## 📑 Stakeholder Report Gas & Credit Risk
<img width="1920" height="1080" alt="1" src="https://github.com/user-attachments/assets/56de4c5c-8889-4e8d-82f1-fe728e4c38bf" />
<img width="1920" height="1080" alt="2" src="https://github.com/user-attachments/assets/2343f6ea-606b-4c5d-a6cf-ea774adf98d3" />
<img width="1920" height="1080" alt="3" src="https://github.com/user-attachments/assets/ce4c8340-93b1-4700-816c-a3bcf20e38fb" />
<img width="1920" height="1080" alt="4" src="https://github.com/user-attachments/assets/8ffb330b-2ce2-4cd7-afba-da675dbf037a" />
<img width="1920" height="1080" alt="5" src="https://github.com/user-attachments/assets/c174559a-0c32-4c11-b847-65be1b136631" />
<img width="1920" height="1080" alt="6" src="https://github.com/user-attachments/assets/ea0541ba-e60a-4ffc-8249-f4ff1f060f5c" />
<img width="1920" height="1080" alt="7" src="https://github.com/user-attachments/assets/34184701-1671-4f8d-b211-dc2e79514c6a" />
<img width="1920" height="1080" alt="8" src="https://github.com/user-attachments/assets/9fa86c6c-7ce1-406f-86b1-57bfaac5353b" />
<img width="1920" height="1080" alt="9" src="https://github.com/user-attachments/assets/78dc4c53-d226-4aba-a127-56badc66733a" />
<img width="1920" height="1080" alt="10" src="https://github.com/user-attachments/assets/5856b8db-112a-4e02-ba06-ea8a714b2920" />
<img width="1920" height="1080" alt="11" src="https://github.com/user-attachments/assets/2a7be377-f2fd-4c91-9d1a-45c918a9013e" />

