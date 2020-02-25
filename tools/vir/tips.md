# Tips

## kubectl ninja commands

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
      ```
9. **Traerte el estado de los componentes**
   1. ```text
      kubectl get componentstatuses
      ```
10. **Traerte los recursos disponibles**
    1. ```text
       kubectl api-resources
       ```





