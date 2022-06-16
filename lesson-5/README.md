# Liveness, Readiness and Startup Probes

## Requirements
`minikube start --kubernetes-version 1.22.1`

## Check Types

### Exec Command

If the command succeeds, it returns 0, and the kubelet considers the container to be alive and healthy.

```
kubectl apply -f liveness-exec.yml
kubectl describe pod liveness-exec
kubectl delete -f liveness-exec.yml
```

### TCP Socket

The kubelet will attempt to open a socket to your container on the specified port. If it can establish a connection, the container is considered healthy.

```
kubectl apply -f configmap-nginx.yml
kubectl apply -f liveness-tcp.yml
kubectl describe pod liveness-tcp
kubectl delete -f liveness-tcp.yml
```

### Http Request

Any HTTP code greater than or equal to 200 and less than 400 indicates success.

```
kubectl apply -f configmap-nginx.yml
kubectl apply -f liveness-readiness-http.yml
kubectl describe pod liveness-http
kubectl delete -f liveness-readiness-http.yml
```

## Startup Probes

### TCP Socket

```
kubectl apply -f startup-tcp.yml
kubectl describe pod startup-tcp
kubectl delete -f startup-tcp.yml
```

## Readiness Probe - FAIL Example

### HTTP Request

```
kubectl apply -f readiness-fail.yml
kubectl describe pod readiness-fail
kubectl delete -f readiness-fail.yml
```




