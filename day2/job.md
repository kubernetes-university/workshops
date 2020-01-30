# Jobs

```
$> cat <<EOF > job.yaml 
apiVersion: batch/v1
kind: Job
metadata:
  name: sleepy
spec:
  template:
    spec:
      containers:
      - name: resting
        image: busybox
        command: ["/bin/sleep"] 
        args: [   ]
      restartPolicy: Never
EOF

$> kubectl apply -f job.yaml 

$> kubectl describe jobs.batch sleepy
Name:           sleepy
Namespace:      default
Selector:       controller-uid=2579d3a0-1605-4951-a1c8-3668ceb12214
Labels:         controller-uid=2579d3a0-1605-4951-a1c8-3668ceb12214
                job-name=sleepy
Annotations:    kubectl.kubernetes.io/last-applied-configuration:
                  {"apiVersion":"batch/v1","kind":"Job","metadata":{"annotations":{},"name":"sleepy","namespace":"default"},"spec":{"template":{"spec":{"con...
Parallelism:    1
Completions:    1
Start Time:     Thu, 30 Jan 2020 15:17:34 +0100
Pods Statuses:  1 Running / 0 Succeeded / 2 Failed
Pod Template:
  Labels:  controller-uid=2579d3a0-1605-4951-a1c8-3668ceb12214
           job-name=sleepy
  Containers:
   resting:
    Image:      busybox
    Port:       <none>
    Host Port:  <none>
    Command:
      /bin/sleep
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From            Message
  ----    ------            ----  ----            -------
  Normal  SuccessfulCreate  30s   job-controller  Created pod: sleepy-bg6jz
  Normal  SuccessfulCreate  26s   job-controller  Created pod: sleepy-rb6zl
  Normal  SuccessfulCreate  16s   job-controller  Created pod: sleepy-w72hh


# add 
  spec:
    completions: 5

# add
  spec:
    parallelism: 2
# add
  spec:
    activeDeadlineSeconds: 15
    ...
    args: ["5"]

$> kubectl apply -f cronjob.yaml

$> kubectl get cronjobs.batch

