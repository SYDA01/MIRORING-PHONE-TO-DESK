# Panduan Pemakaian MPD — Mirroring Phone Desktop

Dibuat oleh **AhmadHidayatulloh**, dengan bantuan AI Claude.

Panduan ini terdiri dari dua bagian:

- **Bagian A — Dari ekstrak sampai bisa dipakai** (langkah demi langkah).
- **Bagian B — Penjelasan semua fitur** (untuk apa, contoh tampilan, cara pakai, dan catatan).

Di akhir ada contoh skenario, pemecahan masalah, dan tanya-jawab.

> **Soal "contoh tampilan":** gambar di panduan ini berupa sketsa teks yang disusun dari kode aplikasi.
> Tampilan aslinya memakai tema gelap (dark mode) dengan tombol berwarna, jadi tata letaknya sama tetapi tidak persis sama.

---

# BAGIAN A — Dari ekstrak sampai bisa dipakai

## A0. Yang perlu disiapkan

| Kebutuhan | Keterangan |
|---|---|
| Laptop/PC | Windows 10 atau 11 |
| HP | Android 5.0 ke atas. iPhone tidak didukung |
| Kabel USB | Harus kabel **data**, bukan kabel charge saja |
| Python | Versi 3.10 ke atas, hanya perlu kalau menjalankan lewat `JALANKAN.bat` atau membuat `MPD.exe` |
| Internet | Hanya untuk install library saat pertama kali jalan |

## A1. Ekstrak file

1. Download `MPD_v1.3.zip`.
2. Klik kanan → **Extract All...** (jangan jalankan langsung dari dalam ZIP).
3. Pilih lokasi yang pendek, contoh `C:\MPD`. Hindari folder yang dilindungi Windows seperti `C:\Program Files`.

Setelah diekstrak, folder `MPD` berisi:

```
MPD/
├─ main.py                  kode aplikasi
├─ mpd.ico, mpd.png         logo
├─ JALANKAN.bat             jalankan aplikasi dari kode
├─ BUILD_EXE.bat            buat file MPD.exe
├─ README.md
├─ guide/guide.md           panduan ini
├─ adb.exe, AdbWinApi.dll, AdbWinUsbApi.dll
├─ scrcpy.exe, scrcpy-server, SDL3.dll, avcodec-62.dll, avformat-62.dll,
│  avutil-60.dll, swresample-6.dll, libusb-1.0.dll
└─ LICENSE-scrcpy.txt
```

**Cek penting:** pastikan ada file bernama **`libusb-1.0.dll`** (pakai titik, bukan garis bawah).
Kalau namanya `libusb-1_0.dll`, ganti namanya, kalau tidak scrcpy akan error "libusb-1.0.dll was not found".

## A2. Install Python (sekali saja)

1. Buka <https://www.python.org/downloads/> dan download Python 3.
2. Saat install, **centang "Add python.exe to PATH"** di jendela pertama, lalu **Install Now**.
3. Cek: buka Command Prompt, ketik `python --version`. Kalau muncul nomor versi, berarti berhasil.

## A3. Aktifkan USB debugging di HP

Nama menu bisa sedikit berbeda tiap merek HP.

1. **Pengaturan → Tentang ponsel** (kadang **Informasi perangkat lunak**).
2. Ketuk **Nomor build** 7 kali sampai muncul tulisan "Anda sekarang adalah pengembang". Masukkan PIN kalau diminta.
3. Kembali ke **Pengaturan → Sistem → Opsi pengembang** (di beberapa HP ada di **Pengaturan tambahan**).
4. Aktifkan **Opsi pengembang**, lalu aktifkan **USB debugging**.
5. **Khusus Xiaomi / Redmi / POCO:** aktifkan juga **USB debugging (Security settings)** supaya mouse dan keyboard bisa mengontrol HP.

## A4. Colok HP dan beri izin

1. Colok HP ke laptop dengan kabel USB.
2. Tarik notifikasi di HP dan pilih mode USB **Transfer file** (kalau ada pilihan).
3. Akan muncul pop-up **"Izinkan debugging USB?"** di layar HP.
   Centang **Selalu izinkan dari komputer ini**, lalu ketuk **Izinkan**.

Kalau pop-up tidak muncul: cabut dan colok lagi kabelnya, atau matikan lalu nyalakan lagi USB debugging.

## A5. Jalankan MPD

1. Klik dua kali **`JALANKAN.bat`**.
2. Pertama kali, akan muncul jendela hitam yang meng-install library (`customtkinter`, `tkinterdnd2`, `pycaw`). Tunggu sampai selesai, jangan ditutup.
3. Jendela **MPD - Mirroring Phone Desktop** akan terbuka.

Kalau Windows atau antivirus menampilkan peringatan untuk `adb.exe` atau `scrcpy.exe`, kedua file ini adalah alat resmi (ADB dari Google, scrcpy dari Genymobile). Pilih **Run anyway / Izinkan** kalau kamu yakin file-nya dari paket ini.

## A6. Pastikan HP terdeteksi

Lihat bagian atas jendela. Statusnya harus berwarna hijau:

```
Device: Connected    [ Infinix_X657B  [077743321M101122] ▾ ]   [Refresh]
```

Kalau masih merah (**Disconnected**): klik **Refresh**, cek kabel, dan cek pop-up izin di HP.

