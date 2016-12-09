# Setting up ARM Arch Linux

After getting ARM Arch Linux install on the SOCs primary memory drive (SD card, eMMC, etc), SSH into the device and follow these steps to get it setup.

I use my initials (ape) as the login and hostname.


### 1. Create the User

`$	useradd --create-home --groups wheel --shell /bin/bash ape`
`$	passwd ape`
`$	userdel alarm`


### 2. Create the Superuser & Privilege Scheme
`$	pacman -Syu sudo`
`$	export EDITOR=nano`
`$	visudo`


Add the lines to the `sudoers` file:
`ape ALL=(ALL) ALL`


### 3. Change the root password:
`$	passwd root`


### 4. Set the hostname:
`$	echo ape-NAME > /etc/hostname`


### 5. Install packages needed for Node:
`$	pacman -Syu base-devel nodejs git python2`


### 6. Install bash autocompletion and enable it:
`$	sudo pacman -Sy bash-completion`
`$	nano ~/.bashrc`


Add the lines:
```
if [-f /etc/bash_completion]; then
	/etc/bash_completion
fi
```

### 6. Set node-gyp’s Python version:
`$	npm config set python /usr/bin/python2`


### 6. Configure git:
`$	git config --global user.email "alexandereden91@gmail.com"`
`$	git config --global user.name "Alexander Eden"`
