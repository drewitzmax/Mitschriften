# Pre Protocol 4
## Firewall
The firewall will be implemented using a iptables ruleset, which will follow along the given example:

```
#!/bin/sh

# Empty all rules
sudo iptables -t filter -F
sudo iptables -t filter -X

# Bloc everything by default
sudo iptables -t filter -P INPUT DROP
sudo iptables -t filter -P FORWARD DROP
sudo iptables -t filter -P OUTPUT DROP

# Authorize already established connexions
sudo iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -t filter -A INPUT -i lo -j ACCEPT
sudo iptables -t filter -A OUTPUT -o lo -j ACCEPT

# ICMP (Ping)
sudo iptables -t filter -A INPUT -p icmp -j ACCEPT
sudo iptables -t filter -A OUTPUT -p icmp -j ACCEPT

# SSH
sudo iptables -t filter -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -t filter -A OUTPUT -p tcp --dport 22 -j ACCEPT

# DNS
sudo iptables -t filter -A OUTPUT -p tcp --dport 53 -j ACCEPT
sudo iptables -t filter -A OUTPUT -p udp --dport 53 -j ACCEPT
sudo iptables -t filter -A INPUT -p tcp --dport 53 -j ACCEPT
sudo iptables -t filter -A INPUT -p udp --dport 53 -j ACCEPT

# HTTP
sudo iptables -t filter -A OUTPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT

#HTTPS
sudo iptables -t filter -A OUTPUT -p tcp --dport 443 -j ACCEPT
sudo iptables -t filter -A INPUT -p tcp --dport 443 -j ACCEPT

# FTP
sudo iptables -t filter -A OUTPUT -p tcp --dport 20:21 -j ACCEPT
sudo iptables -t filter -A INPUT -p tcp --dport 20:21 -j ACCEPT

# Git
sudo iptables -t filter -A OUTPUT -p tcp --dport 9418 -j ACCEPT
sudo iptables -t filter -A INPUT -p tcp --dport 9418 -j ACCEPT

# Mail SMTP
iptables -t filter -A INPUT -p tcp --dport 25 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 25 -j ACCEPT

# Mail POP3
iptables -t filter -A INPUT -p tcp --dport 110 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 110 -j ACCEPT

# Mail IMAP
iptables -t filter -A INPUT -p tcp --dport 143 -j ACCEPT
iptables -t filter -A OUTPUT -p tcp --dport 143 -j ACCEPT

# NTP (server time)
sudo iptables -t filter -A OUTPUT -p udp --dport 123 -j ACCEPT
```
Details will be figured out later

## FTP
### setup
To setup the vsftpd service we run the command `sudo apt-get install vsftpd`

### Allow local user accounts
To allow all useraccounts on our webserver to access via FTP we need to uncomment the line `#local_enable=YES` in the file `/etc/vsftpd.conf`

### Allow writing actions
To allow accessing users to write data to the server additionally add the line `write_enable=YES`

### Require ssl
#### Generate Certificate and Key
First we need to created a new Certificate
```
openssl req -x509 -nodes -days 365 -newkey rsa:8192 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem
```
Fill out the following requests.
After that the private key can be extracted
```
openssl rsa -in /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.key
```
Now we can actually configure our FTP(S) service to be secure. Add the following:
```
# Force ssl on login and data transport
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_ciphers=HIGH

# configure the files used as cert and private key
rsa_cert_file=/etc/ssl/private/vsftpd.pem
rsa_private_key_file=/etc/ssl/private/vsftpd.key

# enable ssl in general
ssl_enable=YES
```

### FTP Client
To test the FTP service a client like filezilla may be used

## Sockets
### Running python scripts
As python3 is already part of the ubuntu installation no installation will be needed

### Server Script
This script will need to run on any host wich shall be the server
```
#!/usr/bin/env python3
import socket
import sys
HOST = sys.argv[1] # IP of the Server
PORT = int(sys.argv[2])  # PORT of the Server
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.bind((HOST, PORT))
sock.listen()
conn, addr = sock.accept()
print('Connected by', addr)
ata = conn.recv(1024)
print("received message:", data) 
```
Run the script as follows `{{scriptFilename}} {{hostIp}} {{port}}`. The port should ideally be in the range of the registered ports to avoid conflict with standard ports. That means  >= 1024
### Client Script
This script will need to run after the server has been started and can run on any host acting as the client. Even the same host as the server.
```
#!/usr/bin/env python3
import socket import sys
HOST = sys.argv[1]  # The server's hostname or IP address
PORT = int(sys.argv[2])  # The port used by the server
MESSAGE = b"Hello, world!"
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((HOST, PORT))
sock.sendto(MESSAGE, (HOST, PORT)) 
```
Same as before: Run the script as follows `{{scriptFilename}} {{hostIp}} {{port}}`
