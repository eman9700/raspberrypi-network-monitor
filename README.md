# raspberrypi-network-monitor

Raspberry Pi Network Monitor Project

Prometheus + Grafana + Node Exporter

1. Update Pi

sudo apt update && sudo apt upgrade -y

2. Install Prometheus

sudo apt install prometheus -y

Check service:

systemctl status prometheus

Prometheus runs on port 9090

3. Install Node Exporter

Let Prometheus scrape system stats (CPU/RAM/network stats)

cd /opt
sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-armv7.tar.gz
sudo tar xvf node_exporter-1.6.1.linux-armv7.tar.gz
sudo mv node_exporter-1.6.1-linux-armv7 node_exporter

Add it as a service:

sudo nano /etc/systemd/system/node_exporter.service

Paste:

[Unit]
Description=Node Exporter

[Service]
User=pi
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=default.target

Enable:

sudo systemctl daemon-reload
sudo systemctl enable --now node_exporter

4. Install Grafana

Grafana now uses a keyring file instead of a raw key.

Download:
wget -q https://apt.grafana.com/gpg.key

Check:
gpg --show-keys gpg.key

You should see fingerprint containing your key.

Convert it and move to the keyring directory
sudo gpg --dearmor gpg.key
sudo mv gpg.key.gpg /etc/apt/keyrings/grafana.gpg
sudo chmod 644 /etc/apt/keyrings/grafana.gpg

Update APT
sudo apt update

Install Grafana
sudo apt install grafana -y

sudo systemctl enable --now grafana-server

Dashboard at:
👉 http://<pi-ip>:3000
Login: admin / admin

5. Add Prometheus as Grafana Data Source

(Open Grafana → Settings → Data Sources → Prometheus → enter http://localhost:9090)

6. Network Monitoring Dashboard

Use this import code:

Grafana → Create → Import → enter ID

Grafana Dashboard ID: 1860 (Node Exporter Full)

7. Network Monitoring Dashboard
## Additional Notes

- Ensure your Raspberry Pi has a stable internet connection during installation.
- Regularly check for updates for Prometheus, Node Exporter, and Grafana to keep your monitoring setup secure and efficient.
