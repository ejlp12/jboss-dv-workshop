
# Instalasi JDV versi 6.3

> Instalasi JDV versi 6.3 sedikit berbeda dengan instalasi versi 6.1, karena proses instalasi JBoss EAP dilakukan terpisah. Jadi ada dua kali proses instalasi.


 Release versi 6.3 ini memiliki beberapa fitur baru pada versi ini adalah:

* In-memory technologies for Big Data processing
 - Apache Spark
 - JDG as materialization target for JDV
 - SAP HANA
 - HPE Vertica
* Development and Deployment productivity
 - OData V4
 - OAuth using RH-SSO
 - Teiid Designer usability improvements
 - VDB Builder CLI (technical preview only)
* Big Data and Cloud data sources
 - Apache Cassandra
 - Apache HBase
 - Amazon RedShift
 - Apache Accumulo
 - Geospatial Support
 - OSIsoft PI (technical preview only)

[JDV 6.3 release notes](https://access.redhat.com/documentation/en/red-hat-jboss-data-virtualization/6.3/paged/release-notes/)

File yang dibutuhkan:

- File installer dapat didownload di [http://developers.redhat.com/products/datavirt/download/?referrer=jbd](http://developers.redhat.com/products/datavirt/download/?referrer=jbd) atau dari Customer Support Portal (CSP) at https://access.redhat.com/

   ![image](https://cloud.githubusercontent.com/assets/3068071/18037488/db7c88e2-6daf-11e6-8eca-d8f19762b20a.png)

- File installer EAP 6.4 yang dapat didownload di [http://developers.redhat.com/products/eap/download/](http://developers.redhat.com/products/eap/download/) dan juga file [EAP 6.4.9 roll up patch](https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=39353)

Dokumentasi JDV versi 6.3 dapat diakses disini [https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.2/index.html](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.2/index.html)

## Instalasi 

Cara instalasi JBoss Data Virtualization 6.3:

1. Instal EAP 6.4
   
   Bisa dilihat disini caranya: [lab0-instalasi-jboss-eap.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab0-instalasi-jboss-eap.md)

2. Instal patch EAP 6.4.9 (`jboss-eap-6.4.9-patch.zip`) 
   
   Bisa dilihat disini caranya: [lab5-patching.md](https://github.com/ejlp12/jboss-eap-workshop-site/blob/master/lab5-patching.md)

3. Instal JBoss DV 6.3 
   
    

## Instalasi JBDS - [Data Virtualization tooling (Teiid Designer)](http://teiiddesigner.jboss.org/designer_summary/downloads.html) 

Untuk development kita membutuhkan JBoss Developer Studio (JBDS) atau Eclipse.

Download JBDS 9.1.0 GA : [jboss-devstudio-9.1.0.GA-installer-standalone.jar](https://developers.redhat.com/download-manager/file/jboss-devstudio-9.1.0.GA-installer-standalone.jar)

Tambahan DV tooling lewar "JBoss Central" panel, pilih tab "Software/Updates" , klik checkbox opsi "JBoss Data Virtualization" lalu klik "Install/Update" button.

Anda juga dapat menginstal Teiid Designer 10.1.0 ke JBDS melalu update site berikut [http://download.jboss.org/jbosstools/updates/release/mars/integration-stack/teiiddesigner/10.1.0.Final/](http://download.jboss.org/jbosstools/updates/release/mars/integration-stack/teiiddesigner/10.1.0.Final/)
