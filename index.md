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
- [📝 Report](#-report)
- [📊 Informasi](#-informasi)
- [📋 Referensi Nilai](#-referensi-nilai)

---

## 👤 User Management

> 🔒 **Admin only**

### `/setuser` — Tambah / update user

```
/setuser @628123456789
nrp : 00001
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

> 🔒 **Admin only**

### `/add item` — Tambah item/task

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
```

| Field      | Keterangan                |
| ---------- | ------------------------- |
| `weight`   | Bobot item dalam persen   |
| `priority` | `HIGH` / `MEDIUM` / `LOW` |
| `pic`      | NRP PIC dipisah koma      |

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

> ✅ **Semua user**

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

## 📝 Report

> ✅ **Semua user**

### `/report` — Kirim laporan progres

Format baris task: `Nama Task | progress_sebelum>progress_sesudah | catatan`

```
/report
project : WABOT
item : Perbaikan halaman login
user : 00001
task :
Login Page | 30>75 | Form sudah selesai
Register | 0>20 | Baru mulai
status : UPDATE
```

| Field    | Keterangan                             |
| -------- | -------------------------------------- |
| `item`   | Nama item atau ID angka                |
| `user`   | NRP pelapor                            |
| `task`   | Daftar task (baris baru, tanpa bullet) |
| `status` | Tipe laporan, misal `UPDATE`           |

---

## 📊 Informasi

> ✅ **Semua user**

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

## 📋 Referensi Nilai

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
