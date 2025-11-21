# RISK REGISTER TEMPLATE
## Project: Pengembangan dan Implementasi Sistem Pembayaran Self Payment Otomatis Berbasis Mobile Payment di Indogrosir Lampung

---

| REF ID | RISK | RISK OWNER | RISK TRIGGER | RISK CATEGORY | PROBABILITY (1-3) | IMPACT (1-3) | PI SCORE (Prob x Impact) | EXPECTED RESULT - NO ACTION | POSITIVE RISK RESPONSE | NEGATIVE RISK RESPONSE | RESPONSE TRIGGER | RESPONSE OWNER | RESPONSE DESCRIPTION | EXPECTED RESPONSE IMPACT |
|--------|------|------------|--------------|---------------|-------------------|--------------|--------------------------|----------------------------|------------------------|------------------------|------------------|----------------|----------------------|--------------------------|
| R-01 | Kegagalan Integrasi Payment Gateway | Bayu Brigas Novaldi | Dokumentasi API tidak lengkap atau perubahan versi API mendadak saat fase integrasi | Technical - Integration | 3 | 3 | 9 | Sistem pembayaran tidak berfungsi sama sekali, transaksi tidak dapat terjadi, proyek gagal total | EXPLOIT | AVOID | Fase integrasi Mobile Payment dimulai | Lead Developer, Project Manager | Meminta dukungan teknis prioritas dari vendor Payment Gateway, menyiapkan modul pembayaran modular yang dapat beralih ke Vendor B jika Vendor A bermasalah | Payment gateway terintegrasi sempurna, sistem pembayaran berjalan lancar dengan fallback option tersedia |
| R-02 | Hardware Kiosk Malfungsi / Tidak Kompatibel | Giovan Lado | Perangkat keras (scanner, printer struk) tidak terbaca software kiosk saat instalasi karena masalah driver OS | Technical - Hardware | 2 | 3 | 6 | Kiosk tidak dapat digunakan untuk scan barang/cetak struk, pelanggan harus pindah ke kasir manual | ENHANCE | MITIGATE | Fase Instalasi & Konfigurasi Kiosk | IT Support, Hardware Vendor | Melakukan Burn-in Test 7x24 jam sebelum instalasi massal, membuat skrip Health Check otomatis setiap booting, validasi kompatibilitas driver, menyediakan spare unit | Hardware berfungsi optimal, kompatibilitas terjamin, downtime minimal dengan spare unit siap |
| R-03 | Kebocoran Data Transaksi & User | Elfa Noviana Sari | Celah keamanan pada RESTful API atau Man-in-the-Middle Attack saat transmisi data pembayaran | Security | 2 | 3 | 6 | Hilangnya data sensitif pelanggan, tuntutan hukum, hilangnya kepercayaan pada Indogrosir, kerusakan reputasi permanen | SHARE | TRANSFER | Deteksi aktivitas mencurigakan atau vulnerability scan positif | Security Engineer, Backend Developer | Menerapkan standar OWASP Top 10, enkripsi SSL/TLS, Database Encryption, Rate Limiting untuk cegah Brute Force, rutin Vulnerability Scanning, tidak menyimpan data sensitif di log | Data pelanggan terlindungi penuh, sistem aman dari serangan, kepatuhan terhadap regulasi data terpenuhi |
| R-04 | Inkonsistensi Status Pembayaran (Dispute Dana) | Bayu Brigas Novaldi | Timeout jaringan tepat setelah user bayar: saldo e-wallet terpotong tapi API gagal kirim respon "Sukses", struk tidak keluar | Transaction Processing | 3 | 3 | 9 | Pelanggan marah besar (saldo hilang tapi barang ditahan security), proses refund manual rumit, merusak citra sistem otomatis | EXPLOIT | AVOID | Tidak ada callback dalam 10 detik setelah pembayaran | Backend Developer, Project Manager | Active Polling otomatis query status transaksi ke gateway tiap 30 detik, Auto-Reversal/Refund jika konfirmasi gagal, Dashboard Admin untuk verifikasi manual real-time | Tidak ada dispute dana, setiap transaksi tercatat akurat, kepuasan pelanggan terjaga, refund otomatis berjalan |
| R-05 | Downtime Server saat Soft Launch | Elfa Noviana Sari | Server backend tidak kuat menampung beban transaksi (High Concurrency) saat jam sibuk | Infrastructure | 2 | 3 | 6 | Transaksi tidak dapat diproses, antrian menumpuk, pelanggan membatalkan belanja, kerugian revenue | ENHANCE | MITIGATE | CPU/Memory threshold >70% atau Load Testing menunjukkan bottleneck | Backend Developer, DevOps Engineer, Project Manager | Setup Load Balancer, Auto-scaling berdasarkan threshold, Load Testing dengan JMeter untuk simulasi 500-1000 concurrent users, Hot Standby server cadangan | Sistem tetap responsif saat peak hours, high availability terjamin, skalabilitas terbukti |
| R-06 | Keterlambatan "Rollback" Saat Error Fatal | Elfa Noviana Sari | Tidak ada rencana Fallback yang jelas pada Deployment sehingga jika update crash, tim butuh waktu lama mengembalikan sistem | Deployment | 2 | 3 | 6 | Waktu pemulihan layanan sangat lama, downtime berkepanjangan, operasional toko terganggu, layanan mandiri ditutup total hingga perbaikan selesai | ENHANCE | MITIGATE | Update baru menyebabkan system crash atau error critical | DevOps Engineer, Lead Backend Developer, Project Manager | Implementasi CI/CD Pipeline dengan One-Click Rollback, snapshot/backup otomatis sebelum deployment, Blue-Green Deployment strategy, runbook/SOP rollback manual sebagai backup | Recovery time minimal (hitungan detik), sistem dapat dikembalikan ke versi stabil dengan cepat, business continuity terjaga |

