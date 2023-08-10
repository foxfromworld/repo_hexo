---
title: Getting started with Jenkins on Ubuntu 18.04
date: 2023-08-09 15:12:11
tags: [Jenkins, Ubuntu]
categories: Jenkins
---

## Check prerequisites

### A machine with:

- 256 MB of RAM, although more than 2 GB is recommended

Check with the command below

```
$ free -h
              total        used        free      shared  buff/cache   available
Mem:            15G        4.6G        872M        165M         10G         10G
```

- 10 GB of drive space (for Jenkins and your Docker image)

Check with the command below

```
$ df -h | head -n 1; df -h | grep /dev/sda
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       916G  599G  271G  69% /
/dev/sda1       511M  5.3M  506M   2% /boot/efi
```

### The following software installed:

- Java 11 or Java 17

```
$ java -version

Command 'java' not found, but can be installed with:

sudo apt install default-jre            
sudo apt install openjdk-11-jre-headless
sudo apt install openjdk-8-jre-headless 

$ sudo apt install openjdk-11-jre-headless

...

$ java -version
openjdk version "11.0.19" 2023-04-18
OpenJDK Runtime Environment (build 11.0.19+7-post-Ubuntu-0ubuntu118.04.1)
OpenJDK 64-Bit Server VM (build 11.0.19+7-post-Ubuntu-0ubuntu118.04.1, mixed mode, sharing)
```

- Docker (navigate to [Get Docker](https://docs.docker.com/get-docker/) site to access the Docker download that’s suitable for your platform)

I choose https://docs.docker.com/desktop/install/linux-install/ because I am using Ubuntu 18.04.

#### System requirements for Docker

- QEMU must be version 5.2 or newer.

```
$ sudo apt install qemu-kvm

$ dpkg -s qemu-kvm | grep Version
Version: 1:2.11+dfsg-1ubuntu7.42
```
- Check if the KVM modules are enabled.

```
$ kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used

$ lsmod | grep kvm
kvm_intel             253952  0
kvm                   659456  1 kvm_intel
```

#### Installation of Docker

Follow steps here:　https://docs.docker.com/desktop/install/ubuntu/

If you encountered the dependency issues, please install required packages.

```
$ sudo apt-get install ./docker-desktop-4.22.0-amd64.deb 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Note, selecting 'docker-desktop' instead of './docker-desktop-4.22.0-amd64.deb'
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 docker-desktop : PreDepends: init-system-helpers (>= 1.54~) but 1.51 is to be installed
                  Depends: docker-ce-cli but it is not installable
E: Unable to correct problems, you have held broken packages.
```

Some fixes

```
$ wget http://ftp.kr.debian.org/debian/pool/main/i/init-system-helpers/init-system-helpers_1.60_all.deb
$ sudo apt-get install ./init-system-helpers_1.60_all.deb
$ sudo apt-get update
$ sudo apt-get install ca-certificates curl gnupg lsb-release
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

#### Launch Docker Desktop

```
$ docker compose version
Docker Compose version v2.20.2-desktop.1

$ docker --version
Docker version 24.0.2, build cb74dfc

$ docker version
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/version": dial unix /var/run/docker.sock: connect: permission denied
Client: Docker Engine - Community
 Cloud integration: v1.0.35-desktop+001
 Version:           24.0.2
 API version:       1.43
 Go version:        go1.20.4
 Git commit:        cb74dfc
 Built:             Thu May 25 21:52:13 2023
 OS/Arch:           linux/amd64
 Context:           default
```

Start Docker. Select Accept to continue.

![](docker.PNG)

If you get the error below, run the command below.

![](error.PNG)

```
sudo usermod -aG kvm $USER
```

Then I got this...

![](error2.PNG)

Tried to run /opt/docker-desktop/bin/com.docker.diagnose check

```
Starting diagnostics

[PASS] DD0039: are KVM user permissions configured?
[PASS] DD0018: does the host support virtualization?
[PASS] DD0001: is the application running?
[FAIL] DD0017: can a VM be started? vm has not started: failed to open kmsg.log: open /home/username/.docker/desktop/log/vm/kmsg.log: no such file or directory
[FAIL] DD0016: is the LinuxKit VM running? prereq failed: can a VM be started?
[FAIL] DD0011: are the LinuxKit services running? prereq failed: is the LinuxKit VM running?
[FAIL] DD0004: is the Docker engine running? prereq failed: are the LinuxKit services running?
[PASS] DD0015: are the binary symlinks installed?
[FAIL] DD0031: does the Docker API work? prereq failed: is the Docker engine running?
[PASS] DD0013: is the $PATH ok?
[FAIL] DD0034: is Context set to a Docker Desktop context? CLI context is set to docker-ce engine
[FAIL] DD0003: is the Docker CLI working? prereq failed: is the Docker engine running?
[FAIL] DD0038: is the connection to Docker working? prereq failed: is the Docker engine running?
[FAIL] DD0014: are the backend processes running? prereq failed: is the LinuxKit VM running?
[FAIL] DD0007: is the backend responding? prereq failed: are the backend processes running?
```

Try to install LinuxKit

```
$ git clone https://github.com/linuxkit/linuxkit
$ cd linuxkit
$ sudo make
$ sudo make install
```

The issue is still not solved. I even checked the setting of Intel virtualization technology and VT-d in the BIOS. They were already enabled...

So I proceeded to install Jenkins...

https://pkg.jenkins.io/debian/

After the installation, browse to http://localhost:8080.

![](unlock.PNG)

Use the command below to get the password to unlock Jenkins.

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Install suggested plugins and wait for the installation to finish.

After the installation, create the first admin user

At "Instance Configuration", click on "Save and Finish", then "Start using Jenkins".