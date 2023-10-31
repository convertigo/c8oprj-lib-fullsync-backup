# lib_FullSyncImportExport #

This project performs backup or restore of Convertigo Fullsync Databases.\
It is aimed for Cloud or Docker Convertigo Server.\
It is based on Daniele Bailo's [**couchdb-dump**](https://github.com/danielebailo/couchdb-dump) bash script.\
The project must be deployed on the target Convertigo Server.

## Studio Installation

Download lib_FullSyncImportExport.car file and import it from menu File > Import... > Convertigo > Convertigo project

## Server Installation

Deploy project from project context menu 'Deploy' in Studio or deploy project lib_FullSyncImportExport.car file from PROJECTS widget in Administration console.

## Sequences

### FS_backup

It performs a backup of the given Fullsync database name.

- Variables:
    - *cdb_name* (Name of the Fullsync database to backup - String)
    - *cdb_gz* (Compress (.gz) the Fullsync database backup file: 1|true - String)

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

It restores a backup file and creates a Fullsync database given its name.\
The file can be an **application/json** or **application/x-gzip** type.

- Variables:
    - *cdb_name* (Name of the Fullsync database to create - String)
    - *cdb_file* (File path of the Fullsync database backup - Input file)

If **cdb_name** Fullsync Database already exists on Convertigo Server, it is first deleted then recreated or else it creates a new Fullsync Database name.

### FS_reset_db_folder

It deletes the Fullsync databases backup folder