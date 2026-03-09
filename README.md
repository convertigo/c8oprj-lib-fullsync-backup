


# lib_FullSyncImportExport

This project performs backup or restore of Convertigo Fullsync Databases.\
It is aimed for Cloud or Docker Convertigo Server.\
It is based on Daniele Bailo's [**couchdb-dump**](https://github.com/danielebailo/couchdb-dump) bash script.\
The project must be deployed on the target Convertigo Server.


For more technical informations : [documentation](./project.md)

- [Installation](#installation)
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


## Sequences

### FS_backup

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_gz</td><td></td>
</tr>
<tr>
<td>cdb_name</td><td></td>
</tr>
<tr>
<td>reset_db_folder</td><td></td>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### FS_backup_all

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_gz</td><td></td>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### FS_get_db_folder

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### FS_reset_db_folder

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>reset_db_folder</td><td></td>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### FS_restore

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>cdb_file</td><td></td>
</tr>
<tr>
<td>cdb_name</td><td></td>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### getProperties

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
</table>

### ungzip

**variables**

<table>
<tr>
<th>name</th><th>comment</th>
</tr>
<tr>
<td>secret</td><td></td>
</tr>
<tr>
<td>sourceFile</td><td></td>
</tr>
<tr>
<td>targetFile</td><td></td>
</tr>
</table>


