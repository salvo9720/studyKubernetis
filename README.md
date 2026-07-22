# studykubernetis

fonte: guida isntallazione k8s su wsl2 : https://kubernetes.io/blog/2020/05/21/wsl-docker-kubernetes-on-the-windows-desktop/

creazione nodi da file yaml: 
1) kind create cluster --name mycluster --config kind-config.yaml

approta modifiche al cluster gia creato:
1) kubectl apply -f deployment.yaml



creazione dashboard: 
1) kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc6/aio/deploy/recommended.yaml
2) kubectl get all -n kubernetes-dashboard
3) kubectl proxy
3.1) kill del proxy pkill -f "kubectl proxy"
4) vai su browser in http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
4.1) oppure qui: http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default
5) ogni volta che ricrei k8s bisogna far ripartire il proxy.

killare kube proxy e rilanciarlo:
1) ps -ef | grep "kubectl proxy" (identificato il pid 82923)
2) kill 82923 
3) kubectl proxy



-------------------------

## Creazione utenti:

1) 
kubectl apply -f - <<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
EOF
# Create a ClusterRoleBinding for the ServiceAccount
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
EOF

## creazioen token 
2) kubectl -n kubernetes-dashboard create token admin-user

3) 

kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

4) prendi il token dalla console e usalo per autenticarti


-------------------------------------


dashboard minicube:
2) minikube dashboard


verifica cluster attivo: 
1) kubectl config get-contexts



## collegare minicube ad un indirizzo raggiungibile da browser 
1) minikube service nginx-nodeport --url
lasciare il terminale aperto per raggiungerlo, nginx-nodeport è il nome del servizio



## instalalzione servizio per fare loadbalancer in minikube
1) kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.16.1/config/manifests/metallb-native.yaml

2) docker network inspect minikube:
per conoscere gli indirizzi ip usabili, prendi la parte di:
"Subnet": "192.168.49.0/24",
"Gateway": "192.168.49.1"
