# learn-hacking-kali-linux

### How to hack web server workflow
NMAP check for ports and OS
```bash
IP_ADDR=
nmap -sV -sC -oA initial $IP_ADDR
```
Enumerate for directories
```bash

```
### How to update kali linux
```bash
wget http://http.kali.org/kali/pool/main/k/kali-archive-keyring/kali-archive-keyring_2024.1_all.deb
sudo dpkg -i kali-archive-keyring_2024.1_all.deb
rm kali-archive-keyring_2024.1_all.deb
sudo apt-get update
```
https://kalitut.com/how-to-update-kali-linux-and-fix-update/
```bash
$ sudo apt update -oAcquire::AllowInsecureRepositories=true
$ sudo apt install kali-archive-keyring
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  kali-archive-keyring
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 7,008 B of archives.
After this operation, 17.4 kB of additional space will be used.
Do you want to continue? [Y/n] 
WARNING: The following packages cannot be authenticated!
  kali-archive-keyring
Install these packages without verification? [y/N] y
```
To exploit against wordpress site
```bash
set wpcheck false
```

