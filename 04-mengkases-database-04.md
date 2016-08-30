### Latihan: Membuat Source Model baru dengan 3 tabel

1. Dengan menggunakan pgAdmin, jalankan query berikut ini

    ```sql
    CREATE TABLE tbl_address
    (
      id_address integer NOT NULL,
      address1 text,
      address2 text,
      city text,
      state text,
      country text,
      address_type integer,
      CONSTRAINT pk_id_address PRIMARY KEY (id_address)
    );
    
    CREATE TABLE tbl_user_address
    (
      userid integer,
      id_address integer,
      pk_user_address integer NOT NULL,
      CONSTRAINT pk_user_address PRIMARY KEY (pk_user_address),
      CONSTRAINT fk_id_address FOREIGN KEY (id_address)
          REFERENCES tbl_address (id_address) MATCH SIMPLE
          ON UPDATE NO ACTION ON DELETE NO ACTION,
      CONSTRAINT fk_userid FOREIGN KEY (userid)
          REFERENCES tbl_user (userid) MATCH SIMPLE
          ON UPDATE NO ACTION ON DELETE NO ACTION
    );
    
    INSERT INTO tbl_address (id_address, address1, address2, city, state, country, address_type) VALUES (1, 'Jl. Sudirman', 'KAV 10', 'Jakarta', 'DKI Jakarta', 'Indonesia', 1);
    INSERT INTO tbl_address (id_address, address1, address2, city, state, country, address_type) VALUES (2, 'Jl. Dudidam', 'Blok E3/10', 'Depok ', 'Jawa Barat', 'Indonesia', 2);
    INSERT INTO tbl_address (id_address, address1, address2, city, state, country, address_type) VALUES (3, 'Jl. Kurawa', 'Perumahan Berlian no.1', 'Bandung', 'Jawa Barat ', 'Indonesia', 1);
    INSERT INTO tbl_address (id_address, address1, address2, city, state, country, address_type) VALUES (4, 'Jl. Tuwaga', 'No.6', 'Surabaya', 'Jawa Timur ', 'Indonesia', 1);
    
    INSERT INTO tbl_user_address (userid, id_address, pk_user_address) VALUES (1, 1, 1);
    INSERT INTO tbl_user_address (userid, id_address, pk_user_address) VALUES (1, 2, 2);
    INSERT INTO tbl_user_address (userid, id_address, pk_user_address) VALUES (2, 3, 3);
    INSERT INTO tbl_user_address (userid, id_address, pk_user_address) VALUES (3, 4, 4);
    INSERT INTO tbl_user_address (userid, id_address, pk_user_address) VALUES (4, 1, 5);
    ```

2.  Buat Source Model baru dengan nama `PostgreSQL_UserAddress.xmi` dengan memasukan semua tabel yang sudah dibuat yaitu `tbl_user`, `tbl_address`, `tbl_user_address`
   
    Pastikan juga saat import anda memilih table type 'TABLE' & 'FOREIGN_TYPE'
   
    Hasil akhirnya yang diharapkan adalah seperti ini:
   
    ![image](https://cloud.githubusercontent.com/assets/3068071/8076623/89e0a3f6-0f78-11e5-82b0-6d3e9b088962.png)

3.  Coba tes Source Model yang sudah dibuat dengan preview data untuk tabel `tbl_address`

### Menambahkan Tabel Baru ke Source Model

Sampai saat ini anda seharusnya punya dua buah Source Model, yaitu:

1. `PostgreSQL_UserDB.xmi` yang memiliki 1 tabel
2. `PostgreSQL_UserAddress.xmi`yang memiliki 3 tabel
    
Bagaimana jika kita tidak ingin membuat Source Model baru, tapi ingin menambahkan `tbl_address` dan `tbl_user_address` ke `PostgreSQL_UserDB.xmi`.

Kita dapat menambahkan __Child__ di Source Model dengan cara mengklik kanan `PostgreSQL_UserDB.xmi`, pilih New Child > Table. Tapi cara ini menyulitkan karena kita menambahkan tabel secara manual, kolom Primary/Forign Key pun didefinisikan manual.

1.  Cobalah untuk melakukan hal tersebut, dan lihat tampilan window berikut untuk mendefinisikan Relational Table baru:

   ![image](https://cloud.githubusercontent.com/assets/3068071/8077033/507dbb54-0f7c-11e5-8ce3-00c1f8555d51.png)

   Klik [Cancel] karena kita tidak akan menambahkan tabel secara manual.
   
   Kita akan lakukan dengan cara yang lebih mudah.
    
    
2.  Cara yang mudah adalah dengan menggunakan cara Import, seperti halnya kita membuat Source Model baru, tetapi saat mendefinisikan nama Source Model kita dapat memilih opsi __Update Source Model__ seperti berikut:

   ![image](https://cloud.githubusercontent.com/assets/3068071/8076784/517fa136-0f7a-11e5-9e7b-fed4a05c912b.png)

3.  Setelah klik Next anda akan lihat perubahan apa yang akan dilakukan pada Source Model `PostgreSQL_UserDB.xmi` seperti berikut:

   ![image](https://cloud.githubusercontent.com/assets/3068071/8076813/7b8b4994-0f7a-11e5-930a-eb427820ef25.png)

4. Hasilnya adalah seperti ini, gambar tabel pada Package Diagram terlihat menumpuk. Kita dapat mengatur manual posisi tiap tabel dengan drag-and-drop kemudian mengklik icon "Refresh" di kiri atas diagram
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8077137/51d4a7b4-0f7d-11e5-82d8-63aee9c962d0.png)
  
