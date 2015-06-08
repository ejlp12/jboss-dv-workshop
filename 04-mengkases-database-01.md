== Instalasi Database PostgreSQL

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
  

4. Download PostgreSQL JDBC driver di [jdbc.postgresql.org/download.html](https://jdbc.postgresql.org/download.html)
   Karena kita menggunakan JDK/JRE 1.8, jadi yang perlu anda download adalah file [**JDBC41** Postgresql Driver Version 9.4-1201](https://jdbc.postgresql.org/download/postgresql-9.4-1201.jdbc41.jar)
   
   Simpan file tersebut ditempat yang mudah diakses, misalnya di /home/postgres
   
   
