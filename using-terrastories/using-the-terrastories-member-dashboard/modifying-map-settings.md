# Modifying map settings

{% hint style="info" %}
Customizing map settings requires `admin` access. If you are logged in as an `editor`, `member`, or `viewer`, you will not be able to access this settings menu.
{% endhint %}

The Terrastories map settings offer a set of controls for the background map behavior and default settings.

Currently, the map settings are accessed in the **Theme** view; in the future, we may move these into their own section.

Access the **Theme** view in the Terrastories member dashboard (as an `admin` user), and scroll down to Map Settings.

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-27 144550.jpg" alt=""><figcaption></figcaption></figure>

The Map Settings can be set either by manually entering values, or by interacting with the map on the **Theme** view. These are the different options available to you:

* **Map bounds**: the boundaries of the map which determine the extent to where you can scroll. This can be useful if you want to keep your community users focused on one geography. (This is particularly helpful for offline Terrastories servers with map tiles available only in a small part of the world, resulting in a blank map view elsewhere). By default, map bounds are deactivated; you must first toggle _Allow unrestricted bounds_ to be able to set them.
* **Map center**: a latitude / longitude coordinate that determines the default starting position of your map.
* **Zoom level**: a zoom level determines how much of the world is visible on a map. Map zoom levels begin with 0 being the lowest zoom level (fully zoomed out) and 22 being the highest (fully zoomed in). At low zoom levels, a small set of map tiles covers a large geographical area. At higher zoom levels, a larger number of tiles cover a smaller geographical area.
* **Pitch degree:** the camera's pitch is the visual tilt of the map, which is determined by the angle towards the horizon measured in degrees. A pitch of 0 results in a two-dimensional map, as if your line of sight forms a perpendicular angle with the earth's surface, while a greater value like 60 looks ahead towards the horizon.
* **Bearing degree:** a bearing is the direction you’re facing, measured clockwise as an angle from true north on a compass. This can also be called a heading. In this system, north is 0, east is 90, south is 180, and west is 270. For the map, the bearing rotates the map around its center the specified number of degrees.
* **Set projection for map:** A map projection is a way to flatten the planet's surface onto a page or screen. Every projection has strengths and weaknesses, so the right projection depends on your use case. To learn more about the available map projections in Terrastories, visit Mapbox's [guide to projections](https://docs.mapbox.com/mapbox-gl-js/guides/projections/).

{% hint style="success" %}
If you are not able to use the inset map on the Map Settings block of the Theme view to set center, zoom and other properties, and have access to the internet, you could use Mapbox's [Location Helper](https://demos.mapbox.com/location-helper/) tool instead.\
\
This may be helpful if you are trying to set up offline map tiles, but your map is blank because you are not zoomed in enough on the right area for them to show up.
{% endhint %}

If you are setting up a map for a community in an online environment, you will see some additional options for Online Map Configuration.

* **Mapbox Style URL**: the Mapbox URL for the online Mapbox map that you want to use. This could be one of Mapbox's [default public styles](https://docs.mapbox.com/api/maps/styles/), or your own custom Mapbox map.
* **Mapbox Access Token**: a Mapbox access token to be used to validate your style. If you are supplying a custom style, it must be an access token that specifically has permission to access your style. To learn more about access tokens, see this [Mapbox guide](https://docs.mapbox.com/help/getting-started/access-tokens/).
* **Activate 3D Terrain view**: Mapbox provides a 3D Terrain service for any of their online maps to render the landscape in 3D. This can be a very nice feature for topographically device geographies. Be mindful that there is a tradeoff with performance, because the Terrain data takes some additional time to load. It is worthwhile to test the 3D Terrain view via the location most of your users will be accessing Terrastories, to ensure it makes sense to activate this feature for your users.

{% hint style="info" %}
If you do not see the Online Map Configuration options, then you are working with Terrastories set up for an offline or mesh environment. See [Broken link](broken-reference "mention") for more details.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-27 144638 (1).jpg" alt=""><figcaption></figcaption></figure>

