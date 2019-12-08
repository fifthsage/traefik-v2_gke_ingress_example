# Traefik V2 Google Kubernetes Example

## requires

- gcloud
- gke

## edit google account

[environment/02_cluster-role.yml](environment/02_cluster-role.yml)

```yml
subjects:
  - apiGroup: rbac.authorization.k8s.io
    kind: User
    name: <user@email.com>
```

## set your domain for cert manager

[cert-manager/00_cluster-issuer.yml](cert-manager/00_cluster-issuer.yml)

```yml
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: email@yourdomain.com
```

## set your domain certification

[cert-manager/01_certification.yml](cert-manager/01_certification.yml)

```yml
apiVersion: cert-manager.io/v1alpha2
kind: Certificate
metadata:
  name: cert-yourdomain
  namespace: development
spec:
  secretName: cert-yourdomain
  issuerRef:
    name: letsencrypt-cluster-issuer
    kind: ClusterIssuer
  commonName: yourdomain.com
  dnsNames:
    - yourdomain.com
    - somthing.yourdomain.com
  acme:
    config:
      - http01:
          ingressClass: traefik
        domains:
          - yourdomain.com
          - somthing.yourdomain.com
```

## kubernetes apply

```bash
kubectl apply -f environment
kubectl apply -f cert-manager
kubectl apply -f services/traefik
```

## Demo

### whoami

```bash
curl [-k] https://whoami.example.com/tls
curl [-k] http://whoami.example.com/notls
```

### dashboard

<https://admin.example.com>

#### id/pass

- test/test
- test2/test2
