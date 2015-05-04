## Instal JBoss Developer Studio 8.1.0 (JBDS)

JBDS adalah developer tool berbasis Eclipse yang dibuat oleh Red Hat atau JBoss Community untuk mempermudah dalam membangun aplikasi Web berbasis Java, aplikasi Java EE atau aplikasi mobile dengan memberikan plugin-plugin tambahan yang dibutuhkan.

> Pertama pastikan dulu OS anda didukung dengan melihat halaman [Red Hat JBoss Developer Studio Components and Supported Configurations](https://access.redhat.com/articles/427493), terutama bagian OS & JDK. 

> Sebaiknya anda menggunakan:
>  * procesor arsitektur x86, x86_64 (Intel), 
>  * OS: Windows 7 atau 8, Linux Fedora 19, 20 atau 21, RHEL 6 atau 7, Ubuntu 12.04.2 LTS atau 14.04 LTS, OS X Mountain Lion (10.8), OS X Mavericks (10.9) and OS X Yosemite (10.10)
>  * JDK 1.8

Berikut langkah instalasi JBDS:

1.  Buka halaman web berikut **[Red Hat JBoss Developer Studio](http://www.jboss.org/products/devstudio/overview/)**
2.  Klik tombol download atau klik link berikut:
    
    [jboss-devstudio-8.1.0.GA-jar_universal.jar](http://www.jboss.org/download-manager/file/jboss-devstudio-8.1.0.GA-jar_universal.jar)
3.  Jalankan file installer tersebut dengan perintah berikut:

    ```
    java -jar jboss-devstudio-8.1.0.GA-jar_universal.jar
    ```
    
4. Ikuti wizard instalasi
  - Introduction, klik Next
  - Accept End User License Agreement, klik Next
  - Pilih lokasi instalasi misalnya di /Applications/jbdevstudio81 atau di /home/username/jbdevstudio81, klik Next
  - Pilih Default Java VM (Jika anda menggunakan Java 1.8 sebagai default), klik Next
  - Pilih Platforms and Servers. Pilih Yes,... lalu klik Next
  - Klik Next untuk konfirmasi
  - Proses instalasi berjalan, tunggu beberapa menit sampai proses selesai, klik Next
  - Selesai. Pilih "Run JBoss Developer Studio after installation", klik Done

5. JBDS akan mulai jalan setelah instalasi selesai, dan anda akan diminta menspesifikasikan direktori workspace dimana file-file project akan disimpan. Setelah itu muncul JBDS main windows dengan welcome view. Klik "Get Started with JBoss Central" 



## Instal JBoss Developer Studio Integration Stack

Integration Stack for JBoss Developer Studio adalah skumpulan plugins untuk Eclipse atau JBDS sebagai tools untuk membangun aplikasi diatas produk berikut:

* JBoss Business Process and Rules Development
* JBoss Data Virtualization Development
* JBoss Integration and SOA Development (atau JBoss Fuse atau JBoss Fuse Service Works)
* JBoss SOA 5.x Development (Produk ini sudah kadaluarsa :-) )


> JBDS Integation Stack dapat diinstal dengan cara online mupun offline. Online berarti anda butuh koneksi internet saat instalasi. Sebaiknya sebisa mungkin anda menginstal secara online jika ada waktu untuk mengunduh langsung sehingga akan **memudahkan saat mengupdate plugin** ini nantinya.

### Instalasi Online

Berikut cara instalasi secara online:

1.  Jalankan JBDS

2.  Pilih "Software/Update" tab pada  "JBoss Central" view.
    Jika ada pilihan (checkbox) "Enable Early Access", klik checkbox tersebut dan klik Yes saat keluar pesan warning.

3.  Lihat pada bagian JBoss Developer Studio Integration Stack. Tick semua items berikut:

    - JBoss Business Process and Rules Development
    - JBoss Data Virtualization Development
    - JBoss Integration and SOA Development
    - JBoss SOA 5.x Development

    Kemudian klik tombol "Install/Update (4)".
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/7453659/b5561c32-f295-11e4-96bf-0c913eda1018.png)

4.  Tunggu proses penampilan daftar komponen yang akan diinstal muncul, lamanya proses ini dan proses instalasi berikutnya akan tergantung dari kecepatan download.

    ![image](https://cloud.githubusercontent.com/assets/3068071/7453846/b05d5572-f297-11e4-9233-25abc207a4a9.png)

5.   Klik "Select All" kemudian Next, Next
6.   Accept the term of the license agreements, kelmudian klik Finish. Tunggu sampai proses instalasi selesai.
     Jika ada pesan "Security Warning" karena __you are installing software that contains unsigned contents__, klik OK
7.   Klik Yes, saat diminta restart JBDS.

### Instalasi Offline

1.  Buka halaman web berikut: [https://devstudio.jboss.com/updates/8.0/integration-stack/](https://devstudio.jboss.com/updates/8.0/integration-stack/)
2.  Download file **[jbdevstudio-integration-stack-updatesite-8.0.1.GA](https://devstudio.jboss.com/updates/8.0.0/jbdevstudio-integration-stack-updatesite-8.0.1.GA.zip)** 
3.  Jalankan JBDS
4.  
