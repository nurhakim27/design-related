# 📄 Design System: Laporan Multi-Halaman (A4 PDF)

Panduan *Design System* ini dirancang khusus untuk dokumen formal bergaya elegan dan modern (seperti Laporan Survey, Dokumen Institusi, dsb) yang format cetaknya adalah **A4 Portrait**.

## 1. Color Palette (Palet Warna)
Palet ini memberikan nuansa profesional, elegan, namun tetap dinamis dan mudah dibaca.

| Warna | Preview | Hex Code | Penggunaan |
| :--- | :---: | :--- | :--- |
| **Deep Maroon** | 🟥 | `#7B1113` | Warna dominan, judul utama (`.text-h1`, `.text-h2`), header tabel, dan background komponen penegas. |
| **Vibrant Orange** | 🟧 | `#F38F2F` | Warna aksen, teks *overline*, ikon *FontAwesome*, dan tombol download. |
| **Off-Black** | ⬛ | `#161616` | Warna dasar untuk teks *body* (paragraf) agar lebih lembut di mata dibanding hitam murni. |
| **Light Grey** | ⬜ | `#F9F9F9` | Background alternatif untuk selang-seling baris tabel dan komponen *card* agar tidak monoton. |
| **Pure White** | 🤍 | `#FFFFFF` | Background utama kertas dokumen (A4). |

## 2. Typography (Tipografi)
**Font Utama:** [Montserrat (Google Fonts)](https://fonts.google.com/specimen/Montserrat)

| Style | Ukuran | Ketebalan (Weight) | Letter Spacing | Penggunaan |
| :--- | :--- | :--- | :--- | :--- |
| **Heading 1 (`.text-h1`)** | 42px | 900 (Black) | -1px | Judul utama dokumen di halaman Cover. |
| **Heading 2 (`.text-h2`)** | 28px | 900 (Black) | -1px | Judul bab/halaman (biasanya diberi garis bawah Orange). |
| **Overline (`.text-overline`)**| 14px | 700 (Bold) | +4px | Label kecil di atas judul utama dokumen (estetik). |
| **Body (`.text-body`)** | 14px | 500 (Medium) | -0.2px | Teks paragraf, deksripsi, dan isi konten biasa. |

## 3. Layout & Dokumen Standar (A4)
- **Dimensi Halaman (`.page`):** `794px` x `1123px` (Merupakan ukuran pas A4 Portrait jika dirender pada 96 DPI).
- **Padding Kertas:** `60px` di setiap sisi.
- **Background Kertas:** `var(--white)` dengan sedikit `box-shadow: 0 10px 30px rgba(0,0,0,0.15)` saat ditampilkan di HTML agar terlihat seperti lembaran kertas asli (shadow ini dihilangkan saat proses render PDF).

## 4. Components (Komponen UI)

### A. Tabel Data (`.data-table`)
- **Header Tabel:** Background Deep Maroon, Teks Pure White tebal 700, *All-Caps* 12px.
- **Zebra Cross:** Baris genap (`nth-child(even)`) menggunakan background Light Grey.
- **Baris Sorotan (`.highlight-row`):** Baris penting (seperti "Grand Total") menggunakan warna teks Maroon dengan background transparan orange tipis `rgba(243, 143, 47, 0.1)`.

### B. Status Badges
Digunakan untuk menyoroti perubahan data atau status. (Penting: Wajib menggunakan `display: inline-block` dan `white-space: nowrap` agar kapsul tidak terpotong ke baris baru).
- **`.badge-up` (Hijau):** Untuk status naik/positif. Background hijau transparan, font `12px/700`.
- **`.badge-down` (Merah):** Untuk status turun/negatif. Background merah transparan, font `12px/700`.
- **`.badge-new` (Orange):** Untuk data baru. Background orange transparan, font `12px/700`.

### C. Information Cards (`.card`)
Komponen kotak untuk merangkum informasi (seperti Metode Survey).
- Background Light Grey dengan aksen **garis batas kiri (border-left)** setebal 4px berwarna Orange.
- Sudut ditekuk elegan (`border-radius: 0 10px 10px 0`).

### D. Findings List (`.finding-item`)
Desain khusus untuk list/poin bernomor.
- Angka (*bullet number*) berada di dalam lingkaran Maroon berukuran `40x40 px`.
- Dilengkapi sedikit *shadow* Maroon tipis agar angkanya tampak timbul.

## 5. Script Generation (HTML to PDF)
Untuk mendownload halaman `.page` HTML menjadi file PDF A4 Murni:
- Kita memadukan **html2canvas** (men-screenshot HTML menjadi gambar berkualitas tinggi).
- Disatukan ke dalam **jsPDF** menggunakan format A4 Murni (`unit: 'mm', format: 'A4'`) untuk menghindari *oversized zoom* pada pembaca PDF.
- Menggunakan parameter `scrollY: 0` agar kanvas membaca dari pixel paling atas, dan perintah `window.scrollTo(0, 0)` sebelum eksekusi untuk memastikan tidak terpotong. Khusus untuk teks dengan spasi yang rawan terpotong baris oleh *library*, gunakan `&nbsp;` untuk menguncinya.
