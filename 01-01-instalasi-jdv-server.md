# Instalasi JBoss Data Virtualization 6.3 Server 

Berikut file-file yang diperlukan untuk installasi:

-  **jboss-dv-installer-6.3.0.jar** (File installer JDV versi 6.3.0) 
-  **jboss-eap-installer-6.4.0.zip** (File installer JBoss EAP versi 6.4.0)

File-file tersebut dapat didownload di:
  
   [http://developers.redhat.com/products/datavirt/download/](http://developers.redhat.com/products/datavirt/download/)

atau di 

   Customer Support Portal (CSP) at https://access.redhat.com/

   ![image](https://cloud.githubusercontent.com/assets/3068071/18037488/db7c88e2-6daf-11e6-8eca-d8f19762b20a.png)

- File installer EAP 6.4 yang dapat didownload di [http://developers.redhat.com/products/eap/download/](http://developers.redhat.com/products/eap/download/)

    dan juga file [EAP 6.4.9 roll up patch](https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=39353)

## Akses ke Dokumentasi Produk

Sebelum melakukan instalasi, mari kita liat dokumentasi yang tersedia untuk JDV:

1.  Buka halaman web berikut: [Red Hat JBoss Data Virtualization 6.3 Documentation](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/)
    
    Baca daftar dokumen yang tersedia disitu, dan identifikasi dokumen mana yang kira-kira perlu dibaca untuk proses instalasi.

2.  Klik dokumen [Getting Started Guide](https://access.redhat.com/documentation/en/red-hat-jboss-data-virtualization/6.3/paged/getting-started-guide/)

    Baca _Chapter 4.3. Installing JBoss Data Virtualization_, ikuti langkah-langkah dasar instalasi menggunakan GUI yang dijelaskan di halaman tersebut. Saat diminta menspesifikasikan direktori untuk instalasi, gunakan path yang mudah dan tidak terlalu panjang misalnya di `/home/jboss/JDV_63`

## Instalasi 

Cara instalasi JBoss Data Virtualization 6.3:

1. Instal EAP 6.4
   
   Bisa dilihat disini caranya: [lab0-instalasi-jboss-eap.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab0-instalasi-jboss-eap.md)

   Gunakan cara termudah yaitu dengan ekstrak file zip

2. **OPSIONAL** Instal patch EAP 6.4.9 (`jboss-eap-6.4.9-patch.zip`) 
   
   Bisa dilihat disini caranya: [lab5-patching.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab5-patching.md)

3. Instal JBoss DV 6.3 
   
   Untuk instalasi mode GUI, jalankan perintah berikut dari Terminal/Console menggunakan non-previledged user (bukan root):
    
    ```
    java -jar jboss-dv-installer-6.3.0.jar
    ```
    
   Jika ingin menggunakan mode console (tanpan GUI), gunakan perintah `java -jar jboss-dv-6.3.0-installer.jar -console`
   
   [Screenshot dari tiap langkah instalasi dapat dilihat disini] (https://github.com/ejlp12/jboss-dv-workshop/issues/2)
    
    > **Jika anda menginstal di sistem operasi Windows sebaiknya jalankan dari CMD prompt yang di-_run as_ Administrator**

4.  Baca dan ikuti sampai step 16 yang dijelaskan di dokumen tersebut.

## Dokumentasi JDV 6.3

Dokumentasi JDV versi 6.3 dapat diakses disini [https://access.redhat.com/documentation/en/red-hat-jboss-data-virtualization/?version=6.3](https://access.redhat.com/documentation/en/red-hat-jboss-data-virtualization/?version=6.3)


## Informasi tambahan 	

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
$ cd <DV_INSTALL_DIR>/jboss-eap-6.4/
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

Port yang digunakan JDV adalah [port standard JBoss EAP](https://access.redhat.com/documentation/en-US/JBoss_Enterprise_Application_Platform/6/html/Administration_and_Configuration_Guide/Network_Ports_Used_By_JBoss_Enterprise_Application_Platform_62.html), serta port **31000** (JDBC) & **35432** (ODBC)

[Referensi](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.1/html/Administration_and_Configuration_Guide/Ports_Used_by_Red_Hat_JBoss_Data_Virtualization.html)

