# comandi 
## creazione prot foward 
kubectl port-forward pod/appdb-56f9567c8f-57hd6 63306:3306, 

da cambiare il nome del pod, tramtie kubectl get po

# delete pod
kubectl delete pod appdb-56f9567c8f-57hd6: la struttura è sempre kubectl + verbo + soggetto(pod) + id

# log
kubectl logs pod appdb-56f9567c8f-57hd6

# apply 
kubectl apply -f appDeploymentWithInit.yaml: -f indica il file da eseguire


# isntallazione k9s per vedere i log 
segui questa guida è ok per ubuntu


# vedere i log del cluster
kubectl describe pod podId

# avvi minikube
1) minikube start:
se fatto senza questo comando il control-panel non sara avviato e no nsara possibile connettersi ai nodi

# eseguire un comando dentro il pod kubernetis 
1) kubectl exec -n test-namespace -it pod-configmap -- sh
dopo -n il nome del namespace 
dopo -it il nome del pod

## dentro il pod con il comando:
2) env: 
vediamo tutte le variabili al suo interno 


## secret e dati 
1) kubectl get secret db-secret -n test-namespace -o yaml
otteniamo i secret di dbsecret
- o yaml: output in formato yaml
vederemo i secret criptati in base 64, ma dentro il pod kubenetis gleieldescripta per questo conviene accedere ai secret del pod



# rete kubernetis
1) ogni pod ha il propio indirizzo ip, l'esterno non puo comunciare con la rete e solo visibile per k8s, i pod posso comunciare senza i nat, e si parlano come se fossero nella stessa macchina. 


## per vedere le regole aggiuntive di ip tables: 
collegati a minicube 
1) minikube ssh
lancia dentro un iptables 
2) sudo iptables -t nat -L KUBE-NODEPORTS -n -v


## attivazione ignresss minucube 
1) minikube addons enable ingress

# per aprire il tunnel e raggiugerlo da browser 
1) minikube tunnel

2) aggiungere i domini nel file hosts widnwos:
127.0.0.1 snake.test.it
127.0.0.1 nginx.test.it


# generazione certificati per https
1) mkdir certs
2) cd certs
3) openssl genrsa -out snake.test.local.key 2048
4) openssl req -x509 \
  -new \
  -nodes \
  -key snake.test.local.key \
  -sha256 \
  -days 365 \
  -out snake.test.local.crt \
  -subj "/CN=snake.test.local"


## creazione del secret con i certificati 
1) kubectl create secret tls hello-world-tls \
  --cert=snake.test.local.crt \
  --key=snake.test.local.key

2) kubectl get secret

3) aggiorna l'ingress con i certificati