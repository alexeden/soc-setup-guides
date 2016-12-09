# ODROID C2 - I2C

Load the I2C driver:
`$	sudo modprobe aml_i2c`

---

Add I2C to load on boot:


Create this file:
`$	sudo nano /etc/modules-load.d/i2c.conf`


Add these 2 lines at the end of the file and save:
```
i2c-dev
aml_i2c
```


---

Add the user to the `tty` user group:

`sudo usermod -aG tty ape`

---

Create a new udev rule that sets the group ownership of I2C devices to `tty`:

`$	nano /etc/udev/rules.d/11-i2c.rules`

Add this to the contents of the file:


```
SUBSYSTEM=="i2c-dev",KERNEL=="i2c-*",GROUP="tty"
```

---

Reboot

---

Test it out:
`i2cdetect -y -r 1`
