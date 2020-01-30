# Tips on using Kubectl

Kubectl is either installed by minikube/kind or obtained by the cloud provider or manually downloaded from [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

```
kubectl explain - -recursive
Kubectl —-dry-run -o -yam
kubectl run — restart=Never #Creates a Pod
kubectl run — restart=OnFailure #Creates a job
kubectl run — restart=OnFailure — schedule=”* * * * 
```