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
- `Using Openshift`
```
login into Openshift
https://github.com/ngtrainings/HelloWorld.git
springboot-helloworld-master
```

### Blue Green Deployment 
- `kubectl apply -f blue-v1.yaml`
- `kubectl apply -f green-v2.yaml`
- `kubectl apply -f switch-blue-to-green.yaml`
- `kubectl delete service/springboot-helloworld-svc-green deployment.apps/springboot-helloworld-v1`
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#7

kubectl apply -f blue-v1.yaml
kubectl apply -f green-v2.yaml

status=true 
while $status
do
echo 'work in progress -> pods not ready yet'
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 5 ]]; then echo false; else echo true; fi`
sleep 5
done
kubectl get pods
kubectl get services
echo 'blue service url shows V1 -> '
url_blue=`minikube service springboot-helloworld-svc --url`
curl $url_blue
url_green=`minikube service springboot-helloworld-svc-green --url`
echo 'green service url shows V2 -> '
curl $url_green

kubectl get all

kubectl apply -f switch-blue-to-green.yaml

url_green=`minikube service springboot-helloworld-svc-green --url`
echo 'green service url shows V2 -> '
curl $url_green

echo 'blue service url post blue to green swtich shows V2 -> '
url_blue=`minikube service springboot-helloworld-svc --url`
curl $url_blue

kubectl get all

kubectl delete service/springboot-helloworld-svc-green deployment.apps/springboot-helloworld-v1


echo 'blue service url post green instance delete. shows V2 -> '
url_blue=`minikube service springboot-helloworld-svc --url`
curl $url_blue

kubectl get all

```


## Canary Deployments
### Type 1 
Using Tags in Kubernetes
- `kubectl apply -f deployment-v1.yaml`
- `kubectl apply -f deployment-v2.yaml`
- Update Service to remove "version" tag.
- `kubectl apply -f service-v1.yml`
- add "v2" for version in the Service object
- `kubectl apply -f service-v2.yml`
```
kubectl apply -f deployment-v1.yaml
kubectl apply -f deployment-v2.yaml

echo 'service url post v1 version applied. shows only V1 -> '
url=`minikube service springboot-helloworld --url`
curl $url

--Update Service to remove "version" tag.
kubectl apply -f service-v1.yaml

echo 'service url post blue to green swtich shows V1 or V2 -> '
url=`minikube service springboot-helloworld --url`
curl $url

--add "v2" for version in the Service object
kubectl apply -f service-v2.yaml

echo 'service url post v2 version applied. shows only V2 -> '
url=`minikube service springboot-helloworld --url`
curl $url
```

### Type 2 using Ingress
- git clone https://github.com/ngtrainings/teamchallenges.git
- cd teamchallenges/Task#7
- Create V5 PROD version with only /home url
- `kubectl apply -f deployment-v5.yaml`
 
- Create V6 NEW version with /ingress and /home url
- `kubectl apply -f deployment-v6.yaml`

- Enable Ingress config to redirect ingress to V6 service and home request to V5 env
- `kubectl apply -f update_service-v5.yaml`
- `kubectl apply -f update_service-v6.yaml`
- `kubectl apply -f ingress.yml`
 
- Remove and make default backend rule in ingress
- `kubectl apply -f ingress-default.yml`
