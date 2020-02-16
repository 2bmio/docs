# Helm

### Install

```text
# get available list for microk8s
snap info helm

sudo snap install helm --classic
sudo snap install helm --classic --channel=3.1/stable

sudo mkdir /var/snap/microk8s/current/bin

# create symbolic link to use helm with microk8s
sudo ln -s /snap/bin/helm /var/snap/microk8s/current/bin/helm

```

### Commands

```text
helm version






```

