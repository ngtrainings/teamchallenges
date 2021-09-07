- run a "Word Press" application on Kubernetes and scale up
```
# clink on https://learning.oreilly.com/scenarios/deploy-containers-to/9781492061984/ url 
# wait for k8s to luanch and execute below commands

git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#6
kubectl apply -f kube
status=true 
while $status
do
echo 'work in progress -> pods not ready yet'
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 0 ]]; then echo false; else echo true; fi`
sleep 5
done
kubectl get pods
kubectl get services
url=`minikube service knote --url`
curl $url
```
