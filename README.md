

## Profil
| #               | Biodata           |
| --------------- | ----------------- |
| **Nama**        | Muhammad Farhan   |
| **NIM**         | 312110128         |
| **Kelas**       | TI.21.A.1         |
| **Mata Kuliah** | Pemrograman Web 2 |



## Labweb10 (***MELANJUTKAN SEBELUMNYA***)

## PRAKTIKUM 12 - FRAMEWORK LANJUTAN (PAGINATION DAN PENCARIAN)

Dipertemuan kali ini kita masih melanjutkan tugas sebelumnya namun kita akan membuat dan juga mempelajari membuat konsep dasar pagination dan pencarian dalam **framework Codeigniter 4**


## LANGKAH - LANGKAH PRAKTIKUM
Pagination merupakan proses yang digunakan untuk membatasi tampilan yang panjang dari data yang banyak pada sebuah website. Fungsi pagination adalah memecah tampilan menjadi beberapa halaman  tergantung banyak nya data yang akan ditampilkan pada setiap halaman.

Pada **Codeigniter 4** fungsi pagination sudah tersedia pada library sehingga cukup mudah menggunakannya.

## 1). MEMBUAT PAGINATION
Untuk membuat pagination,buka Kembali **Controllers Artikel**, kemudian modifikasi kode pada method **admin_index** seperti berikut.

![image](https://github.com/farhanz17/labweb10/assets/92637117/0028ef4d-97c2-4134-91c4-85b3a579fcc5)


**code paginate**
```php
public function admin_index()
    {
         $title = 'Daftar Artikel';
         $model = new ArtikelModel();
         $data = [
           'title' => $title,
           'artikel' => $model->paginate(10), #data dibatasi 10 record perhalaman
           'pager' => $model->pager,
         ];
         return view('artikel/admin_index', $data);
    }
```

* Kemudian buka file **views/artikel/admin_index.php** dan tambahkan kode berikut dibawah deklarasi tabel data.

![image](https://github.com/farhanz17/labweb10/assets/92637117/f413fa2a-baa4-4f68-96dc-ec4a0bc11eb3)

```php
<?= $pager->links(); ?>
```

* Selanjutnya buka kembali menu daftar artikel, tambahkan data lagi untuk melihat hasilnya.

![image](https://github.com/farhanz17/labweb10/assets/92637117/c575458b-0483-46d2-a3c3-c38be05dbeeb)

## 2). MEMBUAT PENCARIAN
Pencarian data digunakan untuk memfilter data.

* Untuk membuat pencarian data, buka kembali **Controllers Artikel,** pada method **admin_index** ubah kode nya seperti berikut

![image](https://github.com/farhanz17/labweb10/assets/92637117/aa4b2ac4-dbdb-40b4-9e0e-5bd695c9bfac)

perubahan isi function
```php
public function admin_index()
    {
	      $title = 'Daftar Artikel';
	      $q = $this->request->getVar('q') ?? '';
	      $model = new ArtikelModel();
	      $data = [
	           'title' => $title,
	           'q' => $q,
	           'artikel' => $model->like('judul', $q)->paginate(2), # data dibatasi 2 record per halaman
	           'pager' => $model->pager,
	         ];
	      return view('artikel/admin_index', $data);
    }
```

* Kemudian buka kembali file **views/artikel/admin_index.php** dan tambahkan form pencarian sebelum deklarasi tabel seperti berikut:

![image](https://github.com/farhanz17/labweb10/assets/92637117/d4522667-dc82-46b6-867f-7f388465a9c7)

```html
<form method="get" class="form-search">
   <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
   <input type="submit" value="Cari" class="btn btn-primary">
</form>
```

* Dan pada link pager ubah seperti berikut.
![image](https://github.com/farhanz17/labweb10/assets/92637117/062f9921-0143-4c81-9fd0-d0f8313b84dc)

```php
<?= $pager->only(['q'])->links(); ?>
```

Selanjutnya ujicoba dengan membuka kembali halaman admin artikel, masukan kata kunci tertentu pada form pencarian.

![image](https://github.com/farhanz17/labweb10/assets/92637117/b137f53a-3508-460c-b2fd-586f9d4c7abb)

## Pertanyaan dan Tugas

Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan
improvisasi.

