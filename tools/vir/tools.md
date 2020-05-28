# Tools

## Iptables

```text
iptables -L
iptables -S
iptables -F



snat_dnat_advantech
https://gist.github.com/tomasinouk/eec152019311b09905cd


```

## [Popeye](https://github.com/derailed/popeye)

```text
# install on centos 7
yum install snapd -y
systemctl enable --now snapd.socket
systemctl start --now snapd.socket
ln -s /var/lib/snapd/snap /snap
snap install popeye 

# install on debian based
snap install popeye 

# get info about popeye
snap info popeye
```

### common commands

```text
popeye --kubeconfig=~/.kube/config

SUMMARY
┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅
Your cluster score: 84 -- B


```

## [Git](https://education.github.com/git-cheat-sheet-education.pdf)

### common commands

```text
# check if local repo is up to date
git fetch -v --dry-run

# download submodules
## Pull all submodules using
git submodule update --init --recursive

## update submodules
git submodule update --recursive --remote
### or
git pull --recurse-submodules


# tell git exclude specific files when doing a git merge

## FIRST activate merge ours
git config --global merge.ours.driver true
git config merge.ours.driver true

    cat .git/config
    [merge "ours"]
        driver = true



## SECOND on the main git directory

touch .gitattributes

    *__dev* merge=ours
    .gitattributes merge=ours
    .gitignore merge=ours

    
git-archive

```

### create private fork of a public repo

```text
# Create a bare clone of the repository.
git clone --bare https://github.com/sherifabdlnaby/elastdocker.git
git clone --bare git@github.com:usi-systems/easytrace.git

# Create a new private repository on Github and name it easytrace.
## Mirror-push your bare clone to your new easytrace repository.

cd easytrace.git
git push --mirror git@github.com:<your_username>/easytrace.git

cd ..
rm -rf easytrace.git
cd 

git clone git@github.com:<your_username>/easytrace.git

# If you want, add the original repo as remote to fetch (potential) future changes. Make sure you also disable push on the remote (as you are not allowed to push to it anyway).

git remote add upstream git@github.com:usi-systems/easytrace.git
git remote set-url --push upstream DISABLE

# You can list all your remotes with git remote -v. You should see:

  origin	git@github.com:<your_username>/easytrace.git (fetch)
  origin	git@github.com:<your_username>/easytrace.git (push)
  upstream	git@github.com:usi-systems/easytrace.git (fetch)
  upstream	DISABLE (push)

```

## Ansible

### common commands

```text
# run independent playbooks
ANSIBLE_CONFIG=./ansible.cfg ansible-playbook playbook.yml --flush-cache
```

### course

## Rundeck

### common commands

```text
############# CREATE USER
https://geekdudes.wordpress.com/2018/02/09/creating-rundec-acl-policies/

ejemplo crear usuario salesforce:

/etc/rundeck/salesforce.aclpolicy
/etc/rundeck/realm.properties


[root@libs01 rundeck]# cat /etc/rundeck/salesforce.aclpolicy
description: salesforce, all access.
context:
  project: 'PibankTest' # all projects
for:
  resource:
    - equals:
        kind: event
      allow: [read]
  adhoc:
    - deny: [read,running,killing] # allow read/running/killing adhoc jobs
  job:
    - equals:
        name: 'chmod_tmp_sdl.log'
      allow: [read,run,kill] # allow read/write/delete/run/kill of all jobs
  node:
    - allow: [read,run]
by:
  group: salesforce

---

description: salesforce, all access.
context:
  application: 'rundeck'
for:
  resource:
    - equals:
        kind: project
      deny: [create] # deny create of projects
    - equals:
        kind: system
      deny: [read] # allow read of system info
    - equals:
        kind: user
      deny: [admin] # allow modify user profiles
  project:
    - equals:
        name: 'PibankTest'
      allow: [read] # allow access
      deny: [import,export,configure,delete] # deny admin actions
  storage:
    - allow: [read]
    - deny: [admin,create] # allow access for /keys/* storage content
by:
  group: salesforce
```

## [Packer](https://packer.io/docs/builders/index.html)

### common commands

```text
# validate
$ packer validate example.json

# build
$ packer build \
    -var 'aws_access_key=YOUR ACCESS KEY' \
    -var 'aws_secret_key=YOUR SECRET KEY' \
    example.json
```

> Packer is a tool focused on create **custom OS** using **templetes** what can be **versionated**.

