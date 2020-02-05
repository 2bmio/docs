# Pods

## HPA → horizontal Pod AutoScaling

## Quarantine technique → labels + selectorS

Service is the handler of traffic cross pod, on that label selector → role → **hello** who match with the same label on the pod send traffic to it.

```text
apiVersion: v1
kind: Service
metadata:
    name: hello
spec:
    selector:
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
            labels:
                role: hello ←←←←←←←←←←←←←←←←←

```

