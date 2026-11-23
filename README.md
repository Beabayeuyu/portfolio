# Portfolio — M. Bayu Adi Putra

Website portfolio satu halaman dengan tema futuristik (dark + cyan–violet), bilingual **ID/EN**, dan responsif penuh untuk desktop maupun mobile.

Dibangun **tanpa framework, tanpa build step** — cukup buka `index.html` di browser.

---

## 1. Struktur file

```
Default Project/
├─ index.html                          ← seluruh HTML + CSS + JS (satu file)
├─ assets/
│  ├─ cv/M-Bayu-Adi-Putra-CV.pdf       ← file untuk tombol "Unduh CV"
│  └─ img/photo.jpg                    ← foto profil (diekstrak dari PDF CV)
└─ README.md
```

## 2. Cara membuka

- **Lokal:** klik dua kali `index.html`, atau drag ke browser.
- **HP:** pindahkan seluruh folder ke hosting (atau jalankan server lokal), lalu buka dari HP.
- Font Google (Space Grotesk & JetBrains Mono) dimuat dari internet. Saat offline, otomatis memakai font sistem — tampilan tetap rapi.

## 3. Cara mengganti konten

### a. Teks yang tampil di halaman
Semua teks punya atribut `data-i18n="nama_kunci"`. Cari kuncinya di file, misalnya:

```html
<p data-i18n="about_p1">Saya bekerja di persimpangan ...</p>
```

### b. Terjemahan (ID & EN)
Kamus terjemahan ada di dalam `<script>` di bagian bawah, pada objek `I18N`:

```js
var I18N = {
  id: { about_p1: 'Saya bekerja di ...', ... },
  en: { about_p1: 'I work at the ...', ... }
};
```

Ubah nilai `id` untuk Bahasa Indonesia dan `en` untuk Bahasa Inggris. Jangan mengubah nama kuncinya.

### c. Deskripsi pengalaman kerja
Setiap bullet pengalaman diberi komentar penanda di HTML:

```html
<!-- EDIT: bullet pencapaian tiap posisi boleh disesuaikan -->
<li data-i18n="e1_b1">Menjaga ketersediaan sistem POS ...</li>
```

Ganti teks bullet **dan** nilai `e1_b1` / `e1_b2` di kedua bahasa (`id` dan `en`) agar konsisten.

### d. Ganti foto
Timpa `assets/img/photo.jpg` dengan foto baru. Rasio ideal **4:5 (portrait)**, minimal 800 px lebar.
Jika nama file berbeda, ubah `src="assets/img/photo.jpg"` pada bagian hero dan kartu profil.

### e. Ganti file CV
Timpa `assets/cv/M-Bayu-Adi-Putra-CV.pdf` dengan PDF terbaru (nama file sama), atau sesuaikan `href` pada tombol **Unduh CV**.

### f. Ubah warna tema
Di bagian `:root` paling atas CSS:

```css
--bg:#05070F;        /* latar utama */
--cyan:#2DE2F2;      /* aksen 1 */
--violet:#7C5CFF;    /* aksen 2 */
--fuchsia:#E879F9;   /* aksen 3 (gradient) */
--txt:#EDF1FA;       /* teks utama */
--muted:#9AA7BE;     /* teks sekunder */
```

### g. Ubah bahasa default
Cari baris berikut di akhir script:

```js
applyLang(saved === 'en' || saved === 'id' ? saved : 'id');
```

Ganti `'id'` terakhir menjadi `'en'` bila ingin default Bahasa Inggris (pilihan pengunjung tetap disimpan di `localStorage`).

## 4. Fitur

- Hero dengan efek *typing*, status "open to opportunities", foto berbingkai HUD + scanline
- Partikel jaringan di background (otomatis berkurang di mobile, nonaktif saat `prefers-reduced-motion`)
- Kursor glow (hanya perangkat dengan mouse)
- Progress bar scroll, navbar glass yang menyusut, scrollspy menu aktif
- Timeline pengalaman dengan node bercahaya dan badge "Sekarang"
- Kartu proyek dengan tilt 3D halus
- Tombol **Salin email** dengan notifikasi dan fallback untuk browser lama
- Toggle **ID / EN** tanpa reload, tersimpan otomatis
- Menu mobile full-screen dengan animasi bertahap
- Aksesibilitas: skip-link, fokus keyboard, `aria-*`, kontras AA, dukungan `prefers-reduced-motion`

## 5. Deploy

### GitHub Pages
1. Buat repository baru, unggah isi folder ini (`index.html` + `assets/`).
2. **Settings → Pages → Source: Deploy from a branch**, pilih `main` dan folder `/root`.
3. Situs tersedia di `https://username.github.io/nama-repo/`.

### Netlify (paling cepat)
1. Buka [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag seluruh folder ke halaman tersebut. Selesai — dapat URL langsung.

### Vercel
Import folder sebagai project statis, tanpa konfigurasi build (output = root).

## 6. Catatan teknis

- Ukuran halaman ± 82 KB (belum termasuk foto & PDF), tanpa dependensi JavaScript eksternal.
- Semua animasi memakai `transform`/`opacity` agar tetap ringan di HP.
- Gambar diberi `width`/`height` untuk mencegah layout shift.
- Untuk og:image media sosial, ganti `assets/img/photo.jpg` dengan gambar 1200×630 bila ingin preview link yang lebih rapi.
