# Exclusion of solar panel areas in Segovia 
1. Exporting the selected feature of Segovia as a geopackage
2. Clipping solar exclusion with Segovia province
```python
print(instruction) #MISSING INSTRUCTIONS FROM GIS
```
3. Dissolve the solar exclusion in Segovia
```python
print(instruction) #MISSING INSTRUCTIONS FROM GIS
```
=> manually made permanent with the name `solarSegoDissolve.gpkg`



# Assignment 2

## Clipping 
### Clip raster by mask → bio1 points and sego limit
```Input parameters:
{ 'ALPHA_BAND' : False, 'CROP_TO_CUTLINE' : True, 'DATA_TYPE' : 0, 'EXTRA' : '', 'INPUT' : 'C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif', 'KEEP_RESOLUTION' : False, 'MASK' : 'C:/Users/localuser/Documents/GIS data/prov_cyl_recintos.gpkg|layername=prov_cyl_recintos', 'MULTITHREADING' : False, 'NODATA' : None, 'OPTIONS' : '', 'OUTPUT' : 'TEMPORARY_OUTPUT', 'SET_RESOLUTION' : False, 'SOURCE_CRS' : None, 'TARGET_CRS' : None, 'TARGET_EXTENT' : None, 'X_RESOLUTION' : None, 'Y_RESOLUTION' : None }
GDAL command:
gdalwarp -overwrite -of GTiff -cutline "C:/Users/localuser/Documents/GIS data/prov_cyl_recintos.gpkg" -cl prov_cyl_recintos -crop_to_cutline "C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif" C:/Users/localuser/AppData/Local/Temp/processing_hEyvbr/b5000b865e5e4a2f99e8693c4c395975/OUTPUT.tif
GDAL command output:
Warning 1: GPKG: unrecognized user_version=0x00000000 (0) on 'C:/Users/localuser/Documents/GIS data/prov_cyl_recintos.gpkg'
Creating output file that is 635P x 378L.
 Using internal nodata values (e.g. -3.4e+38) for image C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif.
 Copying nodata values from source C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif to destination C:/Users/localuser/AppData/Local/Temp/processing_hEyvbr/b5000b865e5e4a2f99e8693c4c395975/OUTPUT.tif.
 Processing C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif [1/1] : 0...10...20...30...40...50...60...70...80...90...100 - done.
```

### SEGO CLIP + bioclim  
```Input parameters:
{ 'ALPHA_BAND' : False, 'CROP_TO_CUTLINE' : True, 'DATA_TYPE' : 0, 'EXTRA' : '', 'INPUT' : 'C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif', 'KEEP_RESOLUTION' : False, 'MASK' : 'C:/Users/localuser/Documents/GIS data/sg_province.gpkg|layername=prov_cyl_recintos', 'MULTITHREADING' : False, 'NODATA' : None, 'OPTIONS' : '', 'OUTPUT' : 'C:/Users/localuser/Documents/GIS data/SG clipped by mask layer.tif', 'SET_RESOLUTION' : False, 'SOURCE_CRS' : None, 'TARGET_CRS' : None, 'TARGET_EXTENT' : None, 'X_RESOLUTION' : None, 'Y_RESOLUTION' : None }
GDAL command:
gdalwarp -overwrite -of GTiff -cutline "C:/Users/localuser/Documents/GIS data/sg_province.gpkg" -cl prov_cyl_recintos -crop_to_cutline "C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif" "C:/Users/localuser/Documents/GIS data/SG clipped by mask layer.tif"
GDAL command output:
Creating output file that is 181P x 114L.
Using internal nodata values (e.g. -3.4e+38) for image C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif.
Copying nodata values from source C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif to destination C:/Users/localuser/Documents/GIS data/SG clipped by mask layer.tif.
 Processing C:/Users/localuser/Documents/GIS data/worldclim_Data/spainwc2.1_30s_bio_1.tif [1/1] : 0...10...20...30...40...50...60...70...80...90...100 - done.
Process completed successfully
Execution completed in 0.27 seconds
Results:
{'OUTPUT': 'C:/Users/localuser/Documents/GIS data/SG clipped by mask layer.tif'}```

