




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

![pager-links](img/pagerlink.png)

```php
<?= $pager->links(); ?>
```

* Selanjutnya buka kembali menu daftar artikel, tambahkan data lagi untuk melihat hasilnya.

![page1](img/page1.png)

Di atas adalah **page 1** sementara dibawah adalah **page 2** dimana saya meminta paginate min adalah 2 sementara data adalah 4

![page2](img/page2.png)

* Sebelumnya tambahkan terlebih dahulu **CSS** di **public/admin.css** untuk mempercantik tampilan **pagination**

## 2). MEMBUAT PENCARIAN
Pencarian data digunakan untuk memfilter data.

* Untuk membuat pencarian data, buka kembali **Controllers Artikel,** pada method **admin_index** ubah kode nya seperti berikut

![search](img/search.png)

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

https://github.com/kyuurazz/Lab10Web/raw/master/img/pagination.png

```html
<form method="get" class="form-search">
   <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
   <input type="submit" value="Cari" class="btn btn-primary">
</form>
```

* Dan pada link pager ubah seperti berikut.
![qlinks](img/qlinks.png)

```php
<?= $pager->only(['q'])->links(); ?>
```

Selanjutnya ujicoba dengan membuka kembali halaman admin artikel, masukan kata kunci tertentu pada form pencarian.

https://github.com/kyuurazz/Lab10Web/blob/master/img/pencarian_data.png?raw=true

## Pertanyaan dan Tugas

Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan
improvisasi.

