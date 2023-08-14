# Preparing offline maps

{% hint style="warning" %}
This page may require some technical knowledge about geospatial data. If the content of this page feels unfamiliar to you, get someone acquainted with geographic information systems (GIS) to help you.
{% endhint %}

For offline or mesh network usage, Terrastories can load a background map using an open-source map tileserver called TileServer-GL and locally hosted map tiles, instead of a map from Mapbox. This requires you to provide your own locally hosted map tiles.

Terrastories does provide a default set of open-license offline map tiles, generated through the [OpenMapTiles API](https://openmaptiles.org/). These tiles cover the entire world, but are only compiled up to zoom level 8 (roughly the extent of a small country like Rwanda, Costa Rica, Slovenia or Bhutan). Once you zoom in past zoom level 8, no further level of detail will show.

When you set up Terrastories for [hosting-terrastories-offline-as-a-field-kit.md](hosting-environments/hosting-terrastories-offline-as-a-field-kit.md "mention") or [hosting-terrastories-on-a-mesh-network.md](hosting-environments/hosting-terrastories-on-a-mesh-network.md "mention"), you will be given the option to use these default offline map tiles. However, you can also provide your own map tiles, which have to be in a [`mbtiles` format](https://docs.mapbox.com/help/glossary/mbtiles/), and provided alongside any map fonts, sprites, and a `style.json` file where the `mbtiles` file is placed on a map canvas.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Our setup script, which detects if you already have a <code>style.json</code> file in your <code>tileserver/data</code> directory, and if not, downloads the default offline tiles for you.</p></figcaption></figure>

### **How to generate or convert MBTiles**

`MBTiles` can be generated from standard geospatial data (Shapefile, GeoJSON) in several ways.

* The open-source GIS software QGIS has several tools for generating `MBTiles` in both raster and vector format. `Generate XYZ tiles (MBTiles)` can be used to create raster tiles of all of the content on your map canvas; this may also include XYZ Tiles from services such as OpenStreetMap, Bing, and Google Satellite. `Generate Vector Tiles (MBTiles)` can be used to create vector tiles from one or more vector layers. You can then further style these vector tiles in your `style.json` file.
  * The page [Generating map files in .mbtiles format for the experimental Background Maps feature](https://docs.mapeo.app/complete-reference-guide/customization-options/custom-base-maps/creating-custom-maps/creating-mbtiles) in the Mapeo support materials has a visual, step-by-step guide for using QGIS to generate raster tiles.
* There is also a command line tool called `tippecanoe` which can be used to generate vector `MBTiles` from Esri Shapefiles and other formats: [guide](https://docs.mapbox.com/help/troubleshooting/large-data-tippecanoe/).
* If you already have tiles in a different format (such as `xyz`), you can use a Node command line tool called `mbutil` to convert them to `MBTiles`. Please see our [xyz to mbtiles conversion repository](https://github.com/digidem/xyz-mbtiles-conversion) or this page [Generating map files in .mbtiles format for the experimental Background Maps feature](https://docs.mapeo.app/complete-reference-guide/customization-options/custom-base-maps/creating-custom-maps/creating-mbtiles) in the Mapeo support materials for more information.

### **Defining your** `MBTiles` **source in** `config.json`**.**

Once generated, place the `MBTiles` in the `tileserver/data/mbtiles/` directory.&#x20;

The source for the `MBTiles` to be used in your map style is defined in `tileserver/data/config.json`. If your `MBTiles` is not called `tiles.mbtiles` , you will need to change the filename here:

```
  "data": {
    "terrastories-map": {
      "mbtiles": "mbtiles/tiles.mbtiles"
    }
```

### **Working with custom styles (**`style.json`**)**

Map styles (per the `style.json` schema) defines the visual appearance of a map: what data to draw on the map canvas, the order in which layers are displayed, and how to style the data when drawing it. Mapbox provides a helpful [guide](https://docs.mapbox.com/mapbox-gl-js/style-spec/) with all of the possible style parameters, but it's generally useful to download an existing `style.json` file and modify it to suit your needs.&#x20;

One of the easiest ways to build a `style.json` file is by uploading and styling your data on [Mapbox Studio](http://mapbox.com/studio) and downloading the `style.json` file from there, in the following way:

* Design your map in Mapbox Studio. Mapbox provides extensive documentation and tutorials on using Studio [here](https://docs.mapbox.com/studio-manual/guides/).
* When you are done designing your map in the Mapbox Studio environment, click "Share" and then download the Map style ZIP file.
* Unzip the file, and extract the `style.json` and place it in `tileserver/data/styles`.
* Next, you will need to make some changes. The `style.json` from Mapbox will be referring to an online URL for the map sources. You need to change this to refer to the local `MBTiles`. Change `sources` > `composite` > `url` to the following format: `"url": "mbtiles://mbtiles/name.mbtiles"`. (Here, `name` is just an example; it can be called whatever you want, so long as the filename is the same.)

Importantly, the layer names referenced in `styles` and `MBTiles` have to match, in order for the tiles to receive a style property. It may be necessary to edit the layer names in `style.json` to reflect the names of the spatial data in the `MBTiles` file.

{% hint style="info" %}
Note: it is also possible to use [Maputnik](https://maputnik.github.io/), the open-source visual editor for the Mapbox style specification, to style your `MBTiles`data.
{% endhint %}

_**Raster tiles**_: If you have raster tiles that you want to load in Terrastories, those will need to defined differently from the vector tiles above. In `sources`, create a new source definition with `url` pointing to the raster `MBTiles` in the same format as above, `type` set to `raster`, and `tileSize` to `256`. Then, in `layers`, create a map object with your `id` of choice, `type` set to `raster`, and `source` set to the name of your raster tiles as defined in `sources`. Here is an example `style.json` file which only loads a raster `MBTiles`:

```
{
  "version": 8,
  "name": "Terrastories offline raster map",
  "sources": {
    "terrastories-raster-mbtiles": {
      "type": "raster",
      "url": "mbtiles://{terrastories-map}",
      "tileSize": 256
    }
  },
  "sprite": "sprite",
  "glyphs": "{fontstack}/{range}.pbf",
  "layers": [
    {
      "id": "background",
      "type": "background",
      "paint": {"background-color": "hsl(47, 26%, 88%)"}
    },
    {
      "id": "terrastories-raster-mbtiles",
      "type": "raster",
      "source": "terrastories-raster-mbtiles"
    }
  ],
  "id": "basic"
}

```

If you want, you can add additional `mbtiles` sources (vector as well as raster), and place your raster tile layer underneath vector layers. This is a good way to have an offline satellite imagery basemap with vector data (points, lines, polygons, and labels) overlaid on top of it.

