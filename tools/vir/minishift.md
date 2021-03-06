# Minishift

```text
minishift status
minishift config view
```

## Standard

### installation

> Step 1: Install Hypervisor VirtualBox or KVM
>
> Step 2: Setting up Minishift hypervisor Driver

#### For Ubuntu / Debian

```text
sudo usermod -a -G libvirt $(whoami)
newgrp libvirt || newgrp libvirtd
curl -L https://github.com/dhiltgen/docker-machine-kvm/releases/download/v0.10.0/docker-machine-driver-kvm-ubuntu16.04 -o docker-machine-driver-kvm
sudo mv docker-machine-driver-kvm /usr/local/bin/docker-machine-driver-kvm
sudo chmod +x /usr/local/bin/docker-machine-driver-kvm
```

#### For Fedora / CentOS

```text
sudo usermod -a -G libvirtd $(whoami)
newgrp libvirt
curl -L https://github.com/dhiltgen/docker-machine-kvm/releases/download/v0.10.0/docker-machine-driver-kvm-centos7 -o docker-machine-driver-kvm
sudo mv docker-machine-driver-kvm /usr/local/bin/docker-machine-driver-kvm
sudo chmod +x /usr/local/bin/docker-machine-driver-kvm
```

#### For Arch Linux / Manjaro

```text
sudo usermod -a -G kvm,libvirt $(whoami)
sudo sed -ri 's/.?group\s?=\s?".+"/group = "kvm"/1' /etc/libvirt/qemu.conf
newgrp libvirt
curl -L https://github.com/dhiltgen/docker-machine-kvm/releases/download/v0.10.0/docker-machine-driver-kvm-centos7 -o docker-machine-driver-kvm
sudo mv docker-machine-driver-kvm /usr/local/bin/docker-machine-driver-kvm
chmod +x /usr/local/bin/docker-machine-driver-kvm
```

#### Start the default KVM network.

```text
sudo virsh net-start default
sudo virsh net-autostart default
```

> Step 3: Install Minishift check version → [https://github.com/minishift/minishift/releases](https://github.com/minishift/minishift/releases)

```text
export VER="1.34.1"
curl -L https://github.com/minishift/minishift/releases/download/v$VER/minishift-$VER-linux-amd64.tgz -o minishift-$VER-linux-amd64.tgz
tar xvf minishift-$VER-linux-amd64.tgz
sudo mv minishift-$VER-linux-amd64/minishift /usr/local/bin 
$ minishift version
    minishift v1.34.1+c2ff9cb

sudo dnf install libvirt qemu-kvm -y
sudo usermod -a -G libvirt $USER
newgrp libvirt

sudo curl -L https://github.com/dhiltgen/docker-machine-kvm/releases/download/v0.7.0/docker-machine-driver-kvm -o /usr/local/bin/docker-machine-driver-kvm
sudo chmod +x /usr/local/bin/docker-machine-driver-kvm
```

### playground

```text
1. Create Template

    - `oc create -f openjdk-web-basic-s2i.yml  -n openshift`

2. Create ImageStream

    - `oc create is "openjdk-11-rhel7" -n openshift`

minishift ssh

3. Docker PULL

    - `docker pull registry.redhat.io/openjdk/openjdk-11-rhel7:1.1`

4. Docker PULL
$(minishift openshift registry)

docker tag registry.redhat.io/openjdk/openjdk-11-rhel7:1.1 172.30.1.1:5000/openshift/openjdk-11-rhel7:1.1
docker login -u admin -p kiCcJoQiI-iaoffUfstXaDnsxLwm3lGSPNY2fxBcUk4 172.30.1.1:5000
docker push 172.30.1.1:5000/openshift/openjdk-11-rhel7:1.1
```

> essntials commands

```text
$ minishift start --cpus=4 --memory=8192 --vm-driver virtualbox
$ minishift config set vm-driver virtualbox
$ minishift console
$ minishift console --url
$ oc login -u system:admin
$ oc login -u admin
```

#### esentials addons

```text
$ minishift addons apply registry-route admin-user
$ eval $(minishift docker-env)
$ eval $(minishift oc-env)
$ oc login -u admin -p admin
$ docker login -u admin -p `oc whoami -t` docker-registry-default.192.168.99.102.nip.io
```

#### pushing images to registry

```text
docker tag rundeck/rundeck:3.2.1 docker-registry-default.192.168.99.102.nip.io/openshift/rundeck:3.2.1
docker push docker-registry-default.192.168.99.102.nip.io/openshift/rundeck:3.2.1
```

oc create is "rundeck" -n openshift

1. Create Template
   * `oc create -f openjdk-web-basic-s2i.yml  -n openshift`
2. Create ImageStream
   * `oc create is "openjdk-11-rhel7" -n openshift`
3. Docker PULL
   * `docker pull registry.redhat.io/openjdk/openjdk-11-rhel7:1.1`
4. Docker TAG
   * `docker tag registry.redhat.io/openjdk/openjdk-11-rhel7:1.1 docker-registry.default.svc:5000/openshift/openjdk-11-rhel7:1.1`
5. Docker PUSH
   * `docker login -u admin -p $(oc whoami -t) -u unused docker-registry.default.svc:5000`
   * `docker push docker-registry.default.svc:5000/openshift/openjdk-11-rhel7:1.1`

```text

```

```text

```

```text

```

