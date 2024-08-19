# README

## Quick Start

Donwload Shapefile from [here](https://www.dgterritorio.gov.pt/download/agt/) and put it on a folder called `data`.

Start composition:

* `docker compose up -d`

Load data:

* `docker run --network=vtiles-postgis_bridge1 -v "${PWD}/data:/mnt" ghcr.io/osgeo/gdal:ubuntu-full-3.8.4 \
ogr2ogr -a_srs "EPSG:3763" -t_srs "EPSG:4326" -f "PostgreSQL" PG:"dbname='db' user='postgres'  host='db'" /mnt/CRUS+_31_julho2024.shp -lco GEOMETRY_NAME=geom -lco FID=OBJECTID -lco precision=NO -lco SPATIAL_INDEX=GIST \
-nlt PROMOTE_TO_MULTI -nln crus_31_julho2024 -overwrite`

Restart docker compose:

* `docker compose restart`

Open [html file](./demo-oat.htm)

comment/uncomment the martin and pg_tileserv code. View the benchmarking results in the console of the developer tools.
