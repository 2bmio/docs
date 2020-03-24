# Tips

## BASH ninja

```text
bash --rcfile /tmp/.xx.sshrc.XXXX/sshrc.bashrc
```

### rbash

```text
# restricted bash

cp /bin/bash /bin/rbash

# new user
useradd -s /bin/rbash localuser

# existing user
usermod -s /bin/rbash localuser

# create dir for allowd progs
mkdir /home/localuser/programs



# cat /home/localuser/.bash_profile  
# .bash_profile  

# Get the aliases and functions  
if [ -f ~/.bashrc ]; then  
. ~/.bashrc  
fi  
# User specific environment and startup programs  
PATH=$HOME/programs  
export PATH


# create soft links to bin
ln -s /bin/date /home/localuser/programs/  
ln -s /bin/ls /home/localuser/programs/  


# add/remove inmutable permissions
chattr +i /home/localuser/.bash_profile
chattr +i /home/localuser/.bashrc
chattr -i /home/localuser/.bash_profile





```

## K8S ninja

### [Essential](https://agrimprasad.com/post/supercharge-kubernetes-setup/)

```text
# use versions
KUBECTLVERSION=v1.16.6
curl -LO https://storage.googleapis.com/kubernetes-release/release/$KUBECTLVERSION/bin/linux/amd64/kubectl
mv kubectl kubectl-$KUBECTLVERSION && mv kubectl-$KUBECTLVERSION ~/.kube/01-extras/bin/
sudo ln -sf ~/.kube/01-extras/bin/kubectl-$KUBECTLVERSION /usr/local/bin/kubectl

# kube-ps1

# get all Deployment and DeploymenConfig
kubectl get dc --all-namespaces > all-dc.txt

# namespaces
kubectl get netnamespaces

```

### Logging

```text
# if you have multiple pods
kubectl -n kube-system logs -f $(kubectl -n kube-system get pods -l app=traefik  -o jsonpath='{.items[0].metadata.name}')

# if you have just one pod
kubectl -n kube-system logs -f -l app=traefik

```

1. **Kubectl Autocomplete**
   1. ```text
      source <(kubectl completion zsh)
      source <(kubectl completion bash)

      ## add to zsh
      echo "if [ $commands[kubectl] ]; then source <(kubectl completion zsh); fi" >> ~/.zshrc

      ## add to bash
      echo "source <(kubectl completion bash)" >> ~/.bashrc

      ## add to sshrc
      echo "source <(kubectl completion bash)" >> ~/.sshrc

      ```
2. **Kubectl delete from file**
   1. ```text
      kubectl apply -f manifest.yaml
      kubectl delete -f manifest.yaml
      ```
3. **Kubectl Run → DEBUG**
   1. ```text
      kubectl run -it alpine --image=alpine -- sh
      ```
4. **Get pods con labels**
   1. ```text
      kubectl get pods -l run=nginx --all-namespaces
      ```
5. **Get pods \(o cualquier cosa\) diferente formato**
   1. ```text
      kubectl get pods -o=name
      kubectl get pods -o=wide
      kubectl get pods -o=yaml
      kubectl get pods -o=json
      ```

      \*\*\*\*
6. **Get pods para hacer un manifest**
   1. ```text
      kubectl -n nginx1 get pod nginx-6fd8984946-8m648 -o yaml --export
      ```
7. **Get the version label of all pods with label app=cassandra**
   1. ```text
      kubectl get pods -l run=nginx --all-namespaces -o \
        jsonpath='{.items[*].spec.containers[*].image}'
      ```
8. **Estadisticas de un o varios nodos**
   1. ```text
      kubectl top node <nombre-del-nodo>
      kubectl top nodes

      kubectl top pods --heapster-namespace='openshift-infra' --heapster-scheme="https" --all-namespaces
      kubectl top nodes --heapster-namespace='openshift-infra' --heapster-scheme="https"

      kubectl top pods --heapster-namespace='openshift-infra' --heapster-scheme="https" | sort -k3 -n
      kubectl top nodes --heapster-namespace='openshift-infra' --heapster-scheme="https" --all-namespaces

      CPU optiona reverse case append -r
      | sort -k2 -n
      MEMORY optiona reverse case append -r
      | sort -k3 -n


      ## OCP 3.6
      oc adm top nodes --heapster-namespace='openshift-infra' --heapster-scheme="https"
      oc adm top pods --heapster-namespace='openshift-infra' --heapster-scheme="https" --all-namespaces


      ```
9. **Traerte el estado de los componentes**
   1. ```text
      kubectl get componentstatuses
      ```
10. **Traerte los recursos disponibles**
    1. ```text
       kubectl api-resources
       kubectl api-versions
       ```

### BatchScale

