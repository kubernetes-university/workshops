# Minikube primer

## Obtain minikube ([instructions](https://kubernetes.io/docs/tasks/tools/install-minikube/))

Linux:

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
```

OSX (use brew):

```bash
brew install minikube
```
or download direcly:

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \
  && chmod +x minikube
```

Windows:

_You need Hyper-V enabled and run from elevated command prompt_

In Powershell:
```powershell
 'Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All'
 ```

Use Chocolatey or download the [installer](https://github.com/kubernetes/minikube/releases/latest/download/minikube-installer.exe)

```powershell
choco install minikube
```

# Deploy

Make sure you enable some basic addons:

```bash
minikube addons enable dashboard
minikube addons enable metrics-server
```

```bash
minikube start --memory='2000mb' --cpus=2
```
It should select the right driver automatically.