# Assignment 3 
## Layers used 
| Layer name | Source | Type and Projection | Relevance | 
|---|---|---|---|
| Spanish ministry grid for species occurrences | [Downloadable shapefile: MITECO](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/biodiversidad/especies-art17-2013_2018.html) | `.shp` | Grid containing occurrences and density of the topillo in Castilla y León | 
| CSV file for cell_code count | [Google sheets](https://docs.google.com/spreadsheets/d/1la7yCrGHUMVWK_n7XQdQ2ZyWhc4d_XerHGkyip7sMl4/edit?gid=1555256628#gid=1555256628) | `.csv` | Count for microtus arvalis and locations | 
| Precipitation for 1970-1979, 2000-2009, and 2020-2021 | [Downloadable tif file](https://www.worldclim.org/data/monthlywth.html) | `.tif` | Minimum and Maximum temperatures in °C, and Total precipitation in mm at 2.5 minutes resolution. Will use it to see climatic variability to relate it to increased favourable conditions for development of the topillo | 


## Tools used 
| N | Tool | Explanation | Processing history | 
|---|---|---|---|
| 1 | Delete duplicate gemotries |  Removes identical data layered on top of each other | ```processing.run("native:deleteduplicategeometries", {'INPUT':'C:/Users/localuser/Documents/GIS data/MITECO grid occurrences/ESArt17_EspeciesDistrib.shp','OUTPUT':'ogr:dbname=\'C:/Users/localuser/Documents/GIS data/clean_grid_occurrences.gpkg\' table="Clean grid Occurrences" (geom)'}) ``` | 
| 2 | Join attributes by location | Joins data from two layers that intersect based on their location | ```processing.run("native:joinattributesbylocation", {'INPUT':'C:/Users/localuser/Documents/GIS data/clean_grid_occurrences.gpkg\|layername=Clean grid Occurrences','PREDICATE':[0],'JOIN':'C:/Users/localuser/Documents/GISdata/microtus_arvalis_whole.gpkg\|layername=points_from_table','JOIN_FIELDS'['fid','scientificName','locality','stateProvince','day','month','year'],'METHOD':0,'DISCARD_NONMATCHING':False,'PREFIX':'','OUTPUT':'ogr:dbname=\'C:/Users/localuser/Documents/GIS data/join microtusGbif X mitecoGrid.gpkg\' table="joined_GbifPointsXMitecoGrid" (geom)'}) ``` | 
| 3 | Join attributes by field value | Joins matching attributes cell_code from Clean grid and Count CSV file | ```processing.run("native:joinattributestable", {'INPUT':'C:/Users/localuser/Documents/GIS data/clean_grid_occurrences.gpkg\|layername=Clean grid Occurrences','FIELD':'cell_code_','INPUT_2':'C:/Users/localuser/Documents/GIS data/MITECO grid occurrences/A3_microtus_countGrid - Pivot Table 1.csv','FIELD_2':'cell_code_','FIELDS_TO_COPY':[],'METHOD':1,'DISCARD_NONMATCHING':False,'PREFIX':'','OUTPUT':'ogr:dbname=\'C:/Users/localuser/Documents/GIS data/grid_microtus_occurrences_counts.gpkg\' table="grid_ma_count" (geom)'}) ``` |
| 4 |  | 
| 5 |  | 
| 6 |  | 
## Google sheets 
`Ctrl+C` attribute table ,`Ctrl+V` in Google sheets, `Insert pivot table`, after filtering, export as `.csv` file and upload to GIS for 3, Delete layer from 2
| Rows | Count | 
|---|---|
| cell_code | Filter: blank cells for scientific name | 
