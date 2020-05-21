# r.accumulate-iterative

This GRASS GIS addon is the iterative version of [`r.accumulate`](https://github.com/OSGeo/grass-addons/tree/master/grass7/raster/r.accumulate). It will be integrated into `r.accumulate` and deprecate [`r.lfp`](https://github.com/OSGeo/grass-addons/tree/master/grass7/raster/r.lfp) soon.

## Test data

* [`create_test_location.sh`](https://isnew.info/data/lfp/create_test_location.sh)
* [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip) (5.3 GB)
* [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip) (397 MB)

### How to create a test GRASS GIS location

1. Download [`create_test_location.sh`](https://isnew.info/data/lfp/create_test_location.sh), [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip) and [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip) in the same directory
2. Run `grass79`
   ```bash
   grass79 -c test --exec ./create_test_location.sh
   ```