## A7. Mirroring pertama (cara paling cepat)

1. Buka tab **Desktop**.
2. Pada **Preset / Performance Mode**, pilih **Ultra Low (A20 Safe)** (paling aman untuk HP low-end).
3. Klik **2. LAUNCH DESKTOP MODE**.
4. Tunggu 3–5 detik. HP akan masuk ke ukuran layar laptop, layar HP mati, dan jendela scrcpy terbuka **fullscreen** di laptop.

Kalau layar laptop sudah menampilkan layar HP dan mouse bisa dipakai untuk mengetuk, berarti **MPD sudah berfungsi**.

## A8. Cara keluar dari mirroring

Pilih salah satu:

- Klik tombol **STOP** di tab Desktop.
- Di jendela scrcpy tekan **MOD + q** (MOD = tombol `Alt` kiri atau tombol `Windows` kiri). Ini bawaan scrcpy 4.0.
- Tutup jendela scrcpy (kalau fullscreen, tekan **F11** dulu).

Setelah berhenti, MPD **otomatis mengembalikan** ukuran layar, density, rotasi, dan brightness HP.

Kalau ada yang tidak kembali normal: klik **Reset Layar HP ke Normal**, atau **EMERGENCY STOP**.

## A9. (Opsional) Supaya lebih terasa "desktop": launcher Taskbar

Tanpa langkah ini, kamu tetap mirroring seperti biasa (layar HP dalam ukuran 16:9). Dengan launcher, muncul taskbar dan jendela mengambang seperti desktop.

1. Download aplikasi **Taskbar** (package `com.farmerbb.taskbar`) dari F-Droid atau Play Store. Kalau kamu mengunduh file APK-nya, simpan dengan nama **`taskbar.apk`** di folder MPD.
2. Di MPD, tab **Desktop**, klik **1. Install Desktop Launcher** (kalau `taskbar.apk` tidak ada di folder, akan muncul dialog untuk memilih file).
3. Klik **Setup Freeform Windows (sekali, lalu reboot HP)**, konfirmasi, tunggu HP restart.
4. Setelah HP menyala, buka aplikasi **Taskbar** di HP dan aktifkan opsi freeform/desktop di pengaturannya.
5. Mulai sekarang, setiap klik **LAUNCH DESKTOP MODE**, MPD otomatis membuka Taskbar.

> Hasilnya tergantung HP dan versi Android. Di HP low-end/Android Go, freeform bisa tidak tersedia atau tidak stabil. Kalau begitu, tampilan akan terasa seperti tablet.

## A10. (Opsional) Membuat `MPD.exe`

1. Klik dua kali **`BUILD_EXE.bat`**. Tunggu sampai muncul tulisan **Selesai**.
2. File **`MPD.exe`** (dengan logo) muncul di folder MPD.
3. Klik dua kali `MPD.exe` untuk menjalankan tanpa jendela hitam.

**Jangan** memindahkan `MPD.exe` keluar dari folder ini. Ia butuh `adb.exe`, `scrcpy.exe`, dan DLL di sebelahnya.

## A11. Checklist "sudah bisa dipakai"

- [ ] Status **Device: Connected** berwarna hijau
- [ ] Klik LAUNCH → jendela scrcpy terbuka dengan tampilan HP
- [ ] Mouse bisa mengetuk/menggeser di layar HP
- [ ] Klik STOP → jendela tertutup dan layar HP kembali normal
- [ ] (Opsional) Tab **Monitor** menampilkan baterai dan suhu HP

---

# BAGIAN B — Penjelasan semua fitur

## B0. Gambaran jendela utama

```
┌──────────────────────────────────────────────────────────────────┐
│ MPD - Mirroring Phone Desktop v1.3                        [_][□][X]│
├──────────────────────────────────────────────────────────────────┤
│                 MPD - Mirroring Phone Desktop                      │
│  Device: Connected  [Infinix_X657B [0777…] ▾] [Refresh] [Panel Cepat]│
│ ┌───────┬──────┬────────┬───────┬─────┬──────┬────────┐            │
│ │Desktop│Preset│Tampilan│Monitor│Macro│Tools │Terminal│            │
│ ├───────┴──────┴────────┴───────┴─────┴──────┴────────┤            │
│ │                                                       │            │
│ │          (isi tab yang sedang dipilih)                │            │
│ │                                                       │            │
│ └───────────────────────────────────────────────────────┘            │
│   Siap.                                    ← pesan status/info       │
│   MPD v1.3 • oleh AhmadHidayatulloh • dibuat dengan bantuan Claude AI │
└──────────────────────────────────────────────────────────────────┘
```

Bagian-bagian tetap:

| Bagian | Fungsi |
|---|---|
| **Device: Connected / Disconnected** | Hijau = ada HP terdeteksi, merah = tidak ada |
| **Dropdown device** | Memilih HP yang dipakai, berguna kalau ada lebih dari satu HP (USB atau WiFi). Formatnya `model [nomor serial]` |
| **Refresh** | Mencari ulang HP yang tersambung |
| **Panel Cepat** | Membuka kotak kecil berisi saklar fitur (lihat B8) |
| **Pesan info** (baris di bawah tab) | Menampilkan progres dan error, mis. "Scrcpy berjalan...", "Preset disimpan" |

---

## B1. Tab Desktop — tempat utama

