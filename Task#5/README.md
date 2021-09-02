- run a "Hello World" application on Kubernetes and scale up
```
# clink on https://learning.oreilly.com/scenarios/deploy-containers-to/9781492061984/ url 
# wait for k8s to luanch and execute below commands

git clone https://github.com/ngtrainings/teamchallenges.git
cd teamchallenges/Task#5
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

#delete services, pods
kubectl delete all --all --all-namespaces

#scale up pods
kubectl scale --replicas=2 deployment/knote
kubectl get pods -l app=knote --watch
```


- Kubernetes Dashboard in katakoda
```
click on https://learning.oreilly.com/scenarios/deploy-containers-to/9781492061984/

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
kubectl -n kubernetes-dashboard get svc
kubectl -n kubernetes-dashboard edit svc kubernetes-dashboard ( ClusterIP to NodePort )

#serviceaccount.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: dashboard-admin
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-rolebinding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: dashboard-admin
  namespace: kube-system

kubectl apply -f serviceaccount.yaml
kubectl -n kube-system describe sa dashboard-admin
kubectl -n kube-system describe secrets dashboard-admin-token-hf7xm (  token name may change )
```
