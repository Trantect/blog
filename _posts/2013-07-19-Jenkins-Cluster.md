---
published: true
layout: default
---

![Jenkins Cluster](https://wiki.jenkins-ci.org/download/attachments/2916393/logo-title.png?version=1&modificationDate=1302753947000)

#This is just a outline for this blog. To be continued...

##Overview

* hardware introduction
* software introduction
* jenkins
* system to be tested
* android
* django



##Jenkins introduction (provide an office link)

##Set up Jenkins Cluster
* Clone VMS
    *  Create a new partition
        *  lvm tool
    *  Convert and copy a file
        *  dd if=input file of=<output file> bs=10M
    *  Clone VMDK Virtual Machine
        * Clone new vmdk
        * cp src.vmdk dst.vmdk
        * Change uuid of vmdk
    *  Clone VDI VirtualBox Disk
        * Clone new vdi 
        * VboxManage clonehd src.vdi dst.vdi
        * Change uuid of vdi
    *  Create a new virtual machine based on new dst.vmdk and dst.vdi
* Configure network
    *  Bridged adapter
    *  Edit configuration file for network /etc/network/interfaces
* Upgrade Jenkins to 1.5
    *  Automatical upgrade always fali so  donwload and replace jenkins.war
* Install SSH Credentials Plugin (version 0.4)
* Build Cluster
    * Add SSH authorization from master to slaves
    * Add new node on jenkins
    * Create projects on master or slaves
* Assign test tasks
    * Check out code and distribute to slaves
    * Trigger

* Real case study
    * screenshots visiable 
    * test environment 
    * time cost
    * performence
    * how many tests, asserts and code lines

##About Trantect

```javascript
  var Trantect = {
    Company : "Trantect"
    Site : "http://www.trantect.com"
  }
```
