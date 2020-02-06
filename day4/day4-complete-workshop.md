# Kubernetes Hands-on workshop


## Install Kubernetes

[AKS](./install/aks-primer.md)  
[GKE](./install//gke-primer.md)  
[KIND](./install//kind-primer.md)  
[Minikube](./install/minikube-primer.md)  

**We will use AKS for this workshop.**

If you don't have the CLI (`kubectl`) install it with this [guide](./install/kubectl-install-and-tips.md).

If you use Linux or macOS, we strongly suggest to install [kubectx/kubens](./install/kubectx-kubens.md). Otherwise, keep in mind that you can switch namespace like this:

```
kubectl config set-context --current --namespace=my-namespace
```

# Import the provided kubeconfig

```
cp kubeconfig-xx ~/.kube/config
```

Test cluster connectivity

```
kubectl get nodes
NAME                           STATUS   ROLES   AGE   VERSION
aks-base-11322803-vmss000000   Ready    agent   8h    v1.17.0
aks-base-11322803-vmss000001   Ready    agent   8h    v1.17.0
```

# Run some containers

```
kubectl run helloworld --image=learncloudnative/helloworld:0.1.0 --port=3000
```

Check what is going on:

```

kubectl get pod

kubectl get replicaset

kubectl get deployments

kubectl describe deployment helloworld
```

## Expose services

```
kubectl expose deployment helloworld --port=8080 --target-port=3000 --type=LoadBalancer
```

```
kubectl get services

kubectl get endpoints

kubectl describe service helloworld
```

If you don't have a cluster in the cloud with access to a LoadBalancer, you can forward a port on your machine to the remote cluster:

```
kubectl port-forward --address localhost service/helloworld 8080:8080
```

## Scale deployments

```
kubectl scale deployment helloworld --replicas=5

kubectl get pods
```

## Access the dashboard

(For AKS you need to apply this patch):

```
kubectl apply -f https://aka.ms/dashboard-viewonly
```


```
kubectl -n kube-system port-forward --address 127.0.0.1 `kubectl get po -n kube-system -l k8s-app=kubernetes-dashboard -o name` 8001:9090

open http://127.0.0.1:8001/
```

## ConfgigMaps

Check this [file](../day3/configmap.md)

## PersistentVolumes

Create a [PVC](../day/pvc.yaml) and a Pod referencing such [PVC](../day3/pod-pvc.yaml) 

## Secrets

Create a few files

```
echo "Hello World" >> hello.txt
echo "secretpassword" >> passwd
echo "some=config" >> config.env
```
Create a secret from such files

```
kubectl create secret generic hello-kube-secret --from-file=./hello.txt --from-file=./passwd --from-file=config.env

kubectl describe secret hello-kube-secret

```
Create a pod that mounts


## Ingress