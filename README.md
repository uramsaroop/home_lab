this# 🏠 Home Lab Monitoring Stack (k3s + OpenTofu)

This project sets up a fully self-hosted observability stack using:

- **k3s** (lightweight Kubernetes)
- **OpenTofu** (Terraform-compatible IaC)
- **Prometheus** (metrics)
- **Grafana** (visualization)
- **Loki** (logs)
- **Alloy** (telemetry agent)
- **Argus** (alerting)

---

## 📦 Components

| Tool       | Function                        |
|------------|----------------------------------|
| `k3s`      | Lightweight Kubernetes distro     |
| `OpenTofu` | Infra as Code (Terraform fork)    |
| `Helm`     | Package manager for Kubernetes    |
| `Prometheus` | Metrics collection              |
| `Grafana`  | Dashboards + visualization        |
| `Loki`     | Log aggregation                   |
| `Alloy`    | Telemetry agent for metrics/logs  |
| `Argus`    | Alert routing from Prometheus     |

---

## 🚀 Getting Started

### 1️⃣ Install k3s

```bash
curl -sfL https://get.k3s.io | sh -
kubectl get nodes
```

### 2️⃣ Clone and Configure

```bash
git clone https://github.com/your-username/k3s-monitoring.git
cd k3s-monitoring
```

Ensure `~/.kube/config` points to your k3s cluster:
```bash
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
```

### 3️⃣ Initialize and Apply OpenTofu

```bash
tofu init
tofu apply
```

---

## 📂 Project Structure

```
k3s-monitoring/
├── main.tf
├── providers.tf
├── variables.tf
├── values/
│   ├── grafana.yaml
│   ├── prometheus.yaml
│   ├── loki.yaml
│   └── alloy.yaml
```

---

## 🌐 Access Grafana

1. Find the NodePort for Grafana:

```bash
kubectl get svc -n monitoring
```

2. Access in browser:

```
http://<k3s-node-ip>:<node-port>
```

> Default credentials: `admin` / `changeme`

---

## ⚙️ Alloy Sample Config (Helm Value)

```yaml
alloy:
  config:
    receivers:
      hostmetrics:
        type: hostmetrics
    exporters:
      prometheus:
        endpoint: 0.0.0.0:12345
    service:
      pipelines:
        metrics:
          receivers: [hostmetrics]
          exporters: [prometheus]
```

---

## 🧙‍♂️ Wizard’s Orb of Observability

> - **Prometheus** scrying metrics from the nodes  
> - **Alloy** whispering logs into **Loki’s** chamber  
> - **Grafana** painting the visions  
> - **Argus** sounding the horns when dragons stir  

---

## ✅ TODO

- [ ] Add SSL via ingress + cert-manager
- [ ] Add storage for persistent metrics/logs
- [ ] Add notification channels to Argus (email, Slack, etc.)
- [ ] Add dashboards as code

---
