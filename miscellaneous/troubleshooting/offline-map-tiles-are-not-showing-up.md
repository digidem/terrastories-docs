# Offline map tiles are not showing up

It may happen that when you have set up Terrastories for an offline environment ("Field Kit" or mesh) that your offline map tiles are not showing up on the Terrastories map.

Typically, there are three reasons for this:

1. **You are still connected to the internet and have not provided a Mapbox access token.** Currently, the map libraries that we are using (even for offline) are in part reliant on Mapbox, and Mapbox GL JS requires that you provide an access token even if the map content is not being provisioned by their servers. This can be resolved by either providing a Mapbox access token in your `.env` file, or by disconnecting the device from the internet. We hope to resolve this very soon by switching to a full MapLibre setup for offline maps.
2. **Your map tiles cover a small area, and you are not sufficiently centered, and zoomed in, on that area.** Many map tilesets start at zoom level 0, which is the whole world; hence, when you zoom out on Terrastories, you should start to see some tiles, and as you zoom in, you can see where the area that your tileset covers is located. However, some map tilesets may start at a much higher zoom level and are therefore hard to find on the map. To resolve this, we recommend setting a Zoom Level and Center coordinates, along with Map Bounds to avoid the user from traveling far away from your tiles. (You might need to get the coordinates for these from the source who created the map tiles, or use a tool like [Mapbox Location Helper](https://demos.mapbox.com/location-helper/) to figure them out.) See [modifying-map-settings.md](../../using-terrastories/using-the-terrastories-member-dashboard/modifying-map-settings.md "mention") for more.
3. **Your map tiles are not properly defined in your style.json file**. The `mbtiles` file must be defined in the `sources` array, and you must have layers which place and style your data (raster or vector) within the `layers` array. See [preparing-offline-maps.md](../../setting-up-a-terrastories-server/preparing-offline-maps.md "mention") for more.

{% hint style="info" %}
Still having issues? Access the console in your browser's developer tools to see if there are any errors. If you need help interpreting these, please see [support.md](../support.md "mention") for ways to get help.
{% endhint %}
