JDV dapat diakses bukan hanya dari JDBC, SOAP Web Service, REST (OData) saja, tapi juga dapat diakses menggunakan ODBC.

Apakah JDV perlu diinstal di Windows untuk bisa diakses menggunakan ODBC? 

Jawabannya adalah "TIDAK".

JDV secara default membuka port untuk akses ODBC yaitu port ``

Jika anda menggunakan OS selain Windows, anda bisa menggunakan [unixODBC](http://www.unixodbc.org/) dan ProsgreSQL ODBC driver untuk mengakses JDV lewat ODBC.

Berikut cara instalasi unixODBC dan PostgreSQL ODBC driver di Linux atau Mac OSX:
[https://gist.github.com/ejlp12/74cdcde11ca01188cbf7](https://gist.github.com/ejlp12/74cdcde11ca01188cbf7)
