> Pada latihan kali ini kita akan membuat View Model yang menggabungkan dua data user dari file CSV dan dari tabel di PostgreSQL database.

> Ada beberapa cara dalam membuat View Model yang memiliki kompleks query (SQL). Pada percobaan pertama ini kita akan lakukan dengan cara **mengubah query secara manual**

1. Buatlah project seperti ini:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18096387/322a0408-6f04-11e6-869b-0d334168d894.png)
   
   Ulangi lagi latihan sebelumnya (membuat Source Model dan View Model dari CSV file dan membuat Source Model dari database PostgreSQL) tapi kali ini lakukan pada satu project yang sama.
   
   
2. Kita akan membuat View Model baru yang berisi sebuah tabel yang merupakan gabungan (union) dari dua sumber data (federated)  yaitu file CSV dan database PostgreSQL.

   Klik kanan pada project tersebut dan pilih New > Teiid Metadata Model 

   ![image](https://cloud.githubusercontent.com/assets/3068071/18096520/abef52de-6f04-11e6-99a6-8792ad1b9e02.png)

3. Pada jendela New Model Wizard, isi fields dengan nilai berikut:

   Model Name: UserUnionView
   Model Type: View Model

   Pilih "Transform from an existing model"

   ![image](https://cloud.githubusercontent.com/assets/3068071/18096616/063c5142-6f05-11e6-8d0a-7683215b8f18.png)

   Kemudian pilih Existing Model, kita bisa pilih `tbl_user` dari `PostgreSQL_UserAddress.xmi`

   ![image](https://cloud.githubusercontent.com/assets/3068071/18106810/6f2315cc-6f2f-11e6-8705-16d40129a745.png)

   **atau** bisa juga pilih `tbl_user` dari `UserView`, karena kita akan membuat view model yang menggabungkan salah satu dari tabel tersebut nantinya.

   
   ![image](https://cloud.githubusercontent.com/assets/3068071/18106869/a4e50134-6f2f-11e6-9267-c163a73666f5.png)

3.   Delete View Model `tbl_address` dan `tbl_user_address` karena kita tidak akan menggunakannya

   ![image](https://cloud.githubusercontent.com/assets/3068071/18107458/3943c246-6f32-11e6-916a-d3183f77e7ea.png)

   
4. Klik dua kali `tbl_user` yang ada di `UserUnionView.xmi` agar kita bisa melihat **transformation diagram** seperti ini

   ![image](https://cloud.githubusercontent.com/assets/3068071/18107564/9d42e0ce-6f32-11e6-9823-463c79d264b0.png)

5. Klik dua kali simbol transformasi bergambar panah dengan huruf "T"

   ![image](https://cloud.githubusercontent.com/assets/3068071/18107643/f5a2a33a-6f32-11e6-9000-01f97bd06187.png)

   Pada transformation editor, kita bisa membuat query untuk menyatukan (union) dengan view `tbl_user` dari `UserView.xmi` yang merupakan view data dari file CSV dengan menambahkan query berikut:

   ```sql
   UNION
   SELECT
		*
	FROM
		UserView.tbl_user
   ```

   ![image](https://cloud.githubusercontent.com/assets/3068071/18107699/4865e816-6f33-11e6-83a3-30c03e79101d.png)

   **Save** file tersebut!

   Kita akan lihat hasilnya error seperti ini karena jumlah dan nama fields dari kedua tabel tidak sama

   ![image](https://cloud.githubusercontent.com/assets/3068071/18107878/015e252c-6f34-11e6-9e9e-931a733519bb.png)

   Kita bisa lihat disini field `userid` tidak ada di view `tbl_user` dari file CSV kemudian field `birthday` memiliki nama dan tipe data yang berbeda dengan `birth_date`, kita bisa lihat juga tipe data string memliki panjang (lenght) yang berbeda.

   ![image](https://cloud.githubusercontent.com/assets/3068071/18108033/b8963270-6f34-11e6-935b-422fd8d30b14.png)

6. Sekarang ganti transformation SQL menjadi seperti ini:

   ```
   SELECT
		*
	FROM
		PostgreSQL_UserAddress.tbl_user
   UNION
   SELECT
		0 AS userid, first_name, last_name, birth_date AS birthday, location
	FROM
		UserView.tbl_user
   ```
   **Save** file tersebut!

   Hasilnya menjadi seperti ini: Masih belum sempurna karena kita belum menangani perbedaan tipe data `birthday` dan `birth_date`

   ![image](https://cloud.githubusercontent.com/assets/3068071/18108626/4606dd1a-6f37-11e6-8bfd-640b09a7a6e1.png)

7. Ganti transformation SQL pada bagian select `birth_date` menjadi seperti ini:

   ```
   PARSEDATE(UserView.tbl_user.birth_date, 'dd-MM-yyyy') AS birthday
  ```
   **Save** file tersebut!


   Hasil akhirnya tanpa error seperti ini:


   ![image](https://cloud.githubusercontent.com/assets/3068071/18109028/611d3bd8-6f39-11e6-932f-b2c253603110.png)

8. Klik kanan `tbl_user` pada `UserUnionView.xmi` lalu pilih **Preview Data** untuk melakukan test pada view yang baru saja kita buat.

  ![image](https://cloud.githubusercontent.com/assets/3068071/18109095/adab20f0-6f39-11e6-85be-b73455119a60.png)

   Hasilnya seperti ini:

   ![image](https://cloud.githubusercontent.com/assets/3068071/18109119/c38830a2-6f39-11e6-92c7-71cccc2c26f3.png)














