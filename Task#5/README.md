- run a "Hello World" application on Kubernetes so that I can understand kubernetes is up and running and some sample application is also up and running
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#5
kubectl apply -f kube
url=`minikube service knote --url`
curl $url
```