```
┌──────────────────────────────────────────────┐
│        [ 1. Install Desktop Launcher ]        │
│  [ Setup Freeform Windows (sekali, lalu reboot HP) ] │
│                                              │
│              Desktop Resolution              │
│        [ HD 1280x720 (laptop)          ▾ ]   │
│          Preset / Performance Mode           │
│        [ Ultra Low (A20 Safe)          ▾ ]   │
│                                              │
│  [x] Matikan layar HP saat mirroring (anti panas) │
│  [x] Cadangan: turunkan brightness ke minimum │
│                                              │
│  [ 2. LAUNCH DESKTOP MODE ]  [  STOP  ]      │
│        [ Reset Layar HP ke Normal ]          │
│  [ EMERGENCY STOP (kill scrcpy + reset layar) ] │
└──────────────────────────────────────────────┘
```

### 1. Install Desktop Launcher
- **Untuk apa:** memasang aplikasi launcher bergaya desktop (default: Taskbar) ke HP, supaya muncul taskbar dan jendela mengambang.
- **Cara kerja:** menjalankan `adb install -r taskbar.apk`. Kalau `taskbar.apk` tidak ada di folder MPD, muncul dialog pilih file `.apk`.
- **Contoh:** klik tombol → pesan info berubah "Meng-install launcher..." → "Launcher berhasil di-install."

### Setup Freeform Windows
- **Untuk apa:** mengaktifkan dukungan jendela mengambang (freeform) di Android. Cukup dilakukan **sekali**.
- **Cara kerja:** mengubah tiga pengaturan sistem (`enable_freeform_support`, `force_resizable_activities`, `force_desktop_mode_on_external_displays`), memberi izin tambahan ke Taskbar, lalu **me-restart HP**. Ada pop-up konfirmasi sebelum jalan.
- **Catatan:** tidak semua HP mendukung. HP Android Go biasanya terbatas.

### Desktop Resolution
Mengubah ukuran dan density layar HP menjadi 16:9 seperti layar laptop selama mirroring (memakai `wm size` dan `wm density`).

| Pilihan | Ukuran | Density | Cocok untuk |
|---|---|---|---|
| Tanpa (layar asli HP) | bawaan HP | bawaan | Game yang butuh layar asli, HP yang tidak mau diubah ukurannya |
| Ringan 1024x576 | 1024×576 | 140 | HP low-end |
| HD 1280x720 (laptop) | 1280×720 | 160 | Penggunaan umum |
| FHD 1920x1080 (Laptop) | 1920×1080 | 240 | HP yang kuat |

- **Density kecil** = ikon dan teks lebih kecil, area kerja lebih luas (rasa desktop).
- Ukuran layar dikembalikan otomatis saat berhenti.

### Preset / Performance Mode
Daftar paket pengaturan siap pakai. Memilih preset langsung mengisi semua kolom di tab Preset.

| Preset | Resolusi layar HP | scrcpy (max-size / bitrate / FPS) | Untuk |
|---|---|---|---|
| Ultra Low (A20 Safe) | 1024×576 | 800 / 2M / 30 | HP low-end (default, paling adem) |
| Medium (HD) | 1280×720 | 1280 / 4M / 45 | HP menengah |
| High (FHD 1080p) | 1920×1080 | 1920 / 8M / 60 | HP kuat |
| Honor of Kings (responsif) | layar asli | 1280 / 8M / 60 | Game cepat di HP kuat |
| Stardew Valley (hemat) | 1280×720 | 1024 / 4M / 30 | Game santai, hemat daya |

> Preset FHD 60 FPS terlalu berat untuk chipset seperti Helio A20. HP bisa panas dan patah-patah.

### Matikan layar HP saat mirroring (anti panas)
- **Untuk apa:** layar HP mati selama mirroring, supaya HP tidak panas karena backlight menyala.
- **Cara kerja:** scrcpy dijalankan dengan `--turn-screen-off`. Layar mati tetapi HP tetap aktif.
- Aktif secara default.

### Cadangan: turunkan brightness ke minimum
- **Untuk apa:** pengaman kalau layar HP menyala lagi sendiri (notifikasi, launcher). Brightness diturunkan ke 0 selama mirroring.
- **Cara kerja:** nilai brightness asli disimpan ke file `brightness_backup.json`, lalu dipulihkan setelah selesai. Kalau MPD tertutup paksa, nilainya dipulihkan lewat tombol **Reset Layar HP ke Normal**.
- Hanya aktif kalau opsi "Matikan layar HP" juga dicentang.

### 2. LAUNCH DESKTOP MODE
Tombol utama. Urutan yang dikerjakan MPD:

```
Cek HP terhubung
      ↓
Kunci rotasi layar
      ↓
Ubah ukuran & density layar HP (sesuai Desktop Resolution)
      ↓
Buka launcher Taskbar (kalau belum ter-install: tekan tombol HOME)
      ↓
Turunkan brightness (kalau opsi aktif)
      ↓
Jalankan scrcpy dengan semua pengaturan
      ↓  (kalau gagal cepat → fitur yang tidak didukung dimatikan lalu dicoba lagi)
Berjalan... sampai kamu STOP / tutup jendela
      ↓
Kembalikan ukuran layar, density, rotasi, brightness
```

