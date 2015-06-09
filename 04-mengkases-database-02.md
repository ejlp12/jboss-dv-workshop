## Tabel sebagai sumber data

## Membuat Source Model 

Sebelum mengikuti latihan ini, sebelumnya ada harus sudah menyiapkan database dan data yang akan digunakan dengan mengikuti langkah sebelumnya pada dokumen [04-mengkases-database-01.md](/04-mengkases-database-01.md).

Sekarang saatnya kita membuat project untuk menakses tabel sebagai sumber data JDV. Kita akan membuat membuat virtual table untuk `tbl_user` yang ada di database PostgreSQL

1.  Buka JBoss Developer Studio (JBDS)
2.  Pastikan anda menggunakan perspective "Teiid Designer Project"
    Buat Model Project baru dengan mengkilik kanan Model Explorer view, kemudian pilih New > Teiid Model Project
    
    Pada wizard New Model Project, beri nama project `teiid_db_test` lalu klik tombol Finish
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8048950/39b1304a-0e82-11e5-845e-af07e6a653b9.png)
   
3.  Anda akan buat Data Source Model yang akan mengakses PostgreSQL menggunakan JDBC driver
    Klik kanan pada Model Explore view lalu pilih Import pada popup menu
    
    ![image](https://cloud.githubusercontent.com/assets/3068071/8049116/adabe22c-0e84-11e5-9d91-b949c3580afe.png)

4.  Pada window Import, ekspansikan folder Teiid Designer kemudian pilih "JDBC Database >> Source Model"

   ![image](https://cloud.githubusercontent.com/assets/3068071/8049142/2cfd946c-0e85-11e5-97c3-459878d2df64.png)
   
5. Pada window "Import Database via JDBC" kita belum bisa memilih Connection Profile karena kita belum membuatnya, jadi klik tombol "New" disebelah field Connection Profile
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8049164/8743507e-0e85-11e5-9871-32ee40f9e1bb.png)
   
6. Pada window "Connection Profile", pilih Connection Profile Type yaitu dengan mengklik "PostgreSQL" di daftar data source.
   Berinama juga Connection Profile yang dibuat misalnya `PostgreSQL DB`, kemudian klik tombol Next

   ![image](https://cloud.githubusercontent.com/assets/3068071/8051127/ac76b742-0ea2-11e5-8630-79a3005b54e6.png)

7. Langkah selanjutnya adalah menentukan driver JDBC untuk Connection Profile tersebut.
   Pada window "New JDBC Connection Profile" pilih PostgreSQL JDBC Driver, lalu klik tab "JAR list", klik tombol "Add JAR/Zip"
   dan pilih file JDBC driver yang sudah didownload.
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8051214/f86caf52-0ea3-11e5-9079-1c0d7cdd4ac8.png)
   
   Klik tombol OK
   
8. Kembali ke window "New JDBC Connection Profile", tentukan nama database, URL, username dan password.
   Jangan sampai ada yang salah. Kemudian klik tombol Test Connection, jika berhasil dan harus berhasil, anda mendapatkan pesan Ping succeeded!
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8051671/a4b955bc-0ea9-11e5-8c8d-5aaacaa942f7.png)
   
   Klik tombol Fisnish
   
9. Anda akan kembali ke window "New JDBC Connection Profile"
   
   Klik Next
   
   Karena kita hanya akan mengakses tabel saja dari JDV maka pilihlah Table di daftar Table Types
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8051805/0ef75748-0eab-11e5-86aa-c0dc64b4778c.png)
   
   Klik Next.
   
10. Ekspansikan menu tree yang mempelihatkan daftar schema di sebelah kiri, lalu klik (checked) `tbl_user`
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8051915/255c8764-0eac-11e5-8dac-55703e51b836.png)
   
   Klik Next
   
11. Berinama Model Name: `PostgreSQL_UserDB.xmi`, lalu klik tombol Finish

   ![image](https://cloud.githubusercontent.com/assets/3068071/8051952/6f7b5fbe-0eac-11e5-8b07-e84a3654732c.png)
   
   Jadilah anda mendapatkan sebuah Source Model seperti ini:
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/8051972/b6c9b168-0eac-11e5-92b0-c1719c6dd94d.png)
