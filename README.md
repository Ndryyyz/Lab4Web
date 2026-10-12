# Lab4Web - Praktikum 4: CSS Layout

**Nama:** Muhamad Prasetyo Andri Wibowo
**NIM:** 312510181
**Kelas:** I251B
**Program Studi:** Teknik Informatika, Universitas Pelita Bangsa
**Mata Kuliah:** Pemrograman Web

---

## Tujuan Praktikum

1. Memahami struktur dasar pembuatan layout.
2. Memahami konsep box element.
3. Memahami CSS Floating.
4. Memahami HTML 5 Semantic Element.
5. Membuat layout web sederhana.

## Struktur Folder

```
Lab4Web/
├── lab4_box/
│   └── lab4_box.html        <- latihan box element, float, clear
├── lab4_layout/
│   ├── home.html            <- layout sederhana (halaman utama)
│   ├── artikel.html         <- halaman artikel (agar menu tidak error)
│   ├── about.html           <- Tugas 1: halaman About
│   ├── kontak.html          <- Tugas 2: halaman Kontak (form)
│   └── style.css            <- semua CSS layout
├── screenshots/             <- screenshot hasil tiap langkah
└── README.md
```

---

# Bagian 1 - Box Element dan CSS Float (`lab4_box.html`)

## Konsep dasar (versi mudah)

**Box Element.** Bayangkan setiap elemen HTML itu sebuah *kardus*. Kardus ini punya empat lapisan, dari dalam ke luar:

| Lapisan | Analogi | Fungsi |
|---|---|---|
| **Content** | Barang di dalam kardus | Isi elemen (teks, gambar) |
| **Padding** | Bubble wrap / busa pelindung | Jarak antara isi dan garis tepi |
| **Border** | Dinding kardus | Garis tepi elemen |
| **Margin** | Jarak antar kardus di rak | Jarak elemen dengan elemen lain |

**Float.** Secara normal, `div` ditata *ke bawah* (satu div satu baris). Dengan `float: left`, div "mengambang" ke kiri sehingga div berikutnya bisa berdiri **di sampingnya**. Inilah cara dasar membuat layout kolom-kolom.

**Clear.** Kalau ada elemen yang tidak ingin ikut berdampingan dengan elemen yang mengambang, kita pakai `clear`. Artinya: *"jangan menempel di samping elemen float, turun dulu ke baris baru"*.

## Langkah 1 - Kerangka HTML

Buat folder `Lab4Web`, lalu buat file `lab4_box.html` berisi kerangka dasar HTML5 dengan `<header>` dan `<h1>Box Element</h1>`.

Penjelasan: `<header>` adalah *semantic element*, yaitu tag yang namanya langsung menjelaskan fungsinya (bagian kepala halaman).

## Langkah 2 - Membuat Box Element dengan div

Tambahkan tiga `div` di dalam `<section>`:

```html
<section>
    <div class="div1">Div 1</div>
    <div class="div2">Div 2</div>
    <div class="div3">Div 3</div>
</section>
```

Tanpa float, ketiga div tersusun **ke bawah** (memanjang penuh satu baris masing-masing).

## Langkah 3 - CSS Float Property

Tambahkan CSS di dalam `<head>`:

```css
div {
    float: left;
    padding: 10px;
}
.div1 { background: red; }
.div2 { background: yellow; }
.div3 { background: green; }
```

Penjelasan:
- `float: left` membuat setiap div mengambang ke kiri, jadi ketiganya berjajar **menyamping**.
- `padding: 10px` memberi ruang 10px di sekeliling teks agar kotaknya tidak terlalu rapat.
- `background` memberi warna latar supaya kotaknya terlihat.

Hasil: **Div 1 (merah), Div 2 (kuning), Div 3 (hijau) berjajar menyamping.**

## Langkah 4 - Mengatur Clearfix

Tambahkan `div4` setelah `div3`:

```html
<div class="div4">Div 4</div>
```

```css
.div4 {
    background-color: blue;
    clear: left;
    float: none;
}
```

Penjelasan:
- `clear: left` berarti div4 tidak boleh berada di samping elemen yang float ke kiri, jadi **turun ke baris baru**.
- `float: none` mematikan float untuk div4 (karena aturan `div { float:left }` tadi berlaku untuk semua div, termasuk div4).

Hasil: Div 4 (biru) tampil **memanjang di bawah** ketiga div sebelumnya.

## Eksperimen nilai `clear`

| Nilai | Artinya | Hasil pada div4 |
|---|---|---|
| `left` | Tidak boleh ada float kiri di sampingnya | Turun ke bawah (karena div1-3 float kiri) |
| `right` | Tidak boleh ada float kanan di sampingnya | Tidak turun, karena tidak ada float kanan. Div 4 naik ke posisi paling atas, berada di belakang Div 1-3, dan teksnya "Div 4" terdorong ke kanan |
| `both` | Tidak boleh ada float di kedua sisi | Turun ke bawah (sama seperti `left`) |
| `none` | Tidak ada aturan clear | Sama seperti `right`: tidak turun, tertimpa Div 1-3 |

