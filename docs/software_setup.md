
## Software Setup

### Install Raspian OS
- Flash the microSD with Raspbian-Lite
- If possible, follow the steps for a [headless config](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md), which involves placing a [``wpa_supplicant.conf``](https://www.raspberrypi.org/documentation/computers/configuration.html#adding-the-network-details-to-your-raspberry-pi) file and a file named ``ssh`` in the root of the flashed SDCard.
- Place the microSD in the Pi and power it on

### Configuring Raspberry Pi
- If you did the headless config, you can log into your home router and find the Pi's IP address and ssh to it: eg ``ssh pi@192.168.1.202``.  Otherwise, connect a keyboard and screen until ssh is enabled.
- ``sudo apt-get update && sudo apt-get upgrade``
- ``sudo raspi-config``
  - configure wifi, including country (skip if you did headless config)
  - enable ssh (skip if you did headless config)
  - enable SPI (Display settings)
  - set localization (timezone, language, keyboard.  The default GB keyboard layout will be a problem if your wifi password has any symbols)

### Installing Dependencies
- ``wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.60.tar.gz``
- ``tar zxvf bcm2835-1.60.tar.gz ``
- ``cd bcm2835-1.60/``
- ``sudo ./configure``
- ``sudo make``
- ``sudo make check``
- ``sudo make install``
- ``sudo apt-get install wiringpi``
- ``wget https://project-downloads.drogon.net/wiringpi-latest.deb``
- ``sudo dpkg -i wiringpi-latest.deb``
- ``gpio -v``
- ``sudo apt-get update``
- ``sudo apt-get install python-pip``
- ``sudo apt-get install python-pil``
- ``sudo apt-get install python-numpy``
- ``sudo pip install RPi.GPIO``
- ``sudo pip install spidev``
- ``sudo apt-get update``
- ``sudo apt-get install python3-pip``
- ``sudo apt-get install python3-pil``
- ``sudo apt-get install python3-numpy``
- ``sudo pip3 install RPi.GPIO``
- ``sudo pip3 install spidev``
- ``sudo apt-get install libopenjp2-7-dev``
- ``sudo apt-get install libopenjp2-7``
- ``sudo apt-get install libtiff5``
- ``sudo apt-get install git``

### Installing SugarPiDisplay
- ``cd ~/``
- ``git clone https://github.com/archynet/SugarPiDisplay.git``
- ``pip3 install SugarPiDisplay/``
- ``SugarPiDisplay/install.sh``
- reboot the Raspberry Pi and SugarPiDisplay should be running

### Configuring SugarPiDisplay
- Once SugarPiDisplay is running, you can configure it using its web interface on port 8080.  It will display its IP address for several seconds during startup.  Enter this IP into your browser with ":8080" on the end and you'll see the config screen.  From here you can pick Dexcom or Nightscout and enter in the necessary fields.
- Nightscout token: If you will be getting your CGM data from nightscout, you'll have to set up a "user" in nightscout.  Under the Admin Tools screen, click the "Add new Subject" button.  Give it a name like SugarPi.  For role, use the "readable" role.  Click Save.  In the list of subjects, your new role will be listed with a generated access token (something like "sugarpi-8c8766b098a988f".  That token is entered under "Nightscout Access Token" in the SugarPiDisplay config.  Note: this requires Nightscout version 0.9 or later.
