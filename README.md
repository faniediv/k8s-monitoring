# Kubernetes Monitoring Stack

This repo contains a prebuilt monitoring setup for Kubernetes using **Kustomize + Helm**.  
It includes:

- **Prometheus + Grafana** (via `kube-prometheus-stack`)
- **SNMP Exporter** (for switches, APs, and network devices)
- **Blackbox Exporter** (for HTTP/DNS/ICMP checks)
- **Speedtest Exporter** (for measuring internet performance)

---

## 🚀 Quick Start

### 1. Create Namespace
```bash
kubectl create ns monitoring

2. Deploy the Stack

kubectl apply -k https://github.com/faniediv/k8s-monitoring/monitoring/overlays/default

This will install Prometheus, Grafana, SNMP exporter, Blackbox exporter, and Speedtest exporter.
📊 Access Grafana

Grafana is deployed in the monitoring namespace.
Port-forward

kubectl port-forward svc/monitoring-grafana -n monitoring 3000:80

Now open http://localhost:3000

    Username: admin

    Password: admin (default, change after login!)

🛠 Customizing

    Add SNMP devices
    Edit the snmp-exporter.yaml with your devices’ IPs and SNMP communities.

    Add Blackbox checks
    Update the Blackbox exporter configuration to include new endpoints (HTTP/DNS/ICMP).

    Adjust Speedtest interval
    Default is every 30 minutes. Change in speedtest-exporter.yaml.

📦 Structure

monitoring/
  base/                # Base resources
    prometheus-stack/  # Helm chart for Prometheus + Grafana
    snmp-exporter/     # SNMP exporter
    blackbox-exporter/ # Blackbox exporter
    speedtest-exporter/# Speedtest exporter
  overlays/default/    # Default overlay for deployment

🔒 Security Notes

    Change Grafana’s default password after login.

    Use Kubernetes secrets for SNMP communities if deploying in production.

    Restrict access to Grafana and Prometheus with ingress + authentication if needed.

🧹 Uninstall

kubectl delete ns monitoring
