# Tips on using Kubectl

Kubectl is either installed by minikube/kind or obtained by the cloud provider or manually downloaded from [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

On Windows:

```
cd AppData\Local\Microsoft\WindowsApps
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/windows/amd64/kubectl.exe

cd ~
mkdir .kube
```

```
kubectl explain - -recursive
Kubectl —-dry-run -o -yam
kubectl run — restart=Never #Creates a Pod
kubectl run — restart=OnFailure #Creates a job
kubectl run — restart=OnFailure — schedule=”* * * * 
```
