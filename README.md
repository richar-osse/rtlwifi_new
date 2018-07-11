rtlwifi_new
===========
### A repo for the newest Realtek rtlwifi codes.

This code will build on any kernel 4.2 and newer as long as the distro has not modified
any of the kernel APIs. IF YOU RUN UBUNTU, YOU CAN BE ASSURED THAT THE APIs HAVE CHANGED.
NO, I WILL NOT MODIFY THE SOURCE FOR YOU. YOU ARE ON YOUR OWN!!!!!

It includes the following drivers:

rtl8192ce, rtl8192cu, rtl8192se, rtl8192de, rtl8188ee, rtl8192ee, rtl8723ae, rtl8723be, and rtl8821ae.

If you are looking for the driver for rtl8822be or rtl8723de, then execute the following command:

git checkout origin/extended -b extended

#### Installation instruction
You can find <<YOUR WIRELESS DRIVER CODE>> using `lspci | grep Wireless`.
Afterwards, execute the following lines of codes in your shell:  
  
```
You will need to install "make", "gcc", "kernel headers", "kernel build essentials", and "git".

If you are running Ubuntu, then

 sudo apt-get install linux-headers-generic build-essential git

Please note the first paragraph above.

For all distros:
git clone https://github.com/lwfinger/rtlwifi_new.git
cd rtlwifi_new
sudo make install
sudo modprobe -r <<YOUR WIRELESS DRIVER CODE>>
sudo modprobe <<YOUR WIRELESS DRIVER CODE>>

#### Option configuration
If it turns out that your system needs one of the configuration options, then do the following:

vim /etc/modprobe.d/<<YOUR WIRELESS DRIVER CODE>>.conf 

There, enter the line below:
`options <<YOUR WIRELESS DRIVER CODE>> <<driver_option_name>>=<value>`



You will need to install "make", "gcc", "kernel headers", "kernel build essentials", and "git".

If you are running Ubuntu, then

 sudo apt-get install linux-headers-generic build-essential git

Please note the first paragraph above.

For all distros:
git clone https://github.com/lwfinger/rtlwifi_new.git
cd rtlwifi_new
sudo make install
sudo modprobe -r <<YOUR WIRELESS DRIVER CODE>>
sudo modprobe <<YOUR WIRELESS DRIVER CODE>>

#### Option configuration
If it turns out that your system needs one of the configuration options, then do the following:

vim /etc/modprobe.d/<<YOUR WIRELESS DRIVER CODE>>.conf 

There, enter the line below:
`options <<YOUR WIRELESS DRIVER CODE>> <<driver_option_name>>=<value>`

STEPS from HERE
And finally I found a solution that works for me (checked on 2 laptops of same model with different versions of Ubuntu: 16.04LTS and 17.04)

Open Terminal, and enter:

iwconfig
And note down the wl* number.

Download the new driver rock.new_btcoex from Github and unzip it to Desktop folder.

In Terminal, now run these commands:

cd Desktop/rtlwifi_new-rock.new_btcoex
make
sudo make install` type your ubuntu password
sudo modprobe -rv rtl8723be
sudo modprobe -v rtl8723be ant_sel=2
sudo ip link set wl* up` use your **wl* number**
sudo iw dev wl* scan` same
To make the settings permanent, use this command:

echo "options rtl8723be ant_sel=2" | sudo tee /etc/modprobe.d/50-rtl8723be.conf
Note: After your OS (Kernel) update, you need to apply these settings again to get a strong signal.


