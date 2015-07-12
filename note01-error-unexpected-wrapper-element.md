Saat menjalankan query **eksekusi prosedur yang memanggil Web Service** diperoleh error seperti ini:

```
org.teiid.runtime.client.TeiidClientException: java.lang.RuntimeException: 
Remote org.teiid.core.TeiidProcessingException: TEIID30504 
CustomerService: Unexpected wrapper element {http://server.service.ejlp12/}getCustomers found.   
Expected {http://service.ejlp12/}getCustomers.
```

Error ini terjadi pada JBoss Developer Studio (Version: 8.1.0.GA Build id: GA-v20150327-1349-B467), saya menggunakan JDV 6.1.0

Error terse but terjadi karena namespace dari web service sesuai WSDL-nya adalah http://service.ejlp12/ sedangkan yang di-generate oleh JBDS adalah http://server.service.ejlp12/ 

Berikut WSDL dari Web Service yang dipanggil:

![image](https://cloud.githubusercontent.com/assets/3068071/8637585/2625dd0e-28c3-11e5-92cb-0c34ebf3da0a.png)

Dan berikut hasil transofrmasi yang dibuat oleh JBDS:

![image](https://cloud.githubusercontent.com/assets/3068071/8637570/820e9ca6-28c2-11e5-9ad9-2b7483f81c0d.png)


SOLUSI:

Untuk mengatasi masalah ini, kita perlu mengubah text transformation diatas secara manual.
