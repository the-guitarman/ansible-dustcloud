ansible-dustcloud
=================

Version: 0.1.0

**Attention:** This is an after work project only. 

Installs the software to root your roborock vacuum cleaner, to disconnect 
it from the Xiaomi cloud and to use it with your own private dustcloud. 
The dustcloud supports some roborock devices only. For more information 
please see: [github.com/dgiese/dustcloud](https://github.com/dgiese/dustcloud)

Workflow:
1. Downloads and installs the required packages and software to the remote host
2. Creates the new firmware for your roborock vacuum cleaner
3. Connects the remote host to the reseted roborock wifi
4. Starts the flash script
  - Disables the remote host LAN devices of the remote host, except lo and wlan-device
  - Flashes the new firmware to the roborock vacuum cleaner asynchronous
  - Enables the remote host LAN devices of the remote host, except lo and wlan-device
5. Prints next todos you have to do manually

This role is heavily inspired by this german blog post [german blog post](https://maker-tutorials.com/xiaomi-roborock-saugroboter-raspberry-pi-hack-root/).

Requirements
------------

I used a raspberry pi with Raspbian GNU/Linux 10 (buster) as remote host. 
No guarantee but may be it works with Debian like systems like Ubuntu as well.

Role Variables
--------------

- defaults/main.yml: 

```yml
account: '<your user name>'
roborock_directory: 'roborock'
version:
  valetudo: '0.4.0'
  firmware: 'v11_001886'
  language: 'de' # one of: de, english, es, fr, it, ja, ko, ru, taiwanese, transformer

wifi_network_device: wlan0
wpa_ctrl_interface: 'DIR=/var/run/wpa_supplicant GROUP=netdev'
wpa_update_config: 1
wpa_country: 'DE'
roborock_wifi_ssid: 'roborock-vacuum-s5_miap9806'
roborock_wifi_ip_address: '192.168.8.1'
```

- vars/main.yml is empty

Dependencies
------------

At your ansible host you need to install python, pip and the python library netaddr, e.g.:

Debian/Ubuntu:

```bash
sudo apt install python python-pip
pip install netaddr
```

MAC:

```bash
brew install python
pip install netaddr
```

Install
-------

```bash
ansible-galaxy install the_guitarman.ansible_dustcloud
```

Example Playbook
----------------

Usage (e.g.: playbook_dustcloud_install.yml):

```yml
    ---
    - hosts: raspberry
      roles:
         - role: the_guitarman.ansible_dustcloud
           become: true
           become_method: sudo
           become_user: "root"
           vars:
             account: "your_account_name"
             roborock_directory: "roborock"
             version:
               valetudo: '0.4.0'
               firmware: 'v11_001856'
               language: 'de'
```

- your_account_name: This is the user name at your remote host.

```bash
ansible-playbook playbook_dustcloud_install.yml
```

License
-------

This project has a dual license.

This package is licensed under
the **LGPL 3.0**. Do whatever you want with it, 
but please give improvements and bugfixes back so everyone can benefit.

For commercial usage please contact me at first.

*Note:* Everything may break at every time.