Selama proses berjalan, tombol LAUNCH, Install Desktop Launcher, dan Setup Freeform dinonaktifkan sementara.

### STOP
Menghentikan scrcpy dengan normal. Setelah itu layar HP dikembalikan seperti semula.

### Reset Layar HP ke Normal
Mengembalikan ukuran layar, density, rotasi (auto-rotate kembali aktif), dan brightness (dari file backup). Pakai kalau MPD tertutup paksa atau HP terasa "aneh" (layar kecil/besar, miring, gelap).

### EMERGENCY STOP
Tombol darurat. Mematikan **paksa semua** proses `scrcpy.exe` (`taskkill /F`), lalu mereset layar dan brightness HP. Pakai kalau jendela hang, lag parah, atau STOP tidak mempan.

---

## B2. Tab Preset — pengaturan detail

```
┌──────────────────────────────────────────────┐
│  Resolusi scrcpy (max-size)   [ 800     ]    │
│  Bitrate                      [ 2M      ]    │
│  Max FPS                      [ 30      ]    │
│                                              │
│  [x] Fullscreen                              │
│  [ ] Rekam gameplay ke PC (MP4)              │
│  [ ] Mode Ghost (jendela, always-on-top, transparan) │
│                                              │
│        Input & kompatibilitas                │
│  [x] Keyboard UHID (keyboard fisik)          │
│  [ ] Mouse UHID (pointer; bikin game sentuh tidak responsif) │
│  [x] Gamepad UHID (Xbox/PS/generic)          │
│  [x] Stay awake (HP tidak tidur)             │
│  [ ] Layar kedua virtual (Android 11+)       │
│  [x] Auto-fallback: matikan fitur yang tidak didukung HP │
│                                              │
│  Simpan pengaturan di atas sebagai preset:   │
│  [ Nama preset        ] [Simpan] [Hapus]     │
└──────────────────────────────────────────────┘
```

### Tiga kolom angka
| Kolom | Artinya | Isi yang valid | Contoh |
|---|---|---|---|
| **Resolusi scrcpy (max-size)** | Sisi terpanjang video yang dikirim ke laptop. Makin besar makin tajam, tapi makin berat | 240–4096 | `800`, `1280`, `1920` |
| **Bitrate** | Jumlah data video per detik. Makin besar makin bagus kualitas, tapi makin berat dan HP makin panas | angka + `K` atau `M` | `2M`, `4M`, `4000K` |
| **Max FPS** | Batas frame per detik. Makin tinggi makin mulus | 1–120 | `30`, `45`, `60` |

Kalau diisi salah, muncul pesan merah di bagian info (mis. "FPS harus angka 1-120") dan LAUNCH tidak jalan.

Patokan aman untuk HP low-end: **800 / 2M / 30**.

### Fullscreen
Jendela scrcpy memenuhi layar laptop. Tekan **F11** (atau MOD+f) untuk keluar atau masuk fullscreen.

### Rekam gameplay ke PC (MP4)
- Merekam mirroring ke file `Rekaman/gameplay_20261121_173045.mp4` di folder MPD (nama memakai tanggal dan jam).
- Tidak memakai memori HP. Kualitas rekaman mengikuti bitrate dan resolusi yang kamu pilih.
- Setelah berhenti, info menampilkan lokasi folder rekaman.

### Mode Ghost
- Jendela scrcpy tampil **berukuran 854×480**, **selalu di atas** jendela lain, dan bisa dibuat **transparan** (atur di tab Tampilan).
- Berguna untuk memantau game sambil mengerjakan hal lain (mis. coding di VS Code).
- Kalau Ghost aktif, **Fullscreen diabaikan**.

### Keyboard UHID
- HP menganggap keyboard laptop sebagai **keyboard fisik sungguhan**. Pengetikan lebih akurat dan mendukung kombinasi tombol.
- Efek samping: keyboard layar HP bisa tidak muncul.

### Mouse UHID
- HP menganggap mouse laptop sebagai **mouse sungguhan** (muncul pointer).
- **Dimatikan secara default** karena game sentuh biasanya **tidak merespons** pointer, hanya sentuhan.
- Aktifkan hanya kalau aplikasi di HP memang mendukung mouse.

### Gamepad UHID
- Gamepad (Xbox/PlayStation/generik) yang dicolok ke laptop diteruskan ke HP seolah dicolok langsung.
- Tidak berefek kalau tidak ada gamepad yang tersambung.

### Stay awake
- HP tidak masuk mode tidur selama mirroring (selama dicolok USB), sehingga mirroring tidak menjadi hitam.

### Layar kedua virtual (Android 11+)
- Alih-alih memirror layar utama, scrcpy membuat **layar virtual terpisah** di HP (mirip DeX).
- **Tidak semua HP mendukung** (HP low-end sering menolak). Kalau ditolak, MPD otomatis kembali ke mirroring biasa.
- Kalau layar virtual dipakai, ukuran layar asli HP tidak diubah.

