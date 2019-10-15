Default locations of wordlists files
--------------------------
```bash
# Shows Kali list of wordlists
root@kali:~#wordlists

# Quick search for workdlists
root@kali:~#locate wordlist
# A few examples
/usr/share/dirbuster/wordlists/apache-user-enum-1.0.txt
/usr/share/dirbuster/wordlists/apache-user-enum-2.0.txt
/usr/share/dirbuster/wordlists/directories.jbrofuzz
/usr/share/dirbuster/wordlists/directory-list-1.0.txt
/usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
/usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
/usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt
/usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-small.txt
```

Basic Buster HTTPS Scan
----------------------------------------------------
```bash
# https://github.com/OJ/gobuster
# -k = Ignore SSL errors
# -n = Do not show HTTP status errors (Better to load into Burp)
gobuster dir -k -u https://xx.xx.xx.xx.xx:443 -w /media/xxxxx/pentest-stuff/dirbuster-ng/wordlists/common.txt -n
```

Use a compressed file for the wordlist
---------------------------------------
```bash
zcat /usr/share/wordlists/rockyou.txt.gz | gobuster dir -k -u https://xx.xx.xx.xx:443 -w -
```
