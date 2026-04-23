# Lab7Web - Praktikum 1: PHP Framework (CodeIgniter 4)

| | |
|---|---|
| **Nama** | [Wahyu Andika] |
| **NIM** | [312410182] |
| **Kelas** | [I241B] |
| **Mata Kuliah** | Pemrograman Web 2 |
| **Universitas** | Universitas Pelita Bangsa |

---

## Tujuan Praktikum

1. Mahasiswa mampu memahami konsep dasar Framework
2. Mahasiswa mampu memahami konsep dasar MVC
3. Mahasiswa mampu membuat program sederhana menggunakan Framework CodeIgniter 4

---

## Langkah-Langkah Praktikum

### 1. Konfigurasi PHP Extension

Sebelum menggunakan CodeIgniter 4, perlu mengaktifkan beberapa ekstensi PHP melalui XAMPP Control Panel. Caranya klik **Apache → Config → PHP.ini**, kemudian hilangkan tanda titik koma (`;`) pada ekstensi berikut:

- `extension=intl`
- `extension=mysqli`
- `extension=curl`
- `extension=xml`

Setelah itu simpan file dan restart Apache.

---

### 2. Instalasi CodeIgniter 4

Download CodeIgniter 4 dari [https://codeigniter.com/download](https://codeigniter.com/download), kemudian ekstrak file ZIP ke direktori `htdocs/lab11_ci/` dan rename folder menjadi `ci4`.

Buka browser dengan alamat:
```
http://localhost/lab11_ci/ci4/public/
```

Tampilan awal CodeIgniter 4 berhasil:
<img width="940" height="502" alt="image" src="https://github.com/user-attachments/assets/97692d99-c8f9-47f5-bd0d-d21f8ccc9224" />

---

### 3. Mengaktifkan Mode Debugging

Rename file `env` menjadi `.env`, kemudian buka file tersebut dan ubah nilai variabel:

```
CI_ENVIRONMENT = development
```

Mode debugging aktif akan menampilkan pesan error yang lebih detail ketika terjadi kesalahan pada kode program.

---

### 4. Menjalankan CLI

Buka terminal/command prompt, arahkan ke direktori `ci4`, kemudian jalankan perintah:

```bash
php spark serve
```

Server akan berjalan di `http://localhost:8080`

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/4ebbbc5e-557c-40ac-b320-bb8d7ba83274" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/a82d9885-688f-4c14-a7ed-c8c2d4636d43" />


---

### 5. Membuat Route Baru

Tambahkan route baru pada file `app/Config/Routes.php`:

```php
$routes->get('/', 'Home::index');
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
$routes->get('/artikel', 'Page::artikel');
$routes->get('/page/tos', 'Page::tos');
```

Verifikasi route menggunakan CLI:

```bash
php spark routes
```

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/ee4ffb61-e600-47ad-8e26-2d11d102fe5f" />


---

### 6. Membuat Controller Page

Buat file baru `Page.php` pada direktori `app/Controllers/`:

```php
<?php

namespace App\Controllers;

class Page extends BaseController
{
    public function about()
    {
        return view('about', [
            'title'   => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }

    public function contact()
    {
        return view('contact', [
            'title'   => 'Halaman Kontak',
            'content' => 'Ini adalah halaman kontak kami.'
        ]);
    }

    public function faqs()
    {
        return view('faqs', [
            'title'   => 'Halaman FAQ',
            'content' => 'Ini adalah halaman FAQ.'
        ]);
    }

    public function artikel()
    {
        return view('artikel', [
            'title'   => 'Halaman Artikel',
            'content' => 'Ini adalah halaman artikel.'
        ]);
    }

    public function tos()
    {
        echo "ini halaman Term of Services";
    }
}
```

---

### 7. Membuat Template Layout

Buat folder `template` di dalam `app/Views/`, kemudian buat dua file:

**File `app/Views/template/header.php`**

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
```

**File `app/Views/template/footer.php`**

```php
            </section>
            <aside id="sidebar">
                <div class="widget-box">
                    <h3 class="title">Widget Header</h3>
                    <ul>
                        <li><a href="#">Widget Link</a></li>
                        <li><a href="#">Widget Link</a></li>
                    </ul>
                </div>
                <div class="widget-box">
                    <h3 class="title">Widget Text</h3>
                    <p>Vestibulum lorem elit, iaculis in nisl volutpat,
                    malesuada tincidunt arcu. Proin in leo fringilla,
                    vestibulum mi porta, faucibus felis.</p>
                </div>
            </aside>
        </section>
        <footer>
            <p>&copy; 2021 - Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```

---

### 8. Membuat View Setiap Halaman

Setiap halaman menggunakan template yang sama dengan memanggil `header` dan `footer`.

**Contoh `app/Views/about.php`:**

```php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer'); ?>
```

File yang sama dibuat untuk `contact.php`, `faqs.php`, dan `artikel.php`.

---

### 9. Membuat CSS Layout

File `public/style.css` berisi styling untuk tampilan web dengan layout dua kolom (main content + sidebar).

---

## Hasil Akhir

### Halaman About
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/991d4007-fd7d-4d2e-b0ae-3c3f16465130" />

### Halaman Kontak
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/dfaa793c-505a-442c-a6df-2541243c139a" />

### Halaman Artikel
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/c0c60975-6dcf-4d7b-98f1-331a87af34d6" />

### Halaman Term of Services (Autoroute)
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/43027a2c-ca0d-46b2-a2d0-758d13720096" />

---


# Praktikum 2: Framework Lanjutan (CRUD)
Tujuan

Mahasiswa mampu memahami konsep dasar Model
Mahasiswa mampu memahami konsep dasar CRUD
Mahasiswa mampu membuat program sederhana menggunakan Framework CodeIgniter 4


# Langkah-Langkah Praktikum 2
## 1. Membuat Database

Buka phpMyAdmin, kemudian jalankan query berikut:
```sqlCREATE DATABASE lab_ci4;
sqlCREATE TABLE artikel (
    id INT(11) auto_increment,
    judul VARCHAR(200) NOT NULL,
    isi TEXT,
    gambar VARCHAR(200),
    status TINYINT(1) DEFAULT 0,
    slug VARCHAR(200),
    PRIMARY KEY(id)
);
```

<img width="940" height="504" alt="image" src="https://github.com/user-attachments/assets/0028b8f9-33c4-42aa-82ab-7ad56905e592" />

## 2. Konfigurasi Database

Buka file .env, kemudian ubah konfigurasi database:
```database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
database.default.DBPrefix =
```

<img width="687" height="371" alt="image" src="https://github.com/user-attachments/assets/2d75c07a-cabf-4287-b338-505856f4c37b" />

## 4. Membuat Model

Buat file ArtikelModel.php pada direktori app/Models/:
```php<?php

namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
```

## 4. Membuat Controller Artikel

Buat file Artikel.php pada direktori app/Controllers/ dengan method:
```index() → menampilkan daftar artikel
view($slug) → menampilkan detail artikel
admin_index() → halaman admin
add() → tambah artikel
edit($id) → edit artikel
delete($id) → hapus artikel
```
```
php<?php

namespace App\Controllers;

use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }

    public function view($slug)
    {
        $model = new ArtikelModel();
        $artikel = $model->where(['slug' => $slug])->first();

        if (!$artikel) {
            throw \CodeIgniter\Exceptions\PageNotFoundException::forPageNotFound();
        }

        $title = $artikel['judul'];
        return view('artikel/detail', compact('artikel', 'title'));
    }

    public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/admin_index', compact('artikel', 'title'));
    }

    public function add()
    {
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();

        if ($isDataValid) {
            $artikel = new ArtikelModel();
            $artikel->insert([
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
                'slug'  => url_title($this->request->getPost('judul')),
            ]);
            return redirect('admin/artikel');
        }

        $title = "Tambah Artikel";
        return view('artikel/form_add', compact('title'));
    }

    public function edit($id)
    {
        $artikel = new ArtikelModel();
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();

        if ($isDataValid) {
            $artikel->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi'   => $this->request->getPost('isi'),
            ]);
            return redirect('admin/artikel');
        }

        $data  = $artikel->where('id', $id)->first();
        $title = "Edit Artikel";
        return view('artikel/form_edit', compact('title', 'data'));
    }

    public function delete($id)
    {
        $artikel = new ArtikelModel();
        $artikel->delete($id);
        return redirect('admin/artikel');
    }
}
```

## 5. Membuat View Artikel

Buat folder artikel di dalam app/Views/, kemudian buat file:
```index.php → tampilan daftar artikel
detail.php → tampilan detail artikel
admin_index.php → tampilan admin
form_add.php → form tambah artikel
form_edit.php → form edit artikel
```

## 6. Menambahkan Data Artikel

Tambahkan data dummy ke database melalui phpMyAdmin:
```sqlINSERT INTO artikel (judul, isi, slug) VALUES
('Artikel pertama', 'Lorem Ipsum adalah contoh teks...', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang...', 'artikel-kedua');
```

## 7. Membuat Route CRUD

Tambahkan routing untuk menu admin pada Routes.php:
```php$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

# Hasil Praktikum 2

<img width="602" height="323" alt="image" src="https://github.com/user-attachments/assets/01e9b911-fab1-4b24-9dbf-c904d77a38eb" />

<img width="940" height="502" alt="image" src="https://github.com/user-attachments/assets/83e27ac0-433b-44d3-afd8-d5c50c2dc2af" />

<img width="940" height="497" alt="image" src="https://github.com/user-attachments/assets/578ba7ce-7358-4203-b77d-038ea0be2e5f" />

<img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/d880fd7f-0281-46ef-aad7-ca9bade5cbf7" />

<img width="940" height="504" alt="image" src="https://github.com/user-attachments/assets/836b2bd6-3fa1-4eac-bffd-1a631e4f9d2b" />

# Lab7Web - Praktikum 3: View Layout dan View Cell

---

## Langkah-Langkah Praktikum

### 1. Membuat Layout Utama

Buat folder `layout` di dalam `app/Views/`, kemudian buat file `main.php`:

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title ?? 'My Website' ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
                <?= $this->renderSection('content') ?>
            </section>
            <aside id="sidebar">
                <?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>
                <div class="widget-box">
                    <h3 class="title">Widget Header</h3>
                    <ul>
                        <li><a href="#">Widget Link</a></li>
                        <li><a href="#">Widget Link</a></li>
                    </ul>
                </div>
                <div class="widget-box">
                    <h3 class="title">Widget Text</h3>
                    <p>Vestibulum lorem elit, iaculis in nisl volutpat,
                    malesuada tincidunt arcu. Proin in leo fringilla,
                    vestibulum mi porta, faucibus felis.</p>
                </div>
            </aside>
        </section>
        <footer>
            <p>&copy; 2021 - Universitas Pelita Bangsa</p>
        </footer>
    </div>
</body>
</html>
```

---

### 2. Modifikasi File View

Ubah semua file view agar menggunakan layout baru dengan `extend` dan `section`.

**Contoh `app/Views/about.php`:**

```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->endSection() ?>
```

Hal yang sama dilakukan untuk `contact.php`, `faqs.php`, dan `artikel/index.php`.

---

### 3. Menambahkan Kolom `created_at` pada Database

Jalankan query berikut di phpMyAdmin untuk menambahkan kolom tanggal:

```sql
ALTER TABLE artikel ADD COLUMN created_at DATETIME DEFAULT CURRENT_TIMESTAMP;
```

---

### 4. Membuat Class View Cell

Buat folder `Cells` di dalam `app/`, kemudian buat file `ArtikelTerkini.php`:

```php
<?php

namespace App\Cells;

use CodeIgniter\View\Cells\Cell;
use App\Models\ArtikelModel;

class ArtikelTerkini extends Cell
{
    public function render(string $library = '', array $params = [], int $ttl = 0, string $cacheName = null): string
    {
        $model = new ArtikelModel();
        $artikel = $model->orderBy('created_at', 'DESC')->limit(5)->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

---

### 5. Membuat View untuk View Cell

Buat folder `components` di dalam `app/Views/`, kemudian buat file `artikel_terkini.php`:

```php
<div class="widget-box">
    <h3 class="title">Artikel Terkini</h3>
    <ul>
        <?php foreach ($artikel as $row): ?>
        <li><a href="<?= base_url('/artikel/' . $row['slug']) ?>"><?= $row['judul'] ?></a></li>
        <?php endforeach; ?>
    </ul>
</div>
```

---

### 6. Struktur Folder Akhir

```
app/
├── Cells/
│   └── ArtikelTerkini.php
└── Views/
    ├── layout/
    │   └── main.php
    ├── components/
    │   └── artikel_terkini.php
    ├── artikel/
    │   ├── index.php
    │   └── detail.php
    ├── about.php
    ├── contact.php
    └── faqs.php
```

---

## Hasil Praktikum

### Halaman Artikel dengan Layout Baru
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c9970d15-699a-441f-8ed5-37b168f532f8" />


### Halaman About dengan Layout Baru
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/d317559f-3024-4ede-8cdb-d754127f0371" />


### Sidebar dengan View Cell Artikel Terkini
<img width="278" height="143" alt="image" src="https://github.com/user-attachments/assets/88991b23-8d82-4221-b685-3d7d0be4c6e9" />


---

## Pertanyaan dan Jawaban

### 1. Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?

View Layout memungkinkan developer untuk membuat **satu template utama** yang digunakan bersama oleh banyak halaman. Manfaatnya antara lain:
- **Konsistensi tampilan** — header, footer, dan navigasi selalu sama di semua halaman
- **Efisiensi kode** — tidak perlu menulis ulang struktur HTML di setiap halaman
- **Mudah diupdate** — cukup ubah satu file layout, semua halaman ikut berubah
- **Lebih terstruktur** — pemisahan antara layout dan konten lebih jelas

### 2. Jelaskan perbedaan antara View Cell dan View biasa

| | View Biasa | View Cell |
|---|---|---|
| **Cara panggil** | `return view('nama_view')` dari Controller | `view_cell('Cells\NamaClass::method')` dari View |
| **Logika data** | Data disiapkan di Controller | Data disiapkan di dalam Class Cell sendiri |
| **Reusability** | Harus dipanggil ulang dari setiap Controller | Bisa dipanggil langsung dari View manapun |
| **Kegunaan** | Halaman utama | Komponen kecil seperti sidebar, widget |

### 3. Ubah View Cell agar hanya menampilkan post dengan kategori tertentu

Tambahkan parameter kategori pada method `render()` di `ArtikelTerkini.php`:

```php
<?php

namespace App\Cells;

use CodeIgniter\View\Cells\Cell;
use App\Models\ArtikelModel;

class ArtikelTerkini extends Cell
{
    public function render(string $library = '', array $params = [], int $ttl = 0, string $cacheName = null): string
    {
        $model = new ArtikelModel();
        $artikel = $model->where('status', 1)
                         ->orderBy('created_at', 'DESC')
                         ->limit(5)
                         ->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

Dengan menambahkan `->where('status', 1)`, View Cell hanya akan menampilkan artikel yang sudah dipublish (status = 1).

---

# Lab7Web - Praktikum 4: Framework Lanjutan (Modul Login)

---

## Langkah-Langkah Praktikum

### 1. Membuat Tabel User
Buka phpMyAdmin, kemudian jalankan query berikut pada database `lab_ci4`:

```sql
CREATE TABLE user (
    id INT(11) auto_increment,
    username VARCHAR(200) NOT NULL,
    useremail VARCHAR(200),
    userpassword VARCHAR(200),
    PRIMARY KEY(id)
);
```

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/a99b7a8f-1f42-45b1-b1dd-a866f315b895" />

---

### 2. Membuat Model User
Buat file `UserModel.php` pada direktori `app/Models/`:

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class UserModel extends Model
{
    protected $table = 'user';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['username', 'useremail', 'userpassword'];
}
```

---

### 3. Membuat Controller User
Buat file `User.php` pada direktori `app/Controllers/` dengan method:
- `index()` → menampilkan daftar user
- `login()` → proses login
- `logout()` → proses logout

```php
<?php

namespace App\Controllers;

use App\Models\UserModel;

class User extends BaseController
{
    public function index()
    {
        $title = 'Daftar User';
        $model = new UserModel();
        $users = $model->findAll();
        return view('user/index', compact('users', 'title'));
    }

    public function login()
    {
        helper(['form']);
        $email    = $this->request->getPost('email');
        $password = $this->request->getPost('password');

        if (!$email) {
            return view('user/login');
        }

        $session = session();
        $model   = new UserModel();
        $login   = $model->where('useremail', $email)->first();

        if ($login) {
            $pass = $login['userpassword'];
            if (password_verify($password, $pass)) {
                $login_data = [
                    'user_id'    => $login['id'],
                    'user_name'  => $login['username'],
                    'user_email' => $login['useremail'],
                    'logged_in'  => TRUE,
                ];
                $session->set($login_data);
                return redirect('admin/artikel');
            } else {
                $session->setFlashdata("flash_msg", "Password salah.");
                return redirect()->to('/user/login');
            }
        } else {
            $session->setFlashdata("flash_msg", "Email tidak terdaftar.");
            return redirect()->to('/user/login');
        }
    }

    public function logout()
    {
        session()->destroy();
        return redirect()->to('/user/login');
    }
}
```

---

### 4. Membuat View Login
Buat folder `user` di dalam `app/Views/`, kemudian buat file `login.php` dengan tampilan profesional tema biru.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>">
    <style>
        body {
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }

        #login-wrapper {
            background-color: #fff;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
        }

        #login-wrapper h1 {
            font-size: 26px;
            color: #1a1a2e;
            margin-bottom: 8px;
            text-align: center;
        }

        #login-wrapper p.subtitle {
            text-align: center;
            color: #888;
            font-size: 13px;
            margin-bottom: 25px;
        }

        #login-wrapper label {
            display: block;
            font-size: 13px;
            font-weight: bold;
            color: #444;
            margin-bottom: 5px;
        }

        #login-wrapper input[type="email"],
        #login-wrapper input[type="password"] {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            margin-bottom: 18px;
            box-sizing: border-box;
            transition: border 0.3s;
        }

        #login-wrapper input:focus {
            border-color: #e94560;
            outline: none;
        }

        #login-wrapper button {
            width: 100%;
            padding: 11px;
            background-color: #e94560;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s;
        }

        #login-wrapper button:hover {
            background-color: #c73652;
        }

        .alert {
            padding: 10px 14px;
            border-radius: 5px;
            margin-bottom: 18px;
            font-size: 13px;
        }

        .alert-danger {
            background-color: #ffe0e6;
            color: #c0392b;
            border: 1px solid #f5c6cb;
        }

        .divider {
            text-align: center;
            color: #aaa;
            font-size: 12px;
            margin: 20px 0 10px;
        }
    </style>