<img width="700" height="800" alt="01-box-element" src="https://github.com/user-attachments/assets/3f72aa70-94a3-4888-a377-791d872e931e" />

![Box element float dan clear](screenshots/01-box-element.png)

---

# Bagian 2 - Layout Web Sederhana (`lab4_layout/`)

## Gambaran umum

Layout web dibagi menjadi beberapa bagian besar, mirip denah rumah:

```
+-----------------------------------+
|              header               |
+-----------------------------------+
|               nav                 |
+-----------------------------------+
|          section#hero             |
+-------------------------+---------+
|  section#main           | aside   |
|  (konten utama)         |#sidebar |
+-------------------------+---------+
|              footer               |
+-----------------------------------+
```

Semua bagian dibungkus oleh `<div id="container">` supaya lebarnya bisa dibatasi dan diletakkan di tengah layar.

## Langkah 1 - Buat folder dan file

Buat folder `lab4_layout`, lalu di dalamnya buat `home.html` dan `style.css`. File HTML dihubungkan ke CSS dengan:

```html
<link rel="stylesheet" href="style.css">
```

## Langkah 2 - Kerangka layout dengan semantic element

Di dalam `div#container` ditulis:

```html
<header>...</header>
<nav>...</nav>
<section id="hero"></section>
<section id="wrapper">
    <section id="main"></section>
    <aside id="sidebar"></aside>
</section>
<footer>...</footer>
```

Fungsi tiap tag:

| Tag | Fungsi |
|---|---|
| `<header>` | Kepala halaman (judul situs) |
| `<nav>` | Kumpulan link navigasi/menu |
| `<section>` | Bagian tertentu dalam dokumen |
| `<aside>` | Konten pendamping (sidebar) |
| `<article>` | Satu konten artikel yang berdiri sendiri |
| `<footer>` | Kaki halaman (copyright) |

Pada tahap ini tampilan masih polos tanpa CSS, hanya teks dan link biasa.

## Langkah 3 - CSS dasar, container, dan header

```css
* { margin: 0; padding: 0; }
body { font-family: 'Open Sans', sans-serif; color: #5a5a5a; }
#container { width: 980px; margin: 0 auto; box-shadow: 0 0 1em #cccccc; }
header { padding: 20px; }
header h1 { margin: 20px 10px; color: #b5b5b5; }
```

Penjelasan:
- `* { margin:0; padding:0 }` adalah **reset CSS**: menghapus jarak bawaan browser supaya semua browser tampil sama.
- `margin: 0 auto` membuat container berada **di tengah** halaman secara horizontal.
- `box-shadow` memberi bayangan tipis di sekeliling halaman.
- `@import` di baris paling atas dipakai untuk memuat font Open Sans dari Google Fonts (butuh internet).

## Langkah 4 - Navigasi

```css
nav { display: block; background-color: #1f5faa; }
nav a { padding: 15px 30px; display: inline-block; color: #ffffff;
        font-size: 14px; text-decoration: none; font-weight: bold; }
nav a.active, nav a:hover { background-color: #2b83ea; }
```

Penjelasan:
- `display: inline-block` membuat link berjajar menyamping **tetapi tetap bisa diberi padding** atas-bawah.
- `text-decoration: none` menghilangkan garis bawah link.
- `a.active` dan `a:hover` memberi warna lebih terang untuk menu aktif dan saat kursor diarahkan ke menu.

## Langkah 5 - Hero Panel

Hero panel adalah **banner besar** di bawah menu berisi judul, deskripsi, dan tombol ajakan (CTA).

```html
<section id="hero">
    <h1>Hello World!</h1>
    <p>Lorem ipsum ...</p>
    <a href="home.html" class="btn btn-large">Learn more &raquo;</a>
</section>
```

CSS `#hero` memberi warna latar abu-abu (`#e4e4e5`), `padding: 50px 20px` agar lega, dan `margin-bottom: 20px` sebagai jarak ke bawahnya.

> Catatan: modul tidak memberikan CSS untuk class `.btn`, `.btn-large`, dan `.btn-default`. Agar tombolnya tampil seperti pada gambar modul (biru dan abu-abu), saya menambahkan CSS tombol sendiri di `style.css`.

## Langkah 6 - Main Content dan Sidebar (CSS Float)

```css
#main    { float: left; width: 640px; padding: 20px; }
#sidebar { float: left; width: 260px; padding: 20px; }
```

Penjelasan: ini penerapan langsung **float** dari Bagian 1. Main dan sidebar sama-sama `float: left` sehingga **berdampingan**.

Hitungan lebar (supaya pas di container 980px):
- Main: 640 + padding kiri-kanan 40 = **680px**
- Sidebar: 260 + padding kiri-kanan 40 = **300px**
- Total: 680 + 300 = **980px** (pas)

