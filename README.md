<p align="center">
  <img src="mpd.png" alt="Logo MPD" width="180">
</p>

<h1 align="center">MPD — Mirroring Phone Desktop</h1>

<p align="center">
  Aplikasi Windows untuk memirror HP Android ke laptop dengan rasa "desktop",<br>
  dibuat supaya HP <b>low budget</b> juga bisa merasakan mirroring seperti HP mahal.
</p>

---

## Pembuat

**AhmadHidayatulloh**

## Latar belakang ide

Ide ini tercipta karena ingin **merasakan HP low budget mirroring seperti HP mahal yang bisa mirroring**
(mode desktop ala Samsung DeX dan sejenisnya). Proyek ini dikerjakan **dengan bantuan AI Claude** (Anthropic).

Awalnya dibuat untuk Infinix Smart 5 (MediaTek Helio A20), lalu dikembangkan supaya bisa dipakai di HP Android lain.

## Apa itu MPD?

MPD adalah antarmuka (GUI) di atas [scrcpy](https://github.com/Genymobile/scrcpy) dan ADB.
Kamu tidak perlu mengetik command panjang. Semua diatur lewat tombol, saklar, dan preset.
Kalau mau mengetik sendiri, ada tab **Terminal** yang bisa diedit bebas.

> **Penting:** MPD adalah *mirroring*. Game/aplikasi tetap dijalankan oleh CPU/GPU **HP**, bukan laptop.
> Laptop hanya menerima video, menampilkannya, dan mengirim input (keyboard/mouse/gamepad).
> Jadi performa tetap dibatasi kemampuan HP. Untuk memakai tenaga laptop, gunakan emulator Android.

## Fitur

| Fitur | Keterangan |
|---|---|
| Preset | Ultra Low, Medium (HD), High (FHD), Honor of Kings, Stardew Valley, dan preset buatan sendiri |
| Layar HP mati | Layar HP dimatikan saat mirroring + brightness minimum sebagai cadangan (anti panas) |
| Simulasi desktop | Mengubah ukuran layar dan density HP jadi 16:9 seperti laptop, lalu membuka launcher (mis. Taskbar) |
| Input lengkap | Keyboard, mouse, dan gamepad lewat UHID |
| Auto-fallback | Fitur yang tidak didukung HP dimatikan otomatis dan scrcpy dicoba lagi |
| Layar kedua virtual | `--new-display` (Android 11+, tidak semua HP mendukung) |
| Monitor | Baterai dan suhu HP, dengan alarm kalau terlalu panas |
| Macro | Script tap, swipe, wait, dan key |
| Mode Ghost | Jendela selalu di atas dengan transparansi |
| Boss Key | Hotkey global untuk menyembunyikan jendela + mute |
| Rekam gameplay | Langsung ke file MP4 di PC (folder `Rekaman`) |
| Drag & drop | Install APK atau push file/folder mod ke HP |
| Multi-device | Pilih HP lewat dropdown, USB maupun WiFi |
| Terminal + command editor | Ketik `adb` / `scrcpy` sendiri dan edit command sebelum dijalankan |
| Quick Panel | Kotak kecil yang bisa di-resize berisi saklar fitur |
| Emergency Stop | Mematikan scrcpy dan mengembalikan layar/brightness HP seketika |

## Kebutuhan

- Windows 10/11
- Python 3.10+ (centang **Add python.exe to PATH** saat install), hanya jika menjalankan dari kode atau membuat `.exe`
- HP Android dengan **USB debugging** aktif
- Kabel USB yang mendukung data (bukan kabel charge saja)

File `adb.exe`, `scrcpy.exe`, DLL, dan `scrcpy-server` sudah ada di folder ini.

## Cara menjalankan

> Panduan lengkap dan bergambar-teks ada di [`guide/guide.md`](guide/guide.md).

1. Extract folder `MPD`.
2. Di HP: **Pengaturan → Tentang ponsel →** ketuk *Nomor build* 7 kali → **Opsi pengembang → USB debugging**.
3. Colok HP ke laptop, izinkan pop-up *USB debugging* di HP.
4. Klik dua kali **`JALANKAN.bat`**. Library yang kurang akan ter-install otomatis.
5. Pastikan status menunjukkan **Device: Connected**, pilih preset, klik **LAUNCH DESKTOP MODE**.

### Membuat `MPD.exe`

Klik dua kali **`BUILD_EXE.bat`**. Hasilnya `MPD.exe` (lengkap dengan logo) muncul di folder ini,
di sebelah `scrcpy.exe` dan `adb.exe`. Jangan pindahkan `MPD.exe` keluar dari folder ini, karena butuh file-file di sebelahnya.

## Kompatibilitas HP

MPD ditujukan untuk **semua HP Android**. iPhone tidak didukung.

| Fitur | Syarat umum |
|---|---|
| Mirroring dan kontrol | Android 5.0 ke atas |
| Layar HP mati, rekam, FPS/bitrate, Ghost, Boss Key, macro | Semua HP yang bisa mirroring |
| Audio HP ke PC | Android 11 ke atas |
| Layar kedua virtual / flex display | Android 11 ke atas, dan tergantung HP (HP low-end sering menolak) |
| UHID (keyboard/mouse/gamepad) | Tergantung kernel HP |
| Ubah ukuran layar/density | Umumnya semua, sebagian HP membatasi |

Fitur yang tidak didukung **tidak akan berefek**: MPD mematikannya otomatis (selama **Auto-fallback** aktif)
lalu melanjutkan mirroring biasa. Fallback hanya menangkap kegagalan yang membuat scrcpy langsung berhenti;
fitur yang diam-diam tidak berfungsi tidak bisa dideteksi.

Tips per merek:
- **Xiaomi / Redmi / POCO:** aktifkan juga **USB debugging (Security settings)** agar mouse/keyboard bisa mengontrol HP.
- Kalau HP tidak terdeteksi, install driver USB dari pabrikan HP-nya.

## Batasan yang perlu diketahui

- Performa mengikuti HP. Untuk chipset seperti Helio A20, target realistis adalah 720p, 30 FPS, bitrate 2–4M.
  Preset FHD 60 FPS bisa membuat HP panas dan patah-patah.
- Mode "desktop" di MPD adalah simulasi (ukuran layar + launcher). Bukan mode desktop resmi seperti Samsung DeX.
- Mouse UHID dimatikan secara default karena membuat game sentuh tidak merespons klik.
- Mengubah ukuran layar HP bersifat sementara. Kalau MPD tertutup paksa, klik **Reset Layar HP ke Normal**
  (atau **EMERGENCY STOP**) untuk mengembalikan ukuran layar, density, rotasi, dan brightness.
- Dipakai dengan risiko sendiri. Selalu cek suhu HP saat memakai resolusi tinggi.

## Pemecahan masalah

| Masalah | Solusi |
|---|---|
| `libusb-1.0.dll was not found` | Pastikan nama filenya `libusb-1.0.dll` (titik, bukan underscore) |
| Device: Disconnected | Cek kabel, USB debugging, dan pop-up izin di HP. Klik **Refresh** |
| Layar HP tidak kembali normal | Klik **Reset Layar HP ke Normal** atau **EMERGENCY STOP** |
| Fitur tertentu tidak jalan | Matikan saklarnya, atau lihat pesan error di bagian bawah / tab Terminal |

## Isi folder

```
MPD/
├─ main.py            kode aplikasi
├─ mpd.ico / mpd.png  logo
├─ guide/guide.md     panduan lengkap pemakaian + penjelasan semua fitur
├─ JALANKAN.bat       jalankan dari kode
├─ BUILD_EXE.bat      buat MPD.exe
├─ adb.exe, scrcpy.exe, *.dll, scrcpy-server   komponen bawaan
├─ presets.json       dibuat otomatis (preset buatanmu)
├─ Rekaman/           dibuat otomatis (hasil rekaman)
└─ LICENSE-scrcpy.txt lisensi scrcpy
```

## Riwayat versi singkat

- **v1.0–1.2:** GUI scrcpy untuk Infinix Smart 5, preset, monitor, macro, terminal, Quick Panel, UHID, auto-fallback.
- **v1.3:** rebrand jadi **MPD – Mirroring Phone Desktop**, logo aplikasi, README, kredit pembuat.

## Kredit dan lisensi

- Dibuat oleh **AhmadHidayatulloh**, dengan bantuan **AI Claude** (Anthropic).
- Mirroring memakai **[scrcpy](https://github.com/Genymobile/scrcpy)** oleh Genymobile (Apache License 2.0, lihat `LICENSE-scrcpy.txt`).
- `adb` adalah bagian dari Android SDK Platform-Tools (Google).
- Antarmuka memakai [CustomTkinter](https://github.com/TomSchimansky/CustomTkinter).

MPD adalah proyek mandiri dan tidak berafiliasi dengan Genymobile maupun Google.
