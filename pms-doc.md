# 📋 PMS Bot — Panduan Command WhatsApp

> Kirim command via WhatsApp untuk mengelola project management system.

---

## 📑 Daftar Isi

- [👤 User Management](#-user-management)
- [📁 Project](#-project)
- [📂 Category](#-category)
- [📌 Item](#-item)
- [🔄 Status & Progress](#-status--progress)
- [👥 Assign PIC](#-assign-pic)
- [🔗 Assign Group ke Project](#-assign-group-ke-project)
- [📝 Report](#-report)
- [📊 Informasi](#-informasi)
- [📋 Referensi Nilai](#-referensi-nilai)
- [🔔 Reminder (API)](#-reminder-api)

---

## 👤 User Management

> 🔒 **Admin only**

### `/setuser` — Tambah / update user

```
/setuser @628123456789
nrp : 00001
nama : abc
role : admin
```

| Field    | Keterangan                        |
| -------- | --------------------------------- |
| `@nomor` | Nomor WhatsApp dengan kode negara |
| `nrp`    | Nomor induk pegawai               |
| `role`   | `admin` atau `user`               |

---

### `/unsetuser` — Hapus user

```
/unsetuser @628123456789
```

---

## 📁 Project

> 🔒 **Admin only**

### `/add project` — Tambah project baru

```
/add project
name : WABOT
description : Aplikasi Bot WA
start date : 2026-05-06
end date : 2026-12-31
```

---

### `/update project` — Ubah nama project

```
/update project
name : WABOT
new name : WABOT v2
```

---

### `/delete project` — Hapus project

```
/delete project
name : WABOT
```

---

## 📂 Category

> 🔒 **Admin only**

### `/add category` — Tambah category ke project

```
/add category
project : WABOT
name : Front End
weight : 40
```

> `weight` adalah bobot category dalam persen (total semua category sebaiknya = 100)

---

### `/update category` — Ubah nama category

```
/update category
project : WABOT
name : Front End
new name : Frontend
```

---

### `/delete category` — Hapus category

```
/delete category
project : WABOT
name : Frontend
```

---

## 📌 Item

### `/add item` — Tambah item/task

> ✅ **Semua user**

```
/add item
project : WABOT
category : Frontend
name : Perbaikan halaman login
start date : 2026-05-06
end date : 2026-05-31
weight : 10
priority : LOW
pic : 00001,00002
type : NEW
```

| Field      | Keterangan                                        |
| ---------- | ------------------------------------------------- |
| `weight`   | Bobot item dalam persen                           |
| `priority` | `HIGH` / `MEDIUM` / `LOW`                         |
| `pic`      | NRP PIC dipisah koma                              |
| `type`     | `NEW` atau `MODIFIKASI` (opsional, default `NEW`) |

---

### `/update item` — Ubah nama item

```
/update item
project : WABOT
category : Frontend
name : Perbaikan halaman login
new name : Perbaikan login & register
```

---

### `/delete item` — Hapus item

```
/delete item
project : WABOT
category : Frontend
name : Perbaikan halaman login
```

---

## 🔄 Status & Progress

> 🔒 **Admin only**

### `/status item` — Update status item

```
/status item
project : WABOT
category : Frontend
name : Perbaikan halaman login
status : IN PROGRESS
```

**Nilai status yang valid:**

| Status        | Keterangan        |
| ------------- | ----------------- |
| `OPEN`        | Belum dikerjakan  |
| `IN PROGRESS` | Sedang dikerjakan |
| `DONE`        | Selesai           |
| `ON HOLD`     | Ditahan sementara |
| `CANCELLED`   | Dibatalkan        |

---

### `/progress item` — Update persentase progress

```
/progress item
project : WABOT
category : Frontend
name : Perbaikan halaman login
progress : 75
```

> Nilai `progress` antara `0` sampai `100`

---

## 👥 Assign PIC

> 🔒 **Admin only**

### `/assign item` — Tambah PIC ke item

```
/assign item
project : WABOT
category : Frontend
name : Perbaikan halaman login
pic : 00001,00002
```

---

## 🔗 Assign Group ke Project

> 🔒 **Admin group only**

Fitur ini memungkinkan group mendaftarkan diri ke project yang sudah ada. Group yang mengirim perintah akan langsung terdaftar dan dapat mengakses project tersebut.

### `/assign group` — Assign group ini ke project

```
/assign group
project : WABOT
```

| Field     | Keterangan                      |
| --------- | ------------------------------- |
| `project` | Nama project yang ingin diikuti |

> Group yang mengirim perintah ini akan langsung terdaftar ke project tersebut. Group harus sudah terdaftar via `/setgroup`.

---

### `/unassign group` — Cabut akses group ini dari project

```
/unassign group
project : WABOT
```

| Field     | Keterangan                               |
| --------- | ---------------------------------------- |
| `project` | Nama project yang ingin dicabut aksesnya |

---

## �📝 Report

> ✅ **Semua user**

### `/report` — Kirim laporan progres

Format baris task: `Nama Item | progress_sebelum>progress_sesudah | catatan`

```
/report
project : WABOT
category : Perbaikan halaman login
user : 00001
task :
Login Page | 30>75 | Sudah selesai bagian form
Register | 0>20 | Baru mulai
status : UPDATE
```

| Field      | Keterangan                                         |
| ---------- | -------------------------------------------------- |
| `category` | Nama category tempat item berada                   |
| `user`     | NRP pelapor                                        |
| `task`     | Daftar item (baris baru); setiap baris = satu item |
| `status`   | Tipe laporan, misal `UPDATE`                       |

> Setiap baris pada `task` adalah **nama item** di dalam category tersebut.
> Progress masing-masing item diperbarui secara individual sesuai nilai `before>after`.

---

## 📊 Informasi

> ✅ **Semua user**

### `/dashboard` — Generate link dashboard

```
/dashboard
```

Mengembalikan link dashboard yang berlaku selama **24 jam**.
- **Admin** → melihat semua project
- **User** → hanya melihat project yang item-nya di-assign ke mereka

---

### `/workload` — Lihat beban kerja per PIC

```
/workload
```

Atau filter per project:

```
/workload
project : WABOT
```

---

### `/list project` — Lihat semua project

```
/list project
```

### `/list project` — Detail satu project

```
/list project
name : WABOT
```

---

### `/summary project` — Ringkasan progress per category

```
/summary project
name : WABOT
```

Contoh output:

```
📊 Summary: WABOT

📂 Frontend
  ████████░░ 80% (4/5 selesai)
📂 Backend
  █████░░░░░ 50% (2/4 selesai)

Overall:
  ██████░░░░ 65% (6/9 item selesai)
```

---

### `/my task` — Lihat task yang di-assign ke kamu

```
/my task
```

---

### `/overdue` — Lihat item yang melewati deadline

```
/overdue
```

---

### `/history item` — Riwayat report suatu item

```
/history item
project : WABOT
category : Frontend
name : Perbaikan halaman login
```

---

## 🔔 Reminder (API)

> Digunakan oleh **n8n Schedule Trigger** untuk mengirim notifikasi otomatis ke WhatsApp group.
> Konfigurasi reminder dapat diubah melalui tabel `reminder_settings` di database atau via API.

### `GET /api/reminder/trigger` — Jalankan semua reminder aktif

Dipanggil oleh n8n pada jadwal tertentu. Mengembalikan daftar pesan yang perlu dikirim.

```
GET /api/reminder/trigger
GET /api/reminder/trigger?type=overdue
```

**Response:**

```json
{
  "success": true,
  "data": [
    {
      "type": "overdue",
      "group_id": "628xxx@g.us",
      "message": "⚠️ Reminder Overdue Items..."
    }
  ]
}
```

> n8n membaca setiap item dalam `data` dan mengirimkan `message` ke `group_id` via WAHA.
> Jika `group_id` null, n8n dapat mengonfigurasi target group secara manual.

---

### `GET /api/reminder/settings` — Lihat semua konfigurasi reminder

```
GET /api/reminder/settings
```

---

### `PATCH /api/reminder/settings/:id` — Update konfigurasi reminder

```
PATCH /api/reminder/settings/1
Content-Type: application/json

{
  "is_active": 1,
  "threshold_days": 5,
  "message_template": "⚠️ Custom pesan reminder overdue:\n{items}"
}
```

| Field              | Keterangan                                                    |
| ------------------ | ------------------------------------------------------------- |
| `is_active`        | `1` = aktif, `0` = nonaktif                                   |
| `threshold_days`   | Jumlah hari untuk tipe `deadline_approaching` / `no_progress` |
| `group_id`         | Target group WA spesifik (null = semua group)                 |
| `message_template` | Template pesan kustom (gunakan `{items}` sebagai placeholder) |
| `label`            | Nama deskriptif reminder                                      |

**Tipe reminder yang tersedia:**

| Type                   | Keterangan                                               |
| ---------------------- | -------------------------------------------------------- |
| `no_report`            | Tidak ada laporan masuk hari ini                         |
| `overdue`              | Item melewati deadline dan belum selesai                 |
| `deadline_approaching` | Item yang deadlinenya dalam N hari ke depan              |
| `no_progress`          | Item yang tidak ada update laporan dalam N hari terakhir |

---

## 📋 Referensi Nilai

### Type Item

| Nilai        | Keterangan            |
| ------------ | --------------------- |
| `NEW`        | Item baru             |
| `MODIFIKASI` | Item hasil modifikasi |

### Status

| Nilai         | Keterangan        |
| ------------- | ----------------- |
| `OPEN`        | Belum dikerjakan  |
| `IN PROGRESS` | Sedang dikerjakan |
| `DONE`        | Selesai           |
| `ON HOLD`     | Ditahan           |
| `CANCELLED`   | Dibatalkan        |

### Priority

| Nilai    | Keterangan       |
| -------- | ---------------- |
| `HIGH`   | Prioritas tinggi |
| `MEDIUM` | Prioritas sedang |
| `LOW`    | Prioritas rendah |

### Role

| Nilai   | Keterangan           |
| ------- | -------------------- |
| `admin` | Akses penuh          |
| `user`  | Hanya baca & laporan |

---

> 💡 **Tips:** Penulisan field tidak harus huruf kapital. `NAME`, `name`, dan `Name` semuanya diterima.

---

_PMS WhatsApp Bot © 2026_
