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
    
5.  Akses JDV Dashboard dengan menggunakan browser pada alamat URL ini: [http://localhost:8080/dashboard/](http://localhost:8080/dashboard/)

    Pastikan ada dapat login dengan username: `dashboardAdmin` dan password sesuai yang anda definisikan saat instalasi. Berikut adalah tampilan awal aplikasi Dashboard

	![image](https://cloud.githubusercontent.com/assets/3068071/7459511/b6c2549c-f2c6-11e4-90f4-bbece137f33a.png)
