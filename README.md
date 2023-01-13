# opendata_bayern_download
Opendata Bayern Download Documentation

## Where to get an overview

https://geodaten.bayern.de/opengeodata/

## Use aria2 to download und update downloaded data

### Install aria2 (debian-based)

```
sudo apt install aria2
```

### Search your wanted data and get the URL to to meta4-File


Search your meta4-Link (looks like ```https://geodaten.bayern.de/[...].meta4```)
  * Click on the Map
  * Right-Click on **Download (Metalink)**
  * Copy URL to clipboard

### download the data

```
# create your target-datadir
mkdir /path/to/local_geodata/
# use aria2 to download data 
# 
aria2c -V --follow-metalink=mem --dir=/path/to/local_geodata/ <paste here your copied url>

```

example
```
aria2c -V --follow-metalink=mem --dir=/tmp https://geodaten.bayern.de/odd/a/lod2/citygml/meta/metalink/09276115.meta4
```



use:
  * ```--follow-metalink=mem``` not to write the meta4-file
  * ```-V``` to verify the downloaded data with the provided checksum
  * ```--dir=/path/to/lod_data/``` to save the data in this directory

### automate the update process

If data is updated by the data-provider, you can use the previous command to update your local data.
The provided parameters make aria2 to check if the remote data has changed and downloads only the updated data.





