# Jobs, CronJobs and InitContainers

## Requirements
```
sudo apt-install terminator -y
minikube start --kubernetes-version 1.22.1
```

## Jobs

Open a terminal and run:
`kubectl watch pod --show-labels`

### Normal Job
```
kubectl apply -f 01-job.yml
kubectl get job
kubectl describe job sleepy

kubectl delete job sleepy
```

### Completions

Run multiple pods until "completions"

Uncomment line 6: `completions`
```
watch kubectl get pod,job --show-labels

kubectl apply -f 01-job.yml
kubectl describe job sleepy

kubectl delete -f 01-job.yml
```

### Paralellism

Run pods in parallel

Uncomment line 6 & 7: `parallelism`
```
watch kubectl get pod,job --show-labels

kubectl apply -f 01-job.yml

kubectl describe job sleepy
kubectl delete job sleepy
```

### Active Deadline Seconds

Stop Job when AGE == activeDeadlineSeconds

Uncomment line 8: `activeDeadlineSeconds`
```
watch kubectl get pod,job --show-labels

kubectl apply -f 01-job.yml
kubectl describe job sleepy

kubectl delete job sleepy
```
It should fail before the Job completion.

## CronJob

Run Job each 2 minutes

```
watch kubectl get pod,job,cronjob --show-labels

kubectl apply -f 02-cronjob.yml
kubectl describe cronjob sleepy

kubectl delete -f 02-cronjob.yml
```

## Init Container

Pod is not Ready until 2 initContainers have finished.

```
kubectl apply -f 03-initContainer.yml
kubectl describe pod myapp-pod

kubectl apply -f 04-services.yml

kubectl logs -f myapp-pod app
kubectl logs -f myapp-pod init-myservice
kubectl logs -f myapp-pod init-mydb

kubectl delete -f .
```