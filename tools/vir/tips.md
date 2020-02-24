# Tips

## K8S ninja

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
       ```

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

