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