```text
#!/bin/bash

LIST='namespace-1 namespace-2 namespace-3'
input=''
for namespace in $LIST
do
  kubectl get dc -n $namespace > /tmp/dc-$namespace.txt
  awk '{print $1, $3, $4}' /tmp/dc-$namespace.txt > /tmp/dc-$namespace-dribble.txt
  sed '1d' /tmp/dc-$namespace-dribble.txt > /tmp/dc-$namespace.txt

  input="/tmp/dc-$namespace.txt"
  while IFS=" " read -r name desired current remainder
    do
      # Skip if the dc have 0 as desired state
      if [ "$desired" -eq 0 ]; then
          echo "nothing to do here! →→→ $name"
      # Scale when desired stata is other than 0
        elif [ "$desired" -gt 0 ]; then
        # kubectl scale dc $1 -n $namespace --replicas=0
          echo "we need scaledown →→→ $name"
      fi
    sleep 3
    done < "$input"
done

```



### [Plugins](https://github.com/kubernetes-sigs/krew)

#### [Krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/)

```text

# search all available plugins
k krew serarch

# show all installed plugins
k krew list

k kubectl krew update

# install a plugin named "view-secret"
kubectl krew install XXXXXX

# use the plugin
kubectl XXXXXX

# upgrade installed plugins
kubectl krew upgrade

# uninstall a plugin
kubectl krew uninstall view-secret

config-cleanup                  Automatically clean up your kubeconfig              no
get-all                         Like `kubectl get all` but _really_ everything      no
resource-capacity               Provides an overview of resource requests, limi...  no
resource-snapshot               Prints a snapshot of nodes, pods and HPAs resou...  no
change-ns                       View or change the current namespace via kubectl.   no
ns                              Switch between Kubernetes namespaces                no
sort-manifests                  Sort manifest files in a proper order by Kind       no
sniff                           Start a remote packet capture on pods using tcp...  no
view-secret                     Decode Kubernetes secrets                           no
view-serviceaccount-kubeconfig  Show a kubeconfig setting to access the apiserv...  no

kubectl get sectrets
kubectl view-secret XXXX

```

#### [Stern](https://github.com/wercker/stern)

#### [Kubeselect](https://github.com/fatliverfreddy/kubeselect)

#### [Kubectx / Kubens](https://github.com/ahmetb/kubectx)

```text
USAGE:
  kubectx                   : list the contexts
  kubectx <NAME>            : switch to context <NAME>
  kubectx -                 : switch to the previous context
  kubectx -c, --current     : show the current context name
  kubectx <NEW_NAME>=<NAME> : rename context <NAME> to <NEW_NAME>
  kubectx <NEW_NAME>=.      : rename current-context to <NEW_NAME>
  kubectx -d <NAME>         : delete context <NAME> ('.' for current-context)
                              (this command won't delete the user/cluster entry
                              that is used by the context)
  kubectx -u, --unset       : unset the current context

USAGE:
  kubens                    : list the namespaces
  kubens <NAME>             : change the active namespace
  kubens -                  : switch to the previous namespace
  kubens -c, --current      : show the current namespace

```

#### 

## SSH ninja

1. **Agent fordwarding**
   1. ```text
      Procedimiento para poder acceder a un servidor (remotehost) al que necesitemos entrar mediante una máquina de salto (jumpserver) con una clave privada que tengamos en nuestro host sin tener que copiarla a la máquina de salto (para no exponer la clave).
      Valdría también para hacer pull a un repo en un host remoto usando nuestras claves de github, por ejemplo, sin copiar estas al host.

      Usamos SSH agent forwarding:

      El procedimiento es comprobar si el ssh-agent está arrancado:

      	$ ssh-agent

      Y si no lo está arrancarlo:

      	$ eval `ssh-agent`

      Añadir la clave (o claves) que queramos usar al agente:

      	$ ssh-add my_private_key.pem

      Comprobar qué claves están añadidas al agente:

      	$ ssh-add -l

      Conectarnos al jumpserver con el flag -A para activar el agent forwarding

      	$ ssh -A -i my_private_key.pem user@jumpserver

      Y desde el jumpserver ya podremos hacer ssh al host remoto usando nuestra clave privada sin tener que exponerla, el agent forwarding se encargará de reenviar las credenciales desde nuestro host si son necesarias:

      	jumpserver$ ssh user@remotehost

      Un poco de literatura:

      https://www.ssh.com/ssh/agent

      https://dev.to/levivm/how-to-use-ssh-and-ssh-agent-forwarding-more-secure-ssh-2c32



      ```
2. Tuner and Port fordwarding
   1. ```text
      # ssh -i ~/.ssh/id_rsa -f <USER>@<HOST> -L <PORT>:localhost:<PORT> -N
      ```