### packages

## Terraform

### common commands

```text

```

### concept - general

* domain providers \(aws-gcp-azure-etc\)
* create replicable platforms
* develop complex infrastructures
* create modules and reuse it. use community modules
* use packer

### concept - provider

### concept - template

* first resource
* states
* variables
* outputs
* data sources
* templates

### concept - import resource and modify

### concept - complex templates

* create n resource
* create reusable templates
* create ans asociate multple resource

### concept - advance

* backend
* modules
* community modules



## CloudFormation

## AWS

## Vagrant

### common commands

```text

# to get all available plugins and grep for specific
gem list --remote vagrant-. | grep yaml

```

### packages and addons

```text
# fedora
## install vagrant-libvirt
sudo dnf install libxslt-devel libxml2-devel libvirt-devel libguestfs-tools-c ruby-devel gcc
CONFIGURE_ARGS='with-ldflags=-L/opt/vagrant/embedded/lib with-libvirt-include=/usr/include/libvirt with-libvirt-lib=/usr/lib' GEM_HOME=~/.vagrant.d/gems GEM_PATH=$GEM_HOME:/opt/vagrant/embedded/gems PATH=/opt/vagrant/embedded/bin:$PATH vagrant plugin install vagrant-libvirt

vagrant plugin install vagrant-hostmanager
```

## Virtualization

### common commands

```text
## uncompatible kvm and virtualbox at same time.
# kvm
systemctl status libvirtd
systemctl start libvirtd
systemctl enable libvirtd
systemctl disable libvirtd
systemctl stop libvirtd


# virtualbox
systemctl status vboxautostart-service.service
systemctl enable vboxautostart-service.service
systemctl start vboxautostart-service.service
systemctl stop vboxautostart-service.service






```

### VirtualBox - mojave

```text
vboxmanage list vms

vboxmanage modifyvm "Mojave" --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff

vboxmanage setextradata "Mojave" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"

vboxmanage setextradata "Mojave" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"

vboxmanage setextradata "Mojave" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"

vboxmanage setextradata "Mojave" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"

vboxmanage setextradata "Mojave" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1

```

## Multipass

### Install

#### macOS

```text
brew cask install multipass
```

#### fedora

```text
# prepare for use snap
sudo dnf install snapd
sudo ln -s /var/lib/snapd/snap /snap

# install using snap
sudo snap install multipass --classic

# fix user permissions
sudo chown $USER:$USER /var/snap/multipass/common/multipass_socket

# get info about multipass
snap info multipass

```

### Comands

```text
# launch:

## single instance
multipass launch --name k8s-master --mem 8G --disk 40G

## multinode 
multipass launch --name k8s-master-1 --mem 2G --disk 20G
multipass launch --name k8s-master-2 --mem 2G --disk 20G
multipass launch --name k8s-master-3 --mem 2G --disk 20G
multipass launch --name k8s-worker-1 --mem 2G --disk 10G
multipass launch --name k8s-worker-2 --mem 2G --disk 10G
multipass launch --name k8s-worker-3 --mem 2G --disk 10G

# getting on
multipass list
multipass shell k8s-master

## using classic ssh with key
### copy the new key to user path
sudo cp /var/snap/multipass/common/data/multipassd/ssh-keys/id_rsa ~/.ssh/id_mpss
### change permissions
sudo chown $USER:$USER ~/.ssh/id_mpss
### connect
ssh ubuntu@<multipass-ip> -i ~/.ssh/id_mpss


```

## Microk8s

### [release](https://microk8s.io/docs/release-notes) notes

### Install

```text
# # # # # # # # # # # # # # # # 
#    MICROK8S
# # # # # # # # # # # # # # # # 

# get available list for microk8s
snap info microk8s

sudo snap install microk8s --classic
sudo snap install microk8s --classic --channel=1.16/stable

sudo usermod -a -G microk8s $USER
sudo iptables -P FORWARD ACCEPT

#---------------------------------------------

# # # # # # # # # # # # # # # # 
#    KUBECTL
# # # # # # # # # # # # # # # # 

# get available list for kubectl
snap info kubectl

sudo snap install kubectl --classic
sudo snap install kubectl --classic --channel=1.16/stable

# logout
mkdir ~/.kube
microk8s.kubectl config view --raw > $HOME/.kube/config


```

### Commands

