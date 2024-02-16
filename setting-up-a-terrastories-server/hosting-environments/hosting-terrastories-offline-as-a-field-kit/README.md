# 🛖 Hosting Terrastories offline as a "Field Kit"

{% hint style="warning" %}
This page may require some technical knowledge about server hosting and deployment. If the content of this page feels unfamiliar to you, get someone acquainted with information technology (IT) to help you.
{% endhint %}

_This workflow is for hosting your own Terrastories server offline on a device like a mini-computer (NUC) running Linux._

The Terrastories "Field Kit" hosting environment is designed to allow one mini-computer device to serve Terrastories as an offline server accessible locally, or a mesh network. There are also some additional steps you can take to get the device to serve a hotspot through which other devices can get access to Terrastories. For more on how this works in practice, see [operating-an-offline-terrastories-field-kit.md](../../../operating-terrastories-offline/operating-an-offline-terrastories-field-kit.md "mention").

The way to set this up requires use of command-line shell (sometimes known as terminal). Fortunately, we've made it easy to go through most of the process by means of an easy setup script. For anyone wishing to go through the setup process in a more granular way, please refer to our [documentation for developers on Github](https://github.com/Terrastories/terrastories).

{% hint style="info" %}
It is possible to install Terrastories on Windows or Mac OS; however, this workflow has only been fully tested on a Linux OS. You may need to take different steps for some of the setup depending on the operating system; for example, the `hosts` and Hotspot network manager files may reside in a different location.
{% endhint %}

## Prerequisites

* **Install Docker:** To install Terrastories, your operating system first has to have Docker installed. The current version of Docker being used to deploy Terrastories as of February 2024 is v25.0.3.
* **Install Docker Compose**: You also need Docker Compose v2 (v1 will not work with our Docker files). The current version of Docker Compose being used to deploy Terrastories as of February 2024 is v2.24.5

## Install Terrastories

{% hint style="success" %}
Quick Install sets up a new database and utilizes Terrastories default map style. If you wish to use your own map style, please see [advanced setup](advanced-setup.md) for more information.
{% endhint %}

To quick install Terrastories for offline usage, run the following command in the terminal:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Terrastories/offline-field-kit/main/install.sh)"
```

This will download all of the appropriate Docker images and dependencies, and run through setting up Host domain and access at `terrastories.local`.&#x20;

Or, instead of running this command, you can also choose to use Git to clone the repository locally to your computer. (Or, you can download the offline field kit as a ZIP file from [our Github repository](https://github.com/terrastories/offline-field-kit) to get the application.) And then, once in the directory, run `bash install.sh`.

Once you run the install script, you will be greeted with the following screen:

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-02-16 12-42-30.png" alt=""><figcaption></figcaption></figure>

Press any key to start, and the script will install everything you need. Once complete, it will boot up your instance of Terrastories, which when completed will show the following on the terminal:

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-02-16 12-43-06.png" alt=""><figcaption></figcaption></figure>

You can now access Terrastories in the browser at `terrastories.local`, where you will be greeted by the community setup screen:

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-02-16 12-43-22.png" alt=""><figcaption></figcaption></figure>

Once you have set up a community, you may access the application, which will run with a default offline map:

<figure><img src="../../../.gitbook/assets/Screenshot from 2024-02-16 12-44-04.png" alt=""><figcaption></figcaption></figure>

If you want to use your own map, please see [advanced-setup.md](advanced-setup.md "mention").

From here on, you can bring down your Terrastories instance by pressing Ctrl-C in the terminal. And you can run your Terrastories instance again at anytime using the following command (while in the directory):

```
docker compose up
```

{% hint style="info" %}
At this point, you may bring your "field kit" offline.&#x20;
{% endhint %}

## Additional steps for configuration

There are a few additional steps needed to configure Terrastories for "Field Kit" usage that are not (yet) handled through the setup script. _Note: the paths for these files may differ depending on operating system. These are the paths for Ubuntu 18.04 - 22.04._

#### Set a static IP

* **Set up a static IP:** using a text editor tool, edit `/etc/NetworkManager/system-connections/Hotspot` and under the `ipv4` section, add the following line:\
  `address1=192.168.0.1/24`
* **Set this static IP address as host**: using a text editor tool, edit `/etc/hosts` and change the IP address for `terrastories.local` to be the following:\
  `192.168.0.1 terrastories.local`

Make sure there are no other entries for `terrastories.local`

#### Configure your hotspot

First, you can create and turn on a Hotspot using the Linux operating system user interface. Modify the Hotspot name and password to be something easy to remember for anyone that is [operating-an-offline-terrastories-field-kit.md](../../../operating-terrastories-offline/operating-an-offline-terrastories-field-kit.md "mention").

<figure><img src="../../../.gitbook/assets/Screenshot from 2022-11-23 16-15-29.png" alt=""><figcaption></figcaption></figure>

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

For the [operating-an-offline-terrastories-field-kit.md](../../../operating-terrastories-offline/operating-an-offline-terrastories-field-kit.md "mention") workflow, it will be helpful to bypass the operating system login screen, since the device will be turned on without keyboard, mouse, or monitor. Here is a [guide for bypassing login screen on boot](https://askubuntu.com/questions/256239/how-to-bypass-login-screen-on-boot).

#### Set operating system to shutdown upon pressing power button

Similarly, for the [operating-an-offline-terrastories-field-kit.md](../../../operating-terrastories-offline/operating-an-offline-terrastories-field-kit.md "mention"), it will be helpful to set the operating system to bypass any logout screen and shut down right away upon pressing the power button, since the device will be operated without keyboard, mouse, or monitor.&#x20;

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
docker compose up
```

And keep the service running. Every time that you shut down the machine, and turn it on again, Terrastories will restart by default, so you don't need to worry about any additional setup.&#x20;

You may now proceed to show anyone administering the offline Terrastories "Field Kit" process the workflow for [operating-an-offline-terrastories-field-kit.md](../../../operating-terrastories-offline/operating-an-offline-terrastories-field-kit.md "mention"), which does not require any technical knowledge.
