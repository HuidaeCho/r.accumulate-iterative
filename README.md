# r.accumulate-iterative

This GRASS GIS addon is the iterative version of [`r.accumulate`](https://github.com/OSGeo/grass-addons/tree/master/grass7/raster/r.accumulate). It will be integrated into `r.accumulate` and deprecate [`r.lfp`](https://github.com/OSGeo/grass-addons/tree/master/grass7/raster/r.lfp) soon.

## Dear Reviewers of ENVSOFT_2020_505

For some reason, Mendeley's data upload did not work successfully and [my dataset page](https://data.mendeley.com/datasets/4zv566xmvw/draft?a=914c7442-264c-4002-ace8-1bb0426c38d8) lists no data files. Sorry for the inconvenience. Please use the following files for your review:
* [`create_test_location.sh`](https://isnew.info/data/lfp/create_test_location.sh)
* [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip) (5.3 GB)
* [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip) (397 MB)

## How to create a test GRASS GIS location

System requirements: [GRASS GIS 7.8.3](https://grass.osgeo.org/) on Linux; this addon was not tested on Windows

1. Download [`create_test_location.sh`](https://isnew.info/data/lfp/create_test_location.sh), [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip), and [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip) in the same directory
2. Unzip [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip) and [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip)
3. Run `grass78`
   ```bash
   grass78 -c test --exec ./create_test_location.sh
   ```

It will create five mapsets in the test location:
1. `PERMANENT`: Not used
2. `lfp-GA-hdd`: All input rasters and vectors for Georgia and results from the Linux HDD system reside in this mapset; the `lfp-GA-ssd` mapset will have access to these maps
3. `lfp-GA-ssd`: Results from the Linux SSD and Windows systems; in addition, you will have access to the maps in `lfp-GA-hdd` from this mapset
4. `lfp-TX-hdd`: Similar to `lfp-GA-hhd`, all input maps for Texas and results from the Linux HDD system are stored in this mapset
5. `lfp-TX-ssd`: Results from the Linux SSD and Windows systems; again, you will have access to the maps in `lfp-TX-hdd` from here
