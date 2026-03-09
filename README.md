


# lib_FullSyncImportExport

This project performs backup or restore of Convertigo Fullsync Databases.\
It is aimed for Cloud or Docker Convertigo Server.\
It is based on Daniele Bailo's [**couchdb-dump**](https://github.com/danielebailo/couchdb-dump) bash script.\
The project must be deployed on the target Convertigo Server.


For more technical informations : [documentation](./project.md)

- [Installation](#installation)
- [Secret Symbol](#secret-symbol)
- [Sequences](#sequences)
    - [FS_backup](#fs_backup)
    - [FS_backup_all](#fs_backup_all)
    - [FS_get_db_folder](#fs_get_db_folder)
    - [FS_reset_db_folder](#fs_reset_db_folder)
    - [FS_restore](#fs_restore)
    - [getProperties](#getproperties)
    - [ungzip](#ungzip)


## Installation

1. In your Convertigo Studio click on ![](https://github.com/convertigo/convertigo/blob/develop/eclipse-plugin-studio/icons/studio/project_import.gif?raw=true "Import a project in treeview") to import a project in the treeview
2. In the import wizard

   ![](https://github.com/convertigo/convertigo/blob/develop/eclipse-plugin-studio/tomcat/webapps/convertigo/templates/ftl/project_import_wzd.png?raw=true "Import Project")
   
   paste the text below into the `Project remote URL` field:
   <table>
     <tr><td>Usage</td><td>Click the copy button at the end of the line</td></tr>
     <tr><td>To contribute</td><td>

     ```
     lib_FullSyncImportExport=https://github.com/convertigo/c8oprj-lib-fullsync-backup.git:branch=8.0.0.0
     ```
     </td></tr>
     <tr><td>To simply use</td><td>

     ```
     lib_FullSyncImportExport=https://github.com/convertigo/c8oprj-lib-fullsync-backup/archive/8.0.0.0.zip
     ```
     </td></tr>
    </table>
3. Click the `Finish` button. This will automatically import the __lib_FullSyncImportExport__ project


## Secret Symbol

The project expects a secret project symbol named <code>${lib_FullSyncImportExport.secretkey.secret}</code> on the target Convertigo server.
Each sequence also exposes a request variable named <code>secret</code>.
At runtime, the received variable is compared with the symbol value.
If the value is missing or invalid, the sequence returns a <code>403 Forbidden</code> error structure.
Internal sequence calls already propagate the <code>secret</code> variable automatically.


## Sequences

### FS_backup

Creates a backup file for one FullSync database and can optionally compress it as .gz.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_gz</td><td>Set to 1 or true to create a compressed .gz backup file.</td>
</tr>
<tr>
<td>cdb_name</td><td>Name of the FullSync database to back up.</td>
</tr>
<tr>
<td>reset_db_folder</td><td>Set to 1 or true to clear the backup folder before creating the new backup.</td>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### FS_backup_all

Backs up all available FullSync databases into the server backup folder.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_gz</td><td>Set to 1 or true to create compressed .gz backup files.</td>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### FS_get_db_folder

Lists the backup files currently available in the backup folder.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### FS_reset_db_folder

Clears and recreates the backup folder before a new backup run.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>reset_db_folder</td><td>Set to 1 or true to delete and recreate the backup folder.</td>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### FS_restore

Restores one FullSync database from a JSON or GZip backup file.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_file</td><td>Uploaded backup file to restore, in JSON or GZip format.</td>
</tr>
<tr>
<td>cdb_name</td><td>Name of the FullSync database to restore.</td>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### getProperties

Loads the FullSync/CouchDB server settings from Convertigo server properties and stores them in HTTP session.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
</table>

### ungzip

Detects whether an input file is already JSON or GZip and decompresses it when required.

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td>Secret value that must match the lib_FullSyncImportExport.secretkey.secret project symbol.</td>
</tr>
<tr>
<td>sourceFile</td><td>Source backup file path, in JSON or GZip format.</td>
</tr>
<tr>
<td>targetFile</td><td>Target JSON file path used when the source file must be decompressed.</td>
</tr>
</table>


