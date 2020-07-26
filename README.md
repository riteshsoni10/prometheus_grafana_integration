# Deployment of Grafana and Prometheus

The project consists of deployment steps and scripts for grafana and prometheus server on Kubernetes Cluster. Prometheus and Grafana applications are widely being used for monitoring of server metrics. Prometheus scraps the metrics from the server and Grafana visualises the metrics excellently.


**Project Infra Diagram**
<p align="center">
  <img src="screenshots/infra_flow.png" width="800" title="Project Infra Flow">
  <br>
  <em>Fig 1.: Project Flow  </em>
</p>


## Pre-Requisites
The following should be configured before proceeding further:

- Kubernetes Cluster

- Kubectl 


## Scope of Project

1. Container Image for Prometheus and Grafana Server
2. Deployment of Prometheus and Grafana Servers

### Prometheus Container Image

Prometheus is a free software application used for event monitoring and alerting. It records real-time metrics in a time series database built using a HTTP pull model, with flexible queries and real-time alerting. The `alpine linux` base operating system is used keeping in mind to minimise the size of image as much as possible. The prometheus server scraps the data or metrics from the target operating system. The difference between the two successive scrapes is defind by parameter `scrape_interval`. 

Command to install packages in `Alpine Linux`
```
apk add --no-cache --update prometheus -X  http://dl-cdn.alpinelinux.org/alpine/edge/community
```

The prometheus server stores the data i.e time series database at location `/var/lib/prometheus`. The prometheus server runs on `9090 port` by default. The Dockerfile is present in the repository at location `Dockerfiles` with name prometheus_dockerfile.

The prometheus server is started by executing the following command
```
/usr/bin/prometheus --config.file /etc/prometheus/prometheus.yml \ 
            --storage.tsdb.path /var/lib/prometheus/ \
            --web.console.libraries=/usr/share/prometheus/console_libraries \
            --web.console.templates=/usr/share/prometheus/consoles
```
> where prometheus.yml contains the configuration of the server.

### Grafana Container Image

Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources. It is expandable through a plug-in system. End users can create complex monitoring dashboards using interactive query builders. 

Command to install packages in `Alpine Linux`
```
apk add --no-cache --update grafana -X  http://dl-cdn.alpinelinux.org/alpine/edge/testing
```

The grafana server details are as follows in `Alpine Linux package`

```
Grafana Configuration File : /etc/grafana.ini
Port                       : 3000
Data Directory             : /var/lib/grafana/
Log Directory              : /var/log/grafana
```

### Prometheus Server Deployment

The project deploys the prometheus container image over kubernetes cluster using kubectl 
### Grafana Server Deployment

### Integration of Grafana with Prometheus
