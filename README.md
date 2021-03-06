# beagle_bone_blue_data_acq

Beagle Bone Blue Data Acquisition is a collection of python scripts which allows owners of beagle bone blue to acquire real time sensing data from MPU9250 and AK8963 9-axis sensor.

## System Requirements
1. Python 3.6
2. Smbus python package
3. I2C-tools, and kernel headers for successful smbus installation
## Quick Start
Install smbus-cffi on your beagle bone. It is recommended to use virtual environment

```commandline
pip install -r requirements.txt
``` 

Run ./bbblue_acq to acquire 12-axis data dump in CLI
```commandline
./bbblue_acq
#usage: bbblue_acq [-h] [-3] [-6] [-9] [-12] [-c] [-d] [--csv CSV]
#                  [--db-server-ip DB_SERVER_IP]

#Beagle Bone Blue Data Acquisition Wrapper

#optional arguments:
#  -h, --help            show this help message and exit
#  -3                    3 Axis Mode
#  -6                    6 Axis Mode
#  -9                    9 Axis Mode
#  -12                   12 Axis Mode
#  -c                    Write CSV
#  -d                    Write Database
#  --csv CSV             Specific CSV File Name Write
#  --db-server-ip DB_SERVER_IP
#                        Mysql Database Server IP
```

## Remote Interpreter Setup
### Requirements
1. Pycharm Profession License
2. Established SSH key authentication

### SSH key authentication Setup
On you PC:
```commandline
ssh-keygen
``` 
You will get .ssh/id_rsa and .ssh/id_rsa.pub (private and public key pairs). Skip this step if you already have both of them.

Copy the **public key** to beagle bone with: (Note: DO NOT copy private key. Never **EVER** do this.) 
```commandline
scp -r .ssh/id_rsa.pub <user>@<beagle_bone_IP>:~
```
Now, login to your beagle bone,
```commandline
cat ~/id_rsa.pub >> .ssh/authorized_keys
```
You now login to your beagle bone without entering password.
### Remote Interpreter Setup
1. Please follow instructions here: https://www.jetbrains.com/help/pycharm/configuring-remote-interpreters-via-ssh.html

### Run/Debug Configuration
Please refer to the following setup, take notes on the relative directory of your remote interpreter. (Remote interpreter cannot access your development PC!)
![Remote run setup](https://raw.githubusercontent.com/taoyilee/beagle_bone_blue_data_acq/master/img/remote_run_setup.png)
## Beagle Bone Blue System Configuration Suggestions
### Requirements:
1. USB RJ 45 Cable
2. Micro SD Card 16GB
### OS Image Download
Beagle bone blue is compatible with beagle bone black wireless, because they both use OSD3359 SoC
Please download OS image from and follow the instructions. 
https://archlinuxarm.org/platforms/armv7/ti/beaglebone-black-wireless

It is recommended to install Archlinux to eMMC and remove SD card.

When installation is done, connect USB-RJ 45 Cable to beagle bone blue USB Type A (regular) socket. Connect beagle bone to a DHCP-enabled network and it will acquire an IP address. Login as the default user **alarm** with the password **alarm**. Business as usual afterwards.   
### UDEV Rules for I2C
Use a root shell to issue following commands:
```commandline
groupadd i2c
usermod -aG i2c myusername
echo 'KERNEL=="i2c-[0-9]*", GROUP="i2c"' >> /etc/udev/rules.d/10-local_i2c_group.rules
```

## Disclaimer
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## LICENSE
MIT License

Copyright (c) 2018 Michael (Tao-Yi) Lee

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

