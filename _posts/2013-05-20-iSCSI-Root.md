---
published: true
layout: post
title: iSCSI Root (part 1)
categories: 
  - blog
tags: 
  - iSCSI
  - ipxe
  - diskless environment

---

## What is iSCSI-Root
iSCSI-Root is an iSCSI based diskless desktop computing solution from Trantect. It supports both Linux and Windows (as client instances). The centralized storage leads to great scalibilties and flexibilities, and also easy backup solutions. With giga-bit ethernet, the performance is good enough comparing the common desktop environment.

## How does it work
Following packages and solutions are applied for iSCSI-Root:

* [iPXE](http://ipxe.org/)
* [iSCSI Enterprise Target(iet)](http://iscsitarget.sourceforge.net/)
* [lvm](http://tldp.org/HOWTO/LVM-HOWTO/)

## How to setup
### Requirements
Three categories of services are applied for iSCSI-Root:

* TFTP/iPXE services
* DHCP service
* iSCSI service

It is unnecessay to host them in seperate machines. It's up to you to orgnized these services. Following is the overview of current Trantect deployment.

* DHCP sevice hosted at a MIPS based WiFi route (OpenWrt).
* TFTP/iPXE, iSCSI services at a PC (Ubuntu Server).

For better performance, gigabit ethernet is recommended for iSCSI server and desktop clients.

### Configuring your DHCP server for iPXE booting
To boot a client, DHCP service needs to be configured correctly.

In Trantect, we use an route(OpenWrt installed) as for DHCP service. So we added configurations to /etc/config/dhcp.

<pre><code>config 'boot'
        option 'networkid' 'ipxe-booted'
        option 'filename' 'iscsi.ipxe'
        option 'servername' 'boot1.secutum.com'
        option 'serveraddress' '192.168.0.194'

config 'boot'
        option 'filename' 'undionly.kpxe'
        option 'servername' 'boot1.secutum.com'
        option 'serveraddress' '192.168.0.194'</code></pre>

if you use dhcpd, add those to your configuration.

<pre><code>next-server 192.168.0.194
if exists user-class and option user-class = "iPXE" {
    filename "iscsi.ipxe";
} else {
    filename "undionly.kpxe";
}</code></pre>

### Setup TFTP/iPXE server
#### Setup TFTP service
First, we need set up an tftp service to host our ipxe executable and ipxe info files in the Ubuntu PC.

```
$ apt-get install tftpd-hpa
```

Next edit the configuration file.The configuration file is located at /etc/default/tftpd-hpa

```
$ vi /etc/default/tftpd-hpa
```

The default configuration is like this.
<pre><code># /etc/default/tftpd-hpa
TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/var/lib/tftpboot"
TFTP_ADDRESS="0.0.0.0:69"
TFTP_OPTIONS="--secure"</code> </pre>

After modifing, remember to restart the tftpd-hpa service.

```
S service tftpd-hpa restart
```

Actually, the default configuration is just ok for Trantect. So we don't modify it.

According the configuration, the tftp root directory is `/var/lib/tftpboot`. We will place our ipxe exectable and files in it.

#### Deploy iPXE exectable binary
Now we are sharing an empty directory via the TFTP protocol. We need add the iPXE binary into the TFTP. You can get the binary or the source code in [http://ipxe.org/download](http://ipxe.org/download).
Once you have the binary, cope it to the tftpboot folder.

```
$ cp undionly.kpxe /var/lib/tftpboot/
```

After that, we need to add the iPXE boot files into the TFTP.

Add a file `iscsi.ipxe` in tftpboot folder. And the file content is like this.

<pre><code>#!ipxe
boot http://192.168.0.194/cgi-bin/iet_boot</code></pre>

This ipxe file tells the client to boot from a url `http://192.168.0.194/cgi-bin/iet_boot`. the `192.168.0.194` is our Ubuntu PC's ip.

Of course, you can also [burn ipxe into ROM](http://ipxe.org/howto/romburning)

#### Setup an http service for ipxe boot file
Install the apache

```
$ apt-get install apache2
```

Start the apache2 service

```
$ service start apache2
```

Add our cgi file `iet_boot` in `/usr/lib/cgi-bin/`.


```
$ touch /usr/lib/cgi-bin/iet_boot
```

Add below content into file `/usr/lib/cgi-bin/iet_boot`, you may need to change the `ipxe_server_ip` to yours.

<pre><code>#!/usr/bin/env python

# enable debugging
from sh import grep, sed

ipxe_server_ip = "192.168.0.194"

def available_volumes():
    volumes = sed(grep("tid:", "/proc/net/iet/volume"),
                  "-n", '-e', 's/^.*name://p').rstrip().split("\n")
    return volumes

def print_menu_head(mac, ip, volumes):
    print """#!ipxe

:start

echo Booting %s

menu iSCSI boot menu [%s/%s]
""" % (mac, ip, mac)
    for volume in volumes:
        print "item %s %s" % (volume, volume)

    print '''
item --gap --
item --gap -- ------------------------------- Manual boot -------------------------------
item hdd Boot from HDD
item shell Shell
'''
    print 'choose os'
    print '''
goto ${os}
goto end
'''

def print_menu_script(volumes):
    print '''
:hdd

sanboot --no-describe --drive 0x80
goto start

:shell

shell
goto start
'''
    for volume in volumes:
        print """
:%s
""" % (volume)
        print """
sanboot iscsi:%s::::%s
goto end
""" % (ipxe_server_ip, volume)

print "Content-Type: text/plain;charset=utf-8"
print

volumes = available_volumes()

print_menu_head(volumes)
print_menu_script(volumes)</code> </pre>

This script can find your running iSCSI targets automatically and use them as a iPXE booting item.
The menu will like this.
![Alt text](/assets/iscsi-root/menu.jpg)

Finished alreay? You can go to [part 2](/blog/2013/05/21/iSCSI-Root-2/) now.
## Other resources
* [iPXE documents](http://ipxe.org/docs)
* [PXE Booting Ubuntu from an iSCSI drive](http://www.heath-bar.com/blog/?p=184)
* [Diskless Windows 7 with iSCSI and gPXE](http://jonmccune.wordpress.com/2011/12/19/diskless-windows-7-with-iscsi-and-gpxe/)
* [Windows XP/Vista/7 iSCSI Boot](http://www.thogan.com/blog/windows-xp-vista-7-iscsi-boot/)
* [Installing Windows Server 2008 to an iSCSI target](http://www.etherboot.org/wiki/sanboot/win2k8_iscsi_install)
* [Diskless Windows 7 iSCSI boot from OpenSolaris 2009.06 ZFS Server](http://blog.zorinaq.com/?e=41)
