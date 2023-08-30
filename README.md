# grafana_installation
Grafana Installation Raspberry 4 

Download and install Raspberry Pi Imager
Before we get started, you need to download and install the Raspberry Pi Imager.

We’ll use the Raspberry Pi Imager to flash the operating system image to the SD card. You download the imager directly from the official Raspberry Pi website and it’s available for Ubuntu Linux, macOS, and Windows.

Follow the directions on the website to download and install the imager.

# Install Raspberry Pi OS
Now it is time to install Raspberry Pi OS.

Insert the SD card into your regular computer from which you plan to install Raspberry Pi OS.
Run the Raspberry Pi Imager that you downloaded and installed.
To select an operating system, click Choose OS in the imager. You will be shown a list of available options.
From the list, select Raspberry Pi OS (other) and then select Raspberry Pi OS Lite, which is a Debian-based operating system for the Raspberry Pi. Since you’re going to run a headless Raspberry Pi, you won’t need the desktop dependencies.
To select where you want to put the operating system image, click Choose Storage in the imager and then select the SD card you already inserted into your computer.
The final step in the imager to click Write. When you do, the imager will write the Raspberry Pi OS Lite image to the SD card and verify that it has been written correctly.
Eject the SD card from your computer, and insert it again.
While you could fire up the Raspberry Pi now, we don’t yet have any way of accessing it.

Create an empty file called ssh in the boot directory. This enables SSH so that you can log in remotely.

The next step is only required if you want the Raspberry Pi to connect to your wireless network. Otherwise, connect the it to your network by using a network cable.

(Optional) Create a file called wpa_supplicant.conf in the boot directory:

ctrl_interface=/var/run/wpa_supplicant
update_config=1
country=<Insert 2 letter ISO 3166-1 country code here>
network={
ssid="<Name of your WiFi>"
psk="<Password for your WiFi>"
}

All the necessary files are now on the SD card. Let’s start up the Raspberry Pi.

Eject the SD card and insert it into the SD card slot on the Raspberry Pi.
Connect the power cable and make sure the LED lights are on.
Find the IP address of the Raspberry Pi. Usually you can find the address in the control panel for your WiFi router.
Connect remotely via SSH
Open up your terminal and enter the following command:
ssh pi@<ip address>
SSH warns you that the authenticity of the host can’t be established. Type “yes” to continue connecting.
When asked for a password, enter the default password: raspberry.
Once you’re logged in, change the default password:
passwd
Congratulations! You’ve now got a tiny Linux machine running that you can hide in a closet and access from your normal workstation.

# Install Grafana

Now that you’ve got the Raspberry Pi up and running, the next step is to install Grafana.

Add the APT key used to authenticate packages:

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
Add the Grafana APT repository:

echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list


# Install Grafana:

sudo apt-get update
sudo apt-get install -y grafana


Grafana is now installed, but not yet running. To make sure Grafana starts up even if the Raspberry Pi is restarted, we need to enable and start the Grafana Systemctl service.

Enable the Grafana server:

sudo /bin/systemctl enable grafana-server


# Start the Grafana server:

sudo /bin/systemctl start grafana-server

Grafana is now running on the machine and is accessible from any device on the local network.

Open a browser and go to http://<ip address>:3000, where the IP address is the address that you used to connect to the Raspberry Pi earlier. You’re greeted with the Grafana login page.

Log in to Grafana with the default username admin, and the default password admin.

Change the password for the admin user when asked.

Congratulations! Grafana is now running on your Raspberry Pi. If the Raspberry Pi is ever restarted or turned off, Grafana will start up whenever the machine regains power.

# Summary

If you want to use Grafana without having to go through a full installation process, check out Grafana Cloud, which is designed to get users up and running quickly and easily. Grafana Cloud offers a forever free plan that is genuinely useful for hobbyists, testing, and small teams.



Getting a ‘unknown error occured’ when trying to log in. 100% positive user and PW are correct.

Grafana 10.1.0 on RPi 4


https://community.grafana.com/t/login-issue-after-update-to-10-1-0-coming-from-10-0-3/101990/7

command to downgrade the grafana installation

sudo apt-get install grafana=10.0.3
