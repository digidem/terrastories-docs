# Importing data

{% hint style="info" %}
Importing data requires `admin` or `editor` access. If you are logged in as a `member` or `viewer`, you will not be able to access this settings menu.
{% endhint %}

Terrastories has an import tool, which allows `admin` or `editor` users of a community to add stories, places, and speakers in one batch operation, rather than manually inputting them one by one. To access the import tool, navigate to the **Import** view in the sidebar.

On this view, you can import data for Places, Speakers, and Stories, and this can be done in one operation (or one by one, as you prefer).

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-27 144720.jpg" alt=""><figcaption></figcaption></figure>

Currently, the Terrastories import tool can interpret a `csv` file. You can either **Download a Sample CSV** file that is provided by Terrastories (online or offline), or you can use your own `csv`.

For Terrastories in an offline environment, it is possible to upload media attachments as well. See the below section [Importing media attachments (Terrastories in an offline or mesh hosting environment only).](importing-data.md#importing-media-attachments-terrastories-in-an-offline-or-mesh-hosting-environment-only)

### Importing CSV files

To begin using the import tool, click **Choose File** and select your `csv` for any of the data types (Places, Speakers, or Stories).

The columns in your `csv` file can be in any order. Once you've uploaded your `csv`, the Terrastories import tool allows you to map your columns the Terrastories data fields.

For any data fields for which there is no column in your `csv` to match, you can just leave that blank.

{% hint style="info" %}
The `Media` and `Name audio` fields are intended for media attachments, and currently will not work for Terrastories hosted in an online environment.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-27 145854.jpg" alt=""><figcaption></figcaption></figure>

Once you are done, click **Import**. The data will now be added to Terrastories.&#x20;

{% hint style="info" %}
Make sure to provide names for each column in the top row of your `csv` so you can map the columns to the Terrastories data fields, as in the screenshot above.
{% endhint %}

{% hint style="warning" %}
Depending on the size of your `csv` (and media attachments if adding for an offline or mesh environment), the importing process may take a while. Do not close the page while this process is ongoing or your import operation will be interrupted.
{% endhint %}

### Importing media attachments (Terrastories in an offline or mesh hosting environment only)

For a Terrastories community on a server that is hosted in an offline or mesh environment, it is possible to add media attachment for each of the Stories, Places, and Speakers being imported. Media attachments include photos, videos, and audio. (In the future, we hope to make this possible for Terrastories hosted in an online environment as well.)

The way this works is that for each row in the `csv`, if there is a filename listed in the `media` or `name audio` fields being imported, then it will look for that filename in the `/rails/import/media` directory of your Terrastories application. If it finds the file, then it will import it for the data row you are importing; if not, it will skip adding a media attachment.

For example, let's say that you have a story in your `csv` called **My Terrastories Story**, and you want to add a video file called **TerrastoriesVid\_Final.mp4**.

1. First, copy your file **TerrastoriesVid\_Final.mp4** to the `/rails/import/media` directory.
2. Next, find the row containing your story **My Terrastories Story** in your `csv`. Ensure that there is a column in which the full filename is written out (e.g. **TerrastoriesVid\_Final.mp4**, with the `.mp4` file type and matching the capitalization of your file).
3. When you click **Import** to import the `csv`, and the tool starts to import your **My Terrastories Story** row, it will look for a file called **TerrastoriesVid\_Final.mp4** in `/rails/import/media`.  Since you placed it there, it successfully locates the file, and proceeds to add the file as a media attachment.

The same will happen for all of your `csv` rows for any Stories, Speakers, and Places that you import, in one batch operation.

{% hint style="info" %}
If one of your rows failed to attach a media file, then it is likely that the filename was misspelled in the `csv`. It is easy to miss a character or capitalization. It can also sometimes happen that a filename ends in all capital letters such as **.MP4**. Make sure the filenames strings in your `csv` match the files exactly.
{% endhint %}

