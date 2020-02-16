---
description: >-
  Multipass is a lightweight VM manager for Linux, Windows and macOS. It's
  designed for developers who want a fresh Ubuntu environment with a single
  command.
---

# Multipass

## Install

### macOS

```text
brew cask install multipass
```

### fedora

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

## Comands

```text
# launch:

## single instance
multipass launch --name k8s-master --mem 8G --disk 40G

## multinode 
multipass launch --name k8s-master --mem 4G --disk 20G
multipass launch --name k8s-app-1 --mem 2G --disk 10G
multipass launch --name k8s-app-2 --mem 2G --disk 10G

# getting on
multipass list
muttipass shell k8s-master

```

