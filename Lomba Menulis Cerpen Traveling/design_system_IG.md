# 🎨 Design System: IG Carousel "Modern Minimalist"

Berikut adalah panduan *Design System* yang kita gunakan untuk desain Carousel. Rangkuman ini akan sangat berguna ketika Anda ingin membuat proyek serupa atau menyamakan desain di platform lain (seperti Figma atau website).

## 1. Color Palette (Palet Warna)

| Warna | Preview | Hex Code | Penggunaan |
| :--- | :---: | :--- | :--- |
| **Deep Maroon** | 🟥 | `#7B1113` | Warna dominan, judul utama, background kontras, & elemen tegas. |
| **Vibrant Orange** | 🟧 | `#F38F2F` | Warna aksen, *highlight* teks, tombol CTA (*Call to Action*), dan ikon. |
| **Off-Black** | ⬛ | `#161616` | Background gelap dan warna teks utama di atas putih/terang. |
| **Light Grey** | ⬜ | `#F9F9F9` | Background alternatif terang agar desain tidak monoton. |
| **Pure White** | 🤍 | `#FFFFFF` | Background utama (*cards*, kanvas), dan warna teks pada background gelap. |

## 2. Typography (Tipografi)

**Font Utama:** [Montserrat (Google Fonts)](https://fonts.google.com/specimen/Montserrat)

| Style | Ukuran | Weight (Ketebalan) | Letter Spacing | Penggunaan |
| :--- | :--- | :--- | :--- | :--- |
| **Heading 1 (`.text-h1`)** | 85px | 900 (Black) | -2px | Judul utama (Sangat tebal, *impactful*) |
| **Heading 2 (`.text-h2`)** | 65px | 900 (Black) | -1.5px | Judul bab atau *section divider* |
| **Overline (`.text-overline`)**| 20px | 700 (Bold) | +6px | Label kecil di atas judul utama (berjarak renggang/estetik) |
| **Body (`.text-body`)** | 28px | 400 (Regular) | -0.3px | Teks paragraf dan deskripsi panjang |

## 3. Layout & Grid

- **Aspek Rasio:** 4:5 (Standar Feed Instagram Portrait)
- **Dimensi Asli Slide:** `1080px` (Lebar) x `1350px` (Tinggi)
- **Safe Zone (Area Aman):** 
  - Bagian tengah slide berukuran presisi **1080px x 1080px** (Rasio 1:1).
  - Margin Atas: `135px` (Area bebas konten penting, biasanya untuk Logo/Kop).
  - Margin Bawah: `135px` (Area bebas konten penting, biasanya untuk Pagination/Footer).
  - Padding Konten: Kiri-Kanan `80px`.

## 4. Components (Komponen UI)

- **Shadow (Bayangan):** Menggunakan shadow lembut namun berdimensi dalam: `box-shadow: 0 20px 60px rgba(0,0,0,0.6)` pada kontainer utama.
- **Tombol & Ikon:** Menggunakan *FontAwesome v6*. Sudut tombol dibulatkan (*border-radius: 30px-50px*) untuk menyeimbangkan tipografi yang tegas.
- **Pagination Dot:** Indikator halaman aktif direpresentasikan dengan kapsul (`width: 24px`, `opacity: 1`), dan halaman tidak aktif dengan lingkaran (`width: 8px`, `opacity: 0.3`).

---

## 🚀 Panduan Memindahkan Desain ke Laptop Kantor

Karena desain kita sudah rampung dalam bentuk file HTML murni, Anda **tidak perlu meng-copy-paste kode yang sangat panjang secara manual**. 

### Cara Paling Mudah & Aman:
1. File Anda saat ini tersimpan di:
   `D:\Hakimku\Bootcamp\Design Testing\Carousel IG Lomba Menulis Cerpen Traveling\`
2. Anda bisa mengirimkan file **`index.html`** dan **`design_system_IG.md`** ini ke WhatsApp Web, Telegram, atau Email Anda.
3. Saat di laptop kantor, cukup download file tersebut. Desain langsung bisa digunakan!

## 5. Script Generation (HTML to Image)

Untuk mendownload halaman `.slide` HTML menjadi file gambar PNG siap posting:
- Menggunakan library **html2canvas** untuk mengambil *screenshot* dari DOM secara langsung.
- **Pengaturan Canvas:** 
  - `scale: 1` agar ukurannya pas dengan deklarasi HTML yaitu 1080x1350px. 
  - `useCORS: true` wajib diaktifkan agar gambar eksternal (seperti dari Unsplash) tidak diblokir oleh sistem keamanan browser.
- **Menghindari Bug Render (Garis Hitam):** Sebelum kanvas difoto, properti `box-shadow` pada `.slide` dihilangkan sementara (`slide.style.boxShadow = 'none'`) karena library html2canvas memiliki kelemahan dalam membaca efek *blur* shadow besar yang kadang berubah jadi garis hitam. Setelah beres difoto, shadow dikembalikan lagi.
- **Mekanisme Download:** Dilakukan menggunakan perulangan *(looping)* `for`. Gambar didownload satu per satu secara otomatis menggunakan elemen `<a>` virtual. Diberikan **jeda (delay) 800ms** antar slide untuk mencegah browser (terutama Chrome) memblokir multiple-download secara massal.
