Project Pertama: Mengakses Flat File
------------------------------------

Di LAB ini kita akan membuat project yang mengakses flat file dalam format CSV (comma separated value), kemudian kita akan mengakses data pada flat file tersebut melalui JDV menggunakan koneksi JDBC.

Kita akan menggunakan [SQuirreL](http://squirrel-sql.sourceforge.net/) sebagai SQL client tool.

1.  Pertama install SQuirreL dengan mendownload file installer (JAR) dari link berikut: http://squirrel-sql.sourceforge.net/#installation
    Lalu install dengan cara mengklik dua kali atau menggunakan perintah `java -jar squirrel-sql-3.6-standard.jar`

2.  Buat file text berikut dengan nama `test-user-data.csv` dengan isi sebagai berikut:

    ```
    first_name, last_name, birth_date, location
    dudi,mustakim,08-09-1981,jakarta
    arman,mualana,30-12-1987,medan
    ketut,bagas,04-05-1986,denpasar
    sosro,diningrat,02-02-1979,tegal
    ```
  
    Simpan file tersebut di direktori misalnya `/home/jboss/data/`
    
    Kita akan gunakan file tersebut sebagai source data yang akan diakses oleh JDV.


## Memulai membuat Model Project

1.  Masih pada perspective Teiid, klik kanan pada "Model Explorer" View lalu pilih **New > Teiid Model Project** pada popup menu.
    
    Membuat "Teiid Model Project" juga bisa diakses dari menu File > New > ...
    
	![image](https://cloud.githubusercontent.com/assets/3068071/7555335/ba508fe2-f772-11e4-8a49-24e5c16aff7c.png)

	Dapat juga diakses dari "Guides" View seperti berikut:
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555348/4b630122-f773-11e4-90ba-81fbc3b5d915.png)
	
2.  Pada window "New Model Project" berinama project name `teiid-file-test`

	![image](https://cloud.githubusercontent.com/assets/3068071/7554746/93b7f6a4-f75e-11e4-9740-a3eaba4d875b.png)

  	Kemudian klik Next.
  	
  	Pada step Project References, skip.. karena project ini tidak memerlukan project lain.
  	
  	![image](https://cloud.githubusercontent.com/assets/3068071/7555358/b336f68c-f773-11e4-8da2-1a7f6703d948.png)
  	
3.  Pada langkah ini kita bisa membuat beberapa folder (directory) untuk mengorganisasi file-file yang akan kita buat nantinya. Pembagian folder tersebut hanya sebuah *best practice* yang memudahkan kita jika nanti dalam satu project akan banyak file.

	![image](https://cloud.githubusercontent.com/assets/3068071/7555398/591e0fea-f774-11e4-8790-99dbc2dc09fe.png)

	Klik Finish
	
	Hasilnya kita dapat lihat `teiid-file-test` Model Project di Model Explorer View
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555405/84f10c94-f774-11e4-992f-7cef2b2e1a4b.png)
	
### Membuat Source Model dari CVS File

1.  Klik kanan pada Model Explorer View, dan pilih **Import** pada popup menu

	![image](https://cloud.githubusercontent.com/assets/3068071/7555421/276a9684-f775-11e4-9bb7-2e990a65df2a.png) 

2.  Pada window Import, pilih folder Teiid, ekspansikan.. lalu pilih **File Source (Flat) >> Source and View Model**, klik Next

	![image](https://cloud.githubusercontent.com/assets/3068071/7555412/dba8b9b0-f774-11e4-896d-caab85975855.png)
	
3. 	Karena kita akan menggunakan file di lokal komputer, pilih "Flat file on local file sytem", klik Next
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555436/a555dc8e-f775-11e4-821b-cd342f94a746.png)

4.  Pada step "Data File Source Selection" di blok "Data File Source", klik tombol **New...** untuk membuat data source baru.
    Beri nama koneksi yang akan kita buat misalnya `User CSVFile (Local)".
   
    Klik Next

	![image](https://cloud.githubusercontent.com/assets/3068071/7555459/7ebdd274-f776-11e4-9281-f552391fe6f0.png)

5.  Pilih _home folder_ sesuai dengan letak file `test-user-data.csv`, misalnya di direktori `/home/jboss/data`. Contoh screenshot saya ini saya menyimpan file csv tersebut di direktori `/Users/ejlp12`.  
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555481/0691de84-f777-11e4-8371-16a560f45a73.png)

	Pilih "CSV" sebagai _flat file type_ 
	
	File type yang lain yang bisa dipilih adalah SSV (semicolon-separated value), PSV (pipe-separated value), TSV (tab-separated value).
	
	Anda juga perlu menspesifikasikan konfigurasi berikut:
		- apakah baris pertama di file adalah nama kolom?
		- apakah barus kedua merupakan tipe data?
		- apakah jika ada data kolom dalam baris yang kosong akan dianggap kolom dengan data null (trainiling null coloumns)?

6.  Test koneksi, klik tombol "Test Connection", klik tombol Finish

7.  Kita akan kembali ke langkah "Data File Source Selection", tapi saat ini file-file yang ada di direktori `/home/jboss/data` akan ditampilkan, pilih file `test-user-data.csv` dengan mengkliknya pada daftar _Data File Name_.
	
	Kita akan simpan Source Model file ini di `teiid-file-test/sources` dan kita berinama `UserSource` jadi,
  ubahlah **Location** menjadi `teiid-file-test/sources` dan **Name** dari "Source Model Definition" seperti terlihat pada gambar.
  

	Lalu klik Next
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555641/e6ade6b2-f77b-11e4-9da9-a1b19bfd9a38.png)

8.  Langkah berikutnya hanya mengkonfirmasi isi file, klik Next
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7555542/6e96a9b8-f779-11e4-9238-ee4d1c5ac381.png)

9.  Ganti tipe data `birth_date` menjadi `date`, lalu klik Next

	![image](https://cloud.githubusercontent.com/assets/3068071/7555586/22d40f42-f77a-11e4-8b0a-b4d5d66ab973.png)

	> Anda juga bisa lihat opsi setting lain terkait funsgi pembacaan text file dengan mengklik _"TEXTTABLE function options"_:
	>
	> ![image](https://cloud.githubusercontent.com/assets/3068071/7555581/d3cf8944-f779-11e4-8900-a337ef9144e7.png) 

10. Spesifikasikan nama dari View Model yang kita buat beserta direktori tempat file akan disinpan yaitu di direktori `views`, kemudian klik Finish

	![image](https://cloud.githubusercontent.com/assets/3068071/7556687/ebb9a184-f7a6-11e4-8c40-5f329b9b2243.png)
	
11. Sebuah Source Model dan View Model secara otomatis dibuat
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556688/f650e99a-f7a6-11e4-8a09-6c2a6f81f180.png)


12. Klik menu-bar "File > Save All"

**Selesai**

## Membuat Virtual Database (VDB)

Setelah kita selesai membuat Source Model dan View Model, sekarang saatnya kita coba test untuk meng-query data ke `UserView.tbluser`, tapi sebelumnya kedua project yang sudah kita buat tersebut perlu di build menjadi file **VDB** kemudian
di-deploy ke JDV server.

1.  Pastikan `JDV 6.1.0` started dengan melihat ke Server View seperti berikut
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556761/0d9e05b8-f7a9-11e4-86cf-29f54fa8cb6f.png)

2.  Klik kanan di Model Explorer lalu pilih di popup menu New > Teiid VDB

	![image](https://cloud.githubusercontent.com/assets/3068071/7556733/247ad5fa-f7a8-11e4-8075-133c07050087.png)

3.  Beri nama VDB, kemudian klik tombol Add untuk memilih Models yang akan kita paketkan dalam file VDB
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556777/9eaacb18-f7a9-11e4-99a9-fb98adcd500c.png)

	Pilih kedua Model file yaitu `UserSource.xmi` dan `UserView.xmi`
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556775/892ddf5a-f7a9-11e4-8ec9-056d771ba288.png)

	Lalu klik Finish
	
4.  Kita dapat lihat di project `teiid-file-test` sudah terbangun (generated) sebuah file dengan mana `companyname-user.vdb`

	![image](https://cloud.githubusercontent.com/assets/3068071/7556792/1b1397e8-f7aa-11e4-9e06-d1f796a73f88.png)
	
	> VDB pada dasarnya adalah file JAR (ZIP) yang berisi file `xmi` beserta metadata `vdb.xml`. Setiap kali kita menambah
	> file `xmi` atau merubah file yang ada dan ingin kita deploy maka kita perlu men-generate ulang (synchronize) file `VDB`

5.  Sebuah editor file VDB dapat kita lihat juga sebagai berikut, jika editor seperti ini tidak muncul coba klik dua kali file `companyname-user.vdb`

	![image](https://cloud.githubusercontent.com/assets/3068071/7556839/b4763354-f7ab-11e4-96fc-e17acdc20b39.png)
	
	* (1) Adalah tombol untuk melakukan synchronization jika ada file Model (`xmi`) yang ada dalam list (2) berubah
	* (2) adalah list file model yang masuk dalam bundle file `VDB`, jika kita ingin menambahkan file Model baru bisa klik ikon dibawahnya (3)
	* (3) Adalah tombol untuk menambah atau menghapus file Model
	* (4) Dibagian paling bawah juga ada tab "Advanced" untuk men-setting beberapa konfigurasi dari VDB seperti user/role, beberapa properties, custom variables atau properties dan translator setting untuk meng-override (menimpa) _default translator setting_.

6.  Depoy file VDB dengan mengklik kanan `companyname-user.vdb` kemudian memilih menu Modeling > Deploy

	![image](https://cloud.githubusercontent.com/assets/3068071/7556850/5b5a12b2-f7ac-11e4-91bf-3ed3366c3308.png)


7.  Kita akan diminta konfirmasi apakah kita akan membuat `Data Sources` atau tidak.
    Klik tombol `Create Source` sehingga sebuah datasource dengan JNDI name `java:/companyname-user` akan dibuat di server JBoss EAP. Datasource ini akan memudahkan kita dalam melakukan query jika aplikasi client kita dideploy di server yang sama dengan JDV.

	![image](https://cloud.githubusercontent.com/assets/3068071/7556854/a5e14aee-f7ac-11e4-9246-2573f4128452.png)
	
8.  Jika proses deploy berhasil, kita akan dapatkan tampilan pada Server View seperti berikut:
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556880/40feb448-f7ae-11e4-82fe-95266b081262.png)

## Test query data ke VDB


1.  Klik kanan di `companyname-user.vdb` di Model Explorer, lalu pilih menu Modeling > Execute VDB
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556893/98ce92ec-f7ae-11e4-93e0-639dd38b26c5.png)

2.  JBDS akan otomatis pindah ke perspective "Database Development", dan akan muncul editor "SQL Scrapbook" seperti dibawah ini. Ubah text query  di editor tersebut menjadi

	```sql
	SELECT * FROM UserView.tbluser
	```
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556930/9f79cd9a-f7af-11e4-8baf-68684f155a5a.png)
	
3.  Blok SQL text tersebut lalu klik kanan dan pilih "Execute selected text".
	Jika sukses, hasilnya akan kita lihat di "SQL Result" View seperti ini:

	![image](https://cloud.githubusercontent.com/assets/3068071/7557316/4c84b906-f7b9-11e4-8084-3bdf8b7041da.png)


	Jika anda mencoba mengkonversi date pada saat membuat Model, maka akan muncul error seperti ini, karena kolom birth_date tidak bisa dikonversi ke tipe data `DATE`
	
	```
	org.teiid.runtime.client.TeiidClientException: java.lang.RuntimeException: Remote org.teiid.core.TeiidProcessingException:
	TEIID30176 Could not convert value for column birth_date in the row ending on text line 2 in file:/Users/ejlp12/test-user-data.csv.
	```
	
	![image](https://cloud.githubusercontent.com/assets/3068071/7556944/66379660-f7b0-11e4-91af-6da950ad2e54.png)

## Eksplorasi file Source Model dan View Model


