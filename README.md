# 🏗️ Self-Hosted Infrastructure Stack

A complete, self-managed infrastructure stack for internal use — replacing cloud-managed services with reliable, open-source, self-hosted alternatives.

This setup includes:

- **MongoDB** – NoSQL document database
- **Oracle DB** – Enterprise relational database
- **PostgreSQL** – Open-source SQL database
- **ToolJet** – Low-code internal tool builder
- **Uptime Kuma** – Website and service monitoring
- **Metabase** – Visual analytics and dashboards
- **Passbolt** – Secure, self-hosted password manager

---

### UPTIME-KUMA
```bash
docker login
docker build -t your-dockerhub-username/uptime-kuma:1.23.16 -f uptime-kuma/Dockerfile .
docker push your-dockerhub-username/uptime-kuma:1.23.16

helm upgrade --install  -f uptimess-kuma/val.yaml --set image.tag="1.23.16" \
    --set image.repository="your-dockerhub-username/uptime-kuma" --atomic --cleanup-on-fail  \
    --timeout 900s -n $NAMESPACE uptime-kuma uptime-kuma/k8s/

```

### TOOLJET

```bash
kubectl apply -f tooljet/deployment.yaml -n $NAMESPACE 

```

### METABASE

```bash
helm repo add pmint93 https://pmint93.github.io/helm-charts
helm repo update
helm upgrade --install -f metabase/val.yaml --name metabase \
pmint93/metabase -n $NAMESPACE 

```