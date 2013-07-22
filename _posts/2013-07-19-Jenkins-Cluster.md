---
published: true
layout: default
---

![Jenkins Cluster](https://wiki.jenkins-ci.org/download/attachments/2916393/logo-title.png?version=1&modificationDate=1302753947000)

#This is just a outline for this blog. To be continued...

##Overview

### What is Jenkins and Jenkins Cluster?

Jenkins is an open source continuous integration tool written in Java. The project was forked from Hudson, it provides continuous integration services for software development and helps developers to build, test and deploy their projects.It is a server-based system running in a servlet container such as Apache Tomcat. It supports SCM tools including CVS, Subversion, Git, Mercurial, Perforce, Clearcase and RTC, and can execute Apache Ant and Apache Maven based projects as well as arbitrary shell scripts and Windows batch commands. Jenkins is released under the MIT License and is a free software.

Jenkins Cluster is a cluster based on Jenkins, it consists of some instances which are individual machines or virtual machines, among these instances one should be selected as master and others should be slaves. Jenkins runs on the master, it manages projects and launches slave agents to build projects concurrently, separately via SSH, Java Web Start or exceuting customized commands.

### Why is Jenkins needed?

Jenkins provides continuous integration services which help developers to build, test and deploy their projects automatically and rapidly. Within Jenkins, developers just need to focus on development and Jenkins will help to do the other things.

### Why is Jenkins Cluster needed?

Overmany or Heavyweight projects on Jenkins will make the machine overloaded, then Jenkins Cluster can deal with that, it allows to distribute our projects onto different instances to run concurrently and separately with a higher performence. If one project is too heavy, we can also divide it into several light subprojects.

### Why Jenkins Cluter has a higher performance than Jenkins without hardware upgrade?

Jenkins on single machine runs projects serially, synchronously and blocking. It means that one project is blocked, others can not be started still.
While Jenkins Cluster runs projects distributedly, so that if we divide our machine into several virtual machines and build Jenkins Cluster based on these instances,
we can have a more sufficient use of resources and a higher performance of projects.

###Jenkins introduction 

Please refer to https://wiki.jenkins-ci.org/display/JENKINS/Use+Jenkins

## Hardware and Software Required

* **host** machine (physics machine)
    * hardware
    
            Memory 8.0 GiB
            Processor Intel® Celeron(R) CPU G1610 @ 2.60GHz x 2
            Disk 500GB
            OS type 64-bit
            
    * software
            
            Ubuntu 11.10 or higher
            Oracle VM VirtualBox 4.1.2

* **virtual** machine as **master**
    * hardware
        
            Memory 2.0 GiB
            Processor Intel® Celeron(R) CPU G1610 @ 2.60GHz
            Disk 20GB
            OS type 64-bit
        
    * software
        
            Ubuntu 11.10 or higher
            JDK 1.6
            Jenkins ver. 1.509.2
            SSH Credentials Plugin (Jenkins Plugin) 0.4 

* **virtual** machine as **slave**
    * hardware
        
            Memory 1.0 GiB
            Processor Intel® Celeron(R) CPU G1610 @ 2.60GHz
            Disk 20GB
            OS type 64-bit
        
    * software
        
            Ubuntu 11.10 or higher
            SSHD
        

##Jenkins Cluster Setup 
* Create Master
    * Use Ubuntu 11.10 as example
    
        `$ VM=Jenkins`

    * Create a 20GB "dynamic" disk
    
        `$ VBoxManage createhd --filename $VM.vdi --size 20480`
    
    * List the OS types VirtualBox recognises
    
        `$ VBoxManage list ostypes`
    
    * Copy the most appropriate one
    
        `$ VBoxManage createvm --name $VM --ostype "Ubuntu_64" --register`
* Create SLave
* Clone SLave
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
        *  
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

## Projects to be tested
* Django
    * This is a web project based on Django framework.
    * dependency
    
            Selenose
            Python 2.7.2
            Django 1.5
            PostgreSQL 9.1.9
            MongoDB 2.0.4

* Android
* SCM

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
