# Scaling an application with Kubernetes

```
#Scaling
$> kubectl scale deployment nginx --replicas=3
deployment.apps/nginx scaled

$> kubectl get deployment nginx
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   3/3     3            3           9m2s

$> kubectl get po -o wide
NAME                     READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
nginx-86c57db685-b7fjs   1/1     Running   0          25s     172.17.0.8   minikube   <none>           <none>
nginx-86c57db685-fgvwz   1/1     Running   0          25s     172.17.0.9   minikube   <none>           <none>
nginx-86c57db685-sg2z6   1/1     Running   0          9m20s   172.17.0.7   minikube   <none>           <none>
```

## Resilience

```
$> kubectl delete po nginx-86c57db685-b7fjs
pod "nginx-86c57db685-b7fjs" deleted

$> kubectl get po -o wide
NAME                     READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
nginx-86c57db685-fgvwz   1/1     Running   0          31m   172.17.0.9    minikube   <none>           <none>
nginx-86c57db685-sg2z6   1/1     Running   0          40m   172.17.0.7    minikube   <none>           <none>
nginx-86c57db685-t426p   1/1     Running   0          18s   172.17.0.10   minikube   <none>           <none>