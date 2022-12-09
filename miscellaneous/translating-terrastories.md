# Translating Terrastories

Terrastories aims to be accessible to a wide range of communities in their native languages, and to facilitate the process of translating the app as needed.

### Translation using Github

Currently, translations for Terrastories are handled through Github. In the future, we aim to use CrowdIn to make it easy for anyone to contribute translations to Terrastories for new or existing languages.

To begin translating, clone the [Github Terrastories repository](https://github.com/terrastories/terrastories), and follow these steps.

1. Find the two or three-digit ISO language code for your language contribution [here](https://en.wikipedia.org/wiki/List\_of\_ISO\_639-1\_codes)
2. Navigate to the `/rails/config/locales` folder.&#x20;
3. Copy the `en` folder (or any other language folder you want to use as your basis for translation) and rename it to your ISO language code. Also rename the `en` in each filename, and the beginning of each file, to your ISO language code.
4. Translate each string to your language of contribution.
5. Add your language to the `languages` list for all of the languages (in `en.yml`, `pt.yml`, `mat.yml`, ... and your new language contribution). You can use Google Translate to figure out how your language is translated in the other languages.
6. Submit your PR 🎉

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>At the time this screenshot was taken, we have the following languages available (in alphabetical order): Amharic, English, Spanish, Hindi, Japanese, Matawai, Dutch, Portuguese, Punjabi, Swahili, and Chinese (Mandarin).</p></figcaption></figure>
