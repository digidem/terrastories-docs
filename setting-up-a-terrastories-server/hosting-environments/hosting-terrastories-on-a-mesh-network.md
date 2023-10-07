# 🖧 Hosting Terrastories on a mesh network

{% hint style="warning" %}
This page may require some technical knowledge about server hosting and deployment. If the content of this page feels unfamiliar to you, get someone acquainted with information technology (IT) to help you.
{% endhint %}

_This workflow is for hosting your own Terrastories server on your own device and then serving as a hostname via a mesh network._

The way to set this up requires use of command-line shell (sometimes known as terminal). Fortunately, we've made it easy to go through most of the process by means of an easy setup script. For anyone wishing to go through the setup process in a more granular way, please refer to our [documentation for developers on Github](https://github.com/Terrastories/terrastories).

{% hint style="success" %}
You should be able to set up Terrastories and serve the application via a mesh network on any operating system: Linux, Mac, Windows (using WSL). However, this workflow has only been fully tested on a Linux OS, specifically Ubuntu 18.04 - 22.04. You may need to take different steps for some of the setup depending on the operating system; for example, the `hosts` and Hotspot network manager files may reside in a different location.
{% endhint %}

## Prerequisites

* **Install Docker:** To install Terrastories, your operating system first has to have Docker installed. The current version of Docker being used to deploy Terrastories as of December 2022 is v20.10.12.
* **Install Docker Compose**: You also need Docker Compose v2 - v1 will not work with our Docker files. The current version of Docker Compose being used to deploy Terrastories as of December 2022 is v2.3.3

## Download Terrastories and set up .env file.

First, you need to create a fork of the Terrastories/terrastories repository. Now clone the repository locally to your computer. (Or, you can download Terrastories as a ZIP file from [our Github repository](https://github.com/Terrastories/terrastories/) to get the application.)

{% hint style="warning" %}
It is recommended to always download the latest version of the Terrastories codebase, as Terrastories is a project in active development. You can also update your Terrastories codebase by running the setup script below.
{% endhint %}

Once you have Terrastories downloaded locally, rename the `.env.example` file to `.env`. This is where your environmental variables will go. You won't need to add anything at this time, but it is necessary for this file to exist to proceed.

## Run the Terrastories setup script

First, in your command-line shell, navigate to the `terrastories/` directory.

Then, run the command:&#x20;

```
bin/setup
```

This will launch a setup script, walking you through a series of prompts.

Your answer to the first question "Setup for offline 'Field kit' mode?" should be `y` or `Y`. (This is a bit confusing at the moment - we will clarify the script to be either offline "Field Kit" or mesh soon.)

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Next, depending on whether you already have offline tiles downloaded and placed in the `tileserver/data/` directory, the script will offer to download the Terrastories default offline tiles for you. This is optional. For more information on the Terrastories default offline tiles, and offline maps in general, see [preparing-offline-maps.md](../../operating-terrastories-offline/preparing-offline-maps.md "mention").

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Next, you will be asked if you want to configure network access. By default, the script sets up a `terrastories.local` hostname in `etc/hosts`, but you may want to use either your own device hostname (option 1) or a custom hostname (option 2). The script detects your machine hostname and provides it to you as an option in option 1.

Select your network access option of choice. As noted, this is only to set up local network access; broader network access will require a reverse proxying service tool.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

At this point, the script will go through a series of setup steps, including registering your hostname, meaning it will be accessible through the browser and pointing to the Terrastories server on your local / mesh network.

The script will also build Terrastories locally, which involves downloading all of the services and dependencies Terrastories needs to run, and placing them in Docker containers.

When that culminates, you should see the following screen.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

As the script suggests, you can now start Terrastories using the command

```
docker compose --profile offline up
```

The first time you run this command, it will actually download and build a few more services that are needed for offline usage specifically.&#x20;

Once you have done so, Terrastories should be accessible on your network on the hostname that you specified.

## Keeping Terrastories running on the network

From here on out, you may want to set up a few customizations to ensure that Terrastories will always start and be accessible on the network, as long as the device is turned on.

* [Configuring Docker to start on boot](https://docs.docker.com/install/linux/linux-postinstall/#configure-docker-to-start-on-boot). (The Terrastories Docker services are always set to restart as long as Docker is active.)

