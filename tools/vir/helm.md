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
helm install <name-deploy> stable/joomla


#---------------------------------------------

# # # # # # # # # # # # # # # # 
#    TESTING INS
# # # # # # # # # # # # # # # # 

h3 install wordpress stable/wordpress
k get services
h3 delete --purge wordpress

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

{% hint style="info" %}
new **Chart.yaml** declaration way:

```yaml
apiVersion: v2
name: mychart
description: A Helm chart for k8s
type: library

dependencies:
- name: mariadb
  version: 5.x.x
  repository: https://kubernetes-charts.storage.googleapis.com
  tags:
    - database

```

* apiVersion: v2
* type: library
* dependencies: ...
{% endhint %}

### Migrating

```text
# installin plugins

h3 plugin install https://github.com/helm/helm-2to3
h3 plugin list
h3 2to3

# migrate 
h3 2to3 move config -h
h3 2to3 move config ./<NameChart>  --dry-run




```

### Local Chart

```text
# Create Your Own Chart
h3 create <NameChart>

# Install 
h3 install [NAME] [CHART → ./<NameChart>]

# Not install anything but print final template
h3 install [NAME] [CHART → ./<NameChart>] [flags  < --debug --dry-run >]

# get info
h3 get manifest <release-name>

# 
h3 uninstall <release-name>
```

### Remote Charts

```text
# adding Helm chart
h3 repo add stable https://kubernetes-charts.storage.googleapis.com/
h3 repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/




# update repo
h3 repo update

# list down all the stable charts
h3 search repo stable
h3 search repo incubator

# searching Charts
h3 search hub mysql
h3 search repo mysql
h3 repo list

# install
h3 install <release-name> <chart-name>


# you can see all your releases with
h3 list

# for modify the default chart values, you can show the values with:
h3 show value <release-name>/<chart-name>
# or
h3 install --set mysqlPassword=admin,mysqlUser=admin stable/mysql
```









