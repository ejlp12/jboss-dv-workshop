## Konfigurasi Cache

Cache adalah penyimpanan data sementara. Cache dapat membantu performansi dari proses query yang dilakukan client 
ke JDV agar dapat memperoleh data dengan cepat.

Penggunaan cache harus diperhitungkan dengan baik, sehingga kita menggunakan resource hardware terutama memori dengan
bijak. Cache yang terlalu besar tentu akan boros memori dan bisa jadi cache yang kita buat juga tidak efektif 
penggunaannya.

Pengguna aplikasi pasti menginginkan semua query berjalan cepat, mereka tidak mau menunggu. Hal tersebut tidak 
menjadi masalah jika kita tidak punya keterbatasan resource hardware. Cache disimpan di memori grid yang _sangat 
scalable_, anda dapat membuat ribuan bahkan jutaan server grid untuk memperoleh memori yang sangat besar untuk menyimpan cache.

### Menggunakan Result Set Cache

Fitur yang didukung Result Set Cache adalah sebagai berikut:

 - Hasil query dapat di-cache, termasuk hasil XML document model.
 - Hasil eksekusi virtual procedure dapat di-cache.
 - Results dapat secara otomatis diset untuk lingkup tingkat VDB/user (replicated) atau bisa juga pada tingkat session.
 - Pengguna atau developer dapat mengkonfigurasi jumlah cache entries dan time to live.
 - Cache dapat dihapus (dibersihkan) dengan menggunakan administration tools (AdminShell).

#### Query result set cache

Hasil *query SELECT* atau *eksekusi Virtual Procedure* yang dilakukan user/developer dari client application dapat secara eksplisit ditentukan untuk di-cache dengan cara:

* setting the JDBC ResultSetCacheMode execution property to true
* menggunakan query hint yaitu /*+ cache */ pada SQL, contoh pada source code kita tulis seperti ini

  ```
  ...
  PreparedStatement ps = connection.prepareStatement("/*+ cache */ select * from TBL_CONTOH where col1 = ?");
  ps.setInt(1, 5);
  ps.execute();
  ...
  ```

  kita juga dapat menspesifikasikan parameter memory preference (penggunaan memori untuk cache) dan time to live (waktu hidup cache) dalam satuan milidetik dengan contoh seperti ini:
  
  ```
  /*+ cache(pref_mem ttl:60000) */ select * from TBL_CONTOH
  ```
  
  Untuk melakukan cache suatu virtual procedure, dapat didefinisikan seperti ini:
  
  ```
  /*+ cache */ CREATE VIRTUAL PROCEDURE
  BEGIN
        ...
  END
  ```
  
  >> Ingat: Untuk satu VDB, cache virtual procedure dibatasi hanya 256 cache keys per virtual procedure.
  
  

### Konfigurasi Default

Ada *DUA jenis caches* yang sudah dikonfigurasi secara _default_.

1.  Cache yang menyimpan hasil (results) yang *spesifik untuk suatu session tertentu*. Cache ini *disimpan di masing-masing lokal JDV instance*

2. Cache yang menyimpan hasil (results) dari *query yang lingkupnya adalah VDB tertentu*. Cache ini dapat *direplikasi* ke JDV instance lain.

Secara _default_, result set caching sudah di-enabled dengan *maksimum 1024 entries* dan dengan *umur entry maksimum selama 2 jam*. 

Result set caching disimpan di BufferManager, dan nilai ini bisa ubah/dituning.

### Menghapus Cache

Cache dapat dihapus menggunakan perintah AdminShell seperti berikut:

```
connectAsAdmin()
clearCache("QUERY_SERVICE_RESULT_SET_CACHE")
```