### Auto-fallback
- **Untuk apa:** supaya MPD bisa dipakai di HP apa saja. Kalau suatu fitur tidak didukung, fitur itu dimatikan otomatis dan mirroring tetap jalan.
- **Cara kerja:** kalau scrcpy gagal dalam ±10 detik pertama, MPD membaca pesan error lalu mematikan fitur yang dicurigai, dalam urutan: *layar virtual → gamepad UHID → mouse UHID → keyboard UHID → stay awake*, kemudian mencoba lagi.
- Fitur yang dimatikan ditampilkan di info, contoh: "Fitur yang otomatis dimatikan: Gamepad UHID, Keyboard UHID."
- **Tidak berlaku** kalau: error karena koneksi/izin HP, scrcpy sudah berjalan lebih dari 10 detik, atau kamu memakai command manual.
- **Keterbatasan:** fitur yang tidak error tetapi diam-diam tidak berfungsi tidak bisa dideteksi.

### Simpan / Hapus preset
- Isi semua kolom dan centang sesuai keinginan, tulis nama di **Nama preset**, klik **Simpan**. Preset muncul di dropdown (tab Desktop dan Panel Cepat).
- Disimpan di file `presets.json` di folder MPD.
- **Hapus** hanya untuk preset buatanmu. Preset bawaan tidak bisa dihapus (kalau disimpan dengan nama yang sama, versimu yang dipakai).
- Contoh: nama `Game Santai`, isi `1024 / 3M / 30`, centang Fullscreen → Simpan.

---

## B3. Tab Tampilan — Ghost, Boss Key, Audio

```
┌──────────────────────────────────────────────┐
│     Mode Ghost (aktifkan di tab Preset)      │
│            Opasitas: 100%                    │
│   ─────────────────●────────────────         │
│                                              │
│   Boss Key (sembunyikan semua + mute)        │
│   [x] Aktifkan, tombol: [ F12 ▾ ]            │
│     [ Tes sembunyikan / tampilkan sekarang ] │
│                                              │
│   Audio HP -> PC (butuh Android 11+)         │
│          [ ] Teruskan audio HP ke PC         │
│            Volume scrcpy: 100%               │
│   ─────────────────────────────●──           │
└──────────────────────────────────────────────┘
```

### Opasitas (Mode Ghost)
- Slider **30%–100%**. Makin kecil makin transparan. Berjalan langsung saat scrcpy berjalan.
- Hanya berefek kalau **Mode Ghost** dicentang di tab Preset.
- **Contoh:** opasitas 50% → kamu bisa melihat VS Code di belakang jendela game.

### Boss Key
- **Untuk apa:** menyembunyikan semuanya dengan satu tombol, misalnya saat ada orang lewat.
- **Cara kerja:** menekan tombol pilihan (F12, F11, F9, F8, atau Pause) menyembunyikan **jendela scrcpy dan jendela MPD**, lalu meng-**mute** suara scrcpy. Tekan lagi untuk menampilkan kembali.
- Tombol ini **hotkey global**, hanya aktif **selama scrcpy berjalan**, jadi tidak mengganggu tombol F12 di aplikasi lain saat MPD tidak sedang mirroring.
- Tombol **Tes sembunyikan / tampilkan sekarang** untuk mencoba tanpa menunggu.
- Tidak ada ikon di system tray. Jendela benar-benar disembunyikan.
- Kalau scrcpy berhenti saat tersembunyi, jendela MPD otomatis ditampilkan kembali.

### Audio HP → PC
- Centang **Teruskan audio HP ke PC** supaya suara HP keluar di speaker laptop.
- Butuh **Android 11 ke atas**. Di HP lebih lama, mirroring tetap jalan tanpa suara.
- **Slider volume** mengatur volume khusus scrcpy lewat mixer Windows (tidak mengubah volume sistem). Slider baru berefek setelah ada suara yang diputar.

---

## B4. Tab Monitor — baterai dan suhu

```
┌──────────────────────────────────────────────┐
│  [x] Aktifkan monitor (cek tiap 5 detik)     │
│                                              │
│            Baterai: 85%                      │
│            Suhu: 37.2°C        ← hijau       │
│     ▓▓▓▓▓▓▓▓░░░░░░░░░░░░░                    │
│                                              │
│     Alarm jika suhu >= [ 45 ] °C             │
└──────────────────────────────────────────────┘
```

- **Untuk apa:** memantau HP secara langsung selama mirroring supaya tidak overheating.
- **Cara kerja:** membaca `dumpsys battery` dari HP tiap 5 detik.
- **Warna suhu:** hijau = aman, **merah** = melewati batas.
- **Alarm:** kalau suhu ≥ batas (default **45°C**), laptop berbunyi *bip* dan muncul peringatan di info. Alarm hanya bunyi maksimal sekali per menit.
- **Batas bisa diubah** di kolom angka. Contoh: isi `42` kalau mau lebih waspada.
- **Kalau panas:** turunkan preset (mis. ke Ultra Low), kecilkan bitrate/FPS, lepas casing, dan jangan sambil mengisi daya.

---

## B5. Tab Macro — otomatis tap dan swipe

```
┌──────────────────────────────────────────────┐
│ ┌──────────────────────────────────────────┐ │
│ │ # Contoh macro                            │ │
│ │ tap 640 360                               │ │
│ │ wait 1                                    │ │
│ │ swipe 300 500 900 500 300                 │ │
│ │ wait 0.5                                  │ │
│ │ key KEYCODE_BACK                          │ │
│ └──────────────────────────────────────────┘ │
│  Ulangi (0 = tanpa henti): [ 1 ]             │
│  [Jalankan] [Stop] [Simpan...] [Buka...]     │
└──────────────────────────────────────────────┘
```

