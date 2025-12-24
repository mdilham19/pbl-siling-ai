# Hardware Setup

Dokumen ini menjelaskan proses konfigurasi awal dan perakitan perangkat keras pada sistem SILING-AI.

---

## Bagian 1: Konfigurasi Headless Raspberry Pi

Konfigurasi headless digunakan agar Raspberry Pi dapat diakses dan dikonfigurasi tanpa menggunakan monitor, keyboard, dan mouse. Proses ini dilakukan melalui jaringan menggunakan koneksi SSH.

### Persiapan Software dan Flashing Sistem Operasi

#### Langkah 1: Instalasi Raspberry Pi Imager
1. Unduh Raspberry Pi Imager dari situs resmi: https://www.raspberrypi.com/software
2. Instal Raspberry Pi Imager pada komputer berbasis Windows, macOS, atau Linux.

#### Langkah 2: Flashing Sistem Operasi dengan Konfigurasi Otomatis
1. Jalankan Raspberry Pi Imager.
2. Pilih konfigurasi berikut:
   - **Operating System**: Raspberry Pi OS (64-bit) Lite  
   - **Storage**: MicroSD Card yang akan digunakan
3. Tekan kombinasi tombol **Ctrl + Shift + X** untuk membuka menu *Advanced Options*.
4. Lakukan konfigurasi sebagai berikut:
   - **Hostname**: raspberry  
   - **WiFi SSID**: Nama jaringan WiFi  
   - **WiFi Password**: Kata sandi jaringan  
   - **Timezone**: Asia/Jakarta  
   - **Username**: pi  
   - **Password**: Kata sandi yang kuat  
   - Aktifkan opsi **Enable SSH**
   - Pilih metode **Password Authentication**
5. Mulai proses flashing dan tunggu hingga selesai.

#### Langkah 3: Konfigurasi WiFi Manual (Opsional / Cadangan)

Sebagai langkah cadangan, konfigurasi WiFi dapat dilakukan secara manual dengan membuat file `wpa_supplicant.conf` pada partisi *boot* MicroSD Card setelah proses flashing selesai.

Isi file konfigurasi sebagai berikut:

```text
country=ID
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="Nama_WiFi_Anda"
    psk="Password_WiFi_Anda"
    key_mgmt=WPA-PSK
}
``` 
#### Langkah 4: Booting dan Verifikasi Perangkat Keras

1. Masukkan MicroSD Card ke Raspberry Pi.
2. Hubungkan Raspberry Pi ke sumber daya menggunakan adaptor **5V 3A**.
3. Tunggu proses booting selama kurang lebih **2–3 menit**.
**Indikator Status LED Raspberry Pi**

| Simbol | Warna LED | Kondisi LED | Keterangan |
|------|-----------|-------------|------------|
| 🔴 | Merah | Menyala stabil | Catu daya terhubung dengan baik (Power OK) |
| 🟢 | Hijau | Berkedip tidak teratur | Proses booting sedang berlangsung |
| 🟢 | Hijau | Menyala stabil | Sistem berhasil melakukan booting |


#### Langkah 5: Koneksi SSH & VS Code Remote

1. Cari IP Address Raspberry Pi

Dari komputer Anda (pastikan berada pada jaringan Wi-Fi yang sama), jalankan perintah berikut:

```bash
ping raspberry.local
```
Jika perintah di atas tidak berhasil, lakukan salah satu langkah berikut:
   - Cek daftar **DHCP Clients** pada router
   - Install `nmap` jika belum ada
```bash
sudo apt install nmap
```
   - Scan jaringan lokal
```bash
nmap -sn 192.168.1.0/24 | grep Raspberry
```
2. SSH Connection Test
   
Langkah ini digunakan untuk memastikan Raspberry Pi dapat diakses dari komputer melalui koneksi SSH.

a. Coba koneksi menggunakan hostname
```bash
ssh pi@raspberry.local
```
Jika muncul permintaan password, masukkan password user **pi** yang dibuat saat instalasi.