</head>
<body>
    <div id="login-wrapper">
        <h1>🔐 Sign In</h1>
        <p class="subtitle">Masuk ke Admin Portal Berita</p>
        
        <?php if(session()->getFlashdata('flash_msg')):?>
        <div class="alert alert-danger">
            ⚠️ <?= session()->getFlashdata('flash_msg') ?>
        </div>
        <?php endif;?>

        <form action="" method="post">
            <label for="InputForEmail">Email Address</label>
            <input type="email" name="email" id="InputForEmail"
                placeholder="contoh@email.com"
                value="<?= set_value('email') ?>">

            <label for="InputForPassword">Password</label>
            <input type="password" name="password"
                id="InputForPassword"
                placeholder="Masukkan password">

            <button type="submit">Login</button>
        </form>

        <p class="divider">© 2021 - Universitas Pelita Bangsa</p>
    </div>
</body>
</html>

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b581538d-a282-44ab-93e3-e95930eb2662" />

```

---

### 5. Membuat Database Seeder
Jalankan perintah berikut di XAMPP Shell untuk membuat seeder:

```bash
php spark make:seeder UserSeeder
```

Buka file `app/Database/Seeds/UserSeeder.php` dan isi dengan:

```php
<?php

namespace App\Database\Seeds;

use CodeIgniter\Database\Seeder;

