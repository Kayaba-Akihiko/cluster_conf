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

## check ip address
```shell 
ip addr
```

## check network connection
```shell
ping 8.8.8.8
```