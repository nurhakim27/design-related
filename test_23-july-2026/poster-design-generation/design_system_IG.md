# 🎨 Design System: IG Carousel "Modern Minimalist" (Updated Style)

Berikut adalah panduan *Design System* terbaru yang telah diperbarui sesuai standar visual dan tata letak *Carousel Instagram* kita.

---

## 1. Color Palette (Palet Warna)

| Warna | Preview | Hex Code | Penggunaan |
| :--- | :---: | :--- | :--- |
| **Deep Maroon** | 🟥 | `#7B1113` | Warna dominan, judul utama, *border accent*, & elemen tegas. |
| **Vibrant Orange** | 🟧 | `#F38F2F` | Warna aksen, *highlight* teks, tombol CTA, & ikon. |
| **Dark Grey** | ⬛ | `#333333` | Warna teks utama (menggantikan hitam pekat agar lebih lembut & elegan). |
| **Body Text Grey** | 🩶 | `#3C3C3C` | Warna teks deskripsi & paragraf panjang agar mudah dibaca. |
| **Light Grey** | ⬜ | `#F9F9F9` | Latar belakang (*background*) kanvas utama slide. |
| **Pure White** | 🤍 | `#FFFFFF` | Latar belakang *cards*, *pill badges*, & teks kontras. |

---

## 2. Tipografi & Bahasa (Typography & Language)

