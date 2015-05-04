Sebelum memulai LAB, ada beberapa hal yang perlu diperhatikan

> Penjelasan dalam dokumen workshop (LAB) ini saya asumsikan anda menggunakan Linux atau OS-X sehingga perintah-perintah (command line) kadang kala spesifik untuk OS tersebut. Saya anggap anda sudah tau padanan perintah tersebut pada OS yang anda gunakan, misalnya Windows.

*  Baca dokumen [JDV supported configuration](https://access.redhat.com/articles/703663) terutama JDK yang dapat digunakan serta versinya.
*  Mesin (laptop/PC) yang akan digunakan minimal memiliki 4GB memory dan beberapa kira-kira 3 GB disk space.
*  Pada dasarnya JDV bisa dijalankan di sistem operasi apa saja, Windows, Linux, Mac OS-X selama JDK diatas bisa dijankan, jadi pada workshop ini anda bebas menggunakan OS apa saja, tapi pada lingkungan Production sebaiknya digunakan OS yang di list di dokumen Supported Configuration diatas.
*  Saya sarankan anda sudah menginstall **Oracle JDK 1.8**
*  Anda sudah menginstall **PostgreSQL minimal versi 9.2**. Database ini akan digunakan sebagai penyedia contoh data.

Kita akan menginstal komponen berikut:
-  **JBoss Data Virtualization (JDV) versi 6.1**

   Link download tersedia di halaman ini: [http://www.jboss.org/products/datavirt/download/](http://www.jboss.org/products/datavirt/download/)
   
   Klik tombol download berwarna hijau, atau link di tabel
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/7456503/23434a12-f2af-11e4-8308-318ac57de3cf.png)
   
   Jika anda sudah memiliki SUBSCRIPTION dari Red Hat, anda bisa mendownload dari link berikut:
   
   [https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?product=data.services.platform](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?product=data.services.platform&downloadType=distributions)
   
   ![image](https://cloud.githubusercontent.com/assets/3068071/7456599/e16ae158-f2af-11e4-8b9e-59225d94f2df.png)

-  **JBoss Developer Studio (JBDS) versi 8.1** dengan plugin JBDS **Integration Stack versi 8.0.1**.
   
   Link untuk download JBDS ada di [halaman ini](https://www.jboss.org/products/devstudio/overview/). 
   
   Anda bisa juga mengunduh langsung dari link berikut, tapi anda akan perlu register dulu untuk bisa mengunduh:
   [jboss-devstudio-8.1.0.GA-jar_universal.jar](https://www.jboss.org/download-manager/file/jboss-devstudio-8.1.0.GA-jar_universal.jar)
   
   Untuk mepercepat regsitrasi anda bisa pakai login dengan account Facebook, Twitter, Google atau sosial media lainnya.
   
   Instalasi JBDS Integation dapat dilakukan secara online maupun offline, lihat detail cara instalasi & link untuk download file yang dapat digunakan untuk instalasi offline bisa dilihat disini:
   
   [https://devstudio.jboss.com/updates/8.0/integration-stack/](https://devstudio.jboss.com/updates/8.0/integration-stack/)
