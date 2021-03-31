# Networking

Commands relating to configuring (including information gathering) networking. Also includes firewalls.

## Basic information gathering
### Modern approach: ip

The ip command is availible on most distros and is used for gathering information on network interfaces and routes. It can also be used to turn interfaces
on and off. For more details: [man ip](https://linux.die.net/man/8/ip)

**Show ip information about all interfaces**

**``ip address``**

**Show the routing table**

**``ip route``**


**Bring an interface up or down**

**``ip link set [interface] [up|down]``**

For example:

**``ip link set eth0 up``**

Will bring interface eth0 up and:

**``ip link set wlp1s0 down``**

will bring interface wlp1s0 down.

### Legacy Approach: ifconfig

These tools are not availible on modern OSs but are still useful to know. For more details [man ifconfig](https://linux.die.net/man/8/ifconfig)

**Show ip information about all interfaces**

**``ifconfig``**


**Show the routing table**
**``route``**



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
In order for your changes to take effect, you need to apply them with:

``netplan apply``

#### CentOS 7

Networking in CentOS is managed with NetworkManager. It can be configured using the configuration files located in: /etc/sysconfig/network-scripts:

```
[root@centos ~]# ls -lh /etc/sysconfig/network-scripts/
total 236K
-rw-r--r--. 1 root root 1.7K Mar 29 19:25 ifcfg-eth0
-rw-r--r--. 1 root root  287 Mar 29 19:32 ifcfg-ethernet-test
-rw-r--r--. 1 root root  254 May 22  2020 ifcfg-lo
```

Each interface has a configuration file with a prefix of "ifcfg-" to set the ipaddress, gateway, dns, etc:

```
[root@centos ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0 | sed -E '/^#|^$/d'
DEVICE="eth0"
NAME="eth0"
ONBOOT="yes"
BOOTPROTO="none"
IPV6INIT="yes"
IPV6_ADDR_GEN_MODE="eui64"
IPV6_PRIVACY="no"
PEERDNS="no"
DOMAIN=members.linode.com
GATEWAY0=139.162.228.1
DNS1=109.74.194.20
DNS2=109.74.193.20
DNS3=212.71.252.5
IPADDR0=139.162.228.74
PREFIX0=24
```





