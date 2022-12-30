# Change password
```
sudo passwd {username}
```

# Disable GUI.
```
sudo systemctl set-default multi-user
```

# Change host name.
```
hostnamectl set-hostname {new_nostname}
```

# Change username.
## set a password for root account
```
sudo passwd root
```
## log out.
```
exit
```
## log in with root and change username and home folder
```
usermod -l {newname} -d /home/{newname} -m {oldname}
```
## lock root and exit
```
passwd -l root
exit
```

# update and upgrade
```
sudo apt-get update
sudo apt-get upgrade -y
```

# install vim
```
sudo apt-get install vim -y
```

# set IP
```
sudo vim /etc/netplan/cloud-init.yaml
```
```
network:
    version: 2
    ethernets:
        {port like enp0***}:
        dhcp4: no
        gateway4: 163.221.196.1
        addresses:
          - 163.221.196.***/24
        nameservers:
            addresses:
              - 163.221.196.150
              - 163.221.196.200
            search:
              - image.local
            
```

```
sudo netplan apply
```

## check ip address
```
ip -a
```