class UserSeeder extends Seeder
{
    public function run()
    {
        $model = model('UserModel');
        $model->insert([
            'username'     => 'admin',
            'useremail'    => 'admin@email.com',
            'userpassword' => password_hash('admin123', PASSWORD_DEFAULT),
        ]);
    }
}
```

Jalankan seeder:
```bash
php spark db:seed UserSeeder
```

---

### 6. Membuat Auth Filter
Buat file `Auth.php` pada direktori `app/Filters/`:

```php
<?php

namespace App\Filters;

use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;
use CodeIgniter\Filters\FilterInterface;

class Auth implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        if (!session()->get('logged_in')) {
            return redirect()->to('/user/login');
        }
    }

    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // Do something here
    }
}
```

---

### 7. Konfigurasi Filters
Buka file `app/Config/Filters.php`, tambahkan `auth` pada bagian `$aliases`:

```php
public array $aliases = [
    'csrf'          => CSRF::class,
    'toolbar'       => DebugToolbar::class,
    'honeypot'      => Honeypot::class,
    'invalidchars'  => InvalidChars::class,
    'secureheaders' => SecureHeaders::class,
    'cors'          => Cors::class,
    'forcehttps'    => ForceHTTPS::class,
    'pagecache'     => PageCache::class,
    'performance'   => PerformanceMetrics::class,
    'auth'          => \App\Filters\Auth::class,
];
```

---

### 8. Update Routes
Buka file `app/Config/Routes.php` dan tambahkan filter auth pada group admin:

```php
// Login & Logout
$routes->get('/user/login', 'User::login');
$routes->post('/user/login', 'User::login');
$routes->get('/user/logout', 'User::logout');

