# vcluster demo


## Prerequisites

For testing purposes you can use Minikube
```bash
minikube start --cpus='2' --memory='4g'
```

or Kind
```bash
 kind create cluster -n vcluster
```

Check for administrator access to a Kubernetes cluster.
```bash
kubectl auth can-i create clusterrole -A
```

Check if Helm version v3.10 is installed.
```bash
helm version
```

Check if kubectl is installed
```bash
kubectl
```

Verify that your cluster satisfies the prerequisites.
```bash
flux check --pre
```
