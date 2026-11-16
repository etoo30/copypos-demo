# CopyPOS Demo

Frontend demo untuk kasir ATK, fotokopi, print, inventory, dan antrean jasa. Dibangun dengan Svelte 5, Vite, TypeScript, Dexie, dan IndexedDB. Tidak ada backend atau sinkronisasi cloud.

## Menjalankan

```sh
npm install
npm run dev
```

Login demo: owner, cashier, atau operator. Password presentasi yang ditampilkan adalah `demo123`; sesi login hanya simulasi browser.

## Fitur yang tersedia

- Seed 38 produk ATK serta kategori, merek, supplier, dan tarif jasa.
- CRUD produk dengan pemeriksaan SKU, pencarian, filter kategori, stok minimum, dan penonaktifan produk yang punya histori.
- POS barang dengan diskon nominal, checkout Dexie transaction, inventory movements, dan riwayat transaksi.
- Penerimaan pembelian supplier menambah stok dan menyimpan histori.
- Pembuatan order print/fotokopi/finishing, input jumlah halaman/copy, simplex/duplex, upload PDF/JPG/PNG (maksimum 8 MB), estimasi tarif, dan antrean status.
- Penyelesaian order mengurangi stok produk kertas sesuai jumlah lembar; transaksi atomik mencegah pemotongan stok berulang.
- Pengaturan harga layanan, ringkasan laporan, export CSV, dan export JSON untuk data tabel.

## Batasan demo

File order disimpan sebagai Blob di IndexedDB lokal. Aplikasi belum mem-parsing jumlah halaman PDF atau menyediakan preview/cetak khusus. Penyelesaian order adalah konfirmasi operator, bukan bukti printer sudah mencetak. Data hanya tersedia di browser/origin ini. Backup JSON saat ini ditujukan untuk data tabel dan belum mengemas Blob order menjadi format restore biner. Satuan produk disimpan per SKU; konversi kemasan ke satuan dasar, retur, pembayaran parsial, pelanggan tersimpan, supplier CRUD, dan backup/restore belum tersedia.

Login bukan autentikasi produksi. Jangan gunakan dokumen sensitif. Hapus data browser dapat menghilangkan data demo.

## Build dan deployment

```sh
npm run check
npm run build
```

Deploy sebagai static site di Vercel dengan preset Vite, build `npm run build`, output `dist`, dan install `npm install`. `vercel.json` menyediakan SPA fallback. IndexedDB berjalan pada origin domain yang dideploy; data antar-browser/perangkat tidak disinkronkan.
