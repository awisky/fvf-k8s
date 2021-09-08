# fvf-k8s

Cloudformation for the FVF project

create the cluster
`eksctl create cluster -f cloudformation/cluster.yaml`

in Amazon IAM management console:

- create the identity provider amazon IAM

- create the policy

- create/update the role with web identity


install the cluster autoscaller
`kubectl apply -f cloudformation/cluster-autoscaller.yaml`

check the pods
`kubectl -n kube-system get pods -w`

check the logs 
`kubectl logs -f cluster-autoscaler-75665f6b86-tntp9  -n kube-system`

create the traefik service
`kubectl apply -f traefik`

manual update the A routing record in route53 to link the load balancer created by traefik

optional dashboard

`bash
kubectl apply -f cloudformation/dashboard.yaml
kubectl get namespaces
kubectl proxy
kubectl create serviceaccount dashboard-admin-sa
kubectl create clusterrolebinding dashboard-admin-sa \n--clusterrole=cluster-admin --serviceaccount=default:dashboard-admin-sa
kubectl get secrets
kubectl describe secret dashboard-admin-sa-token-9rnt2
`

Dashboard:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login

paste the token

## License
[LGPL version 3 ](http://www.gnu.org/licenses/lgpl-3.0.en.html)
