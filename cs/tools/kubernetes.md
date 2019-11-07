
# Kubernetes

## Start a cluster in version v1.11.10 using minikube

Create a cluster:

```
minikube delete
minikube start --cpus 2 --memory 4096 \
    --vm-driver=hyperv [--hyperv-virtual-switch="Primary Virtual Switch"] \
    --kubernetes-version=v1.11.10
```

Check if everything is up and running:

```
kubectl get pods -n kube-system
```

Show `minikube` dashbaord:

```
minikube dashboard
```

## Links

- [Kubernetes Failure Stories](https://srcco.de/posts/kubernetes-failure-stories.html)
- [Declarative Application Management](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/declarative-application-management.md)