// Admin dengan filter auth
$routes->group('admin', ['filter' => 'auth'], function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

---

### 9. Percobaan Akses Menu Admin
Ketika mengakses `localhost:8080/admin/artikel` tanpa login, akan diarahkan ke halaman login secara otomatis.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/54c085a5-8f7f-45da-815d-459a158f7208" />

---

### 10. Hasil Login Berhasil
Setelah login dengan:
- **Email:** admin@email.com
- **Password:** admin123

Akan diarahkan ke halaman Admin Portal Berita.

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/51fbfd0d-3afa-4088-98b2-51b7b5ae7737" />

---

### 11. Fungsi Logout
Tombol logout tersedia di header admin. Setelah logout, session dihapus dan diarahkan kembali ke halaman login.

---

Berikut versi yang sudah **rapi, clean, dan siap di-paste ke README GitHub (Markdown)**:

---

#  Lab7Web - Praktikum 5: Pagination dan Pencarian

Praktikum ini bertujuan untuk memahami konsep dasar serta implementasi fitur:

* **Pagination** (pembatasan tampilan data)
* **Pencarian** (filter data)

Menggunakan framework **CodeIgniter 4**.

---

##  Langkah-Langkah Praktikum

### 1. Membuat Pagination

Pagination digunakan untuk membagi data dalam jumlah besar menjadi beberapa halaman agar performa aplikasi tetap optimal.

Buka file **`Artikel.php` (Controller)**, lalu modifikasi method `admin_index()`:

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();

    $data = [
        'title'   => $title,
        'artikel' => $model->paginate(10), // 10 data per halaman
        'pager'   => $model->pager,        // Object pagination
    ];

    return view('artikel/admin_index', $data);
}
```

---

### 2. Menampilkan Pagination pada View

Tambahkan kode berikut di file:

 `app/Views/artikel/admin_index.php`
(tepat di bawah tabel data)

```php
<?= $pager->links(); ?>
```

####  Hasil Pagination:

```md
![Screenshot Pagination](GANTI_DENGAN_URL_SCREENSHOT_LO)
```

---

### 3. Membuat Fitur Pencarian

Fitur ini memungkinkan admin mencari artikel berdasarkan judul.

Update method `admin_index()` pada Controller:

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $q = $this->request->getVar('q') ?? ''; // Ambil query pencarian

    $model = new ArtikelModel();

    $data = [
        'title'   => $title,
        'q'       => $q,
        'artikel' => $model->like('judul', $q)->paginate(10), // Filter judul
        'pager'   => $model->pager,
    ];

    return view('artikel/admin_index', $data);
}
```

