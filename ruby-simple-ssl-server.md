Simple SSL server using ruby that reflects anything sent to it Works for GET POST etc.... Will create the cert files on first run. 
==================================================================================

```ruby

#!/usr/bin/ruby
# Simple SSL server using ruby that reflects anything sent to it
# Works for GET POST etc....
# Will create the cert files on first run. 
# openssl req -x509 -newkey rsa:4096 -keyout priv.pem -out cert.pem -days 365 -nodes

IO.write('./cert.pem', '-----BEGIN CERTIFICATE-----
MIIFYDCCA0igAwIBAgIJAJjAoMlSo60rMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV
BAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5ldCBX
aWRnaXRzIFB0eSBMdGQwHhcNMTgxMDIyMTY0NTM3WhcNMTkxMDIyMTY0NTM3WjBF
MQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEhMB8GA1UECgwYSW50
ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIIC
CgKCAgEAv00+c7qBOwDbH/jSIe2IrL4qq3QgwEQQxXs040XOdMZeYxt5qcPJOVCr
eel1DjPNY3tuI6USC3Upa578zccZJFQ++QrNsDjyXABUl2Q5T/W2lEbiYAlOIoPp
e8RD6qITVqbLdS9RxZnBjmhLdAugnmaLwt4c9WRDTM0126xvWexq0oiMb7i09L3G
/jizjZ1eb0e/ys4tRn0wKLEAbhVTwpal8EhUA3m1Z+VunWvrnPNSL/ZAolFPr5so
j7jn+Ao0G5JqkaF/esXoQICauMs64V+0A1bpQIKnPK3gHp2q0aFX+18eGKKmeIxB
xLquJHKmt5U9acpiu2c5TWsnr5B60q9bC2JC4DeMsFrrsL19aBl813yYfI9HUV3F
5cRUoJOdepldnAv3M3AfIjyzMUE4O76HpQ2WRkUs7Xb0azraflmTpGFA/T0cUmUy
1SXHGWkiI0oOWj4YDyEYAjN0oRc+x3Cwt0dA9hfGRcwr9IfC2YlgWT4UgUd4g4xE
6NtoRGdAdFR+NfbZxe4suFgX2P2ENAFyfxJKiEtU43V2Y2YNR25ZSyb0OE60eTHC
Wd3LjiIfk7mvVHlNtLfFMeQoGBz3jSivqwt5QTOE4jmGPes7nklsMdmIywr/PheG
sEA11IUsdMdX/rzKswSeLasRKJiq9j9WAIbz88PP4ogJRc0E8psCAwEAAaNTMFEw
HQYDVR0OBBYEFNfnlpbPJb6/Cqob/0hKvl24LDpgMB8GA1UdIwQYMBaAFNfnlpbP
Jb6/Cqob/0hKvl24LDpgMA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQAD
ggIBAFXL12eHzaPukirMEykwPBo4D23Hbd8+6lSffddjRGbLdJbrd2szpuYs+JQV
wGD/jEANZtxuH4K6CJXcVaQw8FOUq1vqvyPO608zpa+d8I2dYStWvC6jUinr3oLg
tni6YAo/s36io+LkLmACxjyb4cRqKVizma5RSG34Al+eFcEVEUygoryh5jvI2f4r
2XO3FUNcnv6kNjlqNZEJ8LE8e+wBNeNJ2mi4FEUhzUYukwdHphJNebW/OnplhkQE
aLR+AiuTNQ9e1gnCWWIW3UWrs4dcgYaIgMQ9wXixVYYjTXGDpl1hvLUxfKRwi2IP
A6T8AcbCJUE/dmseyolR1TPqieFqWQGJ0NQNTso+xUxa47ddMIwAm7FvM69TzQvG
TYhlN5OYHNFKToR0mrxUlYeyIoVpIJ5NfT1GQiz1fXH/7lpDvnpEvYdksv83b/vb
a5tjAMl6g0aDZr05y9eI4dNE8lPhr9TCmMJtka6mAk5QBueZU+asHd2ovZSQkuqa
SmH2Ju1j/oOx2R+ri6cdIkb7jST7kYZCZJ3/m+krdFyktgWZUWH301H0M0o3mIXs
NxF8aU5jyCyUxvR/jb1eFkxXtQ3VzVwUN6hM3G5zpXXW3Cy88DmALi4DJoSpcxh9
n3D6nciDQk5rAi6uulgRNZYCBVEnFEXuRG5V1zE2Vyy/8U8t
-----END CERTIFICATE-----')


IO.write('./priv.pem', '-----BEGIN PRIVATE KEY-----
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
IgA8JXNxdgy5BxzuTE2VXGxi29HoI+c=
-----END PRIVATE KEY-----')

require "socket"
require "openssl"
require "thread"

# listeningPort = Integer(ARGV[0])
listeningPort = Integer(443)

server = TCPServer.new(listeningPort)
sslContext = OpenSSL::SSL::SSLContext.new
sslContext.cert = OpenSSL::X509::Certificate.new(File.open("cert.pem"))
sslContext.key = OpenSSL::PKey::RSA.new(File.open("priv.pem"))
sslServer = OpenSSL::SSL::SSLServer.new(server, sslContext)

puts "Listening on port #{listeningPort}"

loop do
  connection = sslServer.accept
  Thread.new {
    begin
      while (lineIn = connection.gets)
        lineIn = lineIn.chomp
        $stdout.puts lineIn
        lineOut = lineIn
       # $stdout.puts lineOut
        connection.puts lineOut
      end
    rescue
      $stderr.puts $!
    end
  }
end
```

