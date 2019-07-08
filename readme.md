# Install NVIDIA Official Driver On Debian 10

## What is Nouveau?

`Nouveau - the open source project is reverse engineering NVIDIA by X.Org in linux system`

## Step by step

- Conventions
```
$ => require 'regular user'
# => require 'root user'
> => edit in file with your favorite editor
```

- Login with the superuser via sudo
```
$   sudo -i
#   whoami
```

- Add new apt source list non-free and update
```
#   nano /etc/apt/sources.list
    >   deb http://deb.debian.org/debian/ buster main non-free
    >   deb-src http://deb.debian.org/debian/ buster main non-free
#   apt update
```

- Install nvidia-detect
```
#   apt install nvidia-detect
```

- Run nvidia-detect for check your system support driver version
```
#   nvidia-detect
```

- **Download installation file from [NVIDIA Official Website](https://www.nvidia.com/object/unix.html)** OR Try to install driver via apt source with below command
```
#   apt install nvidia-driver
```

- Disable default nouveau to the blacklist
```
#   nano /etc/modprobe.d/blacklist.conf
    >   blacklist nouveau
    >   options nouveau modeset=0
```

- Update initial ramfs
```
#   update-initramfs -u
```

- Switch default from **Graphical Mode** to **CLI Mode**
```
#   systemctl set-default multi-user.target
```

- Reboot your system
```
#   systemctl reboot
```

- Install latest linux headers
```
#   apt install linux-headers-$(uname -r) build-essential
```

- Run command for **Install NVIDIA Official With Root** on sh/bash. *Example: NVIDIA-Linux-x86_64-390.116.run*
```
#   sh ./NVIDIA-Linux-x86_64-390.116.run
#   bash ./NVIDIA-Linux-x86_64-390.116.run
```

- On installing, choose below the choices
```
+ Install NVIDIA's 32-bit compatibility libraries? [Yes]
+ An incomplete installation of libglvnd was found. Do you want to install a full copy of libglvnd? This will overwrite any existing libglvnd libraries. [Install and overwrite existing filesort installation.]
+ Would you like to run the nvidia-xconfig utility to automatically update your X configuration file so that the NVIDIA X driver will be used when you restart X?  Any pre-existing X configuration file will be backed up. [Yes]
```

- Switch default from **CLI Mode** to **Graphical Mode**
```
#   systemctl set-default graphical.target
```

- Reboot your system again
```
#   systemctl reboot
```

**`After install, I found "black screen", "no devices detected" and "no screens found" problem with Xorg. And I Solved the problems by "Remove X11/Xorg Configuration file in /etc/X11/xorg.conf and reboot again"`**

## My Reference

- [how-to-install-nvidia-driver-on-debian-10-buster-linux](https://linuxconfig.org/how-to-install-nvidia-driver-on-debian-10-buster-linux)
