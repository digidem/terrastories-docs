# 🛖 Hosting Terrastories offline as a "Field Kit"

{% hint style="warning" %}
This page may require some technical knowledge about server hosting and deployment. If the content of this page feels unfamiliar to you, get someone acquainted with information technology (IT) to help you.
{% endhint %}

_This workflow is for hosting your own Terrastories server offline on a device like a mini-computer (NUC) running Linux._

The Terrastories "Field Kit" hosting environment is designed to allow one mini-computer device to serve as a hotspot through which other devices can get access to Terrastories. For more on how this works in practice, see [operating-an-offline-terrastories-field-kit.md](../../using-terrastories/operating-an-offline-terrastories-field-kit.md "mention").

The way to set this up requires use of command-line shell (sometimes known as terminal). Fortunately, we've made it easy to go through most of the process by means of an easy setup script. For anyone wishing to go through the setup process in a more granular way, please refer to our [documentation for developers on Github](https://github.com/Terrastories/terrastories).

{% hint style="info" %}
It is possible to install Terrastories on Windows or Mac OS; however, this workflow has only been fully tested on a Linux OS, specifically Ubuntu 18.04 - 22.04. You may need to take different steps for some of the setup depending on the operating system; for example, the `hosts` and Hotspot network manager files may reside in a different location.
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

Your answer to the first question "Setup for offline 'Field kit' mode?" should be `y` or `Y`.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Next, depending on whether you already have offline tiles downloaded and placed in the `tileserver/data/` directory, the script will offer to download the Terrastories default offline tiles for you. This is optional. For more information on the Terrastories default offline tiles, and offline maps in general, see [preparing-offline-maps.md](../preparing-offline-maps.md "mention").

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Next, you will be asked if you want to configure network access. This is if you want to host Terrastories on a local or mesh network; if you are just setting up Terrastories as a "Field Kit", then you can enter `3`.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

At this point, the script will go through a series of setup steps, including registering `terrastories.local` as an accessible hostname, meaning it will be accessible through the browser and pointing to the Terrastories server.

The script will also build Terrastories locally, which involves downloading all of the services and dependencies Terrastories needs to run, and placing them in Docker containers.

{% hint style="success" %}
When Terrastories has successfully been built, you should see the following screen.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

As the script suggests, you can now start Terrastories using the command

```
docker compose --profile offline up
```

The first time you run this command, it will actually download and build a few more services that are needed for offline usage specifically. You should therefore run this command before bringing the "Field Kit" offline.

## Additional steps for configuration

There are a few additional steps needed to configure Terrastories for "Field Kit" usage that are not (yet) handled through the setup script. _Note: the paths for these files may differ depending on operating system. These are the paths for Ubuntu 18.04 - 22.04._

#### Set a static IP

* **Set up a static IP:** using a text editor tool, edit `/etc/NetworkManager/system-connections/Hotspot` and under the `ipv4` section, add the following line:\
  `address1=192.168.0.1/24`
* **Set this static IP address as host**: using a text editor tool, edit `/etc/hosts` and change the IP address for `terrastories.local` to be the following:\
  `192.168.0.1 terrastories.local`

Make sure there are no other entries for `terrastories.local`

#### Configure your hotspot

First, you can create and turn on a Hotspot using the Linux operating system user interface. Modify the Hotspot name and password to be something easy to remember for anyone that is [operating-an-offline-terrastories-field-kit.md](../../using-terrastories/operating-an-offline-terrastories-field-kit.md "mention").

<figure><img src="../../.gitbook/assets/Screenshot from 2022-11-23 16-15-29.png" alt=""><figcaption></figcaption></figure>

Next, you can make your Hotspot autoconnect on reboot by entering the following command in the terminal:

```
nmcli con mod <Hotspot-network-name> connection.autoconnect yes
```

{% hint style="info" %}
Make sure none of your WiFi connections are enabled to connect automatically.
{% endhint %}

#### Install codecs to process H.264 videos

In our experience, NUC devices don't come bundled have the codecs to process H.264 videos such as mp4 files in the browser. Resolve this by installing ubuntu-restricted-extras in the terminal:

```
sudo apt-get install ubuntu-restricted-extras
```

#### Bypass login screen on boot

For the [operating-an-offline-terrastories-field-kit.md](../../using-terrastories/operating-an-offline-terrastories-field-kit.md "mention") workflow, it will be helpful to bypass the operating system login screen, since the device will be turned on without keyboard, mouse, or monitor. Here is a [guide for bypassing login screen on boot](https://askubuntu.com/questions/256239/how-to-bypass-login-screen-on-boot).

#### Set operating system to shutdown upon pressing power button

Similarly, for the [operating-an-offline-terrastories-field-kit.md](../../using-terrastories/operating-an-offline-terrastories-field-kit.md "mention"), it will be helpful to set the operating system to bypass any logout screen and shut down right away upon pressing the power button, since the device will be operated without keyboard, mouse, or monitor.&#x20;

In Ubuntu 18.04 or any similar Linux variants with acpi, use a text editor tool to create a file called `/etc/acpi/events/power` and enter the following in the content:

```
event=button/power
action=/sbin/poweroff
```

Save and close the file, and run:

```
sudo service acpid restart
```

#### Set operating system to start Docker on boot

Here is a [guide for configuring Docker to start on boot](https://docs.docker.com/install/linux/linux-postinstall/#configure-docker-to-start-on-boot), if needed.

#### Set Docker to operate without sudo access

Here is a [guide for configuring Docker to operate without sudo](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user), if needed.

## Bringing Terrastories offline

You are now ready to bring Terrastories to an offline context!

From here, you can run the command:

```
docker compose --profile offline up
```

And keep the service running. Every time that you shut down the machine, and turn it on again, Terrastories will restart by default, so you don't need to worry about any additional setup.&#x20;

You may now proceed to show anyone administering the offline Terrastories "Field Kit" process the workflow for [operating-an-offline-terrastories-field-kit.md](../../using-terrastories/operating-an-offline-terrastories-field-kit.md "mention"), which does not require any technical knowledge.
