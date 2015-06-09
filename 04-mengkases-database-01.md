## Instalasi Database PostgreSQL

Sebelum melakukan latihan untuk membuat Virtual Database (VDB) yang mengakses database (RDBMS), kita akan setup dahulu database dan data yang akan dipergunakan.

Database yang digunakan pada latihan ini adalah PostgreSQL, anda juga bisa menggunakan RDBMS lain.

1.  Download dan instal PostgreSQL
    Untuk instalasi yang lebih mudah, saya sarankan mendownload **graphical installer** dari EnterpriseDB, selain itu installer tersebut juga sudah termasuk PostgreSQL, pgAdmin dan utilitas untuk menginstall paket tambahan yaitu StackBuilder. 
    Graphical installer dari EnterpriseDB hampir tersedia untuk setiap sistem operasi seperti Windows, Mac OS-X, dan Linux.
    
    Download installer tersebut dari halaman berikut: [postgresql.org/download/](http://www.postgresql.org/download/)
    Atau langsung ke [http://www.enterprisedb.com/products-services-training/pgdownload]
    Klik tombol untuk download sesuai dengan OS yang anda pakai.
    
    >> Petunjuk instalasi yang lebih detail bisa dilihat di [dokumentasi](http://www.enterprisedb.com/docs/en/9.3/pginstguide/Table%20of%20Contents.htm), pada halaman download di website EnterpriseDB tersebut dibagian bawah terdapat link ke [Installation Guide](http://www.enterprisedb.com/docs/en/9.3/pginstguide/Table%20of%20Contents.htm)
    
2.  Jalankan PostgreSQL database

    Di Linux atau Mac OS-X: buka terminal, lalu masuk ke user `postgres` dengan perintah `su`
    Jika anda tidak tau password dari user `postgres`, ubah password user tersebut dengan menggunakan user `root`
    
    ```
    su - postgres
    pg_ctl start
    ```
    
    Pastikan PostgreSQL sudah jalan dengan melihat proses yang dijalankan 
    
    ```
    ps aux |grep postgres
    ```
    
    Hasil output di laptop saya (Mac OS-X) adalah sebagai berikut:
    
    ```
    postgres        16432   0.0  0.0  2624960   1040   ??  Ss    1:55AM   0:00.06 postgres: postgres postgres ::1(64714) idle
    postgres        16344   0.0  0.0  2619432   1028   ??  Ss    1:38AM   0:00.01 postgres: postgres postgres ::1(64630) idle
    postgres        16340   0.0  0.0  2619432   1028   ??  Ss    1:37AM   0:00.01 postgres: postgres postgres ::1(64582) idle
    postgres        16308   0.0  0.0  2619432   1068   ??  Ss    1:32AM   0:00.04 postgres: postgres postgres ::1(64566) idle
    postgres        16237   0.0  0.0  2469224    596   ??  S     1:21AM   0:00.03 /usr/sbin/cfprefsd agent
    postgres         4025   0.0  0.0  2474188    400   ??  Ss   31May15   0:03.14 postgres: stats collector process
    postgres         4024   0.0  0.0  2619044   1088   ??  Ss   31May15   0:02.38 postgres: autovacuum launcher process
    postgres         4023   0.0  0.0  2619044    124   ??  Ss   31May15   0:02.51 postgres: wal writer process
    postgres         4022   0.0  0.0  2619044    148   ??  Ss   31May15   0:02.69 postgres: writer process
    postgres         4021   0.0  0.0  2619044    368   ??  Ss   31May15   0:00.14 postgres: checkpointer process
    postgres         4018   0.0  0.0  2474188     40   ??  Ss   31May15   0:00.01 postgres: logger process
    postgres         4014   0.0  0.0  2619044    352   ??  Ss   31May15   0:00.45 /Library/PostgreSQL/9.4/bin/postmaster -D/Library/PostgreSQL/9.4/data
    postgres          749   0.0  0.0  2471544    440   ??  S    30May15   0:00.29 /System/Library/Frameworks/CoreServices.framework/Frameworks/Metadata.framework/Versions/A/Support/mdworker -s mdworker-sizing -c MDSSizingWorker -m com.apple.mdworker.sizing
    postgres          721   0.0  0.0  2469216    288   ??  S    30May15   0:01.78 /System/Library/Frameworks/CoreServices.framework/Frameworks/Metadata.framework/Versions/A/Support/mdflagwriter
    ```    

3.  Jalankan pgAdmin.
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8042502/d2cf6bae-0e49-11e5-91fb-9909b2c0b7bd.png)
    
    Koneksikan pgAdmin ke database server dengan mengklik dua kali pada menu tree **PostgreSQL 9.2 (localhost:5432)**, sehingga muncul daftar Databases, Tablespaces, dan seterusnya
    
    Ekspansikan menu item Database pada tree view tersebut, kemudian pilih item "postgres"
    
    Klik icon Query SQL di icon menu bar atau akses menu Tools > Query Tools.
    Akan muncul Query Window seperti berikut, lalu copy paste text dibawah ini ke teks area (SQL Editor)
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8042510/e2c4196a-0e49-11e5-8e59-c69830089fb6.png)

    ```
    CREATE TABLE tbl_user
    (
      userid integer NOT NULL,
      first_name character(100),
      last_name character(100),
      birthday date,
      location character(100),
      CONSTRAINT pk_userid PRIMARY KEY (userid)
    );
    INSERT INTO tbl_user (userid, first_name, last_name, birthday, location) VALUES (4, 'kinoy', 'supardi', '1986-12-23', 'surabaya');
    INSERT INTO tbl_user (userid, first_name, last_name, birthday, location) VALUES (3, 'unyil', 'wiyono', '1986-06-09', 'yogjakarta');
    INSERT INTO tbl_user (userid, first_name, last_name, birthday, location) VALUES (1, 'ejlp', 'noname', '1978-12-08', 'jakarta');
    INSERT INTO tbl_user (userid, first_name, last_name, birthday, location) VALUES (2, 'budi', 'budiman', '1998-11-12', 'bandung');
```

    Eksekusi SQL tersebut dengan menekan icon Execute Query, atau dengan mengakses menu Query > Execute

    Hasilnya, sebuah tabel `tbl_user` akan terbuat dengan kolom sebagai berikut:
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8042214/efca151c-0e47-11e5-9235-a96f37ff0662.png)
    
    dan kita bisa lihat data pada tabel tersebut dengan mengklik kanan tabel `tbl_user` di menu tree kemudian pilih "View Data" > "View All Rows" dan hasilnya seperti ini:
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8048782/ffc8f87e-0e7f-11e5-8d9b-6874a2278bfb.png)


4.  Download PostgreSQL JDBC driver di [jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html)
    Karena kita menggunakan JDK/JRE 1.8, jadi yang perlu anda download adalah file [**JDBC41** Postgresql Driver Version 9.4-1201](https://jdbc.postgresql.org/download/postgresql-9.4-1201.jdbc41.jar)
   
    Simpan file tersebut ditempat yang mudah diakses, misalnya di `/home/postgres`
   
   
