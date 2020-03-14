# Distos

## Based on Debian

### Ubuntu 18.04

## Based on Red Hat

### RHEL based

### common commands

```text
subcription-manager list
subcription-manager list --available

```

### [Fedora CoreOS](https://docs.fedoraproject.org/en-US/fedora-coreos/faq/) <a id="_what_are_the_communication_channels_around_fedora_coreos"></a>

#### common commands

```text
# install packages
rpm-ostree refresh-md 
rpm-ostree install htop python3 pip

# restart
systemctl reboot

```

#### [source and examples ignition file](https://github.com/coreos/fcct/blob/master/docs/configuration-v1_0.md)

```text
# Fedora CoreOS Config Transpiler 
# https://github.com/coreos/fcct
# https://github.com/coreos/fcct/blob/master/docs/configuration-v1_0.md

./fcct --input fcos.yml --pretty --output fcos.json
```

#### example ignition.ign

```text
{
  "ignition": {
    "config": {
      "replace": {
        "source": null,
        "verification": {}
      }
    },
    "security": {
      "tls": {}
    },
    "timeouts": {},
    "version": "3.0.0"
  },
  "passwd": {
    "users": [
      {
        "name": "core",
        "sshAuthorizedKeys": [
          "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ== vagrant insecure public key"
        ]
      }
    ]
  },
  "storage": {
    "files": [
      {
        "path": "/etc/NetworkManager/system-connections/eth0.nmconnection",
        "mode": 384,
        "overwrite": true,
        "contents": {
          "inline": "[connection]\ntype=ethernet\ninterface-name=eth0\n\n[ethernet]\nmac-address=<insert MAC address>\n\n[ipv4]\nmethod=manual\naddresses=192.168.33.31/25\ngateway=192.168.33.1\ndns=192.168.33.1;1.1.1.1;8.8.8.8\ndns-search=redhat.com\n"
        }
      }
    ]    
  },
  "systemd": {}
}
```

## Based on Arch

### ALMA

```text
sudo alma create /dev/disk/by-id/usb-TOSHIBA_TransMemory_000AEBFFD790B920730C0138-0:0
sudo alma chroot /dev/disk/by-id/usb-TOSHIBA_TransMemory_000AEBFFD790B920730C0138-0:0

pacman -S bridge-utils wireshark-cli net-tools

```

