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

Fork this repository and clone it.

bootstrap Flux
```bash
git clone https://github.com/<YOUR-USERNAME>/gitops-vcluster
cd gitops-vcluster
```

Bootstrap Flux to use your fork. The following command requires ssh-agent
```bash
flux bootstrap git \
  --author-email=<YOUR-EMAIL> \
  --url=ssh://git@github.com/<YOUR-USERNAME>/gitops-vcluster \
  --branch=main \
  --path=clusters/my-cluster
```

You should see the following output.

```
► cloning branch "dev" from Git repository "ssh://git@github.com/<YOUR-USERNAME/gitops-vcluster"
✔ cloned repository
► generating component manifests
✔ generated component manifests
✔ committed component manifests to "main"
► pushing component manifests to "ssh://git@github.com/<YOUR-USERNAME/gitops-vcluster"
► installing components in "flux-system" namespace
✔ installed components
✔ reconciled components
► determining if source secret "flux-system/flux-system" exists
► generating source secret
✔ public key: ecdsa-sha2-nistp384 AAAA...
Please give the key access to your repository: [y/N]:
```

To grant the Flux Git controller access to your forked repo
1. Copy the `public key` and open your fork on Github.
1. Click on `Settings` in the top menu
1. Click on `Deploy keys` in the left menu
1. Click the `Add deploy key`
1. Add a title, paste the key in the Key field, click Allow write access and click Add key
1. Return to the terminal prompt and press 'Y'


You should see the process continue
```
► applying source secret "flux-system/flux-system"
✔ reconciled source secret
► generating sync manifests
✔ generated sync manifests
✔ committed sync manifests to "main"
► pushing sync manifests to "ssh://git@github.com/ceaser/gitops-vcluster"
► applying sync manifests
✔ reconciled sync configuration
◎ waiting for GitRepository "flux-system/flux-system" to be reconciled
✔ GitRepository reconciled successfully
◎ waiting for Kustomization "flux-system/flux-system" to be reconciled
✔ Kustomization reconciled successfully
► confirming components are healthy
✔ helm-controller: deployment ready
✔ kustomize-controller: deployment ready
✔ notification-controller: deployment ready
✔ source-controller: deployment ready
✔ all components are healthy
```
