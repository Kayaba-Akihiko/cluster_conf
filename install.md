# Disable GUI.
```
sudo systemctl set-default multi-user
```

# Change password
```
sudo passwd {username}
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
