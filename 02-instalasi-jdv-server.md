# Instalasi JBoss Data Virtualization Server

Berikut file-file yang diperlukan untuk installasi

*  **jboss-dv-installer-6.1.0.redhat-3.jar** (File installer JDV versi 6.1.0)
*  **PREVIEW-DataVirtWebUI-03Apr2015.war** (Opsional - Komponen WebUI ini hanya untuk _preview_)

> Pastikan Operating System yang digunakan, JDK yang terinstal sudah sesuai dengan dokumen [JDV Supported Configuration](https://access.redhat.com/articles/703663)


## Akses ke Dokumentasi Produk

Sebelum melakukan instalasi, mari kita liat dokumentasi yang tersedia untuk JDV:

1.  Buka halaman web berikut: [Red Hat JBoss Data Virtualization 6.1 Documentation](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/)
    
    Baca daftar dokumen yang tersedia disitu, dan identifikasi dokumen mana yang kira-kira perlu dibaca untuk proses instalasi.

2.  Klik dokumen [Getting Started Guide](https://access.redhat.com/site/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Getting_Started_Guide/index.html)

    Baca _Chapter 7. Installing The Product_, ikuti langkah-langkah dasar instalasi menggunakan GUI yang dijelaskan di halaman tersebut. Saat diminta menspesifikasikan direktori untuk instalasi, gunakan path yang mudah dan tidak terlalu panjang misalnya di `/home/jboss/DV_60`
    
    Instalasi dimulai dengan menjalankan perintah berikut dari Terminal/Console menggunakan non-previledged user (bukan root):
    
    ```
    java -jar jboss-dv-installer-6.1.0.redhat-3.jar
    ```
    
    > **Jika anda menginstal di sistem operasi Windows sebaiknya jalankan dari CMD prompt yang di-_run as_ Administrator**
    
    Proses instalasi akan menginstal JBoss EAP 6.3 sebagai platform yang menjalankan JDV Server.
    
    [Screenshot dari tiap langkah instalasi dapat dilihat disini] (https://github.com/ejlp12/jboss-dv-workshop/issues/2)

3.  Baca dan ikuti sampai step 16 yang dijelaskan di dokumen tersebut.

## Menjalankan JDV

1.  Start JDV server dengan menajalankan JBoss EAP perintah:

	```
	cd <DV_INSTALL_DIR>/jboss-eap-6.3/bin
	./standalone.sh
	```
	
	Jika error karena port yang bentrok (sudah digunakan oleh aplikasi lain), coba jalankan dengan perintah berikut:
	
	```
	./standlone.sh -Djboss.socket.binding.port-offset=10000
	```
	
	Artinya aplikasi JBoss EAP atau JDV akan berjalan di port = default port + 10000
	
	Tunggu sampai proses start selesai, yaitu anda akan melihat log di console seperti ini:
	
	```
	00:16:54,957 INFO  [org.jboss.as.server] (Controller Boot Thread) JBAS018559: Deployed "database-service.jar" (runtime-name : "database-service.jar")
	00:16:54,958 INFO  [org.jboss.as.server] (Controller Boot Thread) JBAS018559: Deployed "ModeShape.vdb" (runtime-name : "ModeShape.vdb")
	00:16:54,958 INFO  [org.jboss.as.server] (Controller Boot Thread) JBAS018559: Deployed "teiid-dashboard-builder.war" (runtime-name : "teiid-dashboard-builder.war")
	00:16:54,959 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 28) JBAS018559: Deployed "integration-platform-console.war" (runtime-name : "integration-platform-console.war")
	00:16:54,963 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 51) JBAS018559: Deployed "teiid-odata-8.7.1.redhat-8.war" (runtime-name : "teiid-odata-8.7.1.redhat-8.war")
	00:16:54,963 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 50) JBAS018559: Deployed "modeshape-cmis.war" (runtime-name : "modeshape-cmis.war")
	00:16:54,963 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 50) JBAS018559: Deployed "modeshape-webdav.war" (runtime-name : "modeshape-webdav.war")
	00:16:54,977 INFO  [org.jboss.as.server] (ServerService Thread Pool -- 50) JBAS018559: Deployed "modeshape-rest.war" (runtime-name : "modeshape-rest.war")
	00:16:54,992 INFO  [org.jboss.as] (Controller Boot Thread) JBAS015961: Http management interface listening on http://127.0.0.1:9990/management
	00:16:54,993 INFO  [org.jboss.as] (Controller Boot Thread) JBAS015951: Admin console listening on http://127.0.0.1:9990
	00:16:54,993 INFO  [org.jboss.as] (Controller Boot Thread) JBAS015874: JBoss Red Hat JBoss Data Virtualization 6.1.0 (AS 7.4.3.Final-redhat-2) started in 111115ms - Started 934 of 976 services (105 services are lazy, passive or on-demand)
	```
2.  Lihat proses java dari JDV server dengan perintah `ps aux|grep java`. Anda akan mendapatkan proses seperti ini:

	```
	user1          34776   0.1  6.4  4404200 537408 s003  S+   12:15AM   2:12.16 /Library/Java/JavaVirtualMachines/jdk1.7.0_71.jdk/Contents/Home/bin/java -D[Standalone] -server -XX:+UseCompressedOops -verbose:gc -Xloggc:/Servers/DV_61/jboss-eap-6.3/standalone/log/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=5 -XX:GCLogFileSize=3M -XX:-TraceClassUnloading -Xms1302m -Xmx1302m -XX:MaxPermSize=256m -Djava.net.preferIPv4Stack=true -Djboss.modules.system.pkgs=org.jboss.byteman -Djava.awt.headless=true -Djboss.modules.policy-permissions=true -Dorg.jboss.boot.log.file=/Servers/DV_61/jboss-eap-6.3/standalone/log/server.log -Dlogging.configuration=file:/Servers/DV_61/jboss-eap-6.3/standalone/configuration/logging.properties -jar /Servers/DV_61/jboss-eap-6.3/jboss-modules.jar -mp /Servers/DV_61/jboss-eap-6.3/modules -jaxpmodule javax.xml.jaxp-provider org.jboss.as.standalone -Djboss.home.dir=/Servers/DV_61/jboss-eap-6.3 -Djboss.server.base.dir=/Servers/DV_61/jboss-eap-6.3/standalone
	```
	
3.  Akses Web Management Console dengan menggunakan browser [http://127.0.0.1:9990](http://127.0.0.1:9990)
	
	Gunakan username dan password yang anda spesifikasikan pada saat instalasi.

4.  Eksplorasi Management Console terutama bagian yang berkaitan konfigurasi JDV (Teiid)
   
    Anda bisa lihat pada [halaman screenshots](https://github.com/ejlp12/jboss-dv-workshop/issues/13), kemudian jawab pertanyaan-pertanyaan berikut:

    * Ada berapa datasources default dan apa fungsi masing-masing datasource tersebut?
    * Apa itu Infinispan? ada berapa Cache Container dan apa fungsi masing-masing?
    * Apa itu Teiid Translator? Lihat seluruh halaman tabel daftar translator, apa saja jenis physical source yang didukung JDV selain relational database (RDBMS)? 
    
      [Baca](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/appe-Configuration_Information.html#Supported_Data_Sources_and_Translators)
      
    * Apa fungsi Teiid Audit Log?
    * Ada berapa jenis transport yang didukung oleh JDV agar client application bisa terkoneksi ke JDV server?
    * Apa itu transport embedded?
    
5.  Akses JDV Dashboard dengan menggunakan browser []()
    Pastikan ada dapat login dengan username: `dashboardAdmin` dan password sesuai yang anda definisikan saat instalasi. Berikut adalah tampilan awal aplikasi Dashboard

	![image](https://cloud.githubusercontent.com/assets/3068071/7459511/b6c2549c-f2c6-11e4-90f4-bbece137f33a.png)
	
## Opsi Instalasi

Jawab pertanyaan berikut:

 *  Bagaimana anda akan menginstall JDV jika sistem operasi tidak memiliki fasilitas GUI, misalnya di Linux yang tidak memiliki xwindows client?
 
    [Baca](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/Installing_JBoss_Data_Virtualization_Using_Text_Based_Installer.html)

 *  Bagaimana anda bisa mempercepat instalasi tanpa perlu menjawab pertanyaan dalam tiap langkah instalasi?
    
    [Baca](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/chap-Installing_the_Product.html#Red_Hat_JBoss_Data_Virtualization_Installation_Methods)

	[Baca juga...](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/chap-Automated_Installation.html#Automated_Installation)

 *  Perlukah kita download S-RAMP Installer? Kapan kita memerlukannya?

    [Baca](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/The_S-RAMP_Installer.html)

    [Baca juga...](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Development_Guide_Volume_2_Governance/chap-Governance_Overview.html)

  
## Pengaturan Data Grid (Infinispan) Caching 

Berdasarkan [dokumentasi ini](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/chap-Installing_JBoss_Data_Grid_Caching.html#Configure_JBoss_Data_Grid_Adaptors), infinispan-cache dan infinispan-cache-dsl translators belum terkonfigurasi secara default, oleh karena itu kita perlu setup dengan cara menjalankan script JBoss CLI seperti berikut:

```
$ cd <DV_INSTALL_DIR>/jboss-eap-6.3/
$ ./bin/jboss-cli.sh -c --file=docs/teiid/datasources/infinispan/add-infinispan-cache-translator.cli
{"outcome" => "success"}
$ ./bin/jboss-cli.sh -c --file=docs/teiid/datasources/infinispan/add-infinispan-cache-dsl-translator.cli
{"outcome" => "success"}
```

## Instalasi dan pengaturan ODBC

Jika anda menginginkan suatu client application menggunakan ODBC untuk terkoneksi ke JDV maka anda perlu melakukan instalasi ODBC driver di mesin JDV. 

Di [section ini](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/chap-ODBC_Support.html) dijelaskan bagaimana melakukan instalasi dan pengaturan ODBC driver di mesin Linux, Windows atau Solaris.

## Penggunaan Database

JDV memerlukan database internal untuk komponen berikut: ModeShape,  Dashboard Builder dan fungsi command/audit logging.


## Instalasi dan konfigurasi untuk lingkungan Production

Untuk mempersiapkan JDV pada lingkungan Production, instalasi sederhana dan menjalankan JDV sebagai standalone server mungkin tidak cukup, jadi sebaiknya anda baca [3.1. Evaluating your architecture and your needs](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Installation_Guide/chap-Platform_requirements.html#Evaluating_your_architecture_and_your_needs)

### Port yang digunakan

Port yang digunakan JDV adalah [port standard JBoss EAP](https://access.redhat.com/documentation/en-US/JBoss_Enterprise_Application_Platform/6/html/Administration_and_Configuration_Guide/Network_Ports_Used_By_JBoss_Enterprise_Application_Platform_62.html), serta port 31000 (JDBC) & 35432 (ODBC)

[Referensi](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Administration_and_Configuration_Guide/Ports_Used_by_Red_Hat_JBoss_Data_Virtualization.html)

