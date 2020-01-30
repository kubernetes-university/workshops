# API access

```
$> kubectl config view

# https://github.com/ahmetb/kubectx
$> kubectx
$> kubens

$> kubectl get secrets
NAME                  TYPE                                  DATA   AGE
default-token-jgt4z   kubernetes.io/service-account-token   3      36m

$> export token=$(kubectl describe secret default-token-jgt4z |grep ^token |cut -f7 -d ' ')

$> echo $token
eyJhbGciOiJSUzI1NiIsImtpZCI6Im1DN1hwUXF1MUk4alFkcHpPRGxKNktRTy1VVjV0X1Zja1lOX3A0UWNxX2MifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tamd0NHoiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGVmYXVsdCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6IjljYjMzMTZmLThhOTAtNGU4Zi04YTczLWUyZTM3OWIzMTJmNSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRlZmF1bHQifQ.KEeeK5jAHBRZ8Y9Oourcuuufv0JGiukd02hB3UhQY1eGYP9PyPoAjuBZxClCcwLGgWiJHkIXZbj4iwKLJr1iNYbCb-4JQyv8lVMS4WEiaZuMZI-wKQfLpvGJZ9D41prZc1SEQZX1sMLWXt0kRt0s7ghLIzcGQrsO24p1h2CGU94V1aeFC1J2pKbRkwPJUsKH6Qq0Y4Kl3WuWijTofhnD7AvCdw9G13bkSkbBkwBlCe70XXWif5VcMey5HqevYKZUctPLn15Iyy_A9HPGYdc0E1eD9q_U2mUpuhZ-Ox-wM38bFSaq-BymgXo1EH-VQxQ2Ox0Wi2KlkIy23FJsDXPJdw

$> curl -k https://`minikube ip`:8443/apis --header "Authorization: Bearer $token"

$> curl -k https://`minikube ip`:8443/api/v1/namespaces --header "Authorization: Bearer $token"

$> kubectl run -i -t busybox --image=busybox   --restart=Never

token=`cat /var/run/secrets/kubernetes.io/serviceaccount/token`

#alternative
kubectl proxy &
curl http://127.0.0.1:8001/api/v1/namespaces
```
