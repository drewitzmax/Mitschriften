# Pre Protocol Nr. 1
**Author:** Max Drewitz
## Network Plan
**Internal Networkaddress:** 192.168.5.0/24
## Credentials
### NETA-GW
**Username:** csdc

**Password:** campus09

**Password (default):** campus09

### NETA-Web
**Username:** csdc

**Password:** campus09

**Password (default):** campus09

## Gateway Server Configuration
**internal address:** 192.168.5.1

**external address:** TBD

**gateway address:** TBD

**DNS1:** 192.168.5.254

**DNS2:** 8.8.8.8

**hostname:** gateway

### Hostname Configuration
To change the hostname use the command `sudo hostnamectl set-hostname {{new-hostname}}`.
The hostname should be "gateway"
### Change Password
To change the password of a user use the command `sudo passwd {{username(optional)}}`. Update the password of the user "csdc" and note it down somewhere safe e.g. a password-safe
### Install SSH Service
To install the ssh-package run: `sudo apt install ssh`

To verify run `service ssh status`. It should state that the service is `active (running)`

Connecting should now be possible the comman is `ssh {{username}}@{{hostname}}` after that it should prompt for a password
### Ignore ICMP Echo-Messages
To ignore ICMP Echo-Messages run the command `echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all`.
Ping requests from other host won't be answered from now on.
### Enable/Disable IP-forwarding
To configure portforwarding use the command `sysctl -w net.ipv4.ip_forward={{val}}`. `val` should be `1` if you want to enable IP-forwarding or `0` if you want to disable.

To configure SNAT use the command `iptables -t nat -A POSTROUTING ! -d 192.168.5.0/24 -o eth1 -j SNAT --to-source 198.51.5.1`
## Web Server Configuration
**address:** 192.168.5.10

**gateway address:** 192.168.5.1

**DNS1:** 192.168.5.254

**DNS2:** 8.8.8.8
## Mail Server Configuration
**address:** 192.168.5.20

**gateway address:** 192.168.5.1

**DNS1:** 192.168.5.254

**DNS2:** 8.8.8.8
## Client Workstation Configuration
**address:** 192.168.5.100

**gateway address:** 192.168.5.1

**DNS1:** 192.168.5.254

**DNS2:** 8.8.8.8
## DNS Server Configuration
**address:** 192.168.5.254

**gateway address:** 192.168.5.1

**DNS1:** 8.8.8.8

**DNS2:** 8.8.4.4
## Monitoring the Network
### nmap
First install nmap `sudo apt install nmap`.

To scan a network you just user the command `nmap {{hostname/ip/network address or range}}`
### tcpdump
The `tcpdump` command dumps incoming headers of TCP, UDP and/or ICMP packets.
Use the `-q`-Option to filter for 

### netstat
netstat shows statistics over requests received by the current host. If there are active connections you can also see the source of the requests
### wireshark
wireshark is a graphical network monitoring tool