---

### 4. Menambahkan Form Pencarian pada View

Tambahkan form berikut di atas tabel data:

```html
<form method="get" class="form-search">
    <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
    <input type="submit" value="Cari" class="btn btn-primary">
</form>
```

---

### 5. Update Link Pagination agar Mendukung Pencarian

Agar keyword tetap tersimpan saat pindah halaman:

```php
<?= $pager->only(['q'])->links(); ?>
```

---

### 6. Hasil Akhir (Pencarian Data)

Setelah fitur pencarian ditambahkan:

* Admin dapat memasukkan kata kunci
* Data artikel akan difilter berdasarkan judul
* Pagination tetap berjalan dengan query pencarian

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/15e6cb3d-1759-4c6c-a420-7a41bcc26c47" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/de4a90e2-f8db-4731-a6ed-ac147ccfea99" />

---

````md
# Lab7Web - Praktikum 6: Relasi Tabel dan Query Builder

Praktikum ini merupakan lanjutan dari praktikum sebelumnya. Pada praktikum ini dilakukan pengembangan aplikasi **CodeIgniter 4** dengan menambahkan **relasi antar tabel**, **Query Builder**, serta **JOIN tabel** untuk menampilkan data artikel beserta kategorinya.

## Tujuan Praktikum

- Memahami konsep relasi antar tabel dalam database.
- Mengimplementasikan relasi **One-to-Many**.
- Menggunakan **Query Builder** pada CodeIgniter 4.
- Menampilkan data dari tabel yang saling berelasi.

