# Assignment 3 
## Layers used 
| Layer name | Source | Type | Relevance | 
|---|---|---|---|
| Spanish ministry grid for species occurrences | [Downloadable shapefile: MITECO](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/biodiversidad/especies-art17-2013_2018.html) | `.shp | Grid containing | 

## Tools used 
| Tool | Explanation | Processing history | 
|---|---|---|
| Delete duplicate gemotries |  Removes identical data layered on top of each other | ```processing.run("native:deleteduplicategeometries", {'INPUT':'C:/Users/localuser/Documents/GIS data/MITECO grid occurrences/ESArt17_EspeciesDistrib.shp','OUTPUT':'ogr:dbname=\'C:/Users/localuser/Documents/GIS data/clean_grid_occurrences.gpkg\' table="Clean grid Occurrences" (geom)'}) ``` | 
| Join attributes by location | Joins data from two layers that intersect based on their location | ```processing.run("native:joinattributesbylocation", {'INPUT':'C:/Users/localuser/Documents/GIS data/clean_grid_occurrences.gpkg\|layername=Clean grid Occurrences','PREDICATE':[0],'JOIN':'C:/Users/localuser/Documents/GISdata/microtus_arvalis_whole.gpkg\|layername=points_from_table','JOIN_FIELDS'['fid','scientificName','locality','stateProvince','day','month','year'],'METHOD':0,'DISCARD_NONMATCHING':False,'PREFIX':'','OUTPUT':'ogr:dbname=\'C:/Users/localuser/Documents/GIS data/join microtusGbif X mitecoGrid.gpkg\' table="joined_GbifPointsXMitecoGrid" (geom)'}) ``` | 
