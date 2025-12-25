# SILING-AI: Sistem Berbasis IoT dan AI untuk Pemantauan Lingkungan Rumah Sehat dan Deteksi Dini Risiko Penyakit

SILING-AI merupakan sistem pemantauan lingkungan rumah sehat berbasis _Internet of Things_ (IoT) dan _Artificial Intelligence_ (AI) yang dirancang untuk memantau kondisi lingkungan secara _real-time_. Sistem ini mencakup pemantauan suhu dan kelembapan, deteksi gas berbahaya dan asap rokok, pemantauan kualitas udara dan kualitas air, serta deteksi jentik nyamuk menggunakan pendekatan _image processing_ berbasis model YOLOv8.
## Features

- Memantau suhu dan kelembapan rumah secara _real-time_;
- Mendeteksi gas berbahaya dan asap rokok;
- Menampilkan kondisi kualitas udara di dalam rumah;
- Menampilkan kondisi kualitas air;
- Mendeteksi keberadaan jentik nyamuk menggunakan kamera;
- Menampilkan hasil pemantauan dalam dashboard web;
- Menyimpan data untuk pemantauan jangka panjang;
- Memberikan rekomendasi atau langkah awal ketika kondisi lingkungan terdeteksi tidak sehat;

## Technologies Used

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Flask](https://img.shields.io/badge/Flask-Web_Framework-black)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Computer_Vision-red)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue)
![Bootstrap](https://img.shields.io/badge/Bootstrap-Frontend_Framework-purple)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Tunnel-orange)

## Hardware / Devices

| Perangkat | Fungsi |
|---------|-------|
| Raspberry Pi 4 | Pemrosesan utama dan server sistem |
| MCP3008 | Konversi sinyal analog ke digital |
| DHT22 | Pengukuran suhu dan kelembapan |
| MQ-2 | Deteksi gas dan asap rokok |
| MQ-135 | Pemantauan kualitas udara |
| Sensor pH analog | Pengukuran kualitas air |
| BH1750 | Pengukuran intensitas cahaya |
| Logitech C920e | Deteksi visual jentik nyamuk |
| Breadboard | Papan penyusun rangkaian sensor |
| Kabel jumper | Menghubungkan antar rankaian sensor |
| Power supply 5V 3A dengan kabel USB-C  | Sumber catu daya listrik |
| MicroSD card 128GB | Media penyimpanan |
| Card Reader | Pembaca kartu memori |

## Folder structure

```
AI 
├── app.py              # Kode utama aplikasi Flask      
├── requirements.txt    # Dependencies Python 
├── .env                # File konfigurasi environment         
├── sensor_cache.json   # Cache data sensor (tergenerate otomatis)         
│ 
├── static/ 
│   ├── uploads/         # Gambar yang diupload      
│   └── results/ 
│       └── detections/  # Hasil deteksi AI dengan bounding box 
│ 
├── templates/ 
│   └── index.html       # Halaman web dashboard     
│ 
├── venv/                # Virtual environment Python                
└── Documents/ 
    └── AI/ 
       └── best (18).pt  # Model YOLO untuk deteksi jentik
```

## System Architecture
![System Architecture](WhatsApp%20Image%202025-12-25%20at%2017.03.07.jpeg)