- **Untuk apa:** menjalankan rangkaian sentuhan otomatis, mis. farming di game atau tugas berulang.
- **Cara pakai:** tulis perintah satu per baris di kotak, atur jumlah ulang, klik **Jalankan**. Baris yang diawali `#` adalah komentar.

| Perintah | Artinya | Contoh |
|---|---|---|
| `tap x y` | Ketuk di koordinat | `tap 640 360` |
| `swipe x1 y1 x2 y2 [ms]` | Geser dari titik 1 ke titik 2 (ms = durasi, default 300) | `swipe 300 500 900 500 300` |
| `wait detik` | Tunggu | `wait 1.5` |
| `key NAMA` | Tekan tombol Android | `key KEYCODE_BACK`, `key KEYCODE_HOME` |

- **Koordinat** mengikuti ukuran layar HP **saat itu**. Kalau layar diubah ke 1280×720, x berkisar 0–1279 dan y 0–719.
- **Cara mencari koordinat:** aktifkan **Lokasi penunjuk (Pointer location)** di Opsi pengembang HP, lalu ketuk layar dan baca angka x dan y.
- **Ulangi `0`** = berulang terus sampai kamu klik **Stop**.
- **Simpan.../Buka...** menyimpan dan memuat macro sebagai file `.txt`.
- Kalau ada baris yang salah, muncul pesan, mis. "Baris 3 tidak valid: tap a b", dan macro tidak jalan.
- **Catatan:** MPD **belum merekam sentuhan secara langsung**. Macro ditulis sebagai script. Tiap perintah bisa terasa agak lambat di HP low-end.

---

## B6. Tab Tools — APK, file, WiFi

```
┌──────────────────────────────────────────────┐
│ ┌──────────────────────────────────────────┐ │
│ │ Tarik file .apk, file, atau folder mod   │ │
│ │ ke jendela ini                           │ │
│ └──────────────────────────────────────────┘ │
│  [Pilih APK...] [Push File...] [Push Folder...] │
│  Tujuan di HP: [ /sdcard/Download/        ]  │
│                                              │
│              Koneksi WiFi                    │
│  [ 192.168.1.5:5555 ] [Connect]              │
│  [ Aktifkan WiFi ADB (HP harus tersambung USB) ] │
└──────────────────────────────────────────────┘
```

### Drag & drop APK / file / folder
- **Seret** file dari Windows ke jendela MPD (di mana saja).
- **`.apk`** → di-install ke HP (`adb install -r`).
- **File atau folder lain** → disalin ke HP (`adb push`) ke folder tujuan.
- **Contoh:** tarik folder mod game ke jendela MPD → folder itu tersalin ke `/sdcard/Download/` di HP.
- Info menampilkan hasilnya: "Selesai: 2 berhasil, 1 gagal (...)".
- Kalau drag & drop tidak aktif (library `tkinterdnd2` tidak terpasang), pakai tiga tombol di bawahnya.

### Pilih APK... / Push File... / Push Folder...
Cara yang sama dengan drag & drop, tapi lewat dialog pilih file. **Pilih APK...** boleh memilih banyak file sekaligus.

### Tujuan di HP
Lokasi tujuan untuk `Push`. Default `/sdcard/Download/`. Ubah kalau butuh folder lain, mis. `/sdcard/Android/data/nama.paket/files/`.

### Koneksi WiFi (tanpa kabel)
Urutan memakai WiFi:

1. Colok HP via USB dulu, pastikan **Connected**.
2. Klik **Aktifkan WiFi ADB**. MPD mengaktifkan mode WiFi (port 5555) dan mengisi alamat IP HP otomatis.
3. Pastikan HP dan laptop memakai **WiFi yang sama**, lalu klik **Connect**.
4. Cabut kabel USB, klik **Refresh**. HP tampil di dropdown device dengan nama `192.168.x.x:5555`.
5. Klik **LAUNCH** seperti biasa.

Kalau perlu, bisa juga isi IP manual (mis. `192.168.1.5:5555`) lalu klik Connect. WiFi biasanya sedikit lebih lag dibanding kabel.

---

## B7. Tab Terminal — ketik command sendiri

```
┌──────────────────────────────────────────────┐
│ Command scrcpy (bisa diedit sendiri)         │
│ ┌──────────────────────────────────────────┐ │
│ │ scrcpy --window-title InfinixDesktop …   │ │
│ └──────────────────────────────────────────┘ │
│ [Generate dari pengaturan] [Jalankan command ini] │
│ [ ] Pakai command ini saat LAUNCH            │
│                                              │
│ Terminal (adb / scrcpy)                      │
│ ┌──────────────────────────────────────────┐ │
│ │ > adb devices                            │ │
│ │ List of devices attached                 │ │
│ │ 077743321M101122  device                 │ │
│ │ [selesai, kode 0]                        │ │
│ └──────────────────────────────────────────┘ │
│ [ ketik di sini...         ] [Run][Stop][Clear] │
└──────────────────────────────────────────────┘
```