## CMD ninja

### Stress tools

#### CPU

The following command will generate a CPU load by compressing a stream of random data and then sending it to `/dev/null`:

```text
cat /dev/urandom | gzip -9 > /dev/null
```

If you require a greater load or have a multi-core system simply keep compressing and decompressing the data as many times as you need e.g.:

```text
cat /dev/urandom | gzip -9 | gzip -d | gzip -9 | gzip -d > /dev/null
```

```text
vi cpu-stress.sh
 
#!/bin/bash
while true
do
  date +"%H:%M:%S"
  sleep 1
  sleep 0.005
  sleep 0.001
done
 
chmod  +x cpu-stress.sh && ./cpu-stress.sh
```

#### Memory

The following process will reduce the amount of free RAM. It does this by creating a file system in RAM and then writing files to it. You can use up as much RAM as you need to by simply writing more files.

First, create a mount point then mount a `ramfs` filesystem there:

```text
mkdir z
mount -t ramfs ramfs z/
```

Then, use `dd` to create a file under that directory. Here a 128MB file is created:

```text
dd if=/dev/zero of=z/file bs=1M count=128
```

The size of the file can be set by changing the following operands:

* **bs=** Block Size. This can be set to any number followed **B** for bytes, **K** for kilobytes, **M** for megabytes or **G** for gigabytes.
* **count=** The number of blocks to write.

#### Disk

We will create disk I/O by firstly creating a file, and then use a for loop to repeatedly copy it.

This command uses `dd` to generate a 1GB file of zeros:

```text
dd if=/dev/zero of=loadfile bs=1M count=1024
```

The following command starts a for loop that runs 10 times. Each time it runs it will copy `loadfile` over `loadfile1`:

```text
for i in {1..10}; do cp loadfile loadfile1; done
```

If you want it to run for a longer or shorter time change the second number in `{1..10}`.

If you prefer the process to run forever until you kill it with `CTRL+C` use the following command:

```text
while true; do cp loadfile loadfile1; done
```



### CPU output

```text
# get CPU env

grep physical.id /proc/cpuinfo | sort -u | wc -l
grep cpu.cores /proc/cpuinfo
grep processor /proc/cpuinfo | sort -u | wc -l
grep processor /proc/cpuinfo | wc -l
cat /proc/cpuinfo

# get CPU usage
ps -eo user,pid,ppid,cmd,%mem,%cpu,stat,start --sort=-%cpu | head
watch "ps -eo user,pid,ppid,cmd,%mem,%cpu,stat,start --sort=-%cpu | head"

# great script that print memory_disk_cpu_usage

vi memory_disk_cpu_usage.sh

#! /bin/bash
printf "Date\t\t\tMemory\t\tDisk\t\tCPU\n"
end=$((SECONDS+3600))
while [ $SECONDS -lt $end ]; do
CURRENTDATE=`date +"%Y-%m-%d %T"`
MEMORY=$(free -m | awk 'NR==2{printf " \t%.2f%%\t\t", $3*100/$2 }')
DISK=$(df -h | awk '$NF=="/"{printf "%s\t\t", $5}')
CPU=$(top -bn1 | grep load | awk '{printf "%.2f%%\t\t\n", $(NF-2)}')
echo  ${CURRENTDATE} "$MEMORY$DISK$CPU"
sleep 5
done

chmod +x memory_disk_cpu_usage.sh && ./memory_disk_cpu_usage.sh
```

### MEMORY output

```text
ps -eo user,pid,ppid,cmd,%mem,%cpu,stat,start --sort=-%mem | head

continuous reporting
watch "ps -eo user,pid,ppid,cmd,%mem,%cpu,stat,start --sort=-%mem | head"

###################
Display top ten processes using swap space with percentage values
Read (see 1st command) or calculate (see 2nd command) total available swap space to calculate and display per process percentage swap usage. Both of these commands are equivalent.

$ find /proc -maxdepth 2 -path "/proc/[0-9]*/status" -readable -exec awk -v FS=":" -v TOTSWP="$(cat /proc/meminfo | sed  -n -e "s/^SwapTotal:[ ]*\([0-9]*\) kB/\1/p")" '{process[$1]=$2;sub(/^[ \t]+/,"",process[$1]);} END {if(process["VmSwap"] && process["VmSwap"] != "0 kB") {used_swap=process["VmSwap"];sub(/[ a-zA-Z]+/,"",used_swap);percent=(used_swap/TOTSWP*100); printf "%10s %-30s %20s %6.2f%\n",process["Pid"],process["Name"],process["VmSwap"],percent} }' '{}' \;  | awk '{print $(NF-2),$0}' | sort -hr | head | cut -d " " -f2-
$ find /proc -maxdepth 2 -path "/proc/[0-9]*/status" -readable -exec awk -v FS=":" -v TOTSWP="$(cat /proc/swaps | sed 1d | awk 'BEGIN{sum=0} {sum=sum+$(NF-2)} END{print sum}')" '{process[$1]=$2;sub(/^[ \t]+/,"",process[$1]);} END {if(process["VmSwap"] && process["VmSwap"] != "0 kB") {used_swap=process["VmSwap"];sub(/[ a-zA-Z]+/,"",used_swap);percent=(used_swap/TOTSWP*100); printf "%10s %-30s %20s %6.2f%\n",process["Pid"],process["Name"],process["VmSwap"],percent} }' '{}' \;  | awk '{print $(NF-2),$0}' | sort -hr | head | cut -d " " -f2-

###################
Print state

$ awk '$3=="kB"{if ($2>1024^2){$2=$2/1024^2;$3="GB";} else if ($2>1024){$2=$2/1024;$3="MB";}} 1' /proc/meminfo | column -t

MemTotal:           19.3539  GB
MemFree:            6.9542   GB
MemAvailable:       15.3463  GB
Buffers:            30.9141  MB
```

