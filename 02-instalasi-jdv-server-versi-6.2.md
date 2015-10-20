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

Cara instalasi JBoss Data Virtualization 6.2:

1. Instal EAP 6.4 
2. Instal patch EAP 6.4.3 (`jboss-eap-6.4.3-patch.zip`) 
3. Instal JBoss DV 6.2 

# Instalasi JBDS - Data Virtualization 6.2 tooling (Teiid Designer 9.0.3.Final) 

Download JBDS 8.1.0 : https://www.jboss.org/products/devstudio/download/

Add DV tooling via the JBoss Central panel select the Software/Updates tab, check JBoss Data Virtualization option and click the Install/Update button.

You could also install Teiid Designer 9.0.3 into an 8.0/8.1 version using this update site [https://devstudio.redhat.com/updates/8.0/](https://devstudio.redhat.com/updates/8.0/)