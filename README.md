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

