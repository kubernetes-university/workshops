# Quotas for namespace

```
$> kubectl create namespace low-usage-limit
namespace/low-usage-limit created

cat <<EOF > low-resource-range.yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: low-resource-range
spec:
  limits:
  - default:
      cpu: 1
      memory: 500Mi
    defaultRequest:
      cpu: 0.5
      memory: 100Mi
    type: Container
EOF

kubectl --namespace=low-usage-limit  \
        create -f low-resource-range.yaml

$> kubectl get LimitRange
No resources found in default namespace.

$> kubectl get LimitRange -A
NAMESPACE         NAME                 CREATED AT
low-usage-limit   low-resource-range   2020-01-30T11:59:53Z

$> kubectl -n low-usage-limit \
>       create deployment limited-hog --image vish/stress
deployment.apps/limited-hog created

$>  kubectl get deployments --all-namespaces
NAMESPACE              NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
kube-system            coredns                     2/2     2            2           44d
kube-system            metrics-server              1/1     1            1           26h
kubernetes-dashboard   dashboard-metrics-scraper   1/1     1            1           26h
kubernetes-dashboard   kubernetes-dashboard        1/1     1            1           26h
low-usage-limit        limited-hog                 1/1     1            1           20s

$> kubectl -n low-usage-limit get pods
NAME                           READY   STATUS    RESTARTS   AGE
limited-hog-5c8d494fc5-dpbr9   1/1     Running   0          43s
```