b. Jika muncul error
```diff
ssh: Could not resolve hostname raspberry.local: Name or service not known
```
Artinya komputer tidak dapat menemukan Raspberry Pi melalui hostname (`.local`).

c. Gunakan IP Raspberry Pi yang diperoleh dari router atau hasil scanning jaringan.
```bash
ssh pi@192.168.1.x
```
3. VS Code Remote Setup

Langkah ini digunakan untuk menghubungkan Visual Studio Code langsung ke Raspberry Pi melalui SSH,
sehingga pengembangan dan pengelolaan file dapat dilakukan dari VS Code.

a. Install Extension Remote - SSH
1. Buka **Visual Studio Code**
2. Masuk ke menu **Extensions** (`Ctrl + Shift + X`)
3. Cari **Remote - SSH**
4. Klik **Install**

b. Hubungkan ke Raspberry Pi
1. Tekan `F1` atau `Ctrl + Shift + P`
2. Pilih **Remote-SSH: Connect to Host**
3. Pilih **Add New SSH Host**
4. Masukkan alamat berikut:
```text
pi@raspberry.local
```

## Bagian 2: Perakitan dan Instalasi Sensor

Bagian ini menjelaskan tahapan perakitan perangkat keras dan instalasi sensor pada Raspberry Pi. Seluruh proses dilakukan secara bertahap untuk memastikan setiap komponen terpasang dengan benar dan aman sebelum sistem dioperasikan.

### Tahap 1: Persiapan Awal

1. Siapkan workspace yang bersih dengan pencahayaan yang baik.
2. Pastikan seluruh sumber daya dalam kondisi mati dan lepaskan baterai apabila digunakan.
3. Urutkan seluruh komponen sesuai dengan daftar checklist perakitan.
4. Siapkan multimeter untuk melakukan pengecekan kontinuitas rangkaian.
5. Pasang Raspberry Pi ke dalam casing dan tambahkan heatsink untuk membantu pendinginan.
6. Pasang kamera USB pada posisi menghadap ke bawah atau ke samping sesuai kebutuhan pengambilan gambar.

### Tahap 2: Instalasi MCP3008 sebagai Pusat ADC

MCP3008 digunakan sebagai Analog-to-Digital Converter (ADC) untuk membaca sensor analog yang terhubung ke Raspberry Pi.

#### Langkah 1: Penempatan MCP3008
1. Letakkan IC MCP3008 di bagian tengah breadboard agar memudahkan pengkabelan.

#### Langkah 2: Koneksi Power dan Ground
1. Pin 16 (VDD) dihubungkan ke 3.3V Raspberry Pi (pin 1).
2. Pin 15 (VREF) dihubungkan ke 3.3V Raspberry Pi (pin 1).
3. Pin 14 (AGND) dihubungkan ke GND Raspberry Pi (pin 6).
4. Pin 9 (DGND) dihubungkan ke GND Raspberry Pi (pin 6).

#### Langkah 3: Koneksi Komunikasi SPI
1. Pin 13 (CLK) dihubungkan ke GPIO11 Raspberry Pi (pin 23).
2. Pin 12 (DOUT) dihubungkan ke GPIO9 Raspberry Pi (pin 21).
3. Pin 11 (DIN) dihubungkan ke GPIO10 Raspberry Pi (pin 19).
4. Pin 10 (CS/SHDN) dihubungkan ke GPIO8 Raspberry Pi (pin 24).

### Tahap 3: Instalasi Sensor DHT22

Sensor DHT22 digunakan untuk mengukur suhu dan kelembapan lingkungan.

#### Langkah 1: Pemasangan Sensor
1. Pasang sensor DHT22 pada breadboard.

#### Langkah 2: Koneksi Kabel
1. Pin VCC dihubungkan ke 3.3V Raspberry Pi.
2. Pin DATA dihubungkan ke GPIO17 Raspberry Pi (pin 11).
3. Pin GND dihubungkan ke GND Raspberry Pi.

### Tahap 4: Instalasi Sensor Gas MQ-2 dan MQ-135

Sensor MQ-2 dan MQ-135 digunakan untuk mendeteksi gas dan kualitas udara.

#### Langkah 1: Pemasangan Sensor
1. Pasang sensor MQ-2 dan MQ-135 pada breadboard.

#### Langkah 2: Koneksi Sensor MQ-2
1. Pin VCC dihubungkan ke 5V Raspberry Pi (pin 2).
2. Pin GND dihubungkan ke GND Raspberry Pi.
3. Pin AO dihubungkan ke MCP3008 channel 0 (pin 1).
4. Pin DO dihubungkan ke GPIO5 Raspberry Pi (pin 29).

#### Langkah 3: Koneksi Sensor MQ-135
1. Pin VCC dihubungkan ke 5V Raspberry Pi (pin 2).
2. Pin GND dihubungkan ke GND Raspberry Pi.
3. Pin AO dihubungkan ke MCP3008 channel 1 (pin 2).
4. Pin DO dihubungkan ke GPIO27 Raspberry Pi (pin 13).

### Tahap 5: Instalasi Sensor Cahaya (LDR)

Sensor LDR digunakan untuk mengukur intensitas cahaya.

#### Langkah 1: Pembuatan Rangkaian Voltage Divider
1. Hubungkan 3.3V Raspberry Pi ke kaki pertama LDR.
2. Hubungkan kaki kedua LDR ke titik tengah rangkaian (kabel abu-abu).
3. Hubungkan titik tengah tersebut ke MCP3008 channel 2 (pin 3).

#### Langkah 2: Penempatan Sensor
1. Posisikan LDR menghadap ke atas agar dapat menerima cahaya secara optimal.

### Tahap 6: Instalasi Sensor pH

Sensor pH digunakan untuk mengukur tingkat keasaman air secara analog.

#### Langkah 1: Pemasangan Sensor
1. Pasang sensor pH analog pada breadboard.
#### Langkah 2: Koneksi Kabel
1. Pin VCC dihubungkan ke 5V Raspberry Pi.
2. Pin GND dihubungkan ke GND Raspberry Pi.
3. Pin AO dihubungkan ke MCP3008 channel 3 (pin 4).
Bagian ini harus dipastikan selesai dengan benar sebelum melanjutkan ke tahap instalasi dan konfigurasi perangkat lunak.

## Bagian 3: Setup Software IoT Siling AI

Bagian ini menjelaskan struktur direktori proyek yang digunakan pada Raspberry Pi
untuk menjalankan sistem IoT Siling AI berbasis Flask dan YOLO.

#### Langkah 1: Struktur Proyek di Raspberry Pi

#### Struktur Direktori

```text
AI/
├── app.py                 # Kode utama aplikasi Flask
├── requirements.txt       # Daftar dependencies Python
├── .env                   # File konfigurasi environment
├── sensor_cache.json      # Cache data sensor (ter-generate otomatis)
│
├── static/
│   ├── uploads/            # Gambar yang diupload
│   └── results/
│       └── detections/     # Hasil deteksi AI dengan bounding box
│
├── templates/
│   └── index.html          # Halaman web dashboard
│
├── venv/                   # Virtual environment Python
│
└── Documents/
    └── AI/
        └── best (18).pt    # Model YOLO untuk deteksi jentik
```
#### Langkah 2: Setup Python Environment

1. Update sistem
```bash
sudo apt update && sudo apt upgrade -y
```
2. Install dependencies sistem yang dibutuhkan
```bash
sudo apt install python3-pip python3-venv libopenblas-dev libatlas-base-dev -y
```
3. Membuat dan mengaktifkan virtual environment
```bash
python3 -m venv venv
```
```bash
source venv/bin/activate
```
4. Upgrade pip
```bash
pip install --upgrade pip
```

5. Install library Python untuk IoT dan AI
```bash
pip install RPi.GPIO spidev adafruit-circuitpython-dht flask flask-cors \
```
```bash
torch torchvision --extra-index-url https://download.pytorch.org/whl/cpu
```
```bash
pip install ultralytics psycopg2-binary python-dotenv opencv-python numpy pillow
```
