### Eksplorasi Source Model

Anda telah membuat sebuah source model yang merupakan virtual data source dari sebuah physical table di PostgreSQL database. Sekarang kita eksplorasi lebih detail dari Source Model tersebut.

1.  Lihat 'Package Diagram' dari source model dengan mengklik dua kali `PostgreSQL_UserDB.xmi` di Model Explorer view
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8073100/91020540-0f4a-11e5-9fe3-03d8435fc9aa.png)

    Kita bisa lihat source model tersebut hanya memiliki satu tabel yaitu `tbl_user`.
    
    Sebuah Source Model dapat memiliki banyak tabel atau obyek yang lain seperti Procedure atau View yang merupakan representasi dari riil obyek prosedur atau view yang ada di RDBMS.
    
2. File `PostgreSQL_UserDB.xmi` pada dasarnya adalah file XML, tapi tidak disarankan untuk mengedit file XML tersebut secara manual.
   
   File tersebut berisi:
   
   1. Definisi model dari physical object (Table, View, Procedure, Index)
   2. Definisi connection profile, jenis translator
   
   Anda bisa lihat source XML dengan membuka file `PostgreSQL_UserDB.xmi` dengan menggunakan XML editor.
   
3. Melihat Connection Profile


4. Bagaimana mengubah connection profile dari Source Model? 

   Mengubah profil koneksi adalah hal yang biasa, misalnya pada saat alamat database yang akan kita akses dari Source Model tersebut berubah. Untuk mengubahnya kita dapat 
