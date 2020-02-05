# Pods

## HPA → horizontal Pod AutoScaling

## Quarantine technique → labels + selectorS

```text
apiVersion: v1
kind: Service
metadata:
    name: hello
spec:
    selector:
        role: hello
```

