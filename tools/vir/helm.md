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
helm repo add stable 
helm search repo mariadb


# deprecated
helm init
helm repo update
helm install stable/joomla


```

### Components

* CLI
* Tiller \(deprecated V3\)
* k8s API

### Vocabulary

* Chart
* Template
* Release

## Helm 3

```yaml
apiVersion: v2
name: mychart
description: A Helm chart for k8s

dependencies:
- name: mariadb
  version: 5.x.x
  repository: https://kubernetes-charts.storage.googleapis.com
  tags:
    - database

```

