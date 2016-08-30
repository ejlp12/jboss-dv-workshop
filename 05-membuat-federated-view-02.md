> Pada latihan kali ini kita akan membuat  View Model lagi yang akan menggabungkan data user dari file CSV dan dari tbl_user di PostgreSQL database.
> Tetapi kali ini caranya sedikit berbeda, kita akan bikin query SQL dulu dari View & Source Model yang sudah kita deploy di JDV.
>
> Setelah query jadi yaitu bisa dieksekusi dengan sukses dan data hasilnya sesuai yang kita harapkan, barulah kita membuat View Model. 

1. Buatlah VDB dari project yang sudah kita buat sebelumnya:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18109670/0631b4b6-6f3d-11e6-9aeb-2aa5f5333c49.png)

2. Berinama VDB, misalnya **latihan05**, Pilih Source Model dan View Model yang akan dimasukkan ke VDB

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18109713/4ecd5694-6f3d-11e6-86a7-3ceb90979315.png)

   Klik [Finish]
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18110767/50ea0ef2-6f44-11e6-9195-d6c7de030673.png)

   Abaikan jika muncul problem seperti ini:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18109814/feef20f2-6f3d-11e6-9b3c-67a25406d018.png)

3. Deploy VDB

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18109837/27b019ba-6f3e-11e6-9a36-2c41894037d5.png)

   Pastikan VDB sukses ter-deploy dan statusnya **ACTIVE**

  > Akan muncul message "TEIID40003 VDB latihan05.1 is set to ACTIVE" di console

   ![image](https://cloud.githubusercontent.com/assets/3068071/18109853/50251328-6f3e-11e6-88ff-196eab5a19d2.png)

4. Execute VDB

  ![image](https://cloud.githubusercontent.com/assets/3068071/18109991/407650d0-6f3f-11e6-9a67-3382e5ce12ed.png)

  Developer Studio anda akan berpindah ke perspective "Database Development"

  Pada "Data Source Explorer" anda bisa melihat schema dan metadata yang ada di JDV server:

  ![image](https://cloud.githubusercontent.com/assets/3068071/18109965/17ca7cce-6f3f-11e6-98eb-d2180c90bc86.png)

5. Anda juga akan mendapatkan editor untuk mengekseskusi query (SQL) namanya **SQL Scrapbook**

   Edit SQL query menjadi seperti ini: `SELECT * FROM PostgreSQL_UserAddress.tbl_user`, kemudian blok teks tersebut dan execute

   ![image](https://cloud.githubusercontent.com/assets/3068071/18110073/c9bcfdda-6f3f-11e6-8231-25cde250ac4c.png)

   Hasilnya akan terlihat seperti ini:

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18110112/fe407622-6f3f-11e6-8668-50f91904cb15.png)

6. Lakukan eksekusi query untuk 


   ![image](https://cloud.githubusercontent.com/assets/3068071/18110158/58921d60-6f40-11e6-97e6-d163651b0de4.png)


7. Buatlah query union select untuk kedua tabel diatas seperti ini:

   ```
   SELECT first_name, last_name, birthday as birth_date, location FROM PostgreSQL_UserAddress.tbl_user
   UNION
   SELECT first_name, last_name, parsedate(birth_date,'dd-MM-yyyy'), location FROM UserView.tbl_user
   ```
   
   Hasilnya sepert ini:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18110247/090001bc-6f41-11e6-85ad-0ae59829e739.png)

8. Copy query union tersebut.

9.  Sekarang kembali ke perspective "Teiid Designer"
 
   ![image](https://cloud.githubusercontent.com/assets/3068071/18110308/5c818c8e-6f41-11e6-9ba3-e92e95504da1.png)
   
   Pilih `UserUnionView.xmi`, klik kanan lalu pilih New Child > Table.

   Kita akan membuat View Model baru yang menggabungkan data user dari CSV file dan tabel tbl_user di PostgreSQL database
 
  ![image](https://cloud.githubusercontent.com/assets/3068071/18110399/efa841f6-6f41-11e6-9823-6c639e7e4f55.png)

  Pada jendela "Create Relational View Table" beri nama View Model (table) yang akan kita buat, yaitu `tbl_user_all`

  Klik tab "Transformation SQL"

  Paste teks yang sudah kita copy dari "SQL Scapbook"

   ![image](https://cloud.githubusercontent.com/assets/3068071/18110493/863b2926-6f42-11e6-9c6f-96c0341bb8f3.png)

   Klik [OK]

   Hasilnya adalah sebagai berikut:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18110573/fef243a4-6f42-11e6-8b80-b32a003ec57f.png)

   Save file `UserUnionView.xmi`!!

10. Preview data dari tabel yang baru saja kita buat `tbl_user_all`

    Hasilnya:

    
    ![image](https://cloud.githubusercontent.com/assets/3068071/18110633/57733a1a-6f43-11e6-9967-c98824918970.png)





 
