# HCGA CONNECT

Portal internal divisi **Human Capital & General Affair (HCGA)** dan **Civil** untuk mengelola layanan karyawan, operasional GA, inventory, proyek, dan pelaporan dalam satu aplikasi web.

## Modul Utama

| Area | Fitur |
| --- | --- |
| **Human Capital** | Database karyawan, MCU periodik, deklarasi & surat tugas dinas, kwitansi obat, anak magang, helpdesk, IR (course & dokumen) |
| **General Affair** | Inventory (Infras, Mess, Electric), stock opname, deviasi stok, safety stock order, work order & serah terima pekerjaan, daily activity, P5M, transport & travel, mess, order pack meal, housekeeping, monitoring RKB |
| **Civil** | e-ProM (monitoring proyek), TPS 3R, electric kWh, monitoring infrastruktur tambang |
| **Administrasi** | Postingan, dokumentasi album, drive dokumen, manajemen akun, audit log |
| **Layanan Karyawan** | Pengaduan layanan, ambil barang (self-order gudang), transport saya |

## Teknologi

- **Frontend:** Next.js 16, React 19, TypeScript
- **Backend:** NestJS 11, TypeScript
- **Database:** PostgreSQL dengan Prisma 7
- **Notifikasi:** Web Push, email (SMTP / Mailgun), WhatsApp

## Struktur Folder

```
backend/    API NestJS + skema & migrasi Prisma (backend/prisma)
frontend/   Aplikasi web Next.js
```

## Menjalankan di Lokal

Prasyarat: Node.js 20+, PostgreSQL.

### 1. Backend

```bash
cd backend
npm install
# buat file .env (lihat bagian Konfigurasi)
npx prisma migrate deploy
npx prisma generate
npm run start:dev
```

API berjalan di `http://localhost:3001/api`.

### 2. Frontend

```bash
cd frontend
npm install
npm run dev
```

Aplikasi berjalan di `http://localhost:3000`.

## Konfigurasi

File `.env` **tidak** disimpan di repository. Variabel utama:

**backend/.env**

| Variabel | Keterangan |
| --- | --- |
| `DATABASE_URL` | Koneksi PostgreSQL |
| `JWT_SECRET` | Kunci token login |
| `PORT` | Port API (default 3001) |
| `FRONTEND_ORIGIN` | Alamat frontend (CORS) |
| `BACKEND_PUBLIC_URL` | Alamat publik API |
| `SMTP_*` / `MAILGUN_*` | Pengiriman email |
| `VAPID_*` | Web push notification |
| `FONNTE_TOKEN*` | Notifikasi WhatsApp |

**frontend/.env**

| Variabel | Keterangan |
| --- | --- |
| `NEXT_PUBLIC_API_URL` | Alamat API backend, mis. `http://localhost:3001/api` |

## Build Produksi

```bash
cd backend && npm run build && npm run start:prod
cd frontend && npm run build && npm run start
```

## Pengujian

```bash
cd backend && npm test
cd frontend && npm test
```
