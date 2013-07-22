---
published: true
layout: default
---

![Jenkins Cluster](https://wiki.jenkins-ci.org/download/attachments/2916393/logo-title.png?version=1&modificationDate=1302753947000)

#This is just a outline for this blog. To be continued...

##Overview

### What is Jenkins and Jenkins Cluster?

### Why is Jenkins needed?

### Why is Jenkins Cluster needed?

### Why Jenkins Cluter has a higher performance than Jenkins without hardware upgrade?

* hardware introduction

        Memory 2.0 GiB
        Processor Intel® Celeron(R) CPU G1610 @ 2.60GHz 
        Disk 80GB
    
* software introduction

        Ubuntu 11.10 or higher
        Python 2.7.2
        JDK 1.6
        Jenkins ver. 1.509.2
        phpPgAdmin
        
* projects to be tested
    * Django
        
        This is a web project based on Django framework (version Django 1.5, Python 2.72).

    * Android

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

##Real case study
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
