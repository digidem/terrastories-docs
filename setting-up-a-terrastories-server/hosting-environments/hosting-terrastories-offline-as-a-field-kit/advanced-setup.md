# Advanced Setup

If you're familiar with Docker and Compose, or want to use custom maps or an existing database, you'll want to follow this advanced setup guide.

## Prerequisites

* **Install Docker:** To install Terrastories, your operating system first has to have Docker installed. The current version of Docker being used to deploy Terrastories as of December 2022 is v20.10.12.
* **Install Docker Compose**: You also need Docker Compose v2 - v1 will not work with our Docker files. The current version of Docker Compose being used to deploy Terrastories as of December 2022 is v2.3.3

## Manual Setup

Clone the repository locally to your computer. (Or, you can download the offline field kit as a ZIP file from [our Github repository](https://github.com/terrastories/offline-field-kit) to get the application.)

Once you have everything downloaded, update the configuration desired below:

### Custom Map Package

{% hint style="info" %}
If you already have a custom map style package, you can proceed. Skip this configuration if you are comfortable using the default maps. Or, [prepare your own map style](../../../operating-terrastories-offline/preparing-offline-maps.md) for offline use and come back.
{% endhint %}

Create the necessary `tileserver` directory and `data` subdirectory and add your map package to the `tileserver/data` folder. You can [prepare your own](../../../operating-terrastories-offline/preparing-offline-maps.md) or download our default map package [here](https://github.com/Terrastories/default-offline-map/). Your folder structure should look like:

```

tileserver/
└── data/
    ├── fonts/
    │   └── ...
    ├── sprites/
    │   ├── sprite.png
    │   └── ...
    ├── mbtiles/
    │   └── tiles.mbtiles
    ├── styles/
    │   └── style.json
    └── config.json
```

If your map package does not have a `config.json` file, create one at the root of your `tileserver/data` folder. It should look something like this, depending on your package files and configuration:

```json
{
  "options": {
    "paths": {
      "fonts": "fonts",
      "sprites": "sprites"
    },
    "serveAllFonts": true
  },
  "data": {
    "your-map-style": {
      "mbtiles": "mbtiles/tiles.mbtiles"
    }
  },
  "styles": {
    "your-map-style": {
      "style": "styles/style.json",
      "tilejson": {
        "type": "overlay"
      }
    }
  }
}
```

Once you have your folders created, assets added, and configuration complete. Update your `compose.yaml` file in your favorite text editor to:

<pre class="language-diff"><code class="lang-diff"><strong> tileserver:
</strong><strong>   restart: unless-stopped
</strong>-  image: terrastories/terrastories-map:latest
+  image: maptiler/tileserver-gl:v4.7.0
   ports:
     - 8080:8080
<strong>+  volumes:
</strong>+    - ./tileserver/data:/data
</code></pre>

This changes the tileserver image to the official Tileserver-GL image, `maptiler/tileserver-gl`, at the tag v4.7.0 which is the current latest tag.

It also mounts the `tileserver` folder you just created into the Tileserver for serving.

### Custom Tileserver

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

### Custom Hostname

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

## Run Terrastories

Once everything is setup to your liking, run your Terrastories instance:

```
docker compose up
```
