# Post flash Raspberry Pi setup instructions

## Configure SSH and Wi-Fi

After flashing the RPi to an SD card add following files to `root` of the SD card (boot partition):

Empty `ssh` file to enable SSH.

`wpa_supplicant.conf` with following configuration to enable Wi-Fi on boot:

    country=FI
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
            ssid="wifi-ssid"
            psk="wifi-pass"
    }

Change country code country=`FI` as needed according to the [2 letter country code standard](https://www.iban.com/country-codes).

Change ssid="`wifi-ssid`" to the network you want the RPi to connect to.

Change psk="`wifi-pass`" to the Wi-Fi password of the network.

## Generate SSH key for login

To SSH to RPi wihtout needing to enter the password.  
It is also recommended to change the password from the default.

### Ubuntu
Create a new key pair if you don't already have one

    ssh-keygen -t rsa -b 2048

Just hit enter to prompts

Copy ssh id to Raspberry Pi with user@ip-address:

    ssh-copy-id pi@ip-address

Enter RPi user pasword to prompt

### Windows CMD
Create a new key pair if you don't already have one

    ssh-keygen

Just hit enter to prompts

Copy public key to RPi Authorized keys.
Insert `{Windows username}`, `{RPi user}` and `{RPi IP address}` to below.

    type C:\Users\{Windows username}\.ssh\id_rsa.pub | ssh {RPi user}@{RPi IP address} "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"

Enter RPi user pasword to prompt