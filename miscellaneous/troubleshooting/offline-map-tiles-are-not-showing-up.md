# Offline map tiles are not showing up

It may happen that when you have set up Terrastories for an offline environment ("Field Kit" or mesh) that your offline map tiles are not showing up on the Terrastories map.

Typically, there are two reasons for this:

1. **Your map tiles are not properly defined in your style.json file**. The `mbtiles` or `pmtiles` file must be defined in the `sources` array, and you must have layers which place and style your data (raster or vector) within the `layers` array. See [preparing-offline-map-packages.md](../../operating-terrastories-offline/preparing-offline-map-packages.md "mention") for more.
2. **Your map tiles cover a small area, and you are not sufficiently centered, and zoomed in, on that area.** Many map tilesets start at zoom level 0, which is the whole world; hence, when you zoom out on Terrastories, you should start to see some tiles, and as you zoom in, you can see where the area that your tileset covers is located. However, some map tilesets may start at a much higher zoom level and are therefore hard to find on the map. To resolve this, we recommend setting a Zoom Level and Center coordinates, along with Map Bounds to avoid the user from traveling far away from your tiles. (You might need to get the coordinates for these from the source who created the map tiles, or use a tool like [Mapbox Location Helper](https://demos.mapbox.com/location-helper/) to figure them out.) See [modifying-map-settings.md](../../using-terrastories/using-the-terrastories-member-dashboard/modifying-map-settings.md "mention") for more.

{% hint style="info" %}
Still having issues? Access the console in your browser's developer tools to see if there are any errors. If you need help interpreting these, please see [support.md](../support.md "mention") for ways to get help.
{% endhint %}
