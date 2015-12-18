# JDV: Mengamankan SOAP Web Service yang diekspos JDV

> Langkah demi langkah cara penggunaan dapat dilihat pada gambar di bawah (di bagian comments).

Mengamankan Web Service dengan _authentication_ untuk mengakses View Model yang ada di JDV ada dua cara (opsi) yaitu:

* Menggunakan HTTPBasic
  
  Saat menggunakan opsi ini, JDV akan mevalidasi user dan password sesuai *security realm* dan *role* yang kita tentukan.  Jika anda tidak membuat security realm baru, JDV memiliki default value yaitu **teiid-security**. 
  
  When using HTTPBasic, a local Teiid connection using the PassthroughAuthentication property is required.
  

* Menggunakan WS-Security (Username Token)

  Sebuah **password callback class** akan dibuat didalam file WAR. File tersebut yang memiliki method untuk  validasi nilai username/password. Secara default code di Java class tersebut adalah sesuai dengan nilai (username dan password) yang anda masukan pada jendela dialog di tab "WS-Security Opstions". Hal tersebut hanya untuk keperluan test, untuk keperluan _production_, anda harus mengimplementasikan sendiri mekanisme security pada class tersebut.


Referensi: [12.4.2.2. Generating a JBossWS-CXF War](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_Data_Virtualization/6.2/html/User_Guide_Volume_1_Teiid_Designer/sect-Web_Services_Modeling.html#Create_Web_Service_Action)

## Tutorial

### Menggunakan HTTP Basic Authentication

1. Pada tab "General" pilih HTTPBasic:

   ![image](https://cloud.githubusercontent.com/assets/3068071/11561323/31228b10-99f9-11e5-9a3d-f047a1275b35.png)

2. Pilih tab "HTTPBasic Options", isi nilai "Realm" dengan `teiid-security` dan "Role" dengan `user` atau role lain yang anda inginkan.

   ![image](https://cloud.githubusercontent.com/assets/3068071/11562721/64e403e4-9a02-11e5-94ba-ba31efb0d09d.png)

3. Pastikan telah diisi "VDB JNDI Name" sesuai dari JNDI dari VDB yang sudah dideploy, klik OK

4. Deloy WAR file 

5. Test menggunakan SoapUI. Saat anda membuat project baru dan memasukan WSDL URL di SoapUI, anda akan diminta memasukan username dan password.

6. Saat anda mencoba memanggil operasi Web Service, maka akan didapati error **401 Unauthorized** seperti ini

   ![image](https://cloud.githubusercontent.com/assets/3068071/11563154/08bd2b42-9a05-11e5-82f7-a7648a282a3b.png)

   hal tersebut karena anda belum men-set HTTP Basic Auth di Request yang dikirimkan oleh SoapUI, set seperti berikut lalu coba sekali lagi. Sekarang seharusnya anda berhasil menerima response jika username dan passwordnya benar:

   ![image](https://cloud.githubusercontent.com/assets/3068071/11563272/ba3fe67a-9a05-11e5-8380-dd96d15ec536.png)


### Menggunakan WS-Security

1.  Pada tab "General" pilih "WS-Security (Username Token)"

   ![image](https://cloud.githubusercontent.com/assets/3068071/11562862/2d4b8848-9a03-11e5-9fe1-16ff3aa2c61a.png)

2. Klik tab "WS-Security Options" dan masukan "username" dan "password" yang digunakan untuk **test** saja.

   Anda perlu mengganti kode dari sebuah Java class untuk membuat cara authenticasi anda sendiri.

   ![image](https://cloud.githubusercontent.com/assets/3068071/11564161/51d7d340-9a0a-11e5-83c0-72bc32538082.png)

3. Rename atau copy file WAR yang dihasilkan menjadi file ber-extension ".ZIP" kemudian ekstrak

    Buka folder hasil ekstraksi, anda masuk ke folder `<VDB_NAME>/WEB-INF/classes/org/teiid/soap/wsse/`

    Buka file `UsernamePasswordCallback.java` dan edit method `handle()` sesuai dengan cara authentication yang anda inginkan.
   

   ```java
	package org.teiid.soap.wsse;

	import java.io.IOException;

	import javax.security.auth.callback.Callback;
	import javax.security.auth.callback.CallbackHandler;
	import javax.security.auth.callback.UnsupportedCallbackException;
	import org.apache.ws.security.WSPasswordCallback;;

	public class UsernamePasswordCallback implements CallbackHandler {

		
		/*
		 * This class should be updated to use implementation specific authentication. it is
		 * not recommended to use for production as-is.
		 * @see javax.security.auth.callback.CallbackHandler#handle(javax.security.auth.callback.Callback[])
		 */
		public void handle(Callback[] callbacks) throws IOException,
				UnsupportedCallbackException {
			WSPasswordCallback pc = (WSPasswordCallback) callbacks[0];
			if (!("testUser".equals(pc.getIdentifier()) && "Passw0rd!".equals(pc //$NON-NLS-1$ //$NON-NLS-2$
					.getPassword())))
				throw new SecurityException("User '" + pc.getIdentifier() //$NON-NLS-1$
						+ "' with password '" + pc.getPassword() + "' not allowed.");  //$NON-NLS-1$//$NON-NLS-2$

		}
	}
      ```

   Authentication menggunakan code yang digenerate diatas akan menghasilkan error karena `pc.getPassword()` akan selalu menghasilkan `null`


   Jadi kode diatas setidaknya perlu diubah seperti ini:

   ```java
	package org.teiid.soap.wsse;

	import java.io.IOException;

	import javax.security.auth.callback.Callback;
	import javax.security.auth.callback.CallbackHandler;
	import javax.security.auth.callback.UnsupportedCallbackException;
	import org.apache.ws.security.WSPasswordCallback;

	public class UsernamePasswordCallback implements CallbackHandler {


	    /*
	     * This class should be updated to use implementation specific authentication. it is
	     * not recommended to use for production as-is.
	     * @see javax.security.auth.callback.CallbackHandler#handle(javax.security.auth.callback.Callback[])
	     */
	    public void handle(Callback[] callbacks) throws IOException,
	            UnsupportedCallbackException {
	        WSPasswordCallback pc = (WSPasswordCallback) callbacks[0];
	        if ( "testUser".equals(pc.getIdentifier()) ) {	
	        	pc.setPassword("Passw0rd!");
	        	return; 
	        } else {
	        	throw new SecurityException("User '" + pc.getIdentifier()  + "' with password '" + pc.getPassword() + "' not allowed."); 
	        }
	        
	    }
	}
   ```

   Untuk meng-compile code tersebut, diperlukan library wss4j, berikut Maven dependency yang diperlukan

   ```xml
       <dependencies>
	    <dependency>
	        <groupId>org.apache.ws.security</groupId>
	        <artifactId>wss4j</artifactId>
	        <version>1.6.17</version>
	    </dependency>
	</dependencies>
   ```
    Setelah itu compile dan build and package lagi menjadi WAR untuk dideploy.

4. Test menggunakan SoapUI

   Buat WS-Security configuration pada project:

   ![image](https://cloud.githubusercontent.com/assets/3068071/11573065/e1109bc4-9a36-11e5-90ea-1c356f87faa4.png)

   
5. Jika saat memanggil web service mendapatkan error mesage: 

   ```
   JBWEB000064: Error report
   JBWEB000071: root cause java.lang.NoClassDefFoundError: org/apache/ws/security/WSPasswordCallback
   ```

   Mungkin anda perlu menambahkan file didalam WAR `WEB-INF/jboss-deployment-structure.xml` yang isinya:

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure>
    <deployment>
        <dependencies>
            <module name="org.apache.ws.security"/>
        </dependencies>
    </deployment>
   </jboss-deployment-structure>
   ```

Buat directory `WEB-INF` dan simpan file `jboss-deployment-structure.xml`

```
jar -uvf  GENERATED_FILE.war WEB-INF/*
```

6. Deploy WAR file 

![image](https://cloud.githubusercontent.com/assets/3068071/11705428/488d398e-9f22-11e5-8cb1-99d4828549d0.png)


7. Buat project di SoapUI untuk test web service yang sudah di-deploy

   * Import WSDL URL 
   * Klik dua kali SoapUI project yang baru dibuat
   * Setting __Outgoing WS-Security Configuration__
      ![image](https://cloud.githubusercontent.com/assets/3068071/11705444/6d70610e-9f22-11e5-9013-53758acce5e6.png)

   * Setting request   
      ![image](https://cloud.githubusercontent.com/assets/3068071/11705611/c833dd40-9f23-11e5-8696-c2df1eeaabd5.png)

   Request HTTP yang dikirim akan seperti ini:
   ```
	POST /csv_vdb/poc_pajak_csv_FACT_PENERIMAAN_MANUAL HTTP/1.1
	Accept-Encoding: gzip,deflate
	Content-Type: text/xml;charset=UTF-8
	SOAPAction: "getFACT_PENERIMAAN_MANUAL"
	Content-Length: 653
	Host: localhost:8080
	Connection: Keep-Alive
	User-Agent: Apache-HttpClient/4.1.1 (java 1.5)

	<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
	   <soapenv:Header>
	   	<wsse:Security xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" 
	   		           xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
	   		<wsse:UsernameToken wsu:Id="UsernameToken-1BF36278E094E98176144971549600327">
	   			<wsse:Username>testUser</wsse:Username>
	   			<wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">Passw0rd!</wsse:Password>
	   		</wsse:UsernameToken>
	   	</wsse:Security>
	   </soapenv:Header>
	   <soapenv:Body/>
	</soapenv:Envelope>

   ```
