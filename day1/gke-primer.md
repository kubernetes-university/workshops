
* Register for [300$ free credit](https://cloud.google.com/gcp)
* Use the cloud shell in the portal

```
gcloud auth login
gcloud config set project kubernetes-univer


gcloud beta container clusters create "dpa-training" --zone "europe-west1-c" --no-enable-basic-auth --release-channel "rapid" --machine-type "n2-standard-2" --num-nodes "2" --enable-stackdriver-kubernetes --enable-ip-alias --enable-network-policy --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair
