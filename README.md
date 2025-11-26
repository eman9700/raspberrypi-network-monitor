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

5. Add Prometheus as Grafana Data Source

6. Network Monitoring Dashboard

7. Network Monitoring Dashboard
