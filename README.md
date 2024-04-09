# Bitnami Keycloak

- keycloak-values.yaml
```yaml
production: true
auth:
  createAdminUser: true
  adminUser: admin
  adminPassword: admin12345
tls:
  enabled: true
  autoGenerated: true
ingress:
  enabled: false
 
postgresql:
  enabled: false
externalDatabase:
  host: "mssql.example.com"
  port: 1433
  user: keycloak
  database: keycloak
  existingSecret: passwords 
```

- Helm Repo
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo bitnami/keycloak
helm search repo bitnami/keycloak --versions
helm show values bitnami/keycloak --version v21.0.0
helm show values bitnami/keycloak --version v21.0.0 > keycloak-values.yaml
helm upgrade --install keycloak bitnami/keycloak --version v21.0.0 --namespace keycloak --create-namespace --values keycloak-values.yaml --wait
```

- postgres connection string
- postgres client
```bash
kubectl run postgres --image=postgres:latest --env="POSTGRES_PASSWORD=examplepass" --port=5432 
kubectl run pgadmin --namespace=default --image=dpage/pgadmin4:latest --port=80 --env="PGADMIN_DEFAULT_EMAIL=admin@pgadmin.org" --env="PGADMIN_DEFAULT_PASSWORD=admin"
```
```bash
psql -h localhost -p 5432 -U user1 -d mydb
psql -h 10.92.192.3 -p 5432 -U postgres

# list databases
\l
\list

# Create database
CREATE DATABASE keycloak;

# Switch to database
\c keycloak

# Show tables
\dt
```

- Ingress
```yaml
apiVersion: traefik.containo.us/v1alpha1
kind: IngressRoute
metadata:
  name: keycloak-ingressroute
  namespace: keycloak
  annotations:
    kubernetes.io/ingress.class: "traefik-external"
spec:
  entryPoints:
    - websecure
  routes:
    - match: Host(`keycloak.saqlainmushtaq.com`) && PathPrefix(`/`)
      kind: Rule
      services:
        - name: keycloak
          namespace: keycloak
          port: 443
```