
* Register for [300$ free credit](https://cloud.google.com/gcp)
* Use the cloud shell in the portal

```
gcloud config set project kubernetes-univer

gcloud beta container clusters create "dpa-training" --zone "europe-west1-c" --no-enable-basic-auth --release-channel "rapid" --machine-type "n2-standard-2" --num-nodes "2" --enable-stackdriver-kubernetes --enable-ip-alias --enable-network-policy --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair
```

Right away you can start using the cluster

```
alessandro@cloudshell:~ (kubernetes-univer)$ kubectl get nodes
NAME                                          STATUS   ROLES    AGE     VERSION
gke-dpa-training-default-pool-b88e49ee-9zb0   Ready    <none>   3m10s   v1.16.4-gke.22
gke-dpa-training-default-pool-b88e49ee-flwn   Ready    <none>   3m10s   v1.16.4-gke.22
```