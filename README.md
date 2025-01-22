# BayernAtlas mit Parzellarkarte / ohne Login / kostenfrei

https://atlas.bayern.de/?c=642082,5419253&z=8&r=0&l=tk,luftbild_parz&t=ba

* Parzellen
* Grundstücke
* Luftbild mit Grundstücksgrenzen


# Download

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

Just put the command from above into your crontab


# TL;DR

## Commands to download all data

### 3D Buildings LOD-2
Format: CITYGML  
EPSG : 25832  
Tile-Size: 2km x 2km

:warning:  Download-Size: about 150 GB
```
aria2c -V --dir=/data/on_big_hdd/lod2/ https://geodaten.bayern.de/odd/a/lod2/citygml/meta/metalink/09.meta4
```

### DEM - Resolution 1m
Format: GeoTiff  
EPSG : 25832  
Tile-Size: 1km x 1km

:warning:  Download-Size: about 240 GB
```
aria2c -V --dir=/data/on_big_hdd/dem/ https://geodaten.bayern.de/odd/a/dgm/dgm1/meta/metalink/09.meta4
```

### Ortho-Photo Resolution 40cm
Format : GeoTiff (RGB)  
EPSG : 25832  
Tile-Size: 1km x 1km 

:warning:  :warning:  :warning: Download-Size: about 1,2 **TB** == 1200 GB
```
for i in 1 2 3 4 5 6 7
do
  aria2c -V --dir=/data/on_big_hdd/dop/ https://geodaten.bayern.de/odd/a/dop40/meta/metalink/09${i}.meta4
done
```
