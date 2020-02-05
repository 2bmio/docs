# Pods

## HPA → Horizontal Pod AutoScaling

isn't handly scale replicas for each one deployment. On this way the best practice is used  **HPA** with rules that apply → if CPU is upper to some percentage increase Pod else ... 

## Quarantine technique → labels + selectorS

Service is the handler of traffic cross pod, on that label selector → role → **hello** who match with the same label on the pod send traffic to it.

```yaml
apiVersion: v1
kind: Service
metadata:
    name: hello
spec:
    selector: ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←
        role: hello ←←←←←←←←←←←←←←←←←←←←←←←←←

---

apiVersion: v1beta1
kind: Deployment
metadata:
    name: hello
spec:
    replicas: 3
    template:
        metadata:
            labels: ←←←←←←←←←←←←←←←←←←←←←←←←←
                role: hello ←←←←←←←←←←←←←←←←←

```

Overwrite label to put it in quarantine.

```bash
kubectl label pod hello-79a8sdf99d-g2939 \
role=quarantine --overwrite
```



