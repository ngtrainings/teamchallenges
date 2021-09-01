- run a "Hello World" application on Kubernetes so that I can understand kubernetes is up and running and some sample application is also up and running
```
git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#5
kubectl apply -f kube
status=true 
while $status
do
echo 'pods not ready yet -->'$status
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 0 ]]; then echo false; else echo true; fi`
done
kubectl get pods
kubectl get services
url=`minikube service knote --url`
curl $url

#delete services, pods
kubectl delete all --all --all-namespaces
```
