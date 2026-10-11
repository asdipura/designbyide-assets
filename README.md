# designbyide-assets

Aset statis publik untuk Web App designbyide, disajikan lewat jsDelivr.
Isi folder ini menjadi root repo GitHub **publik** (mis. `himaide/designbyide-assets`).

```
designbyide-assets/
├── README.md
├── guide/
│   ├── preview-luaran-1440.webp   # 1440 × 300, layar biasa & mobile
│   └── preview-luaran-2880.webp   # 2880 × 600, layar retina
└── konten-demo/                   # dipakai tombol "Isi contoh"
    ├── demo.json                  # daftar & urutan file
    ├── cover.avif                 # 1080 × 1058, tanpa identitas cover
    └── 2-converted.avif …         # 1080 × 1350 per slide isi
```

## Spesifikasi `preview-luaran`

- 6 slide 4:5 berjajar tanpa jarak → rasio **24:5** (6 × 1080 : 1350).
- **Tanpa teks catatan.** Catatan ("diisi hero image…", dst.) ditulis di HTML agar tajam,
  bisa dibaca screen reader, dan bisa diedit tanpa export ulang.
- Urutan kolom harus cocok dengan catatan di `Index.html`:
  1. cover · 2. kolase · 3–4. dua slide digabung · 5–6. bebas.
- Format WebP, kualitas ±80. Nama file dan ukuran harus persis seperti di atas
  (`GUIDE_STRIP` di `Index.html`).

## `konten-demo`

- `demo.json` menentukan file mana yang dipakai dan urutannya:
  `{ "cover": "cover.avif", "images": ["2-converted.avif", …] }`
- Cover 1080 × 1058 (bagian identitas diisi otomatis). Slide isi 1080 × 1350.
- 3–7 gambar isi bila `DEMO_SYNOPSIS` diisi (slide sinopsis dibuat otomatis), 3–8 bila kosong.
- Teks contoh (nama, angkatan, nama karya, kategori, konteks, sinopsis) **tidak** di sini,
  tetapi di Spreadsheet → tab Config (`DEMO_*`), supaya bisa diubah tanpa rilis baru.
- JPG/PNG/WebP/AVIF, maks. 15 MB per file. AVIF paling kecil, tetapi butuh browser
  yang cukup baru (Safari 16+).

## Rilis

1. Commit perubahan gambar.
2. Buat tag baru, mis. `v1.0.1` (jangan menimpa tag lama).
3. Di Spreadsheet → tab **Config**, isi `ASSET_BASE_URL`:
   `https://cdn.jsdelivr.net/gh/USER/REPO@v1.0.1`
4. Jalankan `checkConfig`, lalu buka URL berikut untuk memastikan file ada:
   `https://cdn.jsdelivr.net/gh/USER/REPO@v1.0.1/guide/preview-luaran-1440.webp`

URL dengan `@main` ditolak oleh `Code.gs`: jsDelivr menyimpan cache cabang berhari-hari,
jadi gambar baru belum tentu langsung muncul. Tag/commit selalu memberi versi yang pasti.

Batas jsDelivr untuk repo GitHub: maks. 20 MB per file. Simpan file sumber (PSD/Figma
export resolusi penuh) di tempat lain, bukan di repo ini.
