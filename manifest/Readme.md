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