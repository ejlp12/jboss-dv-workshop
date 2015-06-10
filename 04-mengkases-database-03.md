### Eksplorasi Source Model

Anda telah membuat sebuah source model yang merupakan virtual data source dari sebuah physical table di PostgreSQL database. Sekarang kita eksplorasi lebih detail dari Source Model tersebut.

1.  Lihat 'Package Diagram' dari source model dengan mengklik dua kali `PostgreSQL_UserDB.xmi` di Model Explorer view
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8073100/91020540-0f4a-11e5-9fe3-03d8435fc9aa.png)

    Kita bisa lihat source model tersebut hanya memiliki satu tabel yaitu `tbl_user`.
    
    Sebuah Source Model dapat memiliki banyak tabel atau obyek yang lain seperti Procedure atau View yang merupakan representasi dari riil obyek prosedur atau view yang ada di RDBMS.
 
2.  Table Editor

    Selain Package Diagram view, Source Model juga dapat dilihat dengan menggunakan Table Editor view seperti ini:
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8074673/ad02a42e-0f5f-11e5-83f7-d999444f8c0d.png)
    
    Pada tab 'Base Tables' kita bisa lihat daftar semua tabel yang ada pada Source Model. Properties dari sebuah definisi tabel adalah sebagai berikut:
    
    1. Table name
    2. Nama in source: Nama tabel di physical data source, dalam kasus latihan kita ada di schema "public" dengan nama tabel "tbl_user" 
    3. System:  True atau false
    4. Cardinality: nilai -1 berarti tanpa cardinality, nilai ini menunjukan jumlah rows dari tabel yang akan digunakan saat perhitungan cost untuk optimasi query.
    5. Support Update: True atau false, fitur ini juga akan tergantung pada kemampuan adapter untuk update ke sumber data. Untuk file adapter yang tidak support update maka tidak ada gunanya nilai property ini diset true
    6. Materialized: True atau false, jika kita set true berarti data tabel akan disimpan di cache (memory) atau di tabel lain
    7. Logical Relationships
    8. Materialized Table: Nama dari materialized table yang akan menyimpan data
    9. Object URI
    10. Relational: Native Query
    11. Description
    
    
    
3.  File `PostgreSQL_UserDB.xmi` pada dasarnya adalah file XML, tapi tidak disarankan untuk mengedit file XML tersebut secara manual.
   
    File tersebut berisi:
   
    1. Definisi model dari physical object (Table, View, Procedure, Index)
    2. Definisi connection profile, jenis translator
   
    Anda bisa lihat source XML dengan membuka file `PostgreSQL_UserDB.xmi` dengan menggunakan XML editor.
    Klik kanan **PostgreSQL_UserDB.xmi** lalu pilih Open With > XML Editor
   
4.  Melihat Connection Profile

    Connection profile dari suatu Source Model dapat dilihat dengan cara: klik kanan **PostgreSQL_UserDB.xmi** lalu pilih Modeling > View Connection Profile Info
   
    ![image](https://cloud.githubusercontent.com/assets/3068071/8074338/317be4d6-0f5b-11e5-8d58-a8d60102636e.png)
   
    Hasil view connection profile
   
    ![image](https://cloud.githubusercontent.com/assets/3068071/8073196/018bec1c-0f4c-11e5-8dd8-8de630b77d2d.png)


5.  Bagaimana mengubah connection profile dari Source Model? 

    Mengubah profil koneksi adalah hal yang biasa, misalnya pada saat alamat database yang akan kita akses dari Source Model tersebut berubah. Untuk mengubahnya kita mengklik kanan `PostgreSQL_UserDB.xmi` lalu pilih Modeling > **Set Connection Profile**
   
6.  Bagaimana jika RDBM yang digunakan sebagai sumber data berubah dari PostgreSQL misalnya menjadi MySQL dengan schema atau tabel yang diakses sama. Kita perlu mengubah Translator dari Source Model.

    Translator seperti adapter, suatu komponen yang bertanggung jawab melakukan akses ke physical data source untuk mengambil data. Anda dapat membuat suatu translator sendiri untuk mengakses ke suatu jenis data source jika memang mau.
    
    Untuk kasus perubahan jenis RDBMS kita bisa mengubah dengan cara mengklik kanan `PostgreSQL_UserDB.xmi` lalu pilih Modeling > Set Translator Name
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8074514/f434b816-0f5d-11e5-8305-ac1e6d5175ae.png)
   

6. Tanslator Properties

   Jarang sekali kita perlu mengubah translator properties tapi jika dibutuhkan kita bisa set dengan cara: mengklik kanan `PostgreSQL_UserDB.xmi` lalu pilih Modeling > Edit Translator Overrides
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8073210/36461996-0f4c-11e5-80a3-983ae3896bc8.png)
   
