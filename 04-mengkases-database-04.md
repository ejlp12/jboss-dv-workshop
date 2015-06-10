### Latihan

1. Dengan menggunakan pgAdmin, jalankan query berikut ini

```sql
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
)
CREATE TABLE tbl_address
(
  id_address integer NOT NULL,
  address1 character(500),
  address2 character(500),
  city character(255),
  state character(255),
  country character(100),
  address_type integer,
  CONSTRAINT pk_id_address PRIMARY KEY (id_address)
)

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

2. Buat Source Model baru dengan nama `PostgreSQL_UserAddress.xmi` dengan memasukan semua tabel yang sudah dibuat yaitu `tbl_user`, `tbl_address`, `tbl_user_address`
   Pastikan juga saat import anda memilih table type 'TABLE' & 'FOREIGN_TYPE'
   
   Hasil akhirnya yang diharapkan adalah seperti ini:
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8076623/89e0a3f6-0f78-11e5-82b0-6d3e9b088962.png)
