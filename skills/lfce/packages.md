# Packages

## OpenSSL

```text
# Check certificate Validity:
## just notAfter output:
openssl x509 -enddate -noout -in <cert.name>

## all the cert info output:
openssl x509 -text -noout -in <cert.name>


```

## OpenSSH

```text
# use credentials from first machine with jumping nodes
ssh -A root@gitlab.vass.es
```

## Bash

```text
bash --rcfile /tmp/.user.sshrc.bbYJ/sshrc.bashrc
```

