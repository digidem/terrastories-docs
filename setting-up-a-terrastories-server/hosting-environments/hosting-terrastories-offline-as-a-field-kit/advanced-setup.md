# Advanced Setup

## Use a custom offline map package

{% hint style="info" %}
If you already have a custom map style package, you can proceed. Skip this configuration if you are comfortable using the default maps. Or, [prepare your own map package](../../../operating-terrastories-offline/preparing-offline-map-packages.md) for offline use and come back.
{% endhint %}

Add your map package to the `map/data` folder. You can [prepare your own](../../../operating-terrastories-offline/preparing-offline-map-packages.md) or download our default map package [here](https://github.com/Terrastories/default-offline-map/). Your `map/data` folder structure should look like:

```

data/
├── fonts/
│   └── Font Name/
│       ├── font.pbf
│       └── ...
├── sprites/
│   ├── sprite.png
│   └── ...
├── tiles.pmtiles
├── style.json
└── config.json
```

{% hint style="info" %}
The three files that are absolutely required are `style.json`, `config.json`, and one or more tile sources (in `mbtiles` or `pmtiles` format). Fonts and sprites are only needed if your style is using them.&#x20;
{% endhint %}

Your style specification must include reference to the name of your style:

```json
{
  "sources": {
    "terrastories-map": { // This MUST be terrastories-map OR you MUST update the config.json file to reflect your chosen name
      "type": "vector", // or raster
      "url": "pmtiles://tiles.pmtiles" // or "mbtiles://tiles.mbtiles". If your tile filename has a different name instead of "tiles", then change that too.
    }
  },
  "sprite": "sprite", // optional, only needed if your style utilizes sprites by name
  "glyphs": "{fontstack}/{range}.pbf", // optional, only needed if your style utilizes fonts by name
  // the rest of your style specifications
}
```

For more information on custom maps, please see the Github repository [README.md](https://github.com/Terrastories/offline-field-kit/blob/main/map/README.md).

## Use a custom Tileserver

If you are already hosting your own Tileserver, update compose.yaml file to remove the tileserver service and update the TILESERVER\_URL to point to your hosted Tileserver:

```diff
  web:
    image: terrastories/terrastories:latest
    restart: unless-stopped
    depends_on:
      - db
    ports:
      - 80:3000
      - 3000:3000
    environment:
      - RAILS_ENV=offline
      - HOST_HOSTNAME=terrastories.local
-     - TILESERVER_URL=http://terrastories.local:8080/styles/terrastories-map/style.json
+     - TILESERVER_URL=http://localhost:8080/styles/terrastories-map/style.json
      - DATABASE_URL=postgresql://terrastories:terrastories@db:5432/terrastories
    volumes:
      - ./media:/media
      - ./import:/api/import/media

-  tileserver:
-    restart: unless-stopped
-    image: terrastories/terrastories-map:latest
-    ports:
-      - 8080:8080
```

## Set up a custom Hostname

In order to access your Terrastories instance, you'll need to configure a domain.&#x20;

{% hint style="danger" %}
Access via "localhost" is disabled for offline mode for security. You must set a custom hostname for domain access.
{% endhint %}

You can setup our default `terrastories.local`, but you may also setup your own.

First, update your /etc/hosts file (you will need root/sudo write access), and add the following line:

```
127.0.0.1 terrastories.local
```

Save and close.

{% hint style="info" %}
Replace `terrastories.local` with your desired host name.
{% endhint %}

If you utilized a custom domain (not terrastories.local), update your `compose.yaml` file:

```diff
  web:
    image: terrastories/terrastories:latest
    restart: unless-stopped
    depends_on:
      - db
    ports:
      - 80:3000
      - 3000:3000
    environment:
      - RAILS_ENV=offline
-      - HOST_HOSTNAME=terrastories.local
+      - HOST_HOSTNAME=your-custom-domain.local
-     - TILESERVER_URL=http://terrastories.local:8080/styles/terrastories-map/style.json
+     - TILESERVER_URL=http://your-custom-domain.local:8080/styles/terrastories-map/style.json
      - DATABASE_URL=postgresql://terrastories:terrastories@db:5432/terrastories
    volumes:
      - ./media:/media
      - ./import:/api/import/media
```
