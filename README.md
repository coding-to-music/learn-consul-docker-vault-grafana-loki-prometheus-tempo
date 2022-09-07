# learn-consul-docker-vault-grafana-loki-prometheus-tempo

# 🚀 Service Mesh Observability with Docker Compose consul vault grafana loki prometheus tempo 🚀

https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo

From / By https://learn.hashicorp.com/tutorials/consul/docker-compose-observability?in=consul/docker

Example of a Grafana dashboard, using data from Prometheus:

![The exporter container up and running](https://github.com/coding-to-music/terraform-cloudflare-prometheus-grafana/blob/main/images/image2-5.avif?raw=true)

![Grafana screenshot](https://github.com/coding-to-music/terraform-cloudflare-prometheus-grafana/blob/main/images/grafana_prometheus.png?raw=true)

## Digitalocean Droplet Prices

https://github.com/andrewsomething/do-api-slugs

https://slugs.do-api.dev

```
# https://slugs.do-api.dev/

# s-1vcpu-512mb-10gb  $4    10GB
# s-1vcpu-1gb         $6    25GB
# s-1vcpu-2gb         $12   50GB
# s-2vcpu-2gb         $18   60GB
# s-2vcpu-4gb         $24   80GB
# s-4vcpu-8gb         $48   160GB
```

## Environment variables:

```java

```

## user interfaces:

- Consul http://localhost:8500
- Fake Service http://localhost:9090/ui
- Prometheus http://localhost:9092/targets
- Node exporter metrics http://localhost:9100/metrics
- Grafana Tempo http://localhost:3000/explore
- Grafana Dashboards http://localhost:3000/dashboards
- Grafana Datasources http://localhost:3000/datasources

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo.git
git push -u origin main
```

# Overview

This repository contains all the example assets associated with the Consul
on Docker content on the [HashiCorp Learn](https://learn.hashicorp.com/consul)
website.

Specifically, the following articles and collections are currently supported by this repo.

- [Deploy a Secure Consul Datacenter with Docker Compose](https://learn.hashicorp.com/tutorials/consul/docker-compose-datacenter)

- [Capture Consul Events with Audit Logging](https://learn.hashicorp.com/tutorials/consul/audit-logging)

- [Service Mesh Observability with Docker Compose](https://learn.hashicorp.com/tutorials/consul/docker-compose-observability)

- [Automate Consul Agent Security with Auto Config](https://learn.hashicorp.com/tutorials/consul/docker-compose-auto-config)

- [Use hcdiag with Consul](https://learn.hashicorp.com/tutorials/consul/hcdiag-with-consul)

# Additional Assets

This repository also contains quick start Docker Compose assets that can be used to deploy Consul in various configurations. Rather than a supporting tutorial, a README file is included that will walk you through steps that will highlight various Consul concepts and scenarios.

# Service Mesh Observability with Docker Compose

13 MIN

PRODUCTS USED:
consul

This tutorial also appears in: Monitoring.

In this tutorial, you will create a local Consul service mesh and observability stack using Docker Compose. You will then explore your Consul service mesh with the observability suite.

The complexity of a service mesh environment requires advanced mechanisms to determine where services are running, the traffic patterns of the data flowing, and the health of the connections between them. Having this information makes it easier to not only understand failures occurring in your deployments, but also gives you the granularity needed to identify more subtle failures within your network such as performance degradation, packet loss, memory pressure, etc.

True service mesh observability consist of three core elements: metrics, logs and traces. To explore each of these elements, you will create an observability suite comprised of Prometheus (metrics), Loki (logs), Tempo (traces), and Grafana (visualization). Your Consul service mesh will host an example microservice application that will exhibit the ingress, API, and web layers. As you access the application; metrics, logs, and traces will be sent to your observability stack for you to explore.

This tutorial uses elements that are not suitable for production environments including an unsecured Consul datacenter, relaxed security policies, and container configurations only suited for development. The tutorial will teach you the core concepts for understanding and exploring observability in a Consul service mesh. Refer to the Consul Reference Architecture for Consul best practices and the Docker Documentation for Docker best practices.

## Prerequisites

## Linux or MacOS

Elements of this tutorial require a Linux or MacOS environment for deployment. See the Docker plugin page for more information about OS requirements.

## Docker

You will need a local install of Docker running on your machine for this tutorial. You can find the instructions for installing Docker on your specific operating system here. Docker Engine 19.03.0 was tested in this tutorial.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Visit the Docker Compose install guide for operating system specific installation instructions. Docker Compose format 3.7 was used in this tutorial.

## Loki logging drivers

Install the Loki logging drivers for Docker. See the Loki Docker driver plugin page for more information.

```
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```

## GitHub repository

Clone the GitHub repository containing the configuration files and resources.

```
git clone https://github.com/hashicorp/learn-consul-docker.git
```

Change into the directory with the newly cloned repository. This directory contains the complete configuration files.

```
cd learn-consul-docker/datacenter-deploy-observability
```

## Environment overview

The observability suite provides insight into the metrics, logs, and traces that occur throughout the Consul service mesh. This diagram illustrates the components of the observability suite and Consul service mesh that you will create in this tutorial.

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/environment-overview.png?raw=true)

Image of architecture diagram for this environment.

## Create environment

From within your working directory, run the following Docker Compose command to create your local service mesh environment and observability suite.

```
docker-compose up --detach
```

Output

```
Creating network "datacenter-deploy-observability_vpcbr" with driver "bridge"
Creating node-exporter ... done
Creating tempo         ... done
Creating grafana       ... done
Creating consul-server ... done
Creating prometheus    ... done
Creating loki          ... done
Creating ingress       ... done
Creating web           ... done
Creating api           ... done
Creating api_proxy     ... done
Creating ingress_proxy ... done
Creating web_proxy     ... done
```

Note: Your first run will take the longest as Docker will pull the respective images from the Docker Hub repository. Extra runs will not need you to download the image again and should only take a few seconds to complete.

## Perform testing procedures

Perform the following steps of each section to explore the elements involved in the service mesh and observability suite.

## Explore the Consul UI

Navigate to http://localhost:8500/ on your browser to access the Consul UI. Consul will navigate to the services tab by default.

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/nodes-page-consul.png?raw=true)

Image of Nodes page in Consul UI.

Notice the services monitored by Consul. Each of the applications (ingress, web, and api) includes a sidecar proxy that makes up the service mesh.

Note: If your Consul UI details do not match the image above, restart your container stack environment.

## Explore the sample application

Navigate to http://localhost:9090/ui/ and refresh the page to generate traffic.

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/sample-application.png?raw=true)

Image of sample application UI.

The example application shows the architecture of your complete application stack. Each refresh of this page will generate extra logs, metrics, and traces that your observability suite will ingest.

## Explore Prometheus targets

Navigate to http://localhost:9092/targets

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/prometheus-ui.png?raw=true)

Image of targets page in Prometheus UI.

Notice that Prometheus is pre-configured to scrape metric-related data from four endpoints: Consul, Node-Exporter, Tempo, and itself.

## Explore Grafana data sources

Navigate to http://localhost:3000/datasources

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/grafana.png?raw=true)

Image of data sources page in Grafana UI.

Grafana is pre-configured with Prometheus, Loki, and Tempo as data sources. These sources enable Grafana to visualize metrics, logs, and traces.

## Explore Logs and Traces

Navigate to http://localhost:3000/explore

Execute a search with these parameters: {container_name="web"} |= "trace_id"

Open one of the log lines, locate the TraceID field, then click the nearby Tempo link to jump directly from logs to traces.

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/tempo-traces.png?raw=true)

Image of linked logs and traces in Grafana UI.

Using this functionality, notice how logs and traces provide insight into service mesh performance.

To learn more about how application communication traverses through the service mesh, see the distributed tracing article.

## Explore Metrics

Navigate to http://localhost:3000/dashboards

Explore the metrics-related dashboards: Consul Server Monitoring and Node Exporter.

![](https://github.com/coding-to-music/learn-consul-docker-vault-grafana-loki-prometheus-tempo/blob/main/images/consul-node-exporter-metrics.png?raw=true)

Image of Consul Server Monitoring metrics dashboard in Grafana UI.

The Consul Server Monitoring dashboard presents important application-level metrics for Consul while the Node Exporter dashboard presents system-level metrics. Each of these dimensions provides important insight into the health and performance of your service mesh.

To learn more about the various runtime metrics reported by Consul, see the Consul telemetry docs.

## Clean up your environment

To clean up your environment, execute the following command.

```
docker-compose down --rmi all
```

Output

```
Stopping ingress_proxy ... done
Stopping api_proxy     ... done
Stopping web_proxy     ... done
Stopping web           ... done
Stopping api           ... done
Stopping ingress       ... done
Stopping grafana       ... done
Stopping node-exporter ... done
Stopping prometheus    ... done
Stopping consul-server ... done
Stopping tempo         ... done
Stopping loki          ... done
Removing ingress_proxy ... done
Removing api_proxy     ... done
Removing web_proxy     ... done
Removing web           ... done
Removing api           ... done
Removing ingress       ... done
Removing grafana       ... done
Removing node-exporter ... done
Removing prometheus    ... done
Removing consul-server ... done
Removing tempo         ... done
Removing loki          ... done
Removing network datacenter-deploy-observability_vpcbr
Removing image hashicorp/consul:1.8.10
Removing image nicholasjackson/fake-service:v0.21.0
Removing image nicholasjackson/consul-envoy:v1.6.1-v0.10.0
Removing image prom/node-exporter:v1.1.2
Removing image prom/prometheus:v2.26.0
Removing image grafana/tempo:1f1c40b3
Removing image grafana/grafana:7.5.3
Removing image grafana/loki:2.1.0
```

## Next steps

In this tutorial, you learned how to deploy and configure a local Consul service mesh and observability stack using Docker Compose. You also learned how to explore your Consul service mesh with the open source observability suite. Finally, you learned how to clean up your Docker environment.

You can continue learning the concepts of a secure Consul datacenter by completing the deploy a secure Consul datacenter with Docker Compose tutorial. This will teach you the concepts of Access Control Lists (ACLs), gossip encryption, and transport encryption.

You can also extend your Consul skills by exploring the following tutorials:

- Running Consul on Docker
- Running Consul on Kubernetes
- Service Discovery
- Service Mesh

For additional reference documentation on the technologies and Docker images used in this guide, refer to the following websites:

- hashicorp/docker-consul GitHub Repository
- grafana/grafana GitHub Repository
- grafana/loki GitHub Repository
- grafana/tempo GitHub Repository
- prometheus/prometheus GitHub Repository
- prometheus/node-exporter GitHub Repository
