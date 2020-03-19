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
systemctl disable libvirtd
systemctl stop libvirtd


# virtualbox
systemctl status vboxautostart-service.service
systemctl enable vboxautostart-service.service
systemctl start vboxautostart-service.service
systemctl stop vboxautostart-service.service



```

### VirtualBox

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