### Command scrcpy (bisa diedit)
- **Generate dari pengaturan:** mengisi kotak dengan command yang sesuai pengaturan saat ini (tanpa lokasi `scrcpy.exe`).
- **Edit sesukamu:** tambah atau hapus opsi, mis. tambah `--turn-screen-off`, ubah `--max-fps 60`, atau coba opsi scrcpy lainnya.
- **Jalankan command ini:** menjalankan **persis** command di kotak.
- **Pakai command ini saat LAUNCH:** kalau dicentang, tombol LAUNCH memakai command manual ini. Serial HP dan judul jendela ditambahkan otomatis kalau belum ada.
- Pada mode manual, **auto-fallback tidak aktif**.

**Contoh command:**

```
scrcpy --turn-screen-off --stay-awake --max-size 1024 --video-bit-rate 4M --max-fps 45 --fullscreen
```

### Terminal
- **Fungsi:** mengetik perintah `adb` dan `scrcpy` langsung. Tekan **Enter** untuk menjalankan.
- **Hanya `adb` dan `scrcpy`** yang diterima. Perintah lain (mis. `dir`) ditolak demi keamanan.
- **Serial HP terpilih** ditambahkan otomatis, jadi tinggal ketik perintahnya.
- **Panah atas/bawah** = riwayat perintah. Tombol **Stop** menghentikan perintah yang sedang jalan, **Clear** membersihkan layar, `help` menampilkan contoh.
- Tidak mendukung shell interaktif (mis. `adb shell` tanpa perintah).

**Contoh perintah:**

| Ketik | Fungsi |
|---|---|
| `adb devices` | Daftar HP yang tersambung |
| `adb shell wm size` | Lihat ukuran layar HP |
| `adb shell dumpsys battery` | Lihat baterai dan suhu |
| `adb pair 192.168.1.5:37000` | Pairing wireless debugging (Android 11+) |
| `scrcpy --list-displays` | Lihat daftar layar HP |
| `scrcpy --list-encoders` | Lihat encoder video yang didukung HP |
| `scrcpy --new-display=1280x720/160 -x --start-app=com.android.settings --keep-active` | Coba layar virtual yang bisa di-resize (scrcpy 4.0, Android 11+) |

---

## B8. Panel Cepat — kotak saklar yang bisa di-resize

Klik **Panel Cepat** di bagian atas jendela utama untuk membuka jendela kecil ini.

```
┌─ MPD Quick Panel ──────────────────────[_][X]┐
│ Opasitas ──────●──   [x] Pin                 │
│ [ Ultra Low (A20 Safe)                  ▾ ]  │
│ ┌──────────────────────────────────────────┐ │
│ │ (o) Layar HP mati     (o) Brightness min │ │
│ │ (o) Stay awake        (o) Fullscreen     │ │
│ │ ( ) Mode Ghost        ( ) Rekam gameplay │ │
│ │ ( ) Audio ke PC       (o) Keyboard UHID  │ │
│ │ ( ) Mouse UHID        (o) Gamepad UHID   │ │
│ │ ( ) Layar kedua virtual ( ) Boss Key     │ │
│ │ (o) Monitor suhu      (o) Auto-fallback  │ │
│ └──────────────────────────────────────────┘ │
│  [ LAUNCH ]   [ STOP ]   [ EMERGENCY ]       │
│  Scrcpy berjalan...                          │
└──────────────────────────────────────────────┘
```

- **Untuk apa:** menyalakan/mematikan fitur dengan cepat tanpa pindah-pindah tab, plus tombol LAUNCH, STOP, dan EMERGENCY.
- **Bisa di-resize:** tarik pinggir jendela. Makin lebar, saklarnya tersusun makin banyak kolom; makin sempit, makin banyak baris (bisa di-scroll).
- **Opasitas:** transparansi **panel ini sendiri** (40%–100%). Beda dengan opasitas Ghost di tab Tampilan.
- **Pin:** menjaga panel selalu di atas jendela lain.
- **Sinkron:** saklar di panel sama dengan pengaturan di tab lain. Mengubah satu, yang lain ikut berubah.
- **Dropdown preset** di panel memilih preset seperti di tab Desktop.
- **Catatan:** ini jendela biasa yang bisa di-resize, bukan kotak seleksi seperti Snipping Tool.

---

## B9. Kontrol di jendela scrcpy

Setelah mirroring berjalan, kamu mengontrol HP dari jendela scrcpy:

| Aksi | Hasil |
|---|---|
| Klik kiri | Ketuk layar |
| Klik kiri tahan + geser | Geser (swipe) |
| **Klik kanan** | Tombol Kembali (Back) |
| **Klik tengah** | Tombol Home |
| Scroll mouse | Scroll di HP |
| **MOD + h** / **MOD + b** / **MOD + s** | Home / Back / Aplikasi terbaru |
| **MOD + f** atau **F11** | Fullscreen aktif/nonaktif |
| **MOD + o** / **MOD + Shift + o** | Matikan / nyalakan layar HP |
| **MOD + r** | Putar layar |
| **MOD + i** | Tampilkan FPS |
| **MOD + q** | Keluar dari scrcpy |

**MOD** = tombol `Alt` kiri atau `Windows` kiri.

---

## B10. File yang dibuat otomatis

| File/folder | Isi |
|---|---|
| `presets.json` | Preset buatanmu |
| `Rekaman/` | Hasil rekaman gameplay (`gameplay_tanggal_jam.mp4`) |
| `brightness_backup.json` | Cadangan sementara brightness HP. Dihapus otomatis setelah dipulihkan |

---

# Contoh skenario

