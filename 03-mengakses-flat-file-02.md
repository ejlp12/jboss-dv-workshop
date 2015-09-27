# Project Pertama: Mengakses Flat File

## Eksplorasi file Source Model dan View Model

1.  Klik dua kali file `UserSource.xmi`, akan terlihat *Package Diagram* seperti dibawah ini.

   Kita bisa lihat bahwa Source Model tersebut adalah sebuah Teiid internal procedure dengan nama `getTextFiles`dengan input string yaitu nama dari file yang akan dibaca.
   
   Result dari procedure tersebut adalah clob dari file (isi dari file) dan file path. 

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123365/49871e80-6562-11e5-808f-c0b7612bb2df.png)

2. Klik kanan procedure `getTextFiles` di Model Explorer view, lalu pilih Modeling > Preview Data

   Aksi tersebut akan membuat temporary VDB dengan nama file yang akan di-generate secara random, kemudian mendeploy file VDB tersebut ke JDV runtime

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123360/2c3c34fa-6562-11e5-972d-314367df42c1.png)
   
   lalu JBoss Developer Studio (JBDS) akan menampilkan dialog window untuk memasukan parameter dari procedure yand diekseskusi 

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123387/840a55a4-6562-11e5-93de-65aa7a2ea27f.png)
   
   Setelah itu akan ditampilkan 'SQL Result' view yang menampilkan query yang dijalankan JBDS beserta hasilnya. Berikut adalah tampilan query yang dijalankan oleh JBDS sebagai SQL client

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123391/aecb24b2-6562-11e5-94f7-04750f3c1305.png)

   Berikut adalah hasil (return value) dari JDV server runtime:

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123421/219927e6-6563-11e5-9cd9-d9838ae4c17a.png)

3. Pada saat melakukan Preview Data, JBDS akan mem-build project sehingga menghasilkan file VDB sementara (temporer) untuk kemudian di-deploy di JDV server runtime. Hal ini bisa dilihat di console log serperti ini:

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123621/50ad3e50-6568-11e5-9696-751e760bdad6.png)

   `PREVIEW_dbddb3d1-32c2-46c9-a88a-b433fd2fe06d_teiid-file-test_project.vdb` adalah nama file VDB yang di-generate oleh JBDS.

4. Klik kembali file `UserSource.xmi` lalu klik tab *Table Editor* di bagian bawah editor view.

   Kita bisa lihat kolom atau data yang akan dihasilkan dari eksekusi `UserSource.xmi` dan properties lainnya.
   
   > Pada kasus pembacaan file CSV seperti yang kita lakukan ini, pamater yang ditamilkan di Table Editor ini biasanya tidak pernah diubah.

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123428/67bb8bce-6563-11e5-8680-b571028d0aaf.png)

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123432/8c4dec02-6563-11e5-8bcc-365de65b2f90.png)

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123441/ecfc6592-6563-11e5-95dd-df15dd9ae185.png)

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123446/005276b8-6564-11e5-8bff-dd31e7e58006.png)


### View Connection Profile Info

5.  Klik kanan file `UserSource.xmi`  pada Model Explorer view lalu pilih Modeling > View Connection Profile Info

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123516/b7ff424a-6565-11e5-802a-e0e562f94629.png)


### Model Statistic

6. Klik kanan file `UserSource.xmi`  pada Model Explorer view lalu pilih Modeling > Show Model Statistic

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123517/bf943786-6565-11e5-86d2-ccc84560fd4e.png)
   


## Eksplorasi View Model

1.  Klik dua kali `UserView.xmi` pada Model Explorer view, sehingga muncul Diagram Editor seperti dibawah ini:

     ![image](https://cloud.githubusercontent.com/assets/3068071/10123734/9666a820-656b-11e5-8706-7a33b5c4c6cd.png)

2.  Klik dua kali pada kotak `<<Table>> tbluser` untuk mendapatkan tampilan Transformation Diagram seperti dibawah ini

     ![image](https://cloud.githubusercontent.com/assets/3068071/10123764/36d695cc-656c-11e5-9319-9085efe54795.png)

     Dibawah Transformation Diagram ada Transformation Editor yang merupakan editor SQL. Kita dapat mengubah SQL query yang sudah di-generate dan terlihat pada editor tersebut:


   ```sql
   SELECT
		 A.first_name, A.last_name, A.birth_date, A.location
	 FROM
		 (EXEC UserSource.getTextFiles('test-user-data.csv')) AS f, TEXTTABLE(f.file COLUMNS first_name string, last_name string, birth_date string, location string HEADER) AS A
   ```
   

3. Klik Table Editor pada tab dibawah UserView.xmi view, kita bisa lihat properties dari tabel-tabel yang didefinisikan di View Model ini. Dalam hal ini kita hanya memiliki satu tabel yaitu `tbluser`

   Properties seperti Cardinality, Support Update, Materialized, Materialized Table, dan lain-lain dapat diubah disini.

   ![image](https://cloud.githubusercontent.com/assets/3068071/10123826/bdd8c792-656d-11e5-89c1-0f5c1441603a.png)

   Selain itu detail fields/kolom yang ada pada tabel juga bisa diubah pada tab Columns seperti terlihat dibawah ini:
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/10123827/c5ceec42-656d-11e5-85e1-0e61f3b5b48a.png)