---

# Langkah-Langkah Praktikum

## 1. Membuat Tabel Kategori

Buat tabel baru bernama `kategori` untuk menyimpan data kategori artikel.

```sql
CREATE TABLE kategori (
    id_kategori INT(11) AUTO_INCREMENT,
    nama_kategori VARCHAR(100) NOT NULL,
    slug_kategori VARCHAR(100),
    PRIMARY KEY (id_kategori)
);
````

### Struktur Tabel:

| Field         | Type         | Keterangan                  |
| ------------- | ------------ | --------------------------- |
| id_kategori   | INT(11)      | Primary Key, Auto Increment |
| nama_kategori | VARCHAR(100) | Nama kategori               |
| slug_kategori | VARCHAR(100) | Slug kategori               |

---

## 2. Menambahkan Foreign Key pada Tabel Artikel

Agar tabel `artikel` terhubung dengan tabel `kategori`, tambahkan field `id_kategori`.

```sql
ALTER TABLE artikel
ADD COLUMN id_kategori INT(11),
ADD CONSTRAINT fk_kategori_artikel
FOREIGN KEY (id_kategori) REFERENCES kategori(id_kategori);
```

---

## 3. Membuat Model Kategori

Buat file baru:

`app/Models/KategoriModel.php`

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class KategoriModel extends Model
{
    protected $table = 'kategori';
    protected $primaryKey = 'id_kategori';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['nama_kategori', 'slug_kategori'];
}
```

---

## 4. Memodifikasi ArtikelModel

Edit file:

`app/Models/ArtikelModel.php`

Tambahkan relasi JOIN antara artikel dan kategori.

```php
public function getArtikelDenganKategori()
{
    return $this->db->table('artikel')
        ->select('artikel.*, kategori.nama_kategori')
        ->join('kategori', 'kategori.id_kategori = artikel.id_kategori')
        ->get()
        ->getResultArray();
}
```

---

## 5. Memodifikasi Controller Artikel

Edit file:

`app/Controllers/Artikel.php`

Tambahkan pemanggilan model kategori dan filter pencarian.

```php
use App\Models\ArtikelModel;
use App\Models\KategoriModel;
```

Pada method `admin_index()`:

```php
$q = $this->request->getVar('q') ?? '';
$kategori_id = $this->request->getVar('kategori_id') ?? '';
```

Gunakan Query Builder:

```php
$builder = $model->table('artikel')
    ->select('artikel.*, kategori.nama_kategori')
    ->join('kategori', 'kategori.id_kategori = artikel.id_kategori');
```

Filter pencarian:

```php
if ($q != '') {
    $builder->like('artikel.judul', $q);
}

if ($kategori_id != '') {
    $builder->where('artikel.id_kategori', $kategori_id);
}
```

Pagination:

```php
$data['artikel'] = $builder->paginate(10);
$data['pager'] = $model->pager;
```

---

## 6. Memodifikasi View Frontend

Edit file:

`app/Views/artikel/index.php`

Tambahkan kategori pada daftar artikel.

```php
<p>Kategori: <?= $row['nama_kategori']; ?></p>
```

