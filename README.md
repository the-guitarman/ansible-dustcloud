ansible-dustcloud
=================

**Attention:** This is an after work project and n
either it's finished nor it's ready for production usage.

Installs the software to root your roborock vacuum cleaner, to disconnect 
it from the xiaomi cloud and to use it with your own private dustcloud. 
The dustcloud supports roborock devices with LDS (S5, S50, S55), Xiaomi Mi.

Uses:
- [github.com/dgiese/dustcloud](https://github.com/dgiese/dustcloud)

Requirements
------------

This role can be used with Debian like systems like Ubuntu or Raspbian only.

Role Variables
--------------

- defaults/main.yml: 

```yml
account: '<your user name>'
roborock_directory: 'roborock'
version:
  valetudo: '0.4.0'
  firmware: 'v11_001856'
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

Example Playbook
----------------

Usage:

```yml
    - hosts: servers
      roles:
         - role: dustcloud
           become: true
           become_method: sudo
           become_user: "root"
           vars:
             account: sebastian
             roborock_directory: "roborock"
             version:
               valetudo: '0.4.0'
               firmware: 'v11_001856'
```

License
-------

This project has a dual license.

This package is licensed under
the **LGPL 3.0**. Do whatever you want with it, 
but please give improvements and bugfixes back so everyone can benefit.

For commercial usage please contact me at first.

*Note:* Everything may break at every time.
