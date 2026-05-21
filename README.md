# Lab7Web - Praktikum Web 2 (CodeIgniter 4)

| | |
|---|---|
| **Nama** | Wahyu Andika |
| **NIM** | 312410182 |
| **Kelas** | I241B |
| **Mata Kuliah** | Pemrograman Web 2 |
| **Universitas** | Universitas Pelita Bangsa |

---

## Daftar Praktikum

- [Praktikum 1 — PHP Framework (CodeIgniter 4)](#praktikum-1--php-framework-codeigniter-4)
- [Praktikum 2 — Framework Lanjutan (CRUD)](#praktikum-2--framework-lanjutan-crud)
- [Praktikum 3 — View Layout dan View Cell](#praktikum-3--view-layout-dan-view-cell)
- [Praktikum 4 — Modul Login](#praktikum-4--modul-login)
- [Praktikum 5 — Pagination dan Pencarian](#praktikum-5--pagination-dan-pencarian)
- [Praktikum 6 — Relasi Tabel dan Query Builder](#praktikum-6--relasi-tabel-dan-query-builder)
- [Praktikum 7 — Upload File Gambar](#praktikum-7--upload-file-gambar)
- [Praktikum 8 — AJAX dengan CodeIgniter 4](#praktikum-8--ajax-dengan-codeigniter-4)
- [Praktikum 9 — Pagination & Filter AJAX Admin](#praktikum-9--pagination--filter-ajax-admin)
- [Praktikum 10 — REST API dengan CodeIgniter 4](#praktikum-10--rest-api-dengan-codeigniter-4)

---

# Praktikum 1 — PHP Framework (CodeIgniter 4)

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

**Contoh `app/Views/about.php`:**

```php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer'); ?>
```

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

# Praktikum 2 — Framework Lanjutan (CRUD)

## Tujuan Praktikum

1. Mahasiswa mampu memahami konsep dasar Model
2. Mahasiswa mampu memahami konsep dasar CRUD
3. Mahasiswa mampu membuat program sederhana menggunakan Framework CodeIgniter 4

---

## Langkah-Langkah Praktikum

### 1. Membuat Database

Buka phpMyAdmin, kemudian jalankan query berikut:

```sql
CREATE DATABASE lab_ci4;

CREATE TABLE artikel (
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

---

### 2. Konfigurasi Database

Buka file `.env`, kemudian ubah konfigurasi database:

```
database.default.hostname = localhost
database.default.database = lab_ci4
database.default.username = root
database.default.password = 
database.default.DBDriver = MySQLi
database.default.DBPrefix =
```

<img width="687" height="371" alt="image" src="https://github.com/user-attachments/assets/2d75c07a-cabf-4287-b338-505856f4c37b" />

---

### 3. Membuat Model

Buat file `ArtikelModel.php` pada direktori `app/Models/`:

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table         = 'artikel';
    protected $primaryKey    = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```

---

### 4. Membuat Controller Artikel

Buat file `Artikel.php` pada direktori `app/Controllers/` dengan method:
- `index()` → menampilkan daftar artikel
- `view($slug)` → menampilkan detail artikel
- `admin_index()` → halaman admin
- `add()` → tambah artikel
- `edit($id)` → edit artikel
- `delete($id)` → hapus artikel

---

### 5. Membuat Route CRUD

Tambahkan routing untuk menu admin pada `Routes.php`:

```php
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```

---

## Hasil Praktikum

<img width="602" height="323" alt="image" src="https://github.com/user-attachments/assets/01e9b911-fab1-4b24-9dbf-c904d77a38eb" />

<img width="940" height="502" alt="image" src="https://github.com/user-attachments/assets/83e27ac0-433b-44d3-afd8-d5c50c2dc2af" />

<img width="940" height="497" alt="image" src="https://github.com/user-attachments/assets/578ba7ce-7358-4203-b77d-038ea0be2e5f" />

<img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/d880fd7f-0281-46ef-aad7-ca9bade5cbf7" />

<img width="940" height="504" alt="image" src="https://github.com/user-attachments/assets/836b2bd6-3fa1-4eac-bffd-1a631e4f9d2b" />

---

# Praktikum 3 — View Layout dan View Cell

## Langkah-Langkah Praktikum

### 1. Membuat Layout Utama

Buat folder `layout` di dalam `app/Views/`, kemudian buat file `main.php` sebagai template utama yang digunakan bersama oleh semua halaman menggunakan `renderSection()`.

---

### 2. Membuat Class View Cell

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
        $model   = new ArtikelModel();
        $artikel = $model->orderBy('created_at', 'DESC')->limit(5)->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

---

### 3. Struktur Folder Akhir

```
app/
├── Cells/
│   └── ArtikelTerkini.php
└── Views/
    ├── layout/
    │   └── main.php
    ├── components/
    │   └── artikel_terkini.php
    └── artikel/
        ├── index.php
        └── detail.php
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

---

# Praktikum 4 — Modul Login

## Langkah-Langkah Praktikum

### 1. Membuat Tabel User

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

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class UserModel extends Model
{
    protected $table         = 'user';
    protected $primaryKey    = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['username', 'useremail', 'userpassword'];
}
```

---

### 3. Membuat Controller User

```php
<?php

namespace App\Controllers;

use App\Models\UserModel;

class User extends BaseController
{
    public function login()
    {
        if (session()->get('logged_in')) {
            return redirect()->to(base_url('admin/artikel'));
        }

        if (strtolower($this->request->getMethod()) === 'post') {
            $model    = new UserModel();
            $username = $this->request->getPost('username');
            $password = $this->request->getPost('password');

            $user = $model->where('username', $username)->first();

            if ($user && password_verify($password, $user['userpassword'])) {
                session()->set([
                    'username'  => $user['username'],
                    'email'     => $user['useremail'] ?? '',
                    'logged_in' => true,
                ]);
                return redirect()->to(base_url('admin/artikel'));
            }

            return redirect()->back()->withInput()->with('error', 'Username atau Password salah!');
        }

        return view('user/login', ['title' => 'Login System']);
    }

    public function logout()
    {
        session()->destroy();
        return redirect()->to(base_url('login'));
    }
}
```

---

### 4. Membuat Database Seeder

```bash
php spark make:seeder UserSeeder
```

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

```bash
php spark db:seed UserSeeder
```

---

### 5. Membuat Auth Filter

Buat file `app/Filters/AuthFilter.php`:

```php
<?php

namespace App\Filters;

use CodeIgniter\HTTP\RequestInterface;
use CodeIgniter\HTTP\ResponseInterface;
use CodeIgniter\Filters\FilterInterface;

class AuthFilter implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        if (!session()->get('logged_in')) {
            return redirect()->to('/login');
        }
    }

    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // Do something
    }
}
```

---

### 6. Update Routes

```php
$routes->get('login', 'User::login');
$routes->post('login', 'User::login');
$routes->get('logout', 'User::logout');

$routes->group('admin', ['filter' => 'authFilter'], function ($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->match(['get', 'post'], 'artikel/add', 'Artikel::add');
    $routes->match(['get', 'post'], 'artikel/edit/(:num)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:num)', 'Artikel::delete/$1');
});
```

---

## Hasil Praktikum

### Halaman Login
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b581538d-a282-44ab-93e3-e95930eb2662" />

### Redirect ke Login saat Akses Admin tanpa Sesi
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/54c085a5-8f7f-45da-815d-459a158f7208" />

### Berhasil Login — Dashboard Admin
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/51fbfd0d-3afa-4088-98b2-51b7b5ae7737" />

---

# Praktikum 5 — Pagination dan Pencarian

## Tujuan Praktikum

1. Memahami konsep dasar Pagination
2. Mengimplementasikan fitur pencarian (filter data)

---

## Langkah-Langkah Praktikum

### 1. Membuat Pagination

Modifikasi method `admin_index()` pada `Artikel.php`:

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();

    $data = [
        'title'   => $title,
        'artikel' => $model->paginate(10),
        'pager'   => $model->pager,
    ];

    return view('artikel/admin_index', $data);
}
```

Tambahkan di view (di bawah tabel):

```php
<?= $pager->links(); ?>
```

---

### 2. Membuat Fitur Pencarian

Update method `admin_index()`:

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $q     = $this->request->getVar('q') ?? '';
    $model = new ArtikelModel();

    $data = [
        'title'   => $title,
        'q'       => $q,
        'artikel' => $model->like('judul', $q)->paginate(10),
        'pager'   => $model->pager,
    ];

    return view('artikel/admin_index', $data);
}
```

Tambahkan form pencarian di view:

```html
<form method="get" class="form-search">
    <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
    <input type="submit" value="Cari" class="btn btn-primary">
</form>
```

Pagination dengan support pencarian:

```php
<?= $pager->only(['q'])->links(); ?>
```

---

## Hasil Praktikum

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/15e6cb3d-1759-4c6c-a420-7a41bcc26c47" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/de4a90e2-f8db-4731-a6ed-ac147ccfea99" />

---

# Praktikum 6 — Relasi Tabel dan Query Builder

## Tujuan Praktikum

- Memahami konsep relasi antar tabel dalam database
- Mengimplementasikan relasi One-to-Many
- Menggunakan Query Builder pada CodeIgniter 4
- Menampilkan data dari tabel yang saling berelasi

---

## Langkah-Langkah Praktikum

### 1. Membuat Tabel Kategori

```sql
CREATE TABLE kategori (
    id_kategori INT(11) AUTO_INCREMENT,
    nama_kategori VARCHAR(100) NOT NULL,
    slug_kategori VARCHAR(100),
    PRIMARY KEY (id_kategori)
);
```

### 2. Menambahkan Foreign Key pada Tabel Artikel

```sql
ALTER TABLE artikel
ADD COLUMN id_kategori INT(11),
ADD CONSTRAINT fk_kategori_artikel
FOREIGN KEY (id_kategori) REFERENCES kategori(id_kategori);
```

### 3. Membuat Model Kategori

```php
<?php

namespace App\Models;

use CodeIgniter\Model;

class KategoriModel extends Model
{
    protected $table         = 'kategori';
    protected $primaryKey    = 'id_kategori';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['nama_kategori', 'slug_kategori'];
}
```

### 4. Implementasi JOIN pada Controller

```php
$builder = $model->table('artikel')
    ->select('artikel.*, kategori.nama_kategori')
    ->join('kategori', 'kategori.id_kategori = artikel.id_kategori', 'left');

if ($q != '') {
    $builder->like('artikel.judul', $q);
}

if ($kategori_id != '') {
    $builder->where('artikel.id_kategori', $kategori_id);
}
```

---

## Hasil Praktikum

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/35e09a84-af83-406a-ba15-4a50a6556220" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ad40a841-94d0-4bfd-a982-e6f6c8a76abc" />

---

# Praktikum 7 — Upload File Gambar

## Tujuan Praktikum

- Memahami konsep dasar File Upload pada web
- Mengimplementasikan fitur upload gambar menggunakan CodeIgniter 4
- Menerapkan validasi file upload (tipe, ukuran)
- Menampilkan gambar yang telah diunggah pada halaman artikel

---

## Langkah-Langkah Praktikum

### 1. Membuat Folder Penyimpanan Gambar

```bash
mkdir -p public/gambar
```

### 2. Method `add()` — Upload Gambar

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
            'slug'   => url_title($this->request->getPost('judul'), '-', true),
            'gambar' => $namaFile,
        ]);
        return redirect('admin/artikel');
    }

    $title  = "Tambah Artikel";
    $errors = $validation->getErrors();
    return view('artikel/form_add', compact('title', 'errors'));
}
```

### 3. Method `edit()` — Gambar Opsional

Jika user tidak memilih file baru, gambar lama tetap dipertahankan. Jika user mengunggah gambar baru, file lama dihapus otomatis dari server.

### 4. Method `delete()` — Hapus File Fisik

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

## Hasil Praktikum

### Form Tambah Artikel (dengan Input Gambar)
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/f36804d6-b947-4c23-bf2c-ff2f6d4028b5" />

### Form Edit Artikel (dengan Preview Gambar)
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/22135d3a-5c74-4f1b-a840-0aadb4116896" />

### Halaman Admin — Artikel Berhasil Ditambah dengan Gambar
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/910e5fd9-43a3-4cc0-8c74-2be266203eb1" />

---

# Praktikum 8 — AJAX dengan CodeIgniter 4

## Tujuan Praktikum

1. Memahami konsep AJAX dan cara kerjanya
2. Mampu mengimplementasikan AJAX pada aplikasi web dengan CodeIgniter 4
3. Melatih kemampuan problem solving dan debugging

---

## Apa itu AJAX?

AJAX (*Asynchronous JavaScript and XML*) adalah kumpulan teknik pengembangan web yang memungkinkan aplikasi web berkomunikasi dengan server secara asynchronous — tanpa harus melakukan reload halaman secara keseluruhan.

### Cara Kerja AJAX

```
[User Action] → [JS buat HTTP Request] → [Server proses] → [Server kirim JSON] → [JS update DOM]
```

### Keuntungan AJAX

- **UX lebih baik** — halaman tidak reload penuh setiap ada interaksi
- **Hemat bandwidth** — hanya data yang dibutuhkan yang dikirim
- **State terjaga** — kondisi halaman tidak hilang saat data diperbarui

---

## Langkah-Langkah Praktikum

### 1. Membuat AjaxController

Buat file `app/Controllers/AjaxController.php` yang menangani 5 endpoint:

| Method | URL | Fungsi |
|---|---|---|
| GET | `/admin/ajax/data` | Ambil semua artikel (JSON) |
| GET | `/admin/ajax/get/{id}` | Ambil satu artikel by ID |
| POST | `/admin/ajax/store` | Tambah artikel baru |
| POST | `/admin/ajax/update/{id}` | Update artikel |
| GET | `/admin/ajax/delete/{id}` | Hapus artikel |

### 2. Menambahkan Route AJAX

```php
$routes->group('admin', ['filter' => 'authFilter'], function ($routes) {
    // ... route artikel lainnya ...
    $routes->get('ajax', 'AjaxController::index');
    $routes->get('ajax/data', 'AjaxController::getData');
    $routes->get('ajax/get/(:num)', 'AjaxController::getById/$1');
    $routes->post('ajax/store', 'AjaxController::store');
    $routes->post('ajax/update/(:num)', 'AjaxController::update/$1');
    $routes->get('ajax/delete/(:num)', 'AjaxController::destroy/$1');
});
```

### 3. Perbedaan AJAX vs Full Page Reload

| Aspek | Full Page Reload | AJAX |
|---|---|---|
| Reload halaman | Ya, setiap aksi | Tidak perlu |
| Kecepatan | Lebih lambat | Lebih cepat |
| Bandwidth | Kirim seluruh halaman | Kirim data saja (JSON) |
| UX | Terasa patah-patah | Smooth & responsif |

---

## Hasil Praktikum

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6e43fe22-a22f-41c8-b111-678acb1c467b" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/29be0cd1-1ce7-40a7-a0db-fbce3671e63d" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/106c0435-8930-4250-9303-e5b5f37632b6" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b9df41e2-1df3-46b1-a8ba-3004a75bce3b" />

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ab2b25f0-3ce0-42f9-94fc-951792f3c15b" />

---

# Praktikum 9 — Pagination & Filter AJAX Admin

## Tujuan Praktikum

1. Memahami implementasi pagination server-side dengan AJAX
2. Mengimplementasikan filter kategori dan sort data secara dinamis
3. Mengintegrasikan pencarian, filter, dan pagination dalam satu request AJAX

---

## Langkah-Langkah Praktikum

### 1. Modifikasi Controller — `admin_index()`

Method `admin_index()` diperbarui untuk mendukung parameter query: pencarian (`q`), filter kategori (`kategori_id`), urutan (`sort`), dan halaman (`page`). Jika request berjenis AJAX, controller mengembalikan JSON dengan data artikel dan link pagination.

```php
public function admin_index()
{
    $q           = $this->request->getVar('q') ?? '';
    $kategori_id = $this->request->getVar('kategori_id') ?? '';
    $page        = (int) ($this->request->getVar('page') ?? 1);
    $sort        = $this->request->getVar('sort') ?? 'id_desc';

    $model   = new ArtikelModel();
    $builder = $model->table('artikel')
                     ->select('artikel.*, kategori.nama_kategori')
                     ->join('kategori', 'kategori.id_kategori = artikel.id_kategori', 'left');

    if ($q !== '')          $builder->like('artikel.judul', $q);
    if ($kategori_id !== '') $builder->where('artikel.id_kategori', $kategori_id);

    switch ($sort) {
        case 'judul_asc':  $builder->orderBy('artikel.judul', 'ASC');  break;
        case 'judul_desc': $builder->orderBy('artikel.judul', 'DESC'); break;
        case 'id_asc':     $builder->orderBy('artikel.id', 'ASC');     break;
        default:           $builder->orderBy('artikel.id', 'DESC');    break;
    }

    $artikel = $builder->paginate(10, 'default', $page);
    $pager   = $model->pager;

    if ($this->request->isAJAX()) {
        // Serialisasi pager manual agar JSON-serializable
        $pageCount   = $pager->getPageCount('default');
        $currentPage = $pager->getCurrentPage('default');
        $pagerLinks  = [];

        for ($i = 1; $i <= $pageCount; $i++) {
            $pagerLinks[] = [
                'title'  => (string) $i,
                'url'    => base_url("admin/artikel?q={$q}&kategori_id={$kategori_id}&sort={$sort}&page={$i}"),
                'active' => ($i === $currentPage),
            ];
        }

        return $this->response->setJSON([
            'artikel'     => $artikel,
            'pager_links' => $pagerLinks,
        ]);
    }

    return view('artikel/admin_index', [
        'title'       => 'Daftar Artikel',
        'q'           => $q,
        'kategori_id' => $kategori_id,
        'sort'        => $sort,
        'artikel'     => $artikel,
        'pager'       => $pager,
        'kategori'    => (new KategoriModel())->findAll(),
    ]);
}
```

### 2. Implementasi AJAX pada View

View `admin_index.php` menggunakan jQuery AJAX untuk memanggil controller secara asynchronous. Filter, sort, pencarian, dan pagination semuanya dikirim sebagai query string ke endpoint yang sama tanpa reload halaman.

```javascript
function fetchData(url) {
    $.ajax({
        url: url,
        type: 'GET',
        dataType: 'json',
        headers: { 'X-Requested-With': 'XMLHttpRequest' },
        success: function(res) {
            // render baris tabel dari res.artikel
            // render pagination dari res.pager_links
        }
    });
}

// Trigger filter
$('#btnFilter').on('click', function() {
    fetchData(buildUrl('<?= base_url('admin/artikel') ?>'));
});
```

### 3. Keunggulan Pendekatan Ini

| Fitur | Keterangan |
|---|---|
| Pencarian real-time | Input judul difilter tanpa reload halaman |
| Filter kategori | Dropdown kategori memfilter data via AJAX |
| Sort dinamis | Urutan A-Z, Z-A, terbaru, terlama |
| Pagination server-side | Data dibatasi 10 per halaman di sisi server |

---

## Hasil Praktikum

### Halaman Admin — Daftar Artikel dengan Filter AJAX

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6e43fe22-a22f-41c8-b111-678acb1c467b" />

### Filter Kategori Aktif

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/29be0cd1-1ce7-40a7-a0db-fbce3671e63d" />

---

# Praktikum 10 — REST API dengan CodeIgniter 4

## Tujuan Praktikum

1. Memahami konsep dasar REST API
2. Memahami arsitektur RESTful dan HTTP method
3. Membuat REST API menggunakan CodeIgniter 4

---

## Apa itu REST API?

REST (*Representational State Transfer*) adalah arsitektur API yang menggunakan HTTP request untuk operasi data. Data yang dikirim dan diterima umumnya berformat **JSON**, sehingga mudah diintegrasikan lintas platform dan bahasa pemrograman.

| HTTP Method | Fungsi |
|---|---|
| GET | Mengambil data |
| POST | Menambah data baru |
| PUT | Mengubah data |
| DELETE | Menghapus data |

---

## Langkah-Langkah Praktikum

### 1. Membuat REST Controller

Buat file `app/Controllers/Post.php` yang meng-extend `ResourceController`:

```php
<?php

namespace App\Controllers;

use CodeIgniter\RESTful\ResourceController;
use App\Models\ArtikelModel;

class Post extends ResourceController
{
    protected $modelName = 'App\Models\ArtikelModel';
    protected $format    = 'json';

    // GET /post
    public function index()
    {
        return $this->respond([
            'status'  => 200,
            'message' => 'Success Rest API',
            'data'    => $this->model->orderBy('id', 'DESC')->findAll()
        ]);
    }

    // GET /post/{id}
    public function show($id = null)
    {
        $data = $this->model->find($id);
        if ($data) {
            return $this->respond(['status' => 200, 'data' => $data]);
        }
        return $this->failNotFound('Artikel tidak ditemukan.');
    }

    // POST /post
    public function create()
    {
        $data = $this->request->getPost();
        if (!isset($data['judul'])) {
            return $this->fail('Judul wajib diisi.');
        }
        $data['slug'] = url_title($data['judul'], '-', true);
        $this->model->insert($data);
        return $this->respondCreated(['status' => 201, 'message' => 'Artikel berhasil dibuat via API']);
    }

    // PUT /post/{id}
    public function update($id = null)
    {
        $data = $this->request->getRawInput();
        if (!$this->model->find($id)) {
            return $this->failNotFound('Data target tidak valid.');
        }
        $this->model->update($id, $data);
        return $this->respond(['status' => 200, 'message' => 'Artikel berhasil diupdate via API']);
    }

    // DELETE /post/{id}
    public function delete($id = null)
    {
        if ($this->model->find($id)) {
            $this->model->delete($id);
            return $this->respondDeleted(['status' => 200, 'message' => 'Artikel terhapus dari server']);
        }
        return $this->failNotFound('Gagal menghapus, ID tidak ada.');
    }
}
```

---

### 2. Menambahkan Route Resource

Tambahkan satu baris di `app/Config/Routes.php`:

```php
$routes->resource('post', ['controller' => 'Post']);
```

Satu baris ini otomatis menghasilkan semua endpoint REST. Verifikasi dengan:

```bash
php spark routes
```

**Screenshot — Output `php spark routes` di terminal:**

![php spark routes](screenshot-spark-routes)

---

### 3. Testing dengan Postman

Install Postman dari [https://www.postman.com/downloads/](https://www.postman.com/downloads/), lalu jalankan server:

```bash
php spark serve
```

---

#### a. GET semua artikel

- **Method:** `GET`
- **URL:** `http://localhost:8080/post`

**Screenshot — Postman GET /post:**

![GET /post](screenshot-get-all)

---

#### b. GET artikel by ID

- **Method:** `GET`
- **URL:** `http://localhost:8080/post/1`

**Screenshot — Postman GET /post/{id}:**

![GET /post/1](screenshot-get-by-id)

---

#### c. POST tambah artikel

- **Method:** `POST`
- **URL:** `http://localhost:8080/post`
- **Body:** `form-data`
  - Key: `judul` → Value: judul artikel
  - Key: `isi` → Value: isi artikel

**Screenshot — Postman POST /post:**

![POST /post](screenshot-post-create)

---

#### d. PUT update artikel

- **Method:** `PUT`
- **URL:** `http://localhost:8080/post/1`
- **Body:** `x-www-form-urlencoded`
  - Key: `judul` → Value: judul baru
  - Key: `isi` → Value: isi baru

**Screenshot — Postman PUT /post/{id}:**

![PUT /post/1](screenshot-put-update)

---

#### e. DELETE hapus artikel

- **Method:** `DELETE`
- **URL:** `http://localhost:8080/post/1`

**Screenshot — Postman DELETE /post/{id}:**

![DELETE /post/1](screenshot-delete)

---

## Kesimpulan

Pada praktikum ini berhasil dibangun REST API menggunakan CodeIgniter 4 `ResourceController`. Dengan satu baris `$routes->resource('post')`, semua endpoint CRUD otomatis tersedia. API dapat dikonsumsi oleh aplikasi frontend maupun mobile yang terpisah, menjadikan backend CI4 ini bersifat *platform-agnostic*.

---

*&copy; 2026 — Wahyu Andika · NIM 312410182 · Universitas Pelita Bangsa*