### 1. Main game ringan dengan HP low-end
1. Tab Desktop → preset **Ultra Low (A20 Safe)**.
2. Pastikan **Matikan layar HP** dicentang.
3. Klik **LAUNCH**. Pantau suhu di tab **Monitor**.
4. Kalau suhu mendekati 45°C, klik **STOP**, biarkan HP dingin, lalu coba lagi.

### 2. Memantau game sambil coding
1. Tab Preset → centang **Mode Ghost**.
2. Tab Tampilan → atur **Opasitas** sekitar 60%.
3. Aktifkan **Boss Key** (F12).
4. Klik **LAUNCH**. Jendela kecil transparan muncul di atas VS Code. Tekan F12 untuk menyembunyikan.

### 3. Merekam gameplay
1. Tab Preset → centang **Rekam gameplay ke PC (MP4)**. Naikkan bitrate bila HP kuat (mis. `6M`).
2. Klik **LAUNCH**, mainkan, lalu klik **STOP**.
3. Buka folder `Rekaman` di folder MPD.

### 4. Memasang mod/APK dari laptop
1. Buka tab **Tools**.
2. Tarik file `.apk` atau folder mod ke jendela MPD.
3. Tunggu info "Selesai: ... berhasil".

### 5. Main tanpa kabel
Ikuti langkah **Koneksi WiFi** di B6, lalu LAUNCH seperti biasa.

---

# Pemecahan masalah

| Gejala | Penyebab umum | Solusi |
|---|---|---|
| `libusb-1.0.dll was not found` | Nama file DLL salah | Ganti nama `libusb-1_0.dll` menjadi `libusb-1.0.dll` |
| **Device: Disconnected** | Kabel/izin/USB debugging | Pakai kabel data, aktifkan USB debugging, izinkan pop-up di HP, klik Refresh |
| "HP belum mengizinkan USB debugging" | Pop-up izin belum disetujui | Cek layar HP, ketuk **Izinkan** |
| Python tidak dikenali | PATH belum diatur | Install ulang Python dan centang **Add python.exe to PATH** |
| `JALANKAN.bat` langsung tertutup | Python belum terpasang | Install Python (A2) |
| Mouse/keyboard tidak bisa mengontrol HP (Xiaomi) | Izin tambahan belum aktif | Aktifkan **USB debugging (Security settings)** |
| Klik di game tidak merespons | **Mouse UHID** aktif | Matikan Mouse UHID di tab Preset |
| Layar HP tidak mati | HP menyalakan layar sendiri | Biarkan opsi **brightness minimum** aktif |
| HP panas / patah-patah | Beban resolusi/FPS terlalu tinggi | Pakai **Ultra Low**, kurangi bitrate/FPS, lihat tab Monitor |
| Layar HP tertinggal kecil/besar/miring setelah tutup | MPD tertutup paksa | Klik **Reset Layar HP ke Normal** atau **EMERGENCY STOP** |
| Brightness HP tertinggal sangat gelap | Backup belum dipulihkan | Klik **Reset Layar HP ke Normal** |
| Scrcpy langsung berhenti dengan error | Fitur tidak didukung HP | Pastikan **Auto-fallback** aktif, atau matikan fitur yang dicurigai |
| Layar virtual tidak muncul | HP/Android tidak mendukung | Matikan opsi tersebut. Mirroring biasa tetap bisa dipakai |
| Tidak ada suara | Android di bawah 11 atau audio tidak dicentang | Centang **Teruskan audio** dan pastikan HP Android 11+ |
| Drag & drop tidak jalan | `tkinterdnd2` belum terpasang | Jalankan lewat `JALANKAN.bat` agar ter-install, atau pakai tombol **Pilih APK...** |
| Jendela scrcpy tersembunyi (Boss Key) | Tombol Boss Key aktif | Tekan lagi tombol Boss Key yang sama |
| Antivirus memblokir `MPD.exe` | File baru buatan sendiri | Tambahkan pengecualian untuk folder MPD |

---

# Tanya-jawab

**Apakah game jalan memakai CPU/GPU laptop?**
Tidak. MPD adalah mirroring. Game dijalankan dan dirender oleh HP. Laptop hanya menampilkan video dan mengirim input. Untuk memakai tenaga laptop, gunakan emulator Android (mis. BlueStacks).

**Apakah ini sama dengan Samsung DeX?**
Belum. Mode "desktop" MPD adalah simulasi: ukuran layar 16:9, launcher bergaya desktop, dan opsi layar virtual (kalau HP mendukung). Hasilnya sangat bergantung pada HP.

**Apakah aman untuk HP?**
MPD hanya memakai perintah ADB biasa (ubah ukuran layar, brightness, dan sejenisnya) dan mengembalikannya setelah selesai. Meski begitu, pantau suhu HP, dan gunakan **Reset Layar HP ke Normal** kalau ada yang tidak kembali normal.

**Bisa dipakai di HP selain Infinix?**
Bisa, untuk HP Android 5.0 ke atas. Fitur yang tidak didukung dimatikan otomatis oleh Auto-fallback.

**Di mana saya bisa mengubah command scrcpy secara manual?**
Tab **Terminal** → kotak **Command scrcpy (bisa diedit sendiri)**.

---

*MPD — Mirroring Phone Desktop • dibuat oleh AhmadHidayatulloh, dengan bantuan AI Claude.*
