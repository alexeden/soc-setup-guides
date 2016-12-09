### Setting Up WiFi
- You'll use `netctl`. Ignore anything pertaining to `netcfg`.
- `netctl` profiles are stored in `/etc/netctl`


#### 1. You'll need an interface name


See: [Network Interfaces](https://wiki.archlinux.org/index.php/Network_configuration#Device_names)


`$	ls /sys/class/net` will print the list of possible interfaces.
```
eth0  lo  wlan0
```
Or use `$	ip link` to get more details. To change the name of an interface device, you'll have to add a new rule to `udev`. Create the file `/etc/udev/rules.d/10-network.rules`:
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"  SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"
```


>To get an interface's MAC: `$	cat /sys/class/net/DEVICE_NAME/address`


#### 2. Use `wifi-menu` to generate the `netctl` profile


You might need to install `dialog` and `wpa_supplicant` to do this.
We'll be using the interface device named `wlan0`, so enter: `$	wifi-menu -o wlan0`


This will generate the network profile `wlan0-Ape`:
```
Description='Automatically generated profile by wifi-menu'
Interface=wlan0
Connection=wireless
Security=wpa
ESSID=Ape
IP=dhcp
Key=\"09a09442dd1c905571d887bbdc2902c54b378b553c8299b2d93d89fa2b1d5385
```


#### 3. Start the network profile


With the profile file generated, start it using the profile name:
`$	netctl start wlan0-Ape`


>To get a list of the available network profiles: `$	netctl list`


>If something went wrong or you want more info:`$	netctl status wlan0-Ape`


#### 4. Create & enable the `systemd` service for the new profile:


`$	netctl enable wlan0-Ape` and reboot.
