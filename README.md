# lib_FullSyncImportExport #

This project performs backup or restore of Convertigo Fullsync Databases.\
It is aimed for Cloud or Docker Convertigo Server.\
It is based on Daniele Bailo's [**couchdb-dump**](https://github.com/danielebailo/couchdb-dump) bash script.\
The project must be deployed on the target Convertigo Server.

### FS_backup

It performs a backup of the given Fullsync database name.

- Variables:
    - *cdb_name* (Name of the Fullsync database to backup - String)

**.pxml** requester : You will get an XML response with an attachment element that can be used as a Source for other Convertigo sequences:

```xml
<isSuccess>true</isSuccess>
<attachment content-type="application/octet-stream" local-url="/workspace/projects/lib_FullSyncImportExport/dbs/<cdb_name>_backup.json" name="<cdb_name>_backup.json" type="attachment"/>
```
In case the backup fails, it will return the following:
```xml
<isSuccess>false</isSuccess>
<error>couchdb-dump error message</error>
```

**.bin** requester : This will instruct the client to directly download file (Content-Type : "application/octet-stream")

### FS_restore

It restores a backup file and creates a Fullsync database given its name.

- Variables:
    - *cdb_name* (Name of the Fullsync database to create - String)
    - *cdb_file* (File path of the Fullsync database backup - Input file)

If **cdb_name** Fullsync Database already exists on Convertigo Server, it is first deleted then recreated or else it creates a new Fullsync Database name.