---

## LEGEND

### PROBABILITY (1-3)
- **1** = Low (Jarang terjadi, kemungkinan <30%)
- **2** = Medium (Mungkin terjadi, kemungkinan 30-60%)
- **3** = High (Sangat mungkin terjadi, kemungkinan >60%)

### IMPACT (1-3)
- **1** = Low (Dampak minimal, tidak mengganggu operasional)
- **2** = Medium (Dampak sedang, perlu perhatian dan tindakan)
- **3** = High (Dampak critical, dapat menyebabkan kegagalan proyek)

### PI SCORE INTERPRETATION
- **1-3** = Low Risk (dapat diterima dengan monitoring)
- **4-6** = Medium Risk (perlu mitigasi dan monitoring aktif)
- **7-9** = High/Extreme Risk (perlu tindakan pencegahan segera)

### POSITIVE RISK RESPONSE STRATEGIES
- **ACCEPT** = Menerima risiko positif tanpa tindakan khusus
- **ENHANCE** = Meningkatkan probabilitas atau dampak positif dari risiko
- **SHARE** = Berbagi manfaat dengan pihak ketiga (partnership, kolaborasi)
- **EXPLOIT** = Memastikan risiko positif terjadi dengan mengambil tindakan proaktif

### NEGATIVE RISK RESPONSE STRATEGIES
- **ACCEPT** = Menerima risiko tanpa tindakan mitigasi (untuk risiko rendah)
- **MITIGATE** = Mengurangi probabilitas terjadinya atau mengurangi dampak risiko
- **TRANSFER** = Memindahkan risiko ke pihak ketiga (asuransi, vendor, outsourcing)
- **AVOID** = Menghindari risiko sepenuhnya dengan mengubah rencana proyek

---

## BUDGETARY IMPLICATIONS SUMMARY

| Risk ID | Mitigation Budget Implications |
|---------|-------------------------------|
| R-01 | Biaya lembur tim developer, biaya dukungan teknis prioritas vendor |
| R-02 | Biaya pembelian unit sampel untuk Burn-in Test, biaya spare units |
| R-03 | Biaya sewa jasa Penetration Tester eksternal, biaya implementasi security tools |
| R-04 | Biaya pengembangan backend tambahan untuk Reconciliation Service dan Dashboard Admin |
| R-05 | Biaya sewa server cloud dengan auto-scaling (Rp 5-8 juta/bulan fase soft launch), Load Balancer, monitoring tools |
| R-06 | Biaya setup CI/CD tools (GitLab CI/Jenkins), biaya training tim development |

---

## RISK MONITORING SCHEDULE

| Activity | Frequency | Responsible Parties |
|----------|-----------|-------------------|
| **Risk Review** | Mingguan | Project Manager, QA Expert, Backend Developer |
| **Risk Monitoring** | Harian | Project Manager, Backend Developer, QA Expert |
| **Risk Reporting** | Mingguan | Project Manager, UI/UX Designer, Backend Developer, Training Specialist, Technical Writer, QA Expert |

---

**Project Manager:** Giovan Lado  
**Contact:** 0882-7405-1262 | giovan.123140068@student.itera.ac.id  
**Document Version:** 1.0  
**Date Prepared:** November 21, 2025  
**Next Review Date:** November 28, 2025  

**Distribution:**
- Executive Sponsor (Manajemen Indogrosir) - Email & Rapat Formal
- Tim Proyek (Backend, Frontend, QA, & Teknisi) - Project Management Tool
- Store Manager (Kepala Toko Indogrosir Lampung) - Hard Copy & Sosialisasi

---

**Notes:**
- Risiko dengan Grade A (PI Score 9) memerlukan perhatian tertinggi dan tindakan AVOID/EXPLOIT
- Risiko dengan Grade B (PI Score 6) memerlukan mitigasi aktif dan monitoring ketat
- Semua stakeholder wajib melaporkan indikasi munculnya risk trigger segera setelah terdeteksi
- Contingency budget harus dialokasikan untuk setiap risiko dengan PI Score ≥6
