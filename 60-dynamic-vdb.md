### Create Data Source
Open JBoss EAP Administrator Console

Configuration > Connector > Data Source, [Add]

Name: `jdvworkshop`
JNDI Name: `java:/jdvworkshop`

JDBC Driver: `h2`

Connection URL: `jdbc:h2:tcp://localhost:19091/Servers/h2-data`
Username: `sa`
Password: <BLANK>
Security DOmain: <BLANK>

Test Connection -> Done

### Create VDB

Books.vdb
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<vdb name="Quickstart" version="1">
 
    <description>A Dynamic VDB</description>
    <property name="UseConnectorMetadata" value="true" />
    <model name="Books">
  
        <property name="importer.useFullSchemaName" value="false"/>
        <source name="jdbc-connector" translator-name="h2" connection-jndi-name="java:/jdvworkshop"/>
    </model>
</vdb>
```