```text
microk8s.kubectl get nodes
microk8s.add-node
  ubuntu@k8s-master:~$ microk8s.add-node
  Join node with: microk8s.join 192.168.64.3:25000/GdnlcwJRAWzigHhodFPmFTIMQHgrSCIZ

microk8s.status
microk8s.enable --help
microk8s.enable dns storage dashboard


# old way → microk8s.enable dns dashboard ingress helm

## List of the most important addons

*   dns: Deploy DNS. This addon may be required by others, thus we recommend you always enable it.
*   dashboard: Deploy kubernetes dashboard as well as grafana and influxdb.
*   storage: Create a default storage class. This storage class makes use of the hostpath\-provisioner pointing to a directory on the host.
*   ingress: Create an ingress controller.
*   gpu: Expose GPU(s) to MicroK8s by enabling the nvidia\-docker runtime and nvidia\-device\-plugin\-daemonset. Requires NVIDIA drivers to be already installed on the host system.
*   istio: Deploy the core Istio services. You can use the `microk8s.istioctl` command to manage your deployments.
*   registry: Deploy a docker private registry and expose it on localhost:32000. The storage addon will be enabled as part of this addon.

microk8s.kubectl -n kube-system get secret

microk8s.kubectl -n kube-system describe secret kubernetes-dashboard-token-XXXXX

microk8s.kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443 --address 0.0.0.0

https://[microk8s-master-ip]:10443
```

## Kustomize

### install

```text
curl -s "https://raw.githubusercontent.com/\
kubernetes-sigs/kustomize/master/hack/install_kustomize.sh"  | bash
```

### common commands

```text
kustomize build .
```

## SELinux

## Nginx

```text
server {
    listen *:80;
    server_name pxy.pdam.gos.ooo;
    proxy_set_header Host pxy.pdam.gos.ooo;
    location / {
    rewrite ^(.*)$ https://pxy.pdam.gos.ooo$1 permanent;
    }
}

server {
    listen *:443;
    server_name pxy.pdam.gos.ooo;
    proxy_set_header Host pxy.pdam.gos.ooo;

    #The port used for secured Admin Console access:
    set $second_server-or-proxy_port 443;
    #IP address for machine running second_server-or-proxy server:
    set $second_server-or-proxy_ip 192.168.1.130;
    ssl     off;
    ssl_protocols     SSLv3 TLSv1;
    ssl_certificate     /home/user/dump/traefik/certs/pxy.pdam.gos.ooo.crt;
    ssl_certificate_key     /home/user/dump/traefik/private/pxy.pdam.gos.ooo.key;

location / {
    proxy_pass https://$second_server-or-proxy_ip:$second_server-or-proxy_port;
    }
}

```

## asdf

```text
asdf update
asdf plugin list all
asdf plugin add kubectl

asdf list all kubectl

asdf install kunectl 1.17.4
asdf install kubectl 1.17.4

asdf global kubectl 1.17.4

```

## Clonezilla

```text
backup luks partition




1. Boot clonezilla

2. Drop into the command line

3. open the encrypted external drive partition

  sudo su

  blkid | grep crypto

  cryptsetup luksOpen /dev/sdd1 backup

4. mount as partimag

  mount /dev/mapper/backup /home/partimag













5. open the internal encrypted partitions

  cryptsetup luksOpen /dev/sda3 crypt1
  (enter pass)
  cryptsetup luksOpen /dev/sdb1 crypt2
  (enter pass)

6. lvm should automatically appear in /dev/mapper
  e.g. /dev/mapper/fedora-home
       /dev/mapper/fedora-root
  etc
  if not can try vgchange -ay

7. Perform backup with partclone

  partclone.ext4 -c -s /dev/mapper/fedora-root -o /home/partimag/backup/fedora-root-2017-09-24.img

8. When complete can restore to an image file to be able to mount and read:

  touch /mnt/backup/restored.img
  partclone.restore -C -s /home/partimag/backup/fedora-root-2017-09-24.img -O /mnt/backup/restored.img
  mount -t ext4 /mnt/backup/restored.img /mnt/data -o loop

  try to restore to a different device especially if the image is large as the data transfer speed will be halved. It took 8 hours for a 1.4TB partition that was   50% used.

9. If unable to mount image because of "ext4 bad geometry" then fix the image:

  e2fsck -f /mnt/backup/restored.img
  resize2fs /mnt/backup/restored.img
  
  then try to mount again
```

## Rsync

