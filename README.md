[README.md](https://github.com/user-attachments/files/30220510/README.md)
# Dashboard Monitoring Principal Suretyship

Dashboard pemantauan piutang subrogasi / recovery produk **Suretyship** — PT Asuransi Kredit Indonesia (Askrindo), Divisi Subrogasi / Recovery. Menampilkan pandangan **nasional** dan **per Regional Office** (7 RO, 60 Branch Office), terhubung ke data yang diisi Branch Office pada Google Spreadsheet.

## Cara kerja

```
 Branch Office            Google Spreadsheet             Apps Script            Dashboard (index.html)
 isi sheet         ──►    Data_Entry_<BO> (60 sheet) ──► API JSON (/exec)  ──►  Nasional / per-RO
```

- **`index.html`** — dashboard (HTML mandiri, tanpa library eksternal; ada mode gelap, filter RO/Cabang/COB/Status, tabel prioritas flag risiko).
- **`template/Template_Data_Suretyship_PerBranch.xlsx`** — kerangka data untuk di-upload ke Google Sheets; setiap Branch Office punya sheet sendiri.
- **`apps-script/Code.gs`** — kode Google Apps Script yang menggabungkan semua sheet `Data_Entry_*` menjadi JSON.
- **`docs/Panduan_Setup.md`** — panduan pemasangan lengkap (langkah demi langkah).
- **`docs/Rumus_ARRAYFORMULA.txt`** — rumus otomatis opsional.

Dashboard menarik data dari URL Apps Script yang ditanam pada `index.html` (konstanta `APPS_SCRIPT_URL`). Bila gagal terhubung, dashboard otomatis menampilkan data contoh.

## Mengaktifkan GitHub Pages (agar dashboard punya link)

1. Buat repository baru di GitHub, unggah seluruh isi folder ini (bisa lewat tombol **Add file ▸ Upload files** / drag-drop).
2. Buka **Settings ▸ Pages**.
3. Bagian *Build and deployment* → *Source*: **Deploy from a branch**.
4. *Branch*: **main** , folder **/ (root)** → **Save**.
5. Tunggu 1–2 menit. Situs akan tersedia di:
   `https://<username>.github.io/<nama-repo>/`

Karena file bernama `index.html`, halaman langsung tampil di alamat itu.

## Memperbarui data / URL

- Ganti data: cukup Branch Office mengisi Google Sheet — dashboard menariknya otomatis (tombol **↻ Muat ulang data**).
- Ganti endpoint: edit konstanta `APPS_SCRIPT_URL` di `index.html`, commit ulang.

## ⚠️ Catatan keamanan

Dashboard ini memuat **URL Apps Script** di dalam `index.html`. Bila repo/Pages bersifat **publik**, siapa pun yang membuka halaman (atau melihat source) dapat melihat URL tersebut dan — bila deployment Apps Script disetel **"Anyone"** — ikut membaca data. Untuk data subrogasi yang sensitif, pertimbangkan:

- membatasi akses Apps Script ke **"Anyone within [organisasi Askrindo]"** (pengakses harus login akun organisasi), atau
- menaruh dashboard pada **repo privat / hosting internal** alih-alih GitHub Pages publik, atau
- menambahkan token/parameter rahasia pada Apps Script sebagai gerbang sederhana.

## Acuan regulasi

UU No. 1 Tahun 2016 tentang Penjaminan (Pasal 47 — peralihan hak tagih) · POJK No. 11 Tahun 2025 · POJK No. 40/POJK.03/2019 tentang Penilaian Kualitas Aset Bank Umum.
