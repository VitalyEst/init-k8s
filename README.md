### Install argo-cd

```shell
helm dependency build argo-cd/01_argo-cd-install/
helm upgrade --install -n argo-cd --create-namespace argo-cd argo-cd/01_argo-cd-install/
```

### Install services

Edit argo-cd/02_bootstrap-cluster/values.yaml (enabled service)

```shell
helm upgrade --install -n argo-cd --create-namespace bootstrap-cluster argo-cd/02_bootstrap-cluster/
```

### View admin password and forward port GUI

```
kubectl -n argo-cd get secret argocd-initial-admin-secret --template={{.data.password}} | base64 -d
kubectl -n argo-cd port-forward svc/argo-cd-argocd-server 8080:80
```

Open browser http://127.0.0.1:8080
