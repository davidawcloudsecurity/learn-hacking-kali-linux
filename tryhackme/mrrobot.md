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
### How to bruteforce input fields with hydra
Username
```bash
hydra -L example.txt -p example $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:Invalid username" -t 30
```
Password
```bash
hydra -L example -P example.txt $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The password you enter for the username" -t 30
```
