---
description: Trouble-Sothing
---

# Trouble

## recovering/downgrade kernel version

```text
# on arch


blkid | grep crypto
cryptsetup luksOpen /dev/sda2 recover
mount /dev/vg0/root /mnt
arch-chroot /mnt

yay -s downgrade
downgrade linux

```

## docker

```text

# tar: invalid magic when building docker image
# ar: invalid magic
# tar: short read

docker build --tag=doctl --build-arg DOCTL_VERSION=1.33.1 .


######## enable docker remote API 
Navigate to /lib/systemd/system in your terminal and open docker.service file
vim /lib/systemd/system/docker.service

Find the line which starts with ExecStart and adds -H=tcp://0.0.0.0:2375 to make it look like
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375
Save the Modified File

Reload the docker daemon
sudo systemctl daemon-reload

Restart the container
sudo service docker restart

Test if it is working by using this command, if everything is fine below command should return a JSON
curl http://localhost:2375/images/json



```



