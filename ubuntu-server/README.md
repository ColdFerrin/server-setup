# Guide for setting up ubuntu server cli only

## Ubuntu installation

1. Download ubuntu server from cannonical
1. Install ubuntu server from cannoncial
1. Create user with name `xxxx` and password `xxxxxxxx`

## 1. If wifi is needed Install wifi drivers

1. Install `wpa-supplicant` with command
   1. `sudo apt install wpa-supplicant -y`
2. Install GCC
   1. `sudo apt install gcc -y`
3. Install make
   1. `sudo apt intsall make -y`
4. Install dkms
   1. `sudo apt install dkms -y`
5. Install drivers
   1. `git clone https://github.com/aircrack-ng/rtl8812au`
   2. `cd rtl8812au`
   3. `sudo ./dkms-install.sh`

## 2. Rename network devices

1. Create net rules file 
   1. Create file at `/etc/udev/rules.d/` called `70-persisten-net.rules`
2. Add rules to file in format shown below
   1. `SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="xx:yy:zz:aa:bb:cc", NAME="xxxx"
   2. Replace "xx:yy:zz:aa:bb:cc" With actual mac address, and xxxx in name with desired device name
3. Edit `/etc/default/grub` 
   1. change `GRUB_CMDLINE_LINUX=""` to `GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"`
4. `sudo update-grub`
5. `sudo reboot`

## Setup wifi

1. Create `config.yaml` in `/etc/netplan/`
2. Follow instructions in autogen file to remove it
3. put the code in this config.yaml to the destination
4. `sudo netplan try`
5. `sudo netplan apply`
