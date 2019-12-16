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

On Windows, [chocolatey](https://chocolatey.org/packages/kind) is the best option (remember to install HyperV Windows feature):

```
choco install minikube
```

(note that Minikube will install also the Kubernetes CLI).

## KIND (Kubernetes in Docker)

Full documentation [here](https://kind.sigs.k8s.io/). __KIND requires Docker Desktop to work__!

```
choco install docker-desktop
choco install kind
```


## Kubernetes CLI

For all installation methods, you'll be needing the Kubernetes CLI. Install it:

Mac
```
brew install kubernetes-cli
```

Windows
```
choco install kubernetes-cli
```

## Cloud Providers

Azure, AWS, Google and IBM all offer managed Kubernetes services. They're the easiest way by far to *consume* Kubernetes without the hassle of installing it yourself.

## No-installation methods

An easy way to get access to *some* kubernetes cluster is to use [Play-with-Kubernetes](https://labs.play-with-k8s.com/), [Katacoda](https://www.katacoda.com/) or [Instruqt](https://instruqt.com/)