### Clip vector by mask layer → cattle trails and sego limit
```Input parameters:
{ 'INPUT' : 'C:\\Users\\localuser\\Documents\\GIS data\\znie_cyl_vvpp_ejes.gpkg|layername=znie_cyl_vvpp_ejes', 'MASK' : 'C:/Users/localuser/Documents/GIS data/sg_province.gpkg|layername=prov_cyl_recintos', 'OPTIONS' : '', 'OUTPUT' : 'C:/Users/localuser/Documents/GIS data/vias_pecuarias_sego.gpkg' }
GDAL command:
ogr2ogr -clipsrc "C:/Users/localuser/Documents/GIS data/sg_province.gpkg" -clipsrclayer prov_cyl_recintos "C:/Users/localuser/Documents/GIS data/vias_pecuarias_sego.gpkg" "C:\\Users\\localuser\\Documents\\GIS data\\znie_cyl_vvpp_ejes.gpkg" znie_cyl_vvpp_ejes -f "GPKG"
GDAL command output:
Warning 1: GPKG: unrecognized user_version=0x00000000 (0) on 'C:\\Users\\localuser\\Documents\\GIS data\\znie_cyl_vvpp_ejes.gpkg'
Warning 1: A geometry of type LINESTRING is inserted into layer znie_cyl_vvpp_ejes of geometry type MULTILINESTRING, which is not normally allowed by the GeoPackage specification, but the driver will however do it. To create a conformant GeoPackage, if using ogr2ogr, the -nlt option can be used to override the layer geometry type. This warning will no longer be emitted for this combination of layer and feature geometry type.
Process completed successfully
Execution completed in 1.06 seconds
Results:
{'OUTPUT': 'C:/Users/localuser/Documents/GIS data/vias_pecuarias_sego.gpkg'}```

### Corrected 
```processing.run("gdal:clipvectorbypolygon", {'INPUT':'C:/Users/localuser/Documents/GIS data/m_arvalis_bio1.gpkg|layername=bio1','MASK':'C:/Users/localuser/Documents/GIS data/sg_province.gpkg|layername=prov_cyl_recintos','OPTIONS':'','OUTPUT':'C:/Users/localuser/Documents/GIS data/SG_bio_clip_V.gpkg'})```


### Materia forestal de producción 
```Input parameters:
{ 'INPUT' : '/vsizip/C:\\Users\\localuser\\Downloads\\am.especies_cyl_mfr.zip/am.especies_cyl_mfr.shp|layername=am.especies_cyl_mfr', 'MASK' : 'C:/Users/localuser/Documents/GIS data/sg_province.gpkg|layername=prov_cyl_recintos', 'OPTIONS' : '', 'OUTPUT' : 'C:/Users/localuser/Documents/GIS data/prod_forestal_sego.gpkg' }
GDAL command:
ogr2ogr -clipsrc "C:/Users/localuser/Documents/GIS data/sg_province.gpkg" -clipsrclayer prov_cyl_recintos "C:/Users/localuser/Documents/GIS data/prod_forestal_sego.gpkg" /vsizip/C:\Users\localuser\Downloads\am.especies_cyl_mfr.zip/am.especies_cyl_mfr.shp am.especies_cyl_mfr -f "GPKG"
GDAL command output:
Warning 1: A geometry of type MULTIPOLYGON is inserted into layer am.especies_cyl_mfr of geometry type POLYGON, which is not normally allowed by the GeoPackage specification, but the driver will however do it. To create a conformant GeoPackage, if using ogr2ogr, the -nlt option can be used to override the layer geometry type. This warning will no longer be emitted for this combination of layer and feature geometry type.
Process completed successfully
Execution completed in 0.96 seconds
Results:
{'OUTPUT': 'C:/Users/localuser/Documents/GIS data/prod_forestal_sego.gpkg'}
Loading resulting layers
Algorithm 'Clip vector by mask layer' finished```

## Buffers
### Select within distance → biopoints and rivers
```processing.run("native:selectwithindistance", {'INPUT':'C:/Users/localuser/Documents/GIS data/SG_bio_clip_V.gpkg','REFERENCE':'sego_rivers.gpkg|layername=clipped_mask','DISTANCE':10,'METHOD':0})```

### Buffer → cattle trails
```Input parameters:
{ 'DISSOLVE' : False, 'DISTANCE' : 10, 'END_CAP_STYLE' : 0, 'INPUT' : 'C:/Users/localuser/Documents/GIS data/vias_pecuarias_sego.gpkg', 'JOIN_STYLE' : 0, 'MITER_LIMIT' : 2, 'OUTPUT' : 'TEMPORARY_OUTPUT', 'SEGMENTS' : 5, 'SEPARATE_DISJOINT' : False }
Execution completed in 0.36 seconds
Results:
{'OUTPUT': 'Buffered_7c7ddb58_0111_4825_9ecf_2e7f5db5f5cd'}
Loading resulting layers
Algorithm 'Buffer' finished```
