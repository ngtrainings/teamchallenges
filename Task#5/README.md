- run a "Hello World" application on Kubernetes and scale up
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#5
kubectl apply -f kube
status=true 
while $status
do
echo 'work in progress -> pods not ready yet'
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 0 ]]; then echo false; else echo true; fi`
sleep 2
done
kubectl get pods
kubectl get services
url=`minikube service knote --url`
curl $url

#delete services, pods
kubectl delete all --all --all-namespaces

#scale up pods
kubectl scale --replicas=2 deployment/knote
kubectl get pods -l app=knote --watch
```
