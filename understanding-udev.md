# `udev`

To get information about a device found under `/dev`, try this:


```
sudo udevadm info -a -p $(sudo udevadm info -q path -n /dev/i2c-2)
```


---


To test out a new udev rule (in this example, we're testing /dev/i2c-1):


`$	sudo udevadm test $(sudo udevadm info -q path -n i2c-1) 2>&1`


---


To reload new udev rules, run this:


`$	sudo udevadm control --reload`
