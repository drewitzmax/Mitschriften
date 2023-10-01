# Pre Protocol Nr. 1
## Make the Webserver accessible
The website should be available at the public IP address this can be achieved by setting up a NAT Rule forwording traffic to the port 80 on the webserver

This command should achieve that:
`sudo iptables -A PREROUTING -t nat -i ens18 -p tcp --dport 80 -j DNAT –to-destination 192.168.5.10:80`

## Two websites one host
To serve multiple websites we need to create mulitple virtual hosts on the webserver. Therefore we need multiple configurations at `/etc/apache2/sites-available`

The config should be along the lines of:
´´´
<VirtualHost *:28127>
    ServerAdmin admin@{{prefix}}.fh-campuswien.ac.at
    ServerName {{prefix}}.fh-campuswien.ac.at
    ServerAlias www.{{prefix}}.fh-campuswien.ac.at
    DocumentRoot /var/www/html/{{prefix}}.fh-campuswien.ac.at
</VirtualHost>
´´´

after configuration and cloning both sites need to be loaded and the server to be restarted
```
sudo a2ensite /etc/apache2/sites-available/001-neta1.conf
sudo a2ensite /etc/apache2/sites-available/001-neta2.conf
sudo systemctl restart apache2
```

## Resolving both sites via DNS
The websites need to be added to the zone file created in lab 2.

Here you need to add two lines:
```
neta1 IN    A   192.168.5.10 ;
neta2 IN    A   192.168.5.10 ; 
```

## Adding an MX record
For other mailservers to know where to send our mails to we need an MX record on our DNS server. This also needs to be added to the zone configuration. And looks like that:
```
@   IN  MX 0    mail.MaxDrewitz.neta.fh-campuswien.ac.at.
```
## Mailserver
### Setup the MTA
First install postfix: `sudo apt-get install postfix`. Choose "Internet site" and provide the Domain Name `mail.MaxDrewitz.neta.fh-campuswien.ac.at`

Now we need to do the basic configuration in `/etc/postfix/main.cf` which will look like this:
´´´
myhostname = mail.MaxDrewitz.neta.fh-campuswien.ac.at

alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases

myorigin = /etc/mailname
mydestination = $myhostname, localhost.localdomain, localhost

relayhost =
mynetworks = 127.0.0.0/8 192.168.5.0/24 [::ffff:127.0.0.0]/104 [::1]/128
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
´´´

### Setup the MDA
We also need a MDA to send mails. So we install "dovecot-core dovecore-imapd" and add the line
```
protocols = imap
```
to the file `/etc/dovecot/dovecor.conf`

### Setting up a User Agent
We install thunderbird as our mailclient. `sudo apt-get install thunderbird`

### Adding users
We now need to add some users to test our mailing solution setup `bob` and `alice` with the command 
```
sudo adduser {{username}}
sudo passwd {{username}}
```
and use `campus09` as the set passwords

### Enable portforwarding for the mailserver
Add these two lines on the gateway to make the mailing protocols accessible
```
sudo iptables -A PREROUTING -t nat -i ens18 -p tcp --dport 25 -j DNAT 192.168.5.30:25
sudo iptables -A PREROUTING -t nat -i ens18 -p tcp --dport 143 -j DNAT 192.168.5.30:143
```