Kombinasi font mengusung gaya **Editorial / Literary High-Contrast**:
- **Font Judul / Headline (Serif):** [Lora (Google Fonts)](https://fonts.google.com/specimen/Lora) — Berkarakter hangat, organik, lembut, dan mirip dengan tipografi cetak buku novel/literasi modern.
- **Font Utama / Body & Badge (Sans-Serif):** [Montserrat (Google Fonts)](https://fonts.google.com/specimen/Montserrat) — Modern, bersih, & sangat mudah dibaca.
- **Standar Bahasa:** **100% Bahasa Indonesia Murni** (Tidak ada istilah campuran bahasa Inggris pada *overline*, *badge*, maupun *headline*).

| Style | Font Family | Ukuran | Ketebalan (Weight) | Letter Spacing | Penggunaan |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Heading 1 (`.text-h1`)** | Lora | 85px | 700 (Bold) | -1px | Judul utama cover / hook (*impactful & warm*) |
| **Heading 2 (`.text-h2`)** | Lora | 65px | 700 (Bold) | -0.5px | Judul bab / *section divider* |
| **Overline (`.text-overline`)**| Montserrat | 20px | 700 (Bold) | +6px | Label kecil di atas judul utama (seperti: `LITERASI & POLA PIKIR`) |
| **Body (`.text-body`)** | Montserrat | 24px – 28px | 400 (Regular) | -0.3px | Teks paragraf (menggunakan warna `#3C3C3C`) |


---

## 3. Layout, Alignment & Grid

- **Aspek Rasio:** 4:5 (Standar Feed Instagram Portrait)
- **Dimensi Asli Slide:** `1080px` (Lebar) x `1350px` (Tinggi)
- **Safe Zone (Area Aman):** 
  - Presisi **1080px x 1080px** (Rasio 1:1) di bagian tengah.
  - Margin Atas: `135px` (`.slide-header` dilengkapi `padding-top: 30px` agar logo tidak mepet ke atas).
  - Margin Bawah: `135px` (`.slide-footer` untuk `footer.png`).
- **Kesejajaran Vertikal (Vertical Alignment):**
  - Konten Slide 1 dan Slide 2 wajib menggunakan `justify-content: flex-start` dengan `padding-top: 50px` pada `.safe-zone` agar judul & *overline* berada di garis tinggi Y yang sejajar presisi.

---

## 4. Visual Style & Components (Komponen UI)

- **Ilustrasi 2D Seamless (True Cutout PNG):**
  - Gambar 2D menggunakan format **Cutout PNG Transparan** tanpa kotak/border/shadow/frame background.
  - Ditambahkan ornamen *Soft Radial Glow* (`radial-gradient`) di belakang objek agar karakter melayang secara alami (*floating aesthetic*).
- **Floating Pill Badges (Pengisi Area Kosong):**
  - Mengisi *blank space* di sisi kiri & kanan elemen visual dengan komponen pill semi-transparan (`backdrop-filter: blur(8px); border: 2px solid rgba(243, 143, 47, 0.4)`).
  - Menggunakan label Bahasa Indonesia (Contoh: `Ide Inspiratif`, `Berpikir Terbuka`, `Fokus Mendalam`, `Pola Pikir Maju`).
- **Logo Header:** Logo (`Logo1.png`) diletakkan di sudut kiri atas dengan `padding-top: 30px` dari batas paling atas.
- **Footer:** Menggunakan gambar `footer.png` di bagian paling bawah tengah (*center*).
- **Background Ornaments:** Gradasi radial (*blobs*) halus Vibrant Orange (20% opacity) & Deep Maroon (12% opacity) di sudut slide.

---

## 5. Script Generation (HTML to Image) & Penanganan CORS File Lokal

Untuk mendownload halaman `.slide` HTML menjadi file gambar PNG siap posting tanpa error pembatasan keamanan browser (*CORS / file:// protocol error*):

- **Library:** `html2canvas` v1.4.1 (via CDN `cdnjs.cloudflare.com`).
- **Embedding Base64 Data URI (WAJIB):** 
  - Seluruh aset gambar lokal (seperti `Logo1.png`, `footer.png`, `hook_illustration_cutout.png`) **wajib di-convert ke format Base64 Data URI** (`data:image/png;base64,...`) di dalam `index.html`.
  - Hal ini penting agar file HTML dapat dibuka langsung lewat protokol `file:///` di browser lokal mana pun tanpa diblokir oleh kebijakan keamanan *CORS origin canvas*.
- **Konfigurasi `html2canvas` Mandatori:**
  ```javascript
  const canvas = await html2canvas(slide, {
    scale: 1,
    useCORS: true,
    allowTaint: true,
    backgroundColor: '#F9F9F9',
    width: 1080,
    height: 1350,
    logging: false
  });
  ```
- **Menghindari Bug Render (Garis Hitam):** Sebelum kanvas difoto, properti `box-shadow` pada `.slide` dihilangkan sementara (`slide.style.boxShadow = 'none'`). Setelah selesai difoto, bayangan dikembalikan.
- **Mekanisme Download Otomatis:** Dilakukan menggunakan perulangan (*looping*) `for` dengan **jeda 800ms** antar slide untuk mencegah pemblokiran multiple download oleh browser.

---

## 6. Alur Kerja Standar & Penyimpanan Konten (SOP Efisiensi Kuota)

Untuk menjaga efisiensi penggunaan kuota token AI dan memberikan hasil terbaik secara instan, alur kerja proyek dibagikan sebagai berikut:

1. **Pembuatan Desain & Render Gambar (Tugas Antigravity):**
   - Membuat file `index.html` lengkap (Slide 1 s/d Slide 5) dengan aset ter-embed Base64 Data URI.
   - Menyediakan tombol *"Download Semua Slide (PNG)"* di bagian atas kanvas HTML.
   - **Penyimpanan Gambar ke Folder Lokal:** Setiap slide secara otomatis di-render ke file gambar PNG presisi 4:5 (`1080x1350px`) dan disimpan di folder lokal proyek (`render_slides/`) agar dapat langsung diakses.

2. **Penyediaan Draf Caption & Hashtags (Tugas Antigravity):**
   - Menyusun draf caption lengkap siap pakai di chat/dokumentasi dalam **100% Bahasa Indonesia Murni**:
     - *Hook/Headline* menarik dengan emoji pendukung.
     - Poin-poin ringkasan isi slide.
     - Call-to-Action (CTA) & info pengumuman (seperti Lomba Cerpen Traveling).
     - Deretan *hashtags* resmi (contoh: `#UniversitasBakriePress #UBBakrie #MembacaBuku...`).

3. **Proses Unggah ke Instagram (Tugas Pengguna - Manual):**
   - Pengguna mengunggah 5 file PNG hasil render dari folder `render_slides/` ke Instagram secara manual dalam hitungan detik.
   - Menyalin draf caption & hashtag yang sudah disiapkan oleh AI.
   - *Catatan:* Tidak menggunakan otomatisasi browser upload untuk mencegah pemborosan kuota model AI.


