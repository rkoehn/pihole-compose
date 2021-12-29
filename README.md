# pihole-compose

## Making port 53 availalbe on Ubuntu 20.04

### 1. Disable DNSStubListener in systemd-resolved

Content of `/etc/systemd/resolved.conf`:

```
[Resolve]
#DNS=
#FallbackDNS=
#Domains=
#LLMNR=no
#MulticastDNS=no
#DNSSEC=no
#DNSOverTLS=no
#Cache=no-negative
#DNSStubListener=yes
#ReadEtcHosts=yes
```

Uncomment (remove # from the front of the line) the DNSStubListener= line
and also change the DNSStubListener= value from yes to no.

```
[Resolve]
#DNS=
#FallbackDNS=
#Domains=
#LLMNR=no
#MulticastDNS=no
#DNSSEC=no
#DNSOverTLS=no
#DNSStubListener=yes
DNSStubListener=no
#ReadEtcHosts=yes
```

### Create a symbolic link for /run/systemd/resolve/resolv.conf with /etc/resolv.conf as the destination

```
sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

### Restart systemd-resolved

```
sudo systemctl restart systemd-resolved
```

## Udpate DNS setting in FritzBox

DNS server used by FritzBox can be set in Internet -> Zugangsdaten -> DNS-Sever Tab.
Enter Pihole Address both for "Bevorzugter" and "Alternativer" Server, and both for IPv4 and IPv6. IPv6 can use local address, e.g. `fd00::96de:80ff:fe22:653b`

