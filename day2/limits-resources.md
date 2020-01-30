# Working with limits and resources

```
$> kubectl create deployment hog --image vish/stress
deployment.apps/hog created

$> kubectl get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
hog     1/1     1            1           22s

$> kubectl describe deployment hog
$>  kubectl get deployment hog -o yaml

kubectl get deployment hog \
          --export -o yaml > hog.yaml

<--
edit hog.yaml to add

          limits:
            memory: "4Gi"
          requests:
            memory: "2500Mi"
-->

$> kubectl replace -f hog.yaml
deployment.apps/hog replaced

kubectl get deployment hog -o yaml
kubectl get po
NAME                   READY     STATUS
hog-64cbfcc7cf-lwq66   1/1       Running
RESTARTS 0


kubectl logs hog-64cbfcc7cf-lwq66


<--
Change to 

          limits:
            cpu: "1"
            memory: "4Gi"
          requests:
            cpu: "0.5"
            memory: "500Mi"
        args:
        - -cpus
        - "2"
        - -mem-total
        - "950Mi"
        - -mem-alloc-size
        - "100Mi"
        - -mem-alloc-sleep
        - "1s"
-->


kubectl delete deployment hog
kubectl create -f hog.yaml
