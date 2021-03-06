# r.accumulate-iterative

This GRASS GIS addon is the iterative version of [`r.accumulate -r`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html). It is already integrated into [`r.accumulate`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html) as the default algorithm (`-r` flag for the recursive version) and deprecated [`r.lfp`](https://grass.osgeo.org/grass78/manuals/addons/r.lfp.html).

## Dear the reviewers of ENVSOFT_2020_505

For some reason, Mendeley's data upload did not work successfully and [my dataset page](https://data.mendeley.com/datasets/4zv566xmvw/draft?a=914c7442-264c-4002-ace8-1bb0426c38d8) lists no data files at all. Sorry for the inconvenience. Please use the following files for your review:
* [`create_test_location.sh`](https://data.isnew.info/lfp/create_test_location.sh)
* [`grassdata.zip`](https://data.isnew.info/lfp/grassdata.zip) (5.3 GB)
* [`analysis.zip`](https://data.isnew.info/lfp/analysis.zip) (397 MB)

## How to create a test GRASS GIS location

System requirements: [GRASS GIS 7.8.3](https://grass.osgeo.org/) on Linux; this addon was not tested on Windows

1. Download [`create_test_location.sh`](https://isnew.info/data/lfp/create_test_location.sh), [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip), and [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip) in the same directory
2. Unzip [`grassdata.zip`](https://isnew.info/data/lfp/grassdata.zip) and [`analysis.zip`](https://isnew.info/data/lfp/analysis.zip)
3. Run `grass78`
   ```bash
   grass78 -c test --exec ./create_test_location.sh
   ```

Five mapsets and 1,616 maps will be created in the test location:
1. `PERMANENT`: Not used
2. `lfp-GA-input`: Input rasters and vectors for Georgia (305 maps)
3. `lfp-GA-hdd`: Results for Georgia from the Linux HDD system (202 maps); you will have access to the maps in `lfp-GA-input`
4. `lfp-GA-ssd`: Results for Georgia from the Linux SSD system (202 maps); you will have access to the maps in `lfp-GA-input`
5. `lfp-GA-archydropro`: Results for Georgia from the Windows system (101 maps); you will have access to the maps in `lfp-GA-input`
6. `lfp-TX-input`: Input rasters and vectors for Texas (305 maps)
7. `lfp-TX-hdd`: Results for Texas from the Linux HDD system (200 maps); you will have access to the maps in `lfp-TX-input`
8. `lfp-TX-ssd`: Results for Texas from the Linux SSD system (200 maps); you will have access to the maps in `lfp-TX-input`
9. `lfp-TX-archydropro`: Results for Texas from the Windows system (101 maps); you will have access to the maps in `lfp-TX-input`

## Maps

Both Georgia and Texas analyses used the same map names except for the following close-to-raw input maps:
* `lfp-GA-input` mapset
  * `ned_1_ga`: USGS National Elevation Dataset (NED) raster for Georgia (not clipped to the boundary)
  * `statep010_ga`: Mask raster for Georgia (clipped to the boundary)
* `lfp-TX-input` mapset
  * `ned_1_tx`: USGS NED raster for Texas (not clipped to the boundary)
  * `statep010_tx`: Mask raster for Texas (clipped to the boundary)

Inputs in the `lfp-*-input` mapset
* `drain`: Flow direction raster created by [`r.watershed`](https://grass.osgeo.org/grass78/manuals/r.watershed.html)
* `accum`: Flow accumulation raster created by [`r.accumulate`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html), but it is only an intermediate output and not needed
* `outlets100`: 100 random outlet points vector for the batch experiment
* `outlets100_1` through `outlets100_100`: The same 100 outlets, but each point individually in one vector map for the non-batch experiment
* `basins100_subbasin_1` through `basins100_subbasin_100`: Each subwatershed in an individual raster map for masking
* `basins100_archydropro_1` through `basins100_archydropro_100`: Each subwatershed in an individual vector map for setting the computational region; the above 100 subbasin rasters have the extent of the entire state

Outputs in both `lfp-*-hdd` and `lfp-*-ssd` mapsets
* `lfp100_recursive`: 100 longest flow paths generated by [`r.accumulate -r`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html) from the batch mode experiment
  * Missing in the Texas mapsets because [`r.accumulate -r`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html) failed
* `lfp100_recursive_1` through `lfp100_recursive_100`: 100 individual longest flow paths generated by [`r.accumulate -r`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html) from the non-batch mode experiment
  * `lfp100_recursive_51` is missing in the Texas mapsets because [`r.accumulate -r`](https://grass.osgeo.org/grass78/manuals/addons/r.accumulate.html) failed
* `lfp100_iterative`: 100 longest flow paths generated by this `r.accumulate-iterative` module
* `lfp100_iterative_1` through `lfp100_iterative_100`: 100 individual longest flow paths generated by this `r.accumulate-iterative` module

Outputs in the `lfp-*-archydropro` mapset; imported from ArcGIS Pro geodatabases
* `lfp100_archydropro`: 100 longest flow paths generated by the Longest Flow Path tool in the Arc Hydro toolbox for ArcGIS Pro
* `lfp100_archydropro_1` through `lfp100_archydropro_100`: 100 individual longest flow paths generated by the Longest Flow Path tool
