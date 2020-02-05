# Pods

## HPA → Horizontal Pod AutoScaling

> Using RULES k8s increase or decrease PODs to satisfy it.

**Where is the magic of HPA?**  → it have an end point what are on the controller what collect the metrics `/metrics`  

isn't handly scale replicas for each one deployment. On this way the best practice is used  **HPA** with rules that apply → if CPU/Memory is upper to some percentage increase Pod else ...

```yaml
apiVersion: v1
kind: Service
metadata:
  name: php-apache
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30000
  selector:
    role: php-apache
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: php-apache
spec:
  replicas: 3
  template:
    metadata:
      labels:
        role: php-apache
    spec:
      containers:
      - name: php-apache
        image: k8s.gcr.io/hpa-example
        imagePullPolicy: IfNotPresent        
        ports:
        - containerPort: 80
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: "password"
        resources:
          requests:
            memory: "64Mi"
            cpu: "200m"
          limits:
            memory: "128Mi"
            cpu: "500m"
---
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: php-apache
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: php-apache
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50

---
# extended example of HPA
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: php-apache
  namespace: default
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: php-apache
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
status:
  observedGeneration: 1
  lastScaleTime: <some-time>
  currentReplicas: 1
  desiredReplicas: 1
  currentMetrics:
  - type: Resource
    resource:
      name: cpu
      current:
        averageUtilization: 0
        averageValue: 0
```



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



