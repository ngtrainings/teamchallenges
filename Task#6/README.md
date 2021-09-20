- run a "Drupal, postgres and phadmin" application on Kubernetes and scale up
```
# clink on 
# wait for k8s to luanch and execute below commands

git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#6
kubectl apply -f postgress.yaml
kubectl apply -f drupal.yaml
kubectl apply -f pgadmin.yaml

# Wait for pods to come up
status=true 
while $status
do
echo 'work in progress -> pods not ready yet'
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 2 ]]; then echo false; else echo true; fi`
sleep 5
done

# list down the pod and services details
kubectl get pods
kubectl get svc

```

- run a "Wordpress, phpadmin and mariadb" application on Kubernetes and scale up
```
# clink on 
# wait for k8s to luanch and execute below commands

git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#6
kubectl apply -f mariadb.yaml
sleep 30
kubectl apply -f wordpress.yaml
kubectl apply -f phpadmin.yaml

# Wait for pods to come up
status=true 
while $status
do
echo 'work in progress -> pods not ready yet'
count=`kubectl get pods | grep -i running | wc -l`
status=`if [[ $count -gt 2 ]]; then echo false; else echo true; fi`
sleep 5
done

# list down the pod and services details
kubectl get pods
kubectl get svc

```
