
# Eclipse Che

## Install Eclipse Che on Kubernetes using `minikube` (Windows/HyperV)

Prerequisites: `kubectl`, `helm`, and `minikube` installed.

```shell
cd <somewhere>
git clone https://github.com/eclipse/che
cd che/deploy/kubernetes/helm/che

# Start a cluster in version v1.11.10
minikube start --cpus 2 --memory 4096 \
    --vm-driver=hyperv \
    --extra-config=apiserver.authorization-mode=RBAC \
    --kubernetes-version=v1.11.10

# Set up role bindings
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default

# Create a service account for tiller
kubectl create serviceaccount tiller --namespace kube-system

# Apply RBACs for tiller
kubectl apply -f ./tiller-rbac.yaml

# Init components with helm
helm dep update
helm init --service-account tiller --wait

# Check external cluster IP
minikube ip # use for <minikube_ip_address>

# Install Eclipse Che in cluster
helm upgrade --install che --force --namespace che \
    --set global.ingressDomain=<minikube_ip_address>.nip.io \
    --set cheImage=eclipse/che-server:7.0.0-rc-3.0 \
    --set global.cheWorkspacesNamespace=che \
    .
```

Wait until `curl <minikube_ip_address>.nip.io` resolves.
Start a browser and hit `http://<minikube_ip_address>.nip.io`.
