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

## Men-setup JBDS dan konfigurasi Server JDV di JBDS

1.  Jalankan JBoss Developer Studio (JBDS), pilih/buat new workspace.

    ![image](https://cloud.githubusercontent.com/assets/3068071/7554853/d1c382b6-f762-11e4-83e2-33abbe79e4cf.png)

2.  Klik icon "Open Perspective" di kanan atas, atau dari menu Window > Open Perspective > Others...
    Lalu pilih "Teiid Designer" dan klik OK
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7554898/5d91d306-f763-11e4-8661-ebb98c26f811.png)
    
3.  Tampilan JBDS dengan perspective Teiid akan terlihat seperti ini
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7554906/955c31be-f763-11e4-9810-b759798e100a.png)
    
4.  Sebelum kita memulai membuat sebuah project kita akan setting dulu JBDS agar siap kita gunakan untuk itu ada beberapa langkah yang perlu kita lakukan, langkah-langkah tersebut dapat kita lakukan dengan mudah dengan mengikuti guide (petunjuk) yang ada di View "Guides" yang ada disebelah kanan atas seperti gambar berikut:

    ![image](https://cloud.githubusercontent.com/assets/3068071/7554953/14d0d778-f765-11e4-9c6e-413f206a0086.png)
 
    Pilih Action Set dropdown list pada nilai "Teiid"

5.  Klik action "Configure New JBoss Server >>"
    Akan muncul window _New Server_, pilih __JBoss Enterprise Application Platform 6.1+__
    Biarkan nilai _Server's host name_ = localhost dan _Server name_ bisa anda ganti menjadi "JDV 6.1" seperti gambar berikut, lalu klik Next
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7554985/8785593c-f766-11e4-88b4-c6a442739478.png)
    
6.  Pilih "Create New Runtime" pada tampilan berikutnya seperti gambar ini, lalu klik Next
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7554990/d0e7edce-f766-11e4-9b89-e9d561dc9895.png)
    
7.  Ubah JBoss Runtime dengan memilih Home Directory, dengan mengklik tombol "Browse", pilih directory dimana JDV diinstall.
    Dan pilih _Runtime JRE_  dengan JRE versi 1.8
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555001/854ea3f2-f767-11e4-81fe-6067af332146.png)
    
    Klik Next, skip window berikutnya, kemudian klik Finish
    
    Hasilnya kita akan mendapatkan server dengan nama "JDV 6.1.0" sebagai Default Server dari Teiid.
    Anda akan lihat tampilan seperti ini:
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555013/71d45a28-f768-11e4-81e0-2ef7de5f8746.png)
    
8.  Kembali ke View "Guides" di kanan atas, klik action ke-2 yaitu "Edit JBoss/Teiid Instance Properties >>"
    Akan muncul editor untuk mengubah konfigurasi server JBoss EAP atau Teiid server seperti berikut:
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555035/63246b34-f769-11e4-903d-a4a5bcedad22.png)
    
    Ubah _User Name_ dan _Password_ pada blok "Management Login Credential" sesuai dengan username dan password admin dari JBoss EAP pada saat instalasi JDV.
    
9.  Klik tab **Teiid Instance** pada editor konfigurasi server JBoss EAP, kemudian ubah _User name_ menjadi **teiidUser** dan _Password_ sesuai yang diset pada saat instalasi pada blok "JDBC Connection"
    
    Save dengan cara menekan tombol CTRL+S atau dari menu File > Save. Jangan close editor tersebut, karena setelah menjalankan server, kita akan melakukan test koneksi JDBC ke JDV dari editor tersebut.
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555061/e925db96-f769-11e4-93c2-2e3298e78ff1.png)
    
10. Start Server "JDV 6.1.0" dengan cara mengklik kanan server tersebut pada Servers View kemudian klik menu Start
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555070/62563eac-f76a-11e4-815d-7a3e120c8972.png)
    
    Tunggu sampai server selesai start dengan melihat Console View
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7555113/e6f91200-f76b-11e4-82e6-40a9b0acb184.png)
    
11. Kembali ke editor konfigurasi Server "JDV 6.1.0", lalu klik "Test Administration Connection" dan "Test JDBC Connection"

  ![image](https://cloud.githubusercontent.com/assets/3068071/7555269/c7823c90-f76f-11e4-93cd-d99f6df5f482.png)
  
  Anda harus mendapatkan status OK untuk keduanya.

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
    Beri nama koneksi yang akan kita buat misalnya `User CSVFile (Local)", klik Next

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
7.  Kita akan kembali ke langkah "Data File Source Selection", tapi saat ini file-file yang ada di direktori `/home/jboss/data` akan ditampilkan, pilih file `test-user-data.csv` dengan mengkliknya pada daftar _Data File Name_, lalu klik Next

	![image](https://cloud.githubusercontent.com/assets/3068071/7555527/b3f4f114-f778-11e4-85cc-7a6394d5c374.png)

8.


