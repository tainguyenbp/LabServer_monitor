# Build monitor with docker-compose

Use 

* prometheus
* node-exporter
* grafana
* nvidia-smi

to monitor.

## set up
```
docker pull prom/node-exporter
docker pull prom/prometheus
docker pull grafana/grafana
mkdir grafana_data
chown 472 grafana_data
mkdir prometheus_data
chmod o+w prometheus_data 
cd nvidia_smi_exporter
docker build -t . linnil1/nvidia-smi
cd ..
```

## some custom data you need to set
in `docker-compose.yml`

change this password `- GF_SECURITY_ADMIN_PASSWORD=custom_password`

in `prometheus.yml`

change it if you use node-exporter on localhost
```
  - job_name: 'node-exporter'
    scrape_interval: 5s
    static_configs:
         - targets: ['your.ip:9100']
```

in `nvidia_smi_exporter/nvidia_smi_exporter.go`

change 9101 to 9102

## reference
* `grafana_myserver.json` is modified from  https://grafana.com/dashboards/5573
* `docker-compose.yml` is modified from https://github.com/vegasbrianc/prometheus/blob/master/docker-compose.yml
