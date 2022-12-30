# Assumption
Assuming Ubuntu OS (20.04 or 22.04) is reinstalled.

# Change password
```shell
sudo passwd ${username}
```

# Disable GUI.
```shell
sudo systemctl set-default multi-user
```

# Change host name.
```shell
hostnamectl set-hostname ${new_nostname}
```

# Change username.
## set a password for root account
```shell
sudo passwd root
```
## log out.
```shell
exit
```
## log in with root and change username and home folder
```shell
usermod -l ${newname} -d /home/${newname} -m ${oldname}
```
## lock root and exit
```shell
passwd -l root
exit
```

# update and upgrade
```shell
sudo apt-get update
sudo apt-get upgrade -y
```

# install vim
```shell
sudo apt-get install vim -y
```

# set IP
```shell
sudo vim /etc/netplan/cloud-init.yaml
```
```yaml
network:
    version: 2
    ethernets:
        port_like_enp0***:
            dhcp4: no
#            gateway4: 163.221.196.1
            routes:
              - to: default
                via: 163.221.196.1
            addresses:
              - 163.221.196.***/24
            nameservers:
                addresses:
                  - 163.221.196.150
                  - 163.221.196.200
                search:
                  - image.local
            
```
## Apply 
```shell
sudo netplan apply
```

## Check ip address
```shell 
ip addr
```

## Check network connection
```shell
ping 8.8.8.8
```

# Login via ssh
```shell
ssh ${username}@163.221.196.**
```

# Uninstall old Nvidia driver
```shell
sudo nvidia-uninstall
```
## If docker and nvidia-docker2 are installed, remove.
```shell
sudo apt-get remove nvidia-docker2 -y
sudo apt-get remove docker -y
sudo rm -r /etc/docker
```
## Clean other Nvidia files
```shell
sudo apt-get remove --purge '^nvidia-.*' -y
sudo apt-get remove --purge '^libnvidia-.*' -y
sudo apt-get remove --purge '^cuda-.*' -y
sudo apt-get autoremove -y
```

## reboot
Be careful of enabled Secure Boot.
If it is enabled, you have to access the machine with an connected monitor to proceed with the passwd you were asked to set during the packages removing instead of accessing by ssh.
Select Enroll MOK and enter the passwd you set after reboot if Secure Boot is enabled.
```shell
sudo reboot
```

# Install new Nvidia driver
## Check latest version
```shell
sudo apt-get update
sudo apt search '^nvidia-driver.+server$'
```
## Install the latest one
```shell
sudo apt-get install nvidia-driver-***-server -y
```
## reboot
Samely be careful of enabled Secure Boot.
If driver install failed, uninstall it and install it gain with the previous steps.
```shell
sudo reboot
```

## test
```shell
nvidia-smi
```
We don't need CUDA to be installed.

# Firewall.
```shell
sudo ufw allow from 163.221.196.0/24
sudo ufw enable
```

# SSSD and Active Directory
Baiscally followed steps from [here](https://ubuntu.com/server/docs/service-sssd-ad)
```shell
sudo apt install sssd-ad sssd-tools realmd adcli -y
```
