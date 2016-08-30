[PREVIEW-DataVirtWebUI-11Jun2015.war] (http://downloads.jboss.org/datavirt/6.1.0/PREVIEW-DataVirtWebUI-11Jun2015.war)

[Installation README file](http://downloads.jboss.org/datavirt/install.txt):

1) Install DV61

2) After installing DV61, give the teiidUser the odata and rest roles. The user must have these roles to access the `rest` and `odata` endpoints.
The roles file is `<SERVER_DIR>/standalone/configuration/application-roles.properties`

The teiid user will look like this:
teiidUser=user,odata,rest

3) download the war and copy it into `<SERVER_DIR>/standalone/deployments`

4) access the app at `localhost:8080/dv-ui`

   login with admin/admin

## UPDATE:

Baca dahulu halaman ini [Data Service Builder](http://teiiddesigner.jboss.org/ds_builder_summary.html) sebagai pengenalan tentang apa itu Data Service Builder.

Data Services Builder, adalah alat berbasis web untuk menedit, mengelola dan melakukan test data services terhadap data anda lewat JDV (Teiid runtime framework).

Untuk download tool dan cara instalasi bisa dibaca dihalaman ini [https://developer.jboss.org/wiki/GettingStartedWithDataServicesBuilder](https://developer.jboss.org/wiki/GettingStartedWithDataServicesBuilder) - 287MB


Download [http://download.jboss.org/teiid/web/dsbuilder/DataserviceBuilder-07152016-install.zip](http://download.jboss.org/teiid/web/dsbuilder/DataserviceBuilder-07152016-install.zip)


