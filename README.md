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


`inherits` menentukan: **apakah elemen anak otomatis ikut memakai nilai variabel yang diatur di induknya, atau tidak.**

**Contoh**

```html
<div class="induk">
  <div class="anak">Aku anak</div>
</div>
```

```css
.induk {
  --warna: tomato;
}
.anak {
  background-color: var(--warna);
}
```

**Kalau `inherits: true`**

```css
@property --warna {
  syntax: "<color>";
  inherits: true;
  initial-value: lightgray;
}
```

Induk diatur `--warna: tomato`, maka si anak **ikut mendapat** `tomato`. Hasilnya: background anak berwarna **tomato**.

**Kalau `inherits: false`**

```css
@property --warna {
  syntax: "<color>";
  inherits: false;
  initial-value: lightgray;
}
```

Nilai dari induk **tidak turun** ke anak. Anak dianggap belum diatur, jadi memakai `initial-value`. Hasilnya: background anak berwarna **lightgray**.

**Analogi**

Seperti warisan keluarga:
- `inherits: true` = anak otomatis menerima warisan dari orang tuanya.
- `inherits: false` = anak tidak menerima apa-apa, kecuali diatur sendiri. Dia mulai dari nilai awalnya (`initial-value`).

**Kapan pakai yang mana?**

- `true`: kalau kamu mau satu pengaturan di induk berlaku ke semua isi di dalamnya (misalnya tema warna satu halaman).
- `false`: kalau nilainya khusus untuk satu elemen saja, dan tidak boleh bocor ke anak-anaknya (misalnya warna gradien animasi pada satu kotak).

**Catatan:** variabel CSS biasa (tanpa `@property`) itu selalu mewarisi. Jadi `inherits` ini fitur baru yang memberi kamu pilihan untuk mematikannya.

Coba tempel kedua versi ke file HTML, ganti `true` dan `false`, lalu lihat warna kotak anaknya berubah atau tidak. Itu cara paling cepat untuk paham.

Saat di-hover, warna berubah pelan-pelan dari abu-abu ke tomato. Ini yang tidak bisa dilakukan variabel biasa.

**Coba sendiri:** salin HTML dan CSS di atas ke satu file, buka di browser, lalu ubah `--warna-kotak: 2` jadi `blue` dan lihat bedanya.

Setelah itu, coba tulis ulang penjelasanmu tadi, kali ini dengan contoh kodenya.
