# Traefik V2.0 Google Kubernetes Example

### requires

- gcloud
- gke

### edit google account

[environment/02_cluster-role.yml](environment/02_cluster-role.yml)

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

### Demo

#### whoami

```bash
$ curl [-k] https://whoami.example.com/tls
$ curl [-k] http://whoami.example.com/notls
```

#### dashboard

https://admin.example.com

###### id/pass

- test/test
- test2/test2
