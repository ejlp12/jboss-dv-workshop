> Pada latihan ini kita akan melakukan ekspos data menggunakan RESTful API (HTTP) dari data user yang ada di file CSV dengan menggunakan tabel `tbl_user` yang sudah dibuat di VIew Model `UserView.xmi` pada latihan sebelumnya.

1. Untuk mengespos sebagai REST, kita perlu membuat virtual procedure dari tabel yang akan kita ekspos.

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114463/75677c66-6f61-11e6-94a3-4293610aa7c9.png)

2. Pada jendela "Generate REST Virtual Procedure" definisikan "Result set element name" dan "Row element name" dan pilih tabel yang akan diekspose.

   Klik [OK]

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114490/adb60100-6f61-11e6-8214-98a53e4f42c7.png)

   Hasilnya (result) nantinya akan seperti ini:

   ```
   <users>
       <auser>
           <first_name>dudi</first_name>
           <last_name>mustakim</last_name>
           <birth_date>08-09-1981</birth_date>
           <location>jakarta</location>
      </auser>
      ... dan seterusnya
   ```

   atau dalam bentuk json akan seperti ini:

   ```
{
  "users": {
    "auser": [
      {
        "birth_date": "08-09-1981",
        "last_name": "mustakim",
        "location": "jakarta",
        "first_name": "dudi"
      },
      ... dan seterusnya
   ```

3. Hasilnya akan seperti ini:

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114570/41c996f4-6f62-11e6-85d2-609ab4faf34a.png)

   Klik dua kali `tbl_userRestProc`, kita akan lihat hasilnya seperti ini:

  
  ![image](https://cloud.githubusercontent.com/assets/3068071/18114590/6732ea30-6f62-11e6-9ed9-01e6ef2d8b09.png)

  Jika kita ingin mengubah data atau melakukan transformasi, kita bisa lakukan di transformation editor.

   ***Save file `UserView.xmi`!!***

4.  Update VDB yang sudah dibuat di latihan sebelumnya agar `UserView.xmi` terupdate dengan cara mengklik tombol [Synchronize]

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114626/c13d90a2-6f62-11e6-8b72-6fbb3712114b.png)

5. Deploy VDB ke JDV server runtime

***!!! Perhatikan pada saat deploy kita harus men-generate DataSource untuk VDB tersebut, dan catat nama JNDI-nya karena akan dibutuhkan saat kita set pada aplikasi REST nantinya.***

![image](https://cloud.githubusercontent.com/assets/3068071/18114703/772d5f64-6f63-11e6-8a74-cf124f5ab9b5.png)


6. Generate aplikasi REST. 

   Aplikasi REST adalah aplikasi web berbentuk file WAR (Java EE application).  Aplikasi tersebut akan melakukan koneksi JDBC ke virtual table yang sudah dideploy melalui DataSource.

   ![image](https://cloud.githubusercontent.com/assets/3068071/18114679/4213d6fa-6f63-11e6-8ee3-35badaed91f3.png)

   Perhatikan saat set "VDB JNDI name" nilainya harus sama dengan nama JNDI waktu kita deploy VDB.

   ![image](https://cloud.githubusercontent.com/assets/3068071/18114683/543343d4-6f63-11e6-9884-30419b9d444b.png)

    Tunggu sampai muncul kotak dialog seperti ini:

    
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114696/69d42f1e-6f63-11e6-94e7-3e55e4e62240.png)

   Aplikasi (file WAR) akan terbentuk di folder yang kita tentukan (dalam kasus saya, file disimpan di direktori `/User/ejlp12/warFiles`

7. Deploy file WAR tersebut ke JDV server runtime lewat Administration console.

    Buka admin console menggunakan browser: [http://127.0.0.1:9990](http://127.0.0.1:9990])

    Klik Deployments lalu klik tombol [Add]

    Klik tombol [Choose file] lalu pilih file WAR yang baru saja di-generate, lalu klik [Next]

   
  ![image](https://cloud.githubusercontent.com/assets/3068071/18114767/0f43cfd6-6f64-11e6-9885-9a4ed41b7799.png)

  Klik checkbox "Enable" kemudian klik [Save]

   ![image](https://cloud.githubusercontent.com/assets/3068071/18114772/1ca4eeda-6f64-11e6-89bc-9a0f51a3865b.png)

   Hasilnya adalah seperti ini, kita bisa lihat context root dari aplikasi tersebut:
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114791/4276b288-6f64-11e6-9784-d09c2d5f8aec.png)
 
8. Buka browser untuk melakukan test RESTful API yang sudah kita setup

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114806/65b1df8e-6f64-11e6-9515-24de6299352f.png)

   ![image](https://cloud.githubusercontent.com/assets/3068071/18114816/72ca46f2-6f64-11e6-92b4-7172deeb7833.png)
   
   Coba akses REST dengan mengklik tombol [Try it out!]

   ![image](https://cloud.githubusercontent.com/assets/3068071/18114824/8551b18e-6f64-11e6-9ade-16817d79b1f9.png)

   Hasilnya adalah seperti ini

  ![image](https://cloud.githubusercontent.com/assets/3068071/18114832/95ec69e4-6f64-11e6-8cb0-6fb79304bb46.png)

   Kita juga bisa coba untuk REST dengan format JSON
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18114838/a7403a18-6f64-11e6-938c-df67e75dd292.png)








   



