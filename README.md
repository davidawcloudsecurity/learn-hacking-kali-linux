# learn-hacking-kali-linux

### Run kali in a docker
```bash
sudo docker pull hackersploit/bugbountytoolkit
# run and exit
sudo docker run -it --name example hackersploit/bugbountytoolkit
sudo docker container start example
sudo docker exec -it example /bin/bash
```
```bash
tar -xvzf /root/wordlists/SecList.tar.gz /path/to/source/files
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
### Troubleshooting
If hydra has issue
```bash
sudo apt install libmongoc-dev -y
```
If hashcat has issue
```bash
sudo apt-get install libhwloc-dev ocl-icd-dev ocl-icd-opencl-dev; \
sudo apt-get install pocl-opencl-icd
```