```text
# Copy/Sync Files and Directory Locally
rsync -avzh --progress ubi /home/aa/0-attachup
rsync -avzh --progress /home/aa/0-attachup/ubi /run/media/aa/attachup-1

# Sync with mirror mode
rsync -vazh --delete /home/aa/0-attachup/ubi /run/media/aa/attachup-1

# Copy/Sync Files and Directory to or From a Server
rsync -avz rpmpkgs/ root@192.168.0.101:/home/
rsync -avzh root@192.168.0.100:/home/tarunika/rpmpkgs /tmp/myrpms

# Rsync Over SSH
rsync -avzhe ssh root@192.168.0.100:/root/install.log /tmp/
rsync -avzhe ssh backup.tar root@192.168.0.100:/backups/

# Show Progress While Transferring Data with rsync
rsync -avzhe ssh --progress /home/rpmpkgs root@192.168.0.100:/root/rpmpkgs

# Use of –include and –exclude Options
rsync -avze ssh --include 'R*' --exclude '*' root@192.168.0.101:/var/lib/rpm/ /root/rpm

# Use of –delete Option
rsync -avz --delete root@192.168.0.100:/var/lib/rpm/ .

# Set the Max Size of Files to be Transferred
rsync -avzhe ssh --max-size='200k' /var/lib/rpm/ root@192.168.0.100:/root/tmprpm

# Automatically Delete source Files after successful Transfer
rsync --remove-source-files -zvh backup.tar /tmp/backups/

# Do a Dry Run with rsync
rsync --dry-run --remove-source-files -zvh backup.tar /tmp/backups/

# Set Bandwidth Limit and Transfer File
rsync --bwlimit=100 -avzhe ssh  /var/lib/rpm/  root@192.168.0.100:/root/tmprpm/


```

## Grep

```text
# find specific text into ant .sh file 
grep -r -i --include \*.sh "system:serviceaccount:default:rundeck" ~/000

```

## Scrapy

```text
scrapy startproject sector6202
    cd sector6202
    scrapy genspider example example.com


# Exporting with Feed Export

scrapy crawl myspider -o data.json 
scrapy crawl myspider -o data.csv scrapy crawl myspider -o data.xml
-t json -o outputfile.json
-t csv -o outputfile.csv

# running two crawl at once
scrapy crawl selenium && sleep 5 && scrapy crawl html

____________________________
❯ cat run.py
# !/usr/bin/env python

import subprocess

subprocess.call('for spider in spider-selenium spider-html; do scrapy crawl $spider -L INFO; done', shell=True)


____________________________

#xpath utils 
(//li[@class='arrow'])[last()]/a


(//td[@class="tal website"])[last()-1]/a/text()
(//td[@class="tal website"])[1]/a/text()



Rule(LinkExtractor(allow = (), restrict_xpaths = ('(//li[@class="arrow"])[last()]/a'))),
Rule(LinkExtractor(allow = (), restrict_xpaths = ('(//td[@class="tal"])/a')),

```

## Guacamole

```text

# Archlinux + XFCE

~/.vnc/xstartup

#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
dbus-launch /usr/bin/startxfce4 &



```

## Chrome remote desktop crd

```text
Set up CRD by issuing the command:
crd --setup
as a normal user.

After that, enable access to CRD in your chrome or chromium browser.

To {enable,start} the service, issue the command:
systemctl --user {enable,start} chrome-remote-desktop
This only really makes sense for servers.

You can also start the chrome remote desktop server by issuing the command:
crd --start
as a normal user.
This will prompt you to set up your CRD if it hasn't been set up already.

Go to https://support.google.com/chrome/answer/1649523 for more information.

```

## Ipcalc

```text
ipcalc takes an IP address and netmask and calculates the resulting broadcast,
network

ipcalc 192.168.0.1/24
ipcalc 192.168.0.1/255.255.128.0
ipcalc 192.168.0.1 255.255.128.0 255.255.192.0
ipcalc 192.168.0.1 0.0.63.255

```

## Speed TEST

## Ansible Tower → AWX

```text
## 1. Create a new credential type
## As a Tower admin, you can create a custom credential by clicking on ADMINISTRATION> Credential Types

fields:
  - id: git_private_key
    type: string
    label: private_key
    secret: true
    multiline: true

file:
  template.git_key: "{{ git_private_key  }}"
extra_vars:
  secret_key: "{{ tower.filename.git_key  }}"


```

