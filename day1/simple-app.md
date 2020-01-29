# Deploy a simple application on Kubernetes

Prereqs:
- kubectl installed
- a kubeconfig pointing to a working cluster

```
$> kubectl create deployment nginx --image=nginx

deployment.apps/nginx created

$> kubectl get deployments

NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   1/1     1            1           8s

$> kubectl describe deployment nginx
Name:                   nginx
Namespace:              default
CreationTimestamp:      Wed, 29 Jan 2020 14:51:53 +0100
Labels:                 app=nginx
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx
Replicas:               1 desired | 1 updated | 1 total | 0 available | 1 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      False   MinimumReplicasUnavailable
  Progressing    True    ReplicaSetUpdated
OldReplicaSets:  <none>
NewReplicaSet:   nginx-86c57db685 (1/1 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  2m40s  deployment-controller  Scaled up replica set nginx-86c57db685 to 1

$> kubectl get events
LAST SEEN   TYPE     REASON              OBJECT                        MESSAGE
42m         Normal   RegisteredNode      node/minikube                 Node minikube event: Registered Node minikube in Controller
<unknown>   Normal   Scheduled           pod/nginx-86c57db685-jxfsl    Successfully assigned default/nginx-86c57db685-jxfsl to minikube
28s         Normal   Pulling             pod/nginx-86c57db685-jxfsl    Pulling image "nginx"
20s         Normal   Pulled              pod/nginx-86c57db685-jxfsl    Successfully pulled image "nginx"
20s         Normal   Created             pod/nginx-86c57db685-jxfsl    Created container nginx
20s         Normal   Started             pod/nginx-86c57db685-jxfsl    Started container nginx
29s         Normal   SuccessfulCreate    replicaset/nginx-86c57db685   Created pod: nginx-86c57db685-jxfsl
29s         Normal   ScalingReplicaSet   deployment/nginx              Scaled up replica set nginx-86c57db685 to 1

$> kubectl get deployment nginx -o yaml > first.yaml
$> cat first.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: "2020-01-29T13:51:53Z"
  generation: 1
  labels:
    app: nginx
  name: nginx
  namespace: default
  resourceVersion: "35329"
  selfLink: /apis/apps/v1/namespaces/default/deployments/nginx
  uid: 16e85382-eb55-4f94-a741-2299a6056873
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: nginx
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:

$> kubectl delete deployment nginx
deployment.apps "nginx" deleted

$> kubectl create -f first.yaml
deployment.apps "nginx" created

$>  kubectl create deployment two --image=nginx --dry-run -o yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: two
  name: two
spec:
  replicas: 1
  selector:
    matchLabels:
      app: two
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: two
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}

$> kubectl get deployments nginx --export -o yaml
$> kubectl get deployment nginx --export -o json

$> kubectl expose deployment/nginx  # Will this work?

$> kubectl get deploy,pod,svc
$> kubectl get ep nginx

#Scaling
$> kubectl scale deployment nginx --replicas=3



```