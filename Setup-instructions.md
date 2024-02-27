Our first task is to ensure everything is up to date with our operating system. It will make installing the Spotify software to our Raspberry Pi a little easier.
To do this, we will need to run the following two commands. The first will update the package list. The second command upgrades the installed packages.

sudo apt update
sudo apt upgrade

Next, we need to make sure that both “curl” and “apt-transport-https” packages are installed to our Raspberry Pi.
Without these, we won’t be able to set up the raspotify repository on Raspbian.
Run the following command to install our needed packages.

sudo apt install -y apt-transport-https curl

With the packages we need installed we can go ahead and add the “raspotify” GPG key and its repository.
Without the GPG key, the apt package manager won’t be able to verify the files it’s retrieving from the repository.
You can do these two things by running the following two commands.

curl -sSL https://dtcooper.github.io/raspotify/key.asc | sudo tee /usr/share/keyrings/raspotify-archive-keyrings.asc >/dev/null
echo 'deb [signed-by=/usr/share/keyrings/raspotify-archive-keyrings.asc] https://dtcooper.github.io/raspotify raspotify main' | sudo tee /etc/apt/sources.list.d/raspotify.list

Now that we have the raspotify repository added to our Raspberry Pi, we can now go ahead and install the raspotify package.
This package will handle turning our Raspberry Pi into a Spotify Connect device. We can install the package by running the two commands below.
We need to rerun the update due to us adding the raspotify repository in the previous step. Without an update, the package manager won’t know what’s contained in that repository.

sudo apt update
sudo apt install raspotify

With the “raspotify” software now installed, the software should start automatically and be ready for connections.
You should now be able to connect to your Raspberry Pi’s Spotify software. 
You can do this by opening up the Spotify app on your chosen device and selecting it from the “Connect to a device” menu.


While the Raspotify software works perfectly fine right out of the box, you can make changes to its configuration.
You can use this configuration file to adjust things such as the bitrate or the device name.
Run the command below to begin modifying the “raspotify” config file.

sudo nano /etc/raspotify/conf

Within this file, you will see multiple different options that you can configure yourself. 
We will go into a couple of these and explain what you can use them for.

When changing options within this file, 
make sure that you remove the hashtag (#) at the start of the line. Otherwise, 
the settings will not take effect.

LIBRESPOT_NAME="Librespot"
This option defines the name that Spotify connect
service on the Raspberry Pi will use. You can set this to something to 
easier identify where the Raspberry Pi is or what the Pi is connected to.
By default, Raspotify will set the device name to “raspostify” followed by the hostname of your device.

LIBRESPOT_BITRATE="160"
With this option, you can specify the bitrate that you would like the device to utilize.
You can pick three different values for this option, 96 for low-quality, 160 for medium-quality or 320 for high-quality audio.
