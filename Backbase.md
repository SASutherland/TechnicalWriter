# Import/export command line tool

The **import/export command line tool** can be used to output the model, resources, and Content Services items of an object. Both portals and catalog items can be exported, including:

- master pages
- containers
- widgets
- Structured Content Items

The contents of the exported file depend on whether it belongs to the **Enterprise Catalog** or **Portal Catalog**.

To use the importer tool, run the following command from the class path. You need to specify the path to the archive you are importing from (**-a**), indicate the URL of the server performing the import or export (**-s**), and provide credentials (**-u, -p**):

```
java -jar {importertoolfilename} {command} -a {path/archivefilename.zip} -s {serverurl} -u {username} 
-p {password} -P {portalname1,portalname2}
```

All parameters are necessary, except **-P**, which can be used to import the item directly into a list of portals. Multiple portals can be listed and separated by a comma. Batch operations are not available, so the import will add a single item to the catalog and each of the specified portals. The command only works if all required parameters are given, in any order.

> **_NOTE:_** This can only be executed by an admin, so you will need credentials for an admin account.

**For example**, if you want to import a widget package, and your export output archive is *Widget-StateLinkWidget-1.zip*, enter: 

`-a C:/Temp/Widget-StateLinkWidget-1.zip.`

When exporting, you need to include: 
- the **-i parameter**, which specifies the name of the item to export.
- the **-f parameter**, which defines the name of the export file and where it will be written in the FileSystem (FS). 

The expected extensions for exported files are: 
- **.zip** for archives (in all export commands except, `export-portal-model`).
- **.xml** for the `export-portal-model` command.

### Import/export commands

|Command               |Description                      |
|:---------------------|:--------------------------------|
|`import-archive`      | imports an archive (the archive can contain any of the elements you can export) |
|`import-portal-model` | imports a portal XML model |
|`export-portal`       | exports the portal with content |
|`export-portal-model` | exports the model XML of the portal |
|`export-page`         | exports a master page |
|`export-widget`       | exports a widget |
|`export-layout`       | exports a layout or container |