---

## 7. Memodifikasi View Admin

Edit file:

`app/Views/artikel/admin_index.php`

Tambahkan form pencarian dan filter kategori.

```php
<form method="get">
    <input type="text" name="q" placeholder="Cari Judul">
    
    <select name="kategori_id">
        <option value="">Semua Kategori</option>
    </select>

    <button type="submit">Cari</button>
</form>
```

Tambahkan kolom kategori pada tabel:

```php
<th>Kategori</th>
```

Pagination:

```php
<?= $pager->only(['q', 'kategori_id'])->links(); ?>
```

---

## 8. Form Tambah Artikel

Edit file:

`app/Views/artikel/form_add.php`

Tambahkan dropdown kategori.

```php
<select name="id_kategori">
<?php foreach($kategori as $k): ?>
<option value="<?= $k['id_kategori']; ?>">
<?= $k['nama_kategori']; ?>
</option>
<?php endforeach; ?>
</select>
```

---

## 9. Form Edit Artikel

Edit file:

`app/Views/artikel/form_edit.php`

Tambahkan kategori yang dipilih otomatis.

```php
<option value="<?= $k['id_kategori']; ?>"
<?= ($artikel['id_kategori']==$k['id_kategori']) ? 'selected' : ''; ?>>
<?= $k['nama_kategori']; ?>
</option>
```

---

# Hasil Praktikum

Setelah semua langkah selesai, sistem berhasil menampilkan:

* Artikel beserta nama kategori
* Tambah artikel dengan kategori
* Edit kategori artikel
* Hapus artikel
* Filter artikel berdasarkan kategori
* Pencarian artikel
* Pagination tetap berjalan

---

## Screenshot Hasil

### Halaman Admin Artikel

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/35e09a84-af83-406a-ba15-4a50a6556220" />


<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ad40a841-94d0-4bfd-a982-e6f6c8a76abc" />

```

---

# Lab7Web - Praktikum 7: Upload File Gambar

Praktikum ini merupakan lanjutan dari praktikum sebelumnya. Pada praktikum ini dilakukan pengembangan fitur **upload gambar** pada aplikasi **CodeIgniter 4**, khususnya pada fungsionalitas tambah dan edit artikel di panel admin.

## Tujuan Praktikum

- Memahami konsep dasar File Upload pada web.
- Mengimplementasikan fitur upload gambar menggunakan Framework CodeIgniter 4.
- Menerapkan validasi file upload (tipe, ukuran).
- Menampilkan gambar yang telah diunggah pada halaman artikel.

---

# Langkah-Langkah Praktikum

## 1. Membuat Folder Penyimpanan Gambar

Buat folder `gambar` di dalam direktori `public/` sebagai lokasi penyimpanan file gambar yang diunggah.

```bash
mkdir -p public/gambar
```

Pastikan folder tersebut memiliki permission yang cukup agar dapat ditulis oleh server.

---

## 2. Memodifikasi Controller Artikel — Method `add()`

Edit file:

`app/Controllers/Artikel.php`

Tambahkan logika upload file pada method `add()`. File gambar divalidasi sebelum dipindahkan ke folder tujuan, dan nama file digenerate secara acak menggunakan `getRandomName()` untuk menghindari konflik nama.

```php
public function add()
{
    $validation = \Config\Services::validation();
    $validation->setRules([
        'judul'  => 'required',
        'gambar' => [
            'label' => 'Gambar',
            'rules' => 'uploaded[gambar]|is_image[gambar]|mime_in[gambar,image/jpg,image/jpeg,image/png,image/gif,image/webp]|max_size[gambar,2048]',
        ],
    ]);

    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid) {
        $file     = $this->request->getFile('gambar');
        $namaFile = $file->getRandomName();
        $file->move(ROOTPATH . 'public/gambar', $namaFile);

        $artikel = new ArtikelModel();
        $artikel->insert([
            'judul'  => $this->request->getPost('judul'),
            'isi'    => $this->request->getPost('isi'),
            'slug'   => url_title($this->request->getPost('judul')),
            'gambar' => $namaFile,
        ]);
        return redirect('admin/artikel');
    }

    $title  = "Tambah Artikel";
    $errors = $validation->getErrors();
    return view('artikel/form_add', compact('title', 'errors'));
}
```

---

## 3. Memodifikasi Controller Artikel — Method `edit()`

Pada method `edit()`, upload gambar bersifat **opsional**. Jika user tidak memilih file baru, gambar lama tetap dipertahankan. Jika user mengunggah gambar baru, file lama akan dihapus otomatis dari server.

```php
public function edit($id)
{
    $artikelModel = new ArtikelModel();
    $dataArtikel  = $artikelModel->where('id', $id)->first();

    $validation = \Config\Services::validation();
    $rules = ['judul' => 'required'];

    $file = $this->request->getFile('gambar');
    if ($file && $file->isValid() && !$file->hasMoved()) {
        $rules['gambar'] = 'is_image[gambar]|mime_in[gambar,image/jpg,image/jpeg,image/png,image/gif,image/webp]|max_size[gambar,2048]';
    }

    $validation->setRules($rules);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid) {
        $updateData = [
            'judul' => $this->request->getPost('judul'),
            'isi'   => $this->request->getPost('isi'),
        ];

        if ($file && $file->isValid() && !$file->hasMoved()) {
            if (!empty($dataArtikel['gambar'])) {
                $oldFile = ROOTPATH . 'public/gambar/' . $dataArtikel['gambar'];
                if (file_exists($oldFile)) unlink($oldFile);
            }
            $namaFile             = $file->getRandomName();
            $file->move(ROOTPATH . 'public/gambar', $namaFile);
            $updateData['gambar'] = $namaFile;
        }

        $artikelModel->update($id, $updateData);
        return redirect('admin/artikel');
    }

    $data   = $dataArtikel;
    $title  = "Edit Artikel";
    $errors = $validation->getErrors();
    return view('artikel/form_edit', compact('title', 'data', 'errors'));
}
```

---

## 4. Memodifikasi Controller Artikel — Method `delete()`

Saat artikel dihapus, file gambar terkait juga dihapus otomatis dari folder `public/gambar/`.

```php
public function delete($id)
{
    $artikelModel = new ArtikelModel();
    $dataArtikel  = $artikelModel->where('id', $id)->first();

    if (!empty($dataArtikel['gambar'])) {
        $filePath = ROOTPATH . 'public/gambar/' . $dataArtikel['gambar'];
        if (file_exists($filePath)) unlink($filePath);
    }

    $artikelModel->delete($id);
    return redirect('admin/artikel');
}
```

---

## 5. Memodifikasi View Form Tambah Artikel

Edit file:

`app/Views/artikel/form_add.php`

Tambahkan field input file dan ubah atribut `enctype` pada tag `<form>` menjadi `multipart/form-data` agar form dapat mengirimkan data berupa file.

```php
<form action="" method="post" enctype="multipart/form-data">
    ...
    <div class="form-group">
        <label>Gambar Artikel</label>
        <input type="file" name="gambar" accept="image/*">
        <small>Format: JPG, JPEG, PNG, GIF, WEBP. Maks. 2MB.</small>
    </div>
    ...
