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

### commons commands

```text
popeye --kubeconfig=~/.kube/config

SUMMARY
┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅┅
Your cluster score: 84 -- B


```

## Git

```text
# check if local repo is up to date
git fetch -v --dry-run

```

