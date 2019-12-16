# Setup

You'll need a workstation to go thru the course; depending on _how_ you want to learn (using a cloud service, on-premise clusters, or a test cluster deployed on your machine) the setup can vary. Here are only some examples but there are many more ways to deploy and run Kubernetes, so feel free to experiment and try new things.

## Deployment on your machine

## Minikube

Full installation [here](https://kubernetes.io/docs/tasks/tools/install-minikube/).

On Mac OS X (needs [brew](https://brew.sh/)):

```bash
brew install minikube
minikube start #will ask for administrator password
```

On Windows, [chocolatey](https://chocolatey.org/packages/kind) is the best option:

```
choco install minikube


## KIND (Kubernetes in Docker)

Full documentation [here](https://kind.sigs.k8s.io/).

