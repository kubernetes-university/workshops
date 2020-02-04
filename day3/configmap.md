# Create ConfigMaps

```
$> mkdir primary
$> echo c > primary/cyan
$> echo m > primary/magenta
$> echo y > primary/yellow
$> echo k > primary/black
$> echo "known as key" >> primary/black
$> echo blue > favorite

$> kubectl create configmap colors \
    --from-literal=text=black  \
    --from-file=./favorite  \
    --from-file=./primary/

$> kubectl get configmap colors

$> kubectl get configmap colors -o yaml

$> cat <<EOF >simpleshell.yaml
apiVersion: v1
kind: Pod
metadata:
  name: shell-demo
spec:
  containers:
  - name: nginx
    image: nginx
    env:
    - name: ilike
      valueFrom:
        configMapKeyRef:
          name: colors
          key: favorite
EOF

kubectl exec shell-demo -- /bin/bash -c 'echo $ilike'

```