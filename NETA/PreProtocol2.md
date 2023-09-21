# Pre Protocol 2
## DHCP
### Installation
`sudo apt install isc-dhcp-server`
### Restart
`systemctl restart isc-dhcp-server`
### Configuration
Add the Interfaces which will be providing the DHCP-Service in the file `/etc/default/isc-dhcp-server`

add the following lines: 
```
INTERFACESv4=”ens19”
INTERFACESv6=”ens19”
```

The main configuration will be done in the file `/etc/dhcp/dhcp.conf` and will equate to something like:
```
subnet 192.168.5.0 netmask 255.255.255.0 {
 range 192.168.5.90 192.168.5.140;
 option subnet-mask 255.255.255.0;
 option domain-name-servers 8.8.8.8, 9.9.9.9;
 get-lease-hostnames true;
 default-lease-time: 600;
 max-lease-time 7200;
 host clientWorkstation {
 hardware-ethernet {{ClientWorkstationMAC}};
 fixed-address 192.168.5.149;
}
```
restart to apply configuration

## Apache Webserver
### Install
`sudo apt install apache2`
### Startup
```
sudo systemctl start apache2
sudo systemctl enable apache2
```
### Restart
`sudo systemctl restart apache2`
### Configuration
The default configuration is defined in `/etc/apache2/sites-available/000-default.conf` set the `DocumentRoot` to the path where the index.html file of your website resides

Restart the apache2 Server after you changed the configuration

## DNS
### Installation
`sudo apt install bind9`
### Restart
`sudo systemctl restart bind9`
### Configuration
#### IPv4
To only configure DNS for IPv4 add the -4 flag to the options in `/etc/default/bind9` so you have  `OPTIONS=”-4 -u bind”`

#### Conf
The main configuration lies in ` /etc/bind/named.conf.options`. Add the following codeblock to the options
```
forwarders {
 10.100.0.1,
 10.100.0.2,
};
allow-recursion{ any; };
listen-on {127.0.0.1, 192.168.5.254 };
listen-on-v6 { any; };
```

#### Zones
Zones are configured in `/etc/bind/named.conf.local`. Add your domain information
```
zone “MaxDrewitz.neta.fh-campuswien.ac.at” {
 type master;
 file “/etc/bind/db.MaxDrewitz”
}
```

Then create the zone file for the domain:
`sudo cp /etc/bind/db.local /etc/bind/db.MaxDrewitz`
Open the new zone file:
`sudo nano /etc/bind/db.MaxDrewitz`
and add the DNS records for ns1, ns2 and www:

```
$TTL 604800
@ IN SOA ns1.MaxDrewitz.neta.fh-campuswien.ac.at. root. 
MaxDrewitz.neta.fh-campuswien.ac.at. (
 1 ; Serial
 604800 ; Refresh
 86400 ; Retry
 2419200 ; Expire
 604800 ) ; Negative Cache TTL
; Name servers
@ IN NS ns1.MaxDrewitz.neta.fh-campuswien.ac.at.
@ IN NS ns2.MaxDrewitz.neta.fh-campuswien.ac.at.
@ IN NS www.MaxDrewitz.neta.fh-campuswien.ac.at.
; A records for name servers
ns1 IN A 192.168.5.20 ; dnsServer
ns2 IN A 192.168.5.1 ; gatewayServer internal
www IN A 192.168.5.10 ; webserver
; reverse
1 IN PTR ns1.MaxDrewitz.neta.fh-campuswien.ac.at.
2 IN PTR ns2.MaxDrewitz.neta.fh-campuswien.ac.at.
3 IN PTR www.MaxDrewitz.neta.fh-campuswien.ac.at.
```

#### Zone Transfers
To the file `/etc/bind/named.conf.options` add the following in the zone block 
```
allow-transfer { 192.168.5.1; }
notify yes;
```
Also you need to install bind9 on the gatewayServer and configure it to act as slave.
Config-File: `/etc/bind/named.conf.local`
add the block
```
zone “MaxDrewitz.neta.fh-campuswien.ac.at” {
 type slave;
 masters { 192.168.5.20; };
 file “/var/cache/bind/db.MaxDrewitz”;
}
```

also add the line `allow-notifiy { 192.168.5.254 }` in the file `/etc/bind/named.conf.options`

Restart after everything is configured!!!
