## TryHackMe Walkthrough - Wekor
Added wekor.thm to /etc/hosts
URL=wekor.thm
### How to scan ports with nmap
```bash
IP_ADDR=
nmap -sV -sC -oA initial $IP_ADDR
```
### How to enumerate web server domains
```bash
WORDLISTS=/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt   
gobuster vhost -u http://${IP_ADDR} -w ${WORDLISTS} -t 100 -q -o gobuster.txt
```
```bash
DNSLISTS=/usr/share/amass/wordlists/subdomains-top1mil-5000.txt
wfuzz -c -w $DNSLISTS -t30 --hw 3 -H "Host:FUZZ.${URL}" "http://${URL}"
```
