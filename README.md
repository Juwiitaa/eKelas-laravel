<h1 align="center">eKelas</h1>
<h3 align="center">(Platform Pembelajaran Online Berbasis Web)</h3><br>

<p align="center">
  <img src="public/img/Logo eKelas removebg.png" alt="Logo eKelas" width="150" height="auto"><br><br>
</p>

<p align="center">
  <strong>Nama :</strong> Juwita <br>
  <strong>NIM :</strong> D0223339
</p>
<br><br>

<p align="center">
  Framework Web Laravel <br>
  2025
</p>
<br>

## Tentang eKelas

**eKelas** adalah platform pembelajaran online berbasis web yang menyediakan materi dan kuis secara digital. Sistem ini memungkinkan pengguna untuk belajar secara mandiri melalui materi yang disediakan guru dan mengukur pemahaman melalui kuis online.

### Role dan fitur-fiturnya

#### 1. Admin (Pengelola Sistem)

- Kelola data pengguna (guru dan siswa)
- Kelola data course
- Lihat semua materi dan kuis
- Kontrol penuh terhadap sistem

#### 2. Guru (Pengelola Materi)

- Tambah, edit, dan hapus course
- Upload materi pembelajaran (PDF, video, teks)
- Buat, edit, dan hapus kuis
- Lihat hasil kuis siswa

#### 3. Siswa (Pengguna Pembelajaran)

- Registrasi & login
- Mengakses materi pembelajaran
- Mengerjakan kuis
- Melihat nilai kuis

<br>

### Tabel-tabel database beserta field dan tipe datanya
<br>

#### Tabel 1 (users)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| name       | String    | Nama pengguna |
| email      | String    | Email pengguna |
| password   | String    | Password pengguna |
| role       | enum      | admin, guru, siswa |
| timestamps | datetime  | created_at dan updated_at |
<br>

#### Tabel 2 (profiles)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| user_id    | foreignId | FK dari tabel users |
| foto       | String    | Foto profil pengguna |
| alamat     | Text      | Alamat pengguna |
| bio        | Text      | Deskripsi singkat |
| timestamps | datetime  | created_at dan updated_at |
<br>

#### Tabel 3 (courses)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| title      | String    | Nama course |
| description| Text      | Deskripsi course |
| user_id    | foreignId | ID guru yang membuat |
| timestamps | datetime  | created_at dan updated_at |
<br>

#### Tabel 4 (materials)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| course_id  | foreignId | ID course terkait |
| title      | String    | Judul materi |
| type       | enum      | pdf, video, teks |
| content    | text      | Link/file/isi materi |
| timestamps | datetime  | created_at dan updated_at |
<br>

#### Tabel 5 (quizzes)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| course_id  | foreignId | ID course terkait |
| question   | text      | Pertanyaan kuis |
| options    | JSON      | Pilihan jawaban |
| answer     | String    | Jawaban benar |
| timestamps | datetime  | created_at dan updated_at |
<br>

#### Tabel 6 (results)

| Nama Field | Tipe Data | Keterangan |
|------------|-----------|------------|
| id         | BIGINT    | Primary key |
| user_id    | foreignId | ID siswa |
| quiz_id    | foreignId | ID kuis |
| score      | Integer   | Nilai |
| timestamps | datetime  | created_at dan updated_at |
<br>

### Jenis-jenis Relasi

- **User ke Profile** (One-to-One)  
  Satu user hanya memiliki satu profil. Relasi ini digunakan untuk memisahkan data pribadi tambahan pengguna agar tidak menumpuk di tabel `users`.

- **User ke Course** (One-to-Many)  
  Satu guru bisa membuat banyak course.

- **Course ke Materi** (One-to-Many)  
  Satu course bisa memiliki banyak materi.

- **Course ke Kuis** (One-to-Many)  
  Satu course bisa memiliki banyak kuis.

- **User ke Quiz melalui Results** (Many-to-Many)  
  Satu siswa bisa mengerjakan banyak kuis, dan satu kuis bisa dikerjakan banyak siswa.
