# Networking

Commands relating to configuring (including information gathering) networking. Also includes firewalls.

## Basic information gathering
### Modern approach: ip

The ip command is availible on most distros and is used for gathering information on network interfaces and routes. It can also be used to turn interfaces
on and off. For more details: [man ip](https://linux.die.net/man/8/ip)

#### ``ip address``

Show ip information about all interfaces

#### ``ip route``

Show the routing table

#### ``ip link set [interface] [up|down]``

Bring an interface up or down, e.g. :

##### ``ip link set eth0 up``

Will bring interface eth0 up and:

##### ``ip link set wlp1s0 down``

will bring interface wlp1s0 down.

### Legacy Approach: ifconfig

These tools are not availible on modern OSs but are still useful to know. For more details [man ifconfig](https://linux.die.net/man/8/ifconfig)

#### ``ifconfig``

Show ip information about all interfaces

#### ``route``

Show the routing table

### Configuration

Configuring networking in linux varies by distro, so check the documentation for whatever you are using. Here's a summary of how to do it in Ubuntu and Centos.

#### Ubuntu

Modern versions of Ubuntu (>=18.04) use [Netplan](https://netplan.io/) to manage the configuration of network interfaces. Network settings are configured in YAML files located in /etc/netplan. Netplan uses these files to generate the configuration which is then used by lower level programs such as NetworkManager.

Here's an excerpt of a netplan config file configuring an ethernet interface with a static ip and dns servers:
```
network:
    version: 2
    ethernets:
        eth0:
            dhcp4: false 
            optional: true
            addresses:
                    - 10.1.1.100/24
            gateway4: 10.1.1.1
            nameservers:
                    addresses: [8.8.8.8, 1.1.1.1]
```






