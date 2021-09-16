# Kubernetes Deployment Strategies
       
## Helloworld Spring Boot app
`git clone https://github.com/ngtrainings/teamchallenges.git`

## Reference links
Link to Brandon Potter's YML builder - [https://static.brandonpotter.com/kubernetes/DeploymentBuilder.html](https://static.brandonpotter.com/kubernetes/DeploymentBuilder.html)

Link to Deployment Strategies - [https://blog.container-solutions.com/kubernetes-deployment-strategies](https://blog.container-solutions.com/kubernetes-deployment-strategies) 

Link to Deployment Strategies - [https://dzone.com/articles/blue-green-deployments-ab-testing-and-canary-relea-2] (https://dzone.com/articles/blue-green-deployments-ab-testing-and-canary-relea-2)

## Deployment Strategies
- Recreate
- RollingUpdate
- Blue/Green
- Canary

### Recreate Strategy
- `kubectl apply -f recreate.yaml`


### Rolling Update Strategy
- `kubectl apply -f rolling-update-strategy.yaml`


### Blue Green Deployment 
- `kubectl apply -f blue-v1.yaml`
- `kubectl apply -f green-v2.yaml`
- `kubectl apply -f switch-blue-to-green.yaml`
- `kubectl delete service/springboot-helloworld-svc-green deployment.apps/springboot-helloworld-v1`

















## Canary Deployments
### Type 1 
Using Tags in Kubernetes
- kube-v1.yml
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: springboot-helloworld-v1
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 0
      maxSurge: 1
  template:
    metadata:
      labels:
        app: springboot-helloworld
        version: "v1"
    spec:
      containers:
        - name: springboot-helloworld
          image: 'ngtrainings/springboot-helloworld-master:v1'
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet:
              path: /
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: springboot-helloworld
  labels:
    name: springboot-helloworld
    version: "v1"
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
  selector:
    app: springboot-helloworld
    version: "v1"
  type: LoadBalancer
```

- deployment-v2.yml
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: springboot-helloworld-v2
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 0
      maxSurge: 1
  template:
    metadata:
      labels:
        app: springboot-helloworld
        version: "v2"
    spec:
      containers:
        - name: springboot-helloworld
          image: 'ngtrainings/springboot-helloworld-master:v2'
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet:
              path: /
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
```
- Update Service to remove "version" tag.
service-v1.yml
```
apiVersion: v1
kind: Service
metadata:
  name: springboot-helloworld
  labels:
    name: springboot-helloworld
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
  selector:
    app: springboot-helloworld
  type: LoadBalancer
```
- add "v2" for version in the Service object
service-v2.yml
```
apiVersion: v1
kind: Service
metadata:
  name: springboot-helloworld
  labels:
    name: springboot-helloworld
    version: "v2"
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
  selector:
    app: springboot-helloworld
    version: "v2"
  type: LoadBalancer
```
#### Commands
- `kubectl apply -f kube-v1.yml`
- `kubectl apply -f deployment-v2.yml`
- `kubectl apply -f service-v1.yml`
- `kubectl apply -f service-v2.yml`

### Type 2
- Create V3 version along with Service object
kube-v3.yml
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: springboot-helloworld-v3
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 0
      maxSurge: 1
  template:
    metadata:
      labels:
        app: springboot-helloworld
        version: "v1"
    spec:
      containers:
        - name: springboot-helloworld
          image: 'ngtrainings/springboot-helloworld-master:v3'
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet:
              path: /
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: springboot-helloworld-v3
  labels:
    name: springboot-helloworld
    version: "v3"
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
  selector:
    app: springboot-helloworld
    version: "v3"
  type: LoadBalancer
```
- Ingress config
ingress.yml
```
kind: Ingress
apiVersion: extensions/v1beta1
metadata:
  name: sb-ingress
spec:
  rules:
  - http:
      paths:
      - path: /
        backend:
          serviceName: springboot-helloworld
          servicePort: 8080
      - path: /
        backend:
          serviceName: springboot-helloworld-v3
          servicePort: 8080
```
- Remove and make default backend rule in ingress
ingress-default.yml
```
kind: Ingress
apiVersion: extensions/v1beta1
metadata:
  name: sb-ingress
spec:
  backend:
    serviceName: springboot-helloworld-v3
    servicePort: 8080
```
#### Commands
- `kubectl apply -f kube-v3.yml`
- `kubectl apply -f ingress.yml`
- `kubectl apply -f ingress-default.yml`
