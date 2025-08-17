# k3s-onebox README.md

# k3s-onebox

This repository contains an Ansible playbook to provision a single-node k3s cluster on Ubuntu 24.04. It configures UFW, swap, sysctl settings, and installs cert-manager with a ClusterIssuer. Optionally, it can deploy Loki, Promtail, Grafana, and Bitnami MySQL via Helm.

## Setup Instructions

1. **Install Ansible Collections**:
   Run the following command to install the required Ansible collections:
   ```
   ansible-galaxy install -r requirements.yml
   ```

2. **Edit Inventory**:
   Modify the `inventory/hosts.ini` file to specify your VPS host:
   ```
   [vps]
   your-vps ansible_host=YOUR.VPS.IP ansible_user=root
   ```

3. **Configure Variables**:
   Update the `group_vars/all.yml` file to set your desired configurations, including:
   - Swap size
   - Open ports
   - ACME email
   - MySQL credentials
   - ACME server URLs (production and staging)

4. **Run the Playbook**:
   Execute the following command to run the playbook:
   ```
   ansible-playbook -i inventory/hosts.ini playbooks/site.yml
   ```

## What Gets Installed

- A single-node k3s cluster with Traefik and ServiceLB
- UFW configured to allow specified ports
- Swap file configured
- Sysctl settings applied
- Cert-manager with a ClusterIssuer for ACME
- Optional: Loki, Promtail, Grafana, and Bitnami MySQL

## Default Namespaces

- `kube-system`: For k3s and system components
- `cert-manager`: For cert-manager resources
- `observability`: For Loki and Grafana (if installed)
- `db`: For MySQL (if installed)

## Next Steps

- Deploy your applications to the k3s cluster.
- Configure TLS annotations for your services.
- Use the MySQL service for your database needs.# k3s-onebox
