# Instalasi JDV versi 6.2

> Instalasi JDV versi 6.2 sedikit berbeda dengan instalasi versi 6.1, karena proses instalasi JBoss EAP dilakukan terpisah. Jadi ada dua proses instalasi.


Minor release ini tidak difokuskan untuk penambahan fitur baru tapi lebih ditekankan pada dukungan terhadap Java 1.8 atau EAP 6.4. Beberapa kapabilitas baru pada versi ini adalah:

- Mendukung EAP 6.4 
- Peningkatan (improvement) pada Teiid Designer usability 
- Kerberos passthrough for Cloudera, Oracle and MS SQL Server

File yang dibutuhkan:

- File installer dapat didownload di [http://www.jboss.org/products/datavirt/download](http://www.jboss.org/products/datavirt/download) atau dari Customer Support Portal (CSP) at https://access.redhat.com/

   ![image](https://cloud.githubusercontent.com/assets/3068071/10267525/fd71006e-6ac1-11e5-8a26-a6329cc1e786.png)

- File installer EAP 6.4 yang dapat didownload di [http://www.jboss.org/products/eap/download/](http://www.jboss.org/products/eap/download/) dan juga file [EAP 6.4.3 roll up patch](https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=39353)

Dokumentasi JDV versi 6.2 dapat diakses disini [https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.2/index.html](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.2/index.html)

## Instalasi 

Cara instalasi JBoss Data Virtualization 6.2:

1. Instal EAP 6.4
   
   Bisa dilihat disini caranya: [lab0-instalasi-jboss-eap.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab0-instalasi-jboss-eap.md)

2. Instal patch EAP 6.4.3 (`jboss-eap-6.4.3-patch.zip`) 
   
   Bisa dilihat disini caranya: [lab5-patching.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab5-patching.md)

3. Instal JBoss DV 6.2 

## Instalasi JBDS - Data Virtualization 6.2 tooling (Teiid Designer 9.0.3.Final) 

Untuk development kita membutuhkan JBoss Developer Studio (JBDS) atau Eclipse.

Download JBDS 8.1.0 : https://www.jboss.org/products/devstudio/download/

Tambahan DV tooling lewar "JBoss Central" panel, pilih tab "Software/Updates" , klik cekbox opsi "JBoss Data Virtualization" lalu klik "Install/Update" button.

Anda juga dapat menginstal Teiid Designer 9.0.3 ke JBDS melalu update site berikut [https://devstudio.redhat.com/9.0/stable/updates/](https://devstudio.redhat.com/9.0/stable/updates/)
