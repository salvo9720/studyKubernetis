# studykubernetis

creazione nodi da file yaml: 
1) kind create cluster --name mycluster --config kind-config.yaml

approta modifiche al cluster gia creato:
1) kubectl apply -f deployment.yaml



creazione dashboard: 
1) kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc6/aio/deploy/recommended.yaml
2) kubectl get all -n kubernetes-dashboard
3) kubectl proxy
4) vai su browser in http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
5) ogni volta che ricrei k8s bisogna far ripartire il proxy.

killare kube proxy e rilanciarlo:
1) ps -ef | grep "kubectl proxy" (identificato il pid 82923)
2) kill 82923 
3) kubectl proxy