## Langkah 7 - Sidebar Widget

Sidebar berisi dua kotak widget (`div.widget-box`): satu daftar link, satu teks. CSS-nya memberi border tipis, judul berlatar biru (`.title`), dan efek abu-abu saat link di-hover.

## Langkah 8 - Footer

```css
footer { clear: both; background-color: #1d1d1d; padding: 20px; color: #eee; }
```

Penjelasan: karena `main` dan `sidebar` sedang float, footer **harus** memakai `clear: both`. Kalau tidak, footer akan ikut naik dan menempel di sampingnya atau tertimpa. Ini penerapan `clear` dari Bagian 1.

## Langkah 9 - Elemen lain pada Main Content (tiga kolom)

Tiga kotak (`div.box`) dengan gambar bulat, judul, teks, dan tombol "View detail", dibungkus `div.row`.

```css
.box { float: left; width: 33.333333%; box-sizing: border-box; padding: 0 10px; text-align: center; }
.image-circle { border-radius: 50%; }
.row:after { content: ''; display: table; clear: both; }
```

Penjelasan:
- `width: 33.33%` membuat tiga kotak membagi lebar menjadi tiga sama rata.
- `box-sizing: border-box` membuat padding **dihitung di dalam lebar**, jadi tiga kotak pasti muat sebaris.
- `border-radius: 50%` mengubah gambar persegi menjadi **lingkaran**.
- `.row:after { clear: both }` adalah teknik **clearfix**. Karena isi `.row` semuanya float, tinggi `.row` bisa "runtuh" jadi nol. Elemen bayangan (`:after`) dengan `clear: both` memaksa `.row` menghitung tinggi isinya dengan benar.

## Langkah 10 - Content Artikel

Dua `<article class="entry">`: artikel pertama gambar di **kiri**, artikel kedua gambar di **kanan**.

```css
.entry img { float: left; border-radius: 5px; margin-right: 15px; }
.entry .right-img { float: right; }
```

Gambar float, sehingga teks mengalir di sampingnya. Kelas `right-img` menggeser gambar ke sisi kanan.

> Catatan perbaikan dari modul: di modul, HTML memakai `class="rightimg"` sedangkan CSS memakai `.right-img`, jadi tidak cocok. Saya samakan menjadi `right-img`. Di modul juga ada selector `box img` yang kurang titik, saya perbaiki menjadi `.box img`.

<img width="1100" height="1395" alt="02-home" src="https://github.com/user-attachments/assets/d073bda0-3d51-4567-b099-b182dc05e1bb" />

![Halaman Home](screenshots/02-home.png)

---

# Bagian 3 - Tugas

## Tugas 1 - Layout menu About (`about.html`)

Halaman About memakai kerangka layout yang sama (header, nav, wrapper, sidebar, footer) dan berisi:
- **Deskripsi diri**: foto bulat, nama, NIM, program studi, kelas, dan paragraf perkenalan.
- **Portfolio**: tiga kartu proyek (gambar, judul, deskripsi singkat) yang berjajar tiga kolom memakai float.
- **Sidebar**: widget keahlian dan info praktikum.

<img width="1100" height="901" alt="03-about" src="https://github.com/user-attachments/assets/f0255d30-b552-4874-9743-d711a40819e6" />

![Halaman About](screenshots/03-about.png)

## Tugas 2 - Layout menu Contact (`kontak.html`)

Halaman Kontak berisi form dengan isian:
- **Nama** (`input type="text"`)
- **Email** (`input type="email"`, otomatis dicek formatnya oleh browser)
- **Subjek** (`input type="text"`)
- **Message** (`textarea`)
- Tombol **Kirim Pesan**

Setiap isian dipasangkan dengan `<label for="...">` supaya jika label diklik, kursor otomatis masuk ke kolom yang sesuai. Atribut `required` membuat kolom wajib diisi.

<img width="1100" height="800" alt="04-kontak" src="https://github.com/user-attachments/assets/312eb16b-ae62-414a-ad7e-92f19c42a07a" />

![Halaman Kontak](screenshots/04-kontak.png)

---

## Validasi

Semua file HTML dapat dicek di <http://validator.w3.org> (Validate by File Upload).

## Cara Menjalankan

Buka `lab4_layout/home.html` langsung di browser (klik dua kali). Koneksi internet diperlukan agar font Google dan gambar placeholder dari dummyimage.com tampil.

## Kesimpulan

- **Box element** (content, padding, border, margin) adalah dasar semua tata letak.
- **Float** menyusun elemen berdampingan, sedangkan **clear** dan **clearfix** mencegah elemen setelahnya berantakan.
- **Semantic element** (`header`, `nav`, `section`, `aside`, `article`, `footer`) membuat struktur halaman lebih jelas, baik bagi pembaca kode maupun mesin.
- Dengan kombinasi semuanya, layout web sederhana dengan header, menu, hero, konten, sidebar, dan footer dapat dibuat.
