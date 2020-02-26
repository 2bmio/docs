# Tools

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
systemctl stop libvirtd

# virtualbox
systemctl status vboxautostart-service.service
systemctl enable vboxautostart-service.service
systemctl start vboxautostart-service.service
systemctl stop vboxautostart-service.service



```

### VirtualBox



