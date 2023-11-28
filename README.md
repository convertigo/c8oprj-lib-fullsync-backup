# lib_FullSyncImportExport #

This project performs backup or restore of Convertigo Fullsync Databases.\
It is aimed for Cloud or Docker Convertigo Server.\
It is based on Daniele Bailo's [**couchdb-dump**](https://github.com/danielebailo/couchdb-dump) bash script.\
The project must be deployed on the target Convertigo Server.

## Studio Installation

1. In your Convertigo Studio use `File->Import->Convertigo->Convertigo Project` and hit the `Next` button
2. In the dialog `Project remote URL` field, paste the text below:
   <table>
     <tr><td>Usage</td><td>Click the copy button</td></tr>
     <tr><td>To contribute</td><td>

     ```
     lib_FullSyncImportExport=https://github.com/convertigo/c8oprj-lib-fullsync-backup.git:branch=7.9.0
     ```
     </td></tr>
     <tr><td>To simply use</td><td>

     ```
     lib_FullSyncImportExport=https://github.com/convertigo/c8oprj-lib-fullsync-backup/archive/7.9.0.zip
     ```
     </td></tr>
    </table>
3. Click the `Finish` button. This will automatically import the __lib_FullSyncGrp__ project

## Server Installation

Deploy project from project context menu 'Deploy' in Studio or deploy project from PROJECTS widget in Administration console.

## Sequences

### FS_backup

It performs a backup of the given Fullsync database name.

- Variables:
    - *cdb_name* (Name of the Fullsync database to backup - String)
    - *cdb_gz* (Compress (.gz) the Fullsync database backup file: 1|true - String)
    - *reset_db_folder* (Deletes the fs backup folder before making a new fs backup file: 1|true - String)

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

### FS_backup_all

It performs a backup of all the present Fullsync databases.

- Variables:
    - *cdb_gz* (Compress (.gz) the Fullsync database backup file: 1|true - String)

No direct download.
All backup files are stored in the backup folder.
You can have the files list using the **FS_get_db_folder** sequence.

### FS_restore

It restores a backup file and creates a Fullsync database given its name.\
The file can be an **application/json** or **application/x-gzip** type.

- Variables:
    - *cdb_name* (Name of the Fullsync database to create - String)
    - *cdb_file* (File path of the Fullsync database backup - Input file)

If **cdb_name** Fullsync Database already exists on Convertigo Server, it is first deleted then recreated or else it creates a new Fullsync Database name.

### FS_reset_db_folder

It deletes the Fullsync databases backup folder

### FS_get_db_folder

It gets the file names of the Fullsync databases backup folder