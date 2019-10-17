# Traefik V2.0 Google Kubernetes Example

### requires

- gcloud
- gke

### edit google account

[permissions.yml](environment/02_cluster-role.yml)

```yml
subjects:
  - apiGroup: rbac.authorization.k8s.io
    kind: User
    name: <user@email.com>
```

### kubernetes apply

```bash
$ kubectl apply -f environment
$ kubectl apply -f services/traefik
```
