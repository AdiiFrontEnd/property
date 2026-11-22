# @property
Adalah Sebuah At Rule Untuk Mendaftar Sebuah Variabel Css Dengan Menentukan tipe datanya Dsb.

Cara pakainya ada **2 langkah**: daftarkan variabelnya, lalu pakai seperti variabel CSS biasa.

**Langkah 1: Daftarkan dengan `@property`**

Tulis di bagian atas CSS (di luar selector apa pun):

```css
@property --warna-kotak {
  syntax: "<color>";
  inherits: false;
  initial-value: lightgray;
}
```

Aturannya:
- Nama variabel **wajib diawali `--`**.
- Tiga deskriptor ini perlu ditulis semua: `syntax`, `inherits`, `initial-value`.
- Nilai `syntax` ditulis dalam tanda kutip dan kurung sudut, misalnya `"<color>"`.

**Langkah 2: Pakai dengan `var()`**

```css
.kotak {
  width: 200px;
  height: 100px;
  background-color: var(--warna-kotak);
}

.merah {
  --warna-kotak: tomato;
}

.salah {
  --warna-kotak: 2; /* salah tipe, otomatis jadi lightgray */
}
```

HTML-nya:

```html
<div class="kotak"></div>
<div class="kotak merah"></div>
<div class="kotak salah"></div>
```

**Hasilnya**
- Kotak 1: tidak diatur, jadi pakai `initial-value` (abu-abu).
- Kotak 2: `tomato` diterima karena itu warna.
- Kotak 3: `2` bukan warna, jadi ditolak dan kembali ke abu-abu.

**Tipe `syntax` yang sering dipakai**

| syntax | untuk |
|---|---|
| `"<color>"` | warna |
| `"<number>"` | angka (`2`, `0.5`) |
| `"<length>"` | ukuran (`10px`, `2rem`) |
| `"<percentage>"` | persen (`50%`) |
| `"<angle>"` | sudut (`45deg`) |

**Contoh bonus: animasi halus**

```css
.kotak {
  transition: --warna-kotak 0.5s;
}
.kotak:hover {
  --warna-kotak: tomato;
}
```

Saat di-hover, warna berubah pelan-pelan dari abu-abu ke tomato. Ini yang tidak bisa dilakukan variabel biasa.

**Coba sendiri:** salin HTML dan CSS di atas ke satu file, buka di browser, lalu ubah `--warna-kotak: 2` jadi `blue` dan lihat bedanya.

Setelah itu, coba tulis ulang penjelasanmu tadi, kali ini dengan contoh kodenya.
