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