# MapProxy cache the online map tiles to the local machine
[MapProxy官网](https://mapproxy.org/ "MapProxy官网")

install MapProxy

```bash
pip install MapProxy

```
pyproj should not be too high, it is the version 1.9.6 could be worked well
```bash
pip install pyproj
```
Clone the project.
```bash
git clone https://github.com/yangdengxian/mymapproxy.git
```
run the project by these yaml config files, such as gaode.yaml.

```bash
cd mymapproxy/gaode
mapproxy-util serve-develop gaode_normal.yaml

```

view the website in your browser.

[http://127.0.0.1:8080/demo](http://127.0.0.1:8080/demo)




### osm config demo
```yaml
services:
    demo:
    tms:
        use_grid_names: true
        # origin for /tiles service
        origin: 'nw'
    kml:
        use_grid_names: true
    wmts:
    wms:
        md:
            title: MapProxy WMS Proxy
            abstract: This is a minimal MapProxy example.

layers:
    - name: osm
      title: OSM in UTM
      sources: [osm_cache]

caches:
    osm_cache:
        grids: [utm32n]
        meta_size: [4, 4]
        sources: [osm_cache_in]

    osm_cache_in:
        grids: [GLOBAL_WEBMERCATOR]
        disable_storage: true
        sources: [osm_source]

sources:
    osm_source:
        type: tile
        grid: GLOBAL_WEBMERCATOR
        url: http://a.tile.openstreetmap.org/%(z)s/%(x)s/%(y)s.png

grids:
    utm32n:
        srs: 'EPSG:25832'
        bbox: [4, 46, 16, 56]
        bbox_srs: 'EPSG:4326'
        origin: 'nw'
        min_res: 5700
```
