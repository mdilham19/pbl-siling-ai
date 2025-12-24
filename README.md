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

- **Raspberry Pi 4** - Perangkat pemrosesan utama dan server sistem
- **MCP3008** - Analog-to-Digital Converter (ADC) untuk membaca sensor analog
- **Sensor DHT22** - Mengukur suhu dan kelembapan lingkungan
- **Sensor MQ-2** - Mendeteksi gas berbahaya dan asap rokok
- **Sensor MQ-135** - Memantau kualitas udara di dalam ruangan
- **Sensor pH Meter** - Mengukur tingkat keasaman air sebagai indikator kualitas air
- **Sensor BH1750 (LDR)** - Mengukur intensitas cahaya lingkungan
- **Kamera Logitech C920e** - Mendeteksi jentik nyamuk berbasis _Image Processing_