</form>
```

> **Penting:** Tag `<form>` wajib ditambahkan atribut `enctype="multipart/form-data"`. Tanpa atribut ini, file tidak akan terkirim ke server.

---

## 6. Memodifikasi View Form Edit Artikel

Edit file:

`app/Views/artikel/form_edit.php`

Tambahkan preview gambar saat ini dan field input file untuk mengganti gambar.

```php
<form action="" method="post" enctype="multipart/form-data">
    ...
    <div class="form-group">
        <label>Gambar Artikel</label>
        <?php if (!empty($data['gambar'])): ?>
            <div>
                <img src="<?= base_url('gambar/' . $data['gambar']); ?>"
                     style="max-width:200px; max-height:150px; object-fit:cover;">
                <p>Gambar saat ini: <strong><?= esc($data['gambar']) ?></strong></p>
            </div>
        <?php endif; ?>
        <input type="file" name="gambar" accept="image/*">
        <small>Kosongkan jika tidak ingin mengganti gambar.</small>
    </div>
    ...
</form>
```

---

## 7. Struktur Folder Hasil

```
lab7_php_ci/
├── app/
│   ├── Controllers/
│   │   └── Artikel.php       ← method add, edit, delete dimodifikasi
│   ├── Models/
│   │   ├── ArtikelModel.php
│   │   └── KategoriModel.php
│   └── Views/
│       └── artikel/
│           ├── form_add.php  ← ditambah input file + enctype
│           └── form_edit.php ← ditambah preview + input file + enctype
└── public/
    └── gambar/               ← folder penyimpanan gambar (buat manual)
```

---

# Hasil Praktikum

Setelah semua langkah selesai, sistem berhasil menampilkan:

- Form tambah artikel dengan input upload gambar
- Validasi file: hanya menerima format gambar, maksimal 2MB
- Gambar tersimpan di folder `public/gambar/` dengan nama unik
- Form edit artikel menampilkan preview gambar saat ini
- Gambar lama otomatis terhapus saat diganti atau artikel dihapus

---

## Screenshot Hasil

### Form Tambah Artikel (dengan Input Gambar)

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/f36804d6-b947-4c23-bf2c-ff2f6d4028b5" />

```

### Form Edit Artikel (dengan Preview Gambar)

```
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/22135d3a-5c74-4f1b-a840-0aadb4116896" />

```

### Halaman Admin — Artikel Berhasil Ditambah dengan Gambar

```
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/910e5fd9-43a3-4cc0-8c74-2be266203eb1" />

hanya contoh gambar saja yang saya masukan

```
