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

1. 

  
