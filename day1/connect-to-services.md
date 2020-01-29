# Connect to service with Minikube


```
kg svc nginx
NAME    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
nginx   ClusterIP   10.96.47.252   <none>        80/TCP    2m12s

# edit to NodePort

$> minikube ip

$> kubectl get svc nginx
NAME    TYPE       CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
nginx   NodePort   10.96.215.5   <none>        80:30506/TCP   99s  # note the Node Port

$> curl <minikube-ip>:nodeport
```


