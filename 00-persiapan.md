Sebelum memulai LAB, ada beberapa hal yang perlu diperhatikan

*  Baca dokumen [JDV supported configuration](https://access.redhat.com/articles/703663) terutama JDK yang dapat digunakan serta versinya.
*  Mesin (laptop/PC) yang akan digunakan minimal memiliki 4GB memory dan beberapa kira-kira 3 GB disk space.
*  Pada dasarnya JDV bisa dijalankan di sistem operasi apa saja, Windows, Linux, Mac OS-X selama JDK diatas bisa dijankan, jadi pada workshop ini anda bebas menggunakan OS apa saja, tapi pada lingkungan Production sebaiknya digunakan OS yang di list di dokumen Supported Configuration diatas.
*  Saya sarankan anda sudah menginstall **Oracle JDK 1.8**
*  Anda sudah menginstall **PostgreSQL minimal versi 9.2**. Database ini akan digunakan sebagai penyedia contoh data.



   Penjelasan dalam dokumen workshop (LAB) ini saya asumsikan anda menggunakan Linux atau OS-X sehingga perintah-perintah (command line) kadang kala spesifik untuk OS tersebut. Saya anggap anda sudah tau padanan perintah tersebut pada OS yang anda gunakan, misalnya Windows.

Kita akan menginstal komponen berikut:
-  **JBoss Data Virtualization (JDV) versi 6.1**
-  **JBoss Developer Studio (JBDS) versi 8.1** dengan plugin JBDS **Integration Stack versi 8.0.1**.
   
   Link untuk download JBDS ada di [halaman ini](https://www.jboss.org/products/devstudio/overview/). 
   
   Anda bisa juga mengunduh langsung dari link berikut, tapi anda akan perlu register dulu untuk bisa mengunduh:
   [jboss-devstudio-8.1.0.GA-jar_universal.jar](https://www.jboss.org/download-manager/file/jboss-devstudio-8.1.0.GA-jar_universal.jar)
   
   Untuk mepercepat regsitrasi anda bisa pakai login dengan account Facebook, Twitter, Google atau sosial media lainnya.
   
   Instalasi JBDS Integation dapat dilakukan secara online maupun offline, lihat detail cara instalasi & link untuk download file yang dapat digunakan untuk instalasi offline bisa dilihat disini:
   
   [https://devstudio.jboss.com/updates/8.0/integration-stack/](https://devstudio.jboss.com/updates/8.0/integration-stack/)