### SPACE output

```text
du -ksh * | sort -nr
df -h  | sort -nr
du -sm * | sort -nr

# example
cd /var/log
du -ksh * | sort -h

# list block devices
lsblk

```

### MODELING output

```text
man sort

  -M, --month-sort            compare (unknown) < 'JAN' < ... < 'DEC'
  -r, --reverse               reverse the result of comparisons
  -n, --numeric-sort          compare according to string numerical value
  
#################  
  
#!/bin/bash

while : ; do

w
sleep 3
true
done


#################
```

## Vi - Vim ninja

```text
### Vim

# Append absolute line numbers
# open .vimrc and add
set number

# teporarily disable absolute line numbers
:set nonumber

# Append relative line numbers
# open .vimrc and add
set relativenumber

# teporarily disable relative line numbers
:set norelativenumber

# find and replace

:%s/foo/bar/g
    Find each occurrence of 'foo' (in all lines), and replace it with 'bar'. 

:s/foo/bar/g
    Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'. 

:%s/foo/bar/gc
    Change each 'foo' to 'bar', but ask for confirmation first. 

:%s/\<foo\>/bar/gc
    Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation. 

:%s/foo/bar/gci
    Change each 'foo' (case insensitive due to the i flag) to 'bar'; ask for confirmation. 
    :%s/foo\c/bar/gc is the same because \c makes the search case insensitive. 
    This may be wanted after using :set noignorecase to make searches case sensitive (the default). 

:%s/foo/bar/gcI
    Change each 'foo' (case sensitive due to the I flag) to 'bar'; ask for confirmation. 
    :%s/foo\C/bar/gc is the same because \C makes the search case sensitive. 
    This may be wanted after using :set ignorecase to make searches case insensitive. 

```

## [jq](https://stedolan.github.io/jq/) + [yq](https://github.com/mikefarah/yq) + [jid](https://github.com/simeji/jid)

```text

#
kubectl get no -o json | jid -q | pbcopy

# Boxing the result into it's own array and constructing a new object combining several nested attributes gives us the following query:
kubectl get no -o json | jq -r '[.items[] | {name:.metadata.name, id:.spec.externalID, unschedulable:.spec.unschedulable}]'

# Converting the json array into a tabular output with jq can be done using @tsv as follows:
kubectl get no -o json | jq -r '.items[] | select(.spec.unschedulable!=true) | [.metadata.name,.spec.externalID] | @tsv'

# Jq also allows us to sort:
kubectl get po -o json | jq -r '.items | sort_by(.spec.nodeName)[] | [.spec.nodeName,.metadata.name] | @tsv'

#
kubectl get po -o wide --sort-by=.spec.nodeName


```

## Curl

```text
# get trace
curl -lv https://sub.domain.tld/checks
# get response
curl -kI https://sub.domain.tld


```

## Sort

```text

```

## Sed

```text
# remove 'deploymentconigs/' from a text
sed 's/deploymentconfigs[\/&]//g'

# remove first line in a text
sed '1d' dc-temp2.txt  > dc.txt

```

## [awk](https://www.tutorialspoint.com/awk/awk_basic_examples.htm)

**Parámetros de awk**

Por otro lado, puedes utilizar algunos parámetros que te facilitarán enormemente el trabajo con `awk`. Algunos de estos parámetros son los siguientes,

* `$0`. Se corresponde con una línea completa.
* `$1, $2, $3,....`. Se corresponden con la primera palabra, con la segunda palabra, etc.
* `FS`. Es el separador.
* `NF`. Es el número de palabras de una línea.

```text
awk '{print $1, $3, $4}' dc-temp.txt
```

