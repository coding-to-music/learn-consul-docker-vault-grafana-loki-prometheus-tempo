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

## Install Consul

https://learn.hashicorp.com/tutorials/consul/get-started-install?in=consul/getting-started

HashiCorp officially maintains and signs packages for the following Linux distributions.

Consul for HCP: Install the Enterprise binary for your OS distribution if you intend to connect to HCP. Enterprise editions are available at https://releases.hashicorp.com/consul and are identified by the +ent in the file name.

Add the HashiCorp GPG key.

```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

Add the official HashiCorp Linux repository.

```
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

Update and install (for OSS Consul binary)

```
sudo apt-get update

sudo apt-get install consul
```

Update and install (for Enterprise Consul binary)

```
sudo apt-get update && sudo apt-get install consul-enterprise.x86_64
```

TIP: Now that you have added the HashiCorp repository, you can install Terraform, Vault, Nomad and Packer with the same command.

### Verify the installation

After installing Consul, verify that the installation worked by opening a new terminal session and running the command consul.

```
consul
```

```
usage: consul [--version] [--help] <command> [<args>]

Available commands are:
    agent          Runs a Consul agent
    event          Fire a new event
```

## Start the agent

https://learn.hashicorp.com/tutorials/consul/get-started-agent?in=consul/getting-started

Start the Consul agent in development mode.

```
consul agent -dev
```

## Discover datacenter members

Check the membership of the Consul datacenter by running the consul members command in a new terminal window. The output lists the agents in the datacenter. We'll cover ways to join Consul agents together later on, but for now there is only one member (your machine).

```
consul members
```

```
Node         Address         Status  Type    Build  Protocol  DC   Segment
Judiths-MBP  127.0.0.1:8301  alive   server  1.5.2  2         dc1  <all>
```

The output displays your agent, its IP address, its health state, its role in the datacenter, and some version information. You can discover additional metadata by providing the -detailed flag.

The members command runs against the Consul client, which gets its information via gossip protocol. The information that the client has is eventually consistent, but at any point in time its view of the world may not exactly match the state on the servers. For a strongly consistent view of the world, query the HTTP API, which forwards the request to the Consul servers.

```
curl localhost:8500/v1/catalog/nodes
```

```
[
  {
    "ID": "019063f6-9215-6f2c-c930-9e84600029da",
    "Node": "Judiths-MBP",
    "Address": "127.0.0.1",
    "Datacenter": "dc1",
    "TaggedAddresses": {
      "lan": "127.0.0.1",
      "wan": "127.0.0.1"
    },
    "Meta": {
      "consul-network-segment": ""
    },
    "CreateIndex": 9,
    "ModifyIndex": 10
  }
]
```

In addition to the HTTP API, you can use the DNS interface to discover the nodes. The DNS interface will send your query to the Consul servers unless you've enabled caching. To perform DNS lookups you have to point to the Consul agent's DNS server, which runs on port 8600 by default. The format of the DNS entries (such as Judiths-MBP.node.consul) will be covered in more detail later.

```
dig @127.0.0.1 -p 8600 Judiths-MBP.node.consul

dig @127.0.0.1 -p 8600 docker-ubuntu-s-1vcpu-1gb-nyc1-01
```

```
; <<>> DiG 9.10.6 <<>> @127.0.0.1 -p 8600 Judiths-MBP.node.consul
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7104
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;Judiths-MBP.node.consul. IN A

;; ANSWER SECTION:
Judiths-MBP.node.consul. 0 IN A 127.0.0.1

;; ADDITIONAL SECTION:
Judiths-MBP.node.consul. 0 IN TXT "consul-network-segment="

;; Query time: 0 msec
;; SERVER: 127.0.0.1#8600(127.0.0.1)
;; WHEN: Mon Jul 15 19:43:58 PDT 2019
;; MSG SIZE rcvd: 104

```

## Consul UI

http://localhost:8500/ui/dc1/services

http://localhost:8500/ui/dc1/overview/server-status

## Stop the agent

Stop the Consul agent by using the consul leave command. This will gracefully stop the agent, causing it to leave the Consul datacenter and shut down.

```

consul leave

```

```

Graceful leave complete

```

If you switch back to the window with Consul's streaming log output, the logs indicate that the Consul agent left the datacenter.

[INFO] consul: server starting leave
[INFO] serf: EventMemberLeave: Judiths-MBP.dc1 127.0.0.1
[INFO] consul: Handled member-leave event for server "Judiths-MBP.dc1" in area "wan"
[INFO] manager: shutting down
[INFO] serf: EventMemberLeave: Judiths-MBP 127.0.0.1
[INFO] consul: Removing LAN server Judiths-MBP (Addr: tcp/127.0.0.1:8300) (DC: dc1)
[WARN] consul: deregistering self (Judiths-MBP) should be done by follower
[ERR] autopilot: Error updating cluster health: error getting server raft protocol versions: No servers found
[INFO] consul: Waiting 5s to drain RPC traffic
[ERR] autopilot: Error updating cluster health: error getting server raft protocol versions: No servers found
[ERR] autopilot: Error updating cluster health: error getting server raft protocol versions: No servers found
[ERR] agent: Coordinate update error: No cluster leader
[ERR] autopilot: Error updating cluster health: error getting server raft protocol versions: No servers found
[INFO] agent: Requesting shutdown
[WARN] agent: dev mode disabled persistence, killing all proxies since we can't recover them
[DEBUG] agent/proxy: Stopping managed Connect proxy manager
[INFO] consul: shutting down server
[INFO] agent: consul server down
[INFO] agent: shutdown complete
[DEBUG] http: Request PUT /v1/agent/leave (11.004695827s) from=127.0.0.1:54434
[INFO] agent: Stopping DNS server 127.0.0.1:8600 (tcp)
[INFO] agent: Stopping DNS server 127.0.0.1:8600 (udp)
[INFO] agent: Stopping HTTP server 127.0.0.1:8500 (tcp)
[INFO] agent: Waiting for endpoints to shut down
[INFO] agent: Endpoints down
[INFO] agent: Exit code: 0

```

When you issue the leave command, Consul notifies other members that the agent left the datacenter. When an agent leaves, its local services running on the same node and their checks are removed from the catalog and Consul doesn't try to contact that node again.

Forcibly killing the agent process indicates to other agents in the Consul datacenter that the node failed instead of left. When a node fails, its health is marked as critical, but it is not removed from the catalog. Consul will automatically try to reconnect to a failed node, assuming that it may be unavailable because of a network partition, and that it may be coming back.

If an agent is operating as a server, a graceful leave is important to avoid causing a potential availability outage affecting the consensus protocol. Check the Adding and Removing Servers tutorial for details on how to safely add and remove servers.
```

# Additional consul tutorial

https://learn.hashicorp.com/tutorials/consul/get-started-service-discovery?in=consul/getting-started

# Secure Service Communication with Consul Service Mesh and Envoy

https://learn.hashicorp.com/tutorials/consul/service-mesh-with-envoy-proxy?in=consul/getting-started

Download two binaries and unzip them

```
wget https://github.com/hashicorp/demo-consul-101/releases/download/0.0.3.1/counting-service_linux_amd64.zip | unzip

wget https://github.com/hashicorp/demo-consul-101/releases/download/0.0.3.1/dashboard-service_linux_amd64.zip | unzip

mv dashboard-service_linux_amd64 dashboard-service

mv counting-service_linux_amd64 counting-service
```

This tutorial also appears in: Associate Tutorials, Service Mesh Security, Interactive Labs and Service Mesh & Gateways.
Consul service mesh secures service-to-service communication with authorization and encryption. Applications can use sidecar proxies in a service mesh configuration to automatically establish TLS connections for inbound and outbound connections without being aware of the network configuration and topology. In addition to securing your services, Consul service mesh can also intercept data about service-to-service communications and surface it to monitoring tools.

In this tutorial, you will register two services and their sidecar proxies in the Consul catalog. You will then start the services and sidecar proxies. Finally, you will demonstrate that the service-to-service communication is going through the proxies by stopping traffic with an "intention".

Flow diagram showing end user traffic being sent to the Dashboard Service at
port 9002. The dashboard service makes requests for the counting service to the
local sidecar proxy at port 5000. This traffic then traverses the service mesh
over dynamic ports. The traffic exits the service mesh from the counting
service's local proxy. The proxy sends this traffic to the counting service
itself at port 9003.

While this tutorial uses elements that are not suitable for production environments – Consul dev agents and mock services – it will teach you the common process for deploying your own services using Consul service mesh. At the end of this tutorial, we also present additional information about adapting this process to more production-like environments.

## Prerequisites

A running Consul server with Consul service mesh enabled. For this tutorial you will use a local dev agent, which enables Consul service mesh by default.

Envoy binary installed on the Consul agents. Consul includes a built-in Layer 4 (L4) proxy for testing and development but also offers first class support for Envoy as a sidecar proxy. This tutorial provides commands for both, with Envoy being the recommended proxy.

Two service applications which need to securely communicate. For this tutorial you will use two example service applications, a counter service and a dashboard. Download and unzip the executables to follow along.

Linux

MacOS
Counting Service (linux_amd64)
Dashboard Service (linux_amd64)

## Interactive tutorial

Launch Terminal
This tutorial includes a free interactive command-line lab that lets you follow along on actual cloud infrastructure.

Start Interactive Lab

Note: The interactive tutorial does not use the exact commands listed in this tutorial. You can consider the lab as a way to extend the concepts explained in this tutorial.

## Install Envoy on the agent

Note: Consul ships with a built-in proxy that you can use to test the Consul service mesh, as well as follow the tutorial. The built-in proxy should only be used where it is not possible to run Envoy, such as an older or unsupported operating system.

You can obtain container-based builds of Envoy directly from the Envoy Website or obtain a package of Envoy binary builds from a third-party project, such as func-e.io.

For your version of Consul, we recommend installing the latest compatible Envoy version listed in the Consul documentation. You can check your version of Consul with the command consul version. Set an environment variable with the latest compatible Envoy version string:

```
export ENVOY_VERSION_STRING=x.y.z
```

Issue the following command to download and install the func-e utility, which fetches and installs Envoy.

```
curl -L https://func-e.io/install.sh | bash -s -- -b /usr/local/bin
```

Note: If your machine uses an ARM64 chip (i.e., Apple M1), set the following environment variable before proceeding to the next step.

```
export FUNC_E_PLATFORM=darwin/amd64
```

Issue the following command to download the specified version of Envoy.

```
func-e use $ENVOY_VERSION_STRING
```

Open a new tab in your terminal or stop the Envoy process by pressing Control+C to use the current tab.

Copy the envoy binary to a location in your $PATH. This enables Consul to automatically start Envoy without specifying the binary location.

```
sudo cp ~/.func-e/versions/$ENVOY_VERSION_STRING/bin/envoy /usr/local/bin/
```

Verify that Envoy is in your $PATH by running the following command.

```
envoy --version
```

## Verify Consul agent health

To ensure that Consul is running and accessible from the command line, use the consul members command to verify your agent status.

```
consul members
Node            Address         Status  Type    Build   Protocol  DC   Segment
hostname.local  127.0.0.1:8301  alive   server  1.10.0  2         dc1  <all>
```

If you receive an error message, verify that a local Consul dev agent is running and try again.

## Register the services and sidecar proxies

Services have to be registered with Consul. Consul shares this information around the datacenter so that operators or other services can determine the location of a service. Consul service mesh also uses service registrations to determine where to send proxied traffic to.

There are several ways to register services in Consul:

- directly from a Consul-aware application

- from an orchestrator, like Nomad or Kubernetes

- using configuration files that are loaded at node startup

- using the API to register them with a JSON or HCL specification

- using the CLI to simplify this submission process

For this tutorial, we will use the consul service register CLI command to load them into the catalog.

## Create the counting service definition

First, define the Counting service and its sidecar proxy in a file named counting.hcl. The definition should include the name of the service, the port the service listens on, and a connect block with the sidecar_service block. This block is empty so Consul will use default parameters. The definition also includes an optional service health check.

counting.hcl

```
service {
  name = "counting"
  id = "counting-1"
  port = 9003

  connect {
    sidecar_service {}
  }

  check {
    id       = "counting-check"
    http     = "http://localhost:9003/health"
    method   = "GET"
    interval = "1s"
    timeout  = "1s"
  }
}
```

Services and sidecar proxies can be defined in either HCL or JSON. There is a JSON version of the service definition in the demo-consul-101 project.

## Create the dashboard service definition

Create the Dashboard service and proxy definition in the same way. First, create a file named dashboard.hcl.

dashboard.hcl

```
service {
  name = "dashboard"
  port = 9002

  connect {
    sidecar_service {
      proxy {
        upstreams = [
          {
            destination_name = "counting"
            local_bind_port  = 5000
          }
        ]
      }
    }
  }

  check {
    id       = "dashboard-check"
    http     = "http://localhost:9002/health"
    method   = "GET"
    interval = "1s"
    timeout  = "1s"
  }
}
```

There is a JSON version of the service definition in the demo-consul-101 project.

Note that the dashboard definition also includes an upstream block. Upstreams are ports on the local host that will be proxied to the destination service. The upstream block's local_bind_port value is the port your service will communicate with to reach the service you depend on. The destination name is the Consul service name that the local_bind_port will proxy to.

In our scenario, the dashboard service depends on the counting service. With this configuration, when dashboard service connects to localhost:5000 it is proxied across the service mesh to the counting service.

When applying these concepts to your production environments, verify that the values in the proxy configuration's upstreams block correctly specify the destination service and port number to avoid potential issues. For example, specifying the same values for the listener's port and target service will result in a proxy loop that will cause the server to crash. Refer to the Upstream Configuration Reference for additional information.

## Register the services and proxies

Finally, you can submit the service definitions to your Consul agent. If you are using the JSON definitions, ensure that the filenames end in ".json" instead of ".hcl".

```
consul services register counting.hcl
Registered service: counting
```

```
consul services register dashboard.hcl
Registered service: dashboard
```

Challenge: After completing the tutorial, try doing it again using one of the other service registration mechanisms mentioned earlier in the tutorial to register the services.

## Verify the services are registered

Now that you have registered your services and sidecar proxies, run consul catalog services to verify that they are present.

```
consul catalog services
```

```
consul
counting
counting-sidecar-proxy
dashboard
dashboard-sidecar-proxy
```

From the output you can notice that two extra services \*-sidecar-proxy are automatically registered alongside the one defined in the configuration files.

## Create a Consul intention

Intentions define authorization policies for services in the service mesh and are used to control which services may establish connections. The default intention behavior is defined by the default ACL policy.

In this tutorial, this step is not necessary since the default ACL policy for the dev agent is "allow all", so connections across the services in the service mesh are automatically allowed as well. However, you will create explicit intentions as a part of deploying service mesh enabled services.

Best Practice: Creating an explicit intention helps protect your service against changes to the implied permissions. For example, a change in default_policy or the introduction of a global deny-all intention would impact services without explicit intentions defined.

First, create a file for a config entry definition named intention-allow-config.hcl.

intention-allow-config.hcl

```
Kind = "service-intentions"
Name = "counting"
Sources = [
  {
    Name   = "dashboard"
    Action = "allow"
  }
]
```

From the same directory where you saved this file, run the following command on your terminal to initialize these intention rules.

```
consul config write intention-allow-config.hcl
Config entry written: service-intentions/counting
```

Note To learn more about intentions, feel free to check out the Service Intentions Docs.

## Start the services and sidecar proxies

Now that you have created all the necessary configuration to describe your service's connections, it's time to start your services and their sidecar proxies. We are using the & operator to run the services as background tasks. However, because they write to the console, it's best to run them in their own shell session.

Establish the local URL and start the dashboard service.

```
PORT=9002 COUNTING_SERVICE_URL="http://localhost:5000" ./dashboard-service &
```

Start the counting service.

```
PORT=9003 ./counting-service &
```

Next, start the sidecar proxies that will run as sidecar processes along with the service applications.

Start the Envoy sidecar proxy for the counting service.

```
consul connect envoy -sidecar-for counting-1 -admin-bind localhost:19001 > counting-proxy.log &
```

Start the Envoy sidecar proxy for the dashboard service.

```
consul connect envoy -sidecar-for dashboard > dashboard-proxy.log &
```

Note: The -sidecar-for argument takes a Consul service ID, not a service name.

## Check the dashboard interface

Open a browser and navigate to http://localhost:9002

You should see a screen similar to the following. There is a connection indicator in the top right that will turn green and say "Connected" when the dashboard service is in communication with the counting service.

Warning: If you use curl, or a browser that does not support Javascript, the status indicator will always say "Disconnected", even if the dashboard service is connected to the counting service.

Image of Dashboard UI. There is white text on a magenta background, with the
page title "Dashboard" at the top left. There is a green indicator in the top
right with the word connected in white. There is a large number 19 to show
sample counting output. The node name that the counting service is running on,
host01, is in very small monospaced type underneath the large
numbers.

If your application is not connected, check that the Counting service is running and healthy by viewing it in the Consul UI at http://localhost:8500.

## Test the sidecar proxy connections

To test that traffic is flowing through the sidecar proxies, you will control traffic with an intention.

First, deny the Dashboard service access to the Counting service. You'll do this by overwritting the previous intention with intention-deny-config.hcl. Create the file, then apply the new configuration.

intention-deny-config.hcl

```
Kind = "service-intentions"
Name = "counting"
Sources = [
  {
    Name   = "dashboard"
    Action = "deny"
  }
]
```

```
consul config write intention-deny-config.hcl

Config entry written: service-intentions/counting
```

Refresh your browser, the connection indicator in the Dashboard UI will now say "Disconnected"

Image of Dashboard UI. There is white text on a magenta background, with the
page title "Dashboard" at the top left. There is a red indicator in the top
right with the words "Counting Service is Unreachable" in white. There is a
large number -1 to show sample counting output. The word "Unreachable"
surrounded by square brackets is in monospaced type underneath the large
numbers.

You can restore communication between the services with the command you ran earlier to initialize your intentions.

```
consul config write intention-allow-config.hcl

Config entry written: service-intentions/counting
```

Back in the browser, verify that the dashboard reconnects to the counting service.

## Clean up

Once you are done with this tutorial, you can begin cleaning up by closing the terminal in which your counting-service, dashboard-service, and proxies are running. This should automatically stop these processes.

Delete the intention from Consul.

```
consul config delete -kind service-intentions -name counting

Config entry deleted: service-intentions/counting
```

Deregister the counting service.

```
consul services deregister counting.hcl

Deregistered service: counting
```

Deregister the dashboard service.

```
consul services deregister dashboard.hcl

Deregistered service: dashboard
```

## Extend these concepts

When you want to apply this learning to a proof-of-concept or production environment, there are some additional considerations.

## Enable Connect and gRPC

When a Consul server is started with the -dev flag, it will automatically enable Consul service mesh and provide a default port for gRPC communication. These have to be configured explicitly for regular Consul agents.

Consul server agent configuration

HCL

```
ports {
  grpc = 8502
}

connect {
  enabled = true
}
```

The connect section in the configuration is only needed for server agents. Client agents only need to configure the gRPC port.

## Next steps

Now that you have completed this tutorial, you have familiarized yourself with a basic service mesh enabled service deployment. You created and registered Consul service definitions that describe how two services communicate with each other. After starting the application and sidecar proxies, you used Consul service mesh intentions to control traffic flow between services. Finally, you learned about additional requirements required to take the concepts to a proof-of-concept environment.

# Create a Local Consul Datacenter

https://learn.hashicorp.com/tutorials/consul/get-started-create-datacenter?in=consul/getting-started

Now that you have practiced using Consul, it's time to learn a bit more about how Consul operates. In this tutorial, you'll create your first datacenter with multiple members.

When a new Consul agent starts, it doesn't know about other agents; it is essentially a datacenter with one member. To add a new agent to an existing datacenter you give it the IP address of any other agent in the datacenter (either a client or a server), which causes the new agent to join the datacenter. Once the agent is a member of the new datacenter, it automatically learns about the other agents via gossip.

In this tutorial, you will join two agents together to create a two-member Consul datacenter.

Architecture diagram with two nodes a client and a server

## Prerequisites

Consul is a distributed application that is designed to have one agent per machine. To run two agents on the same computer you will need to install VirtualBox, and Vagrant, which will run virtual machines to simulate a distributed environment.

Note: VirtualBox does not currently support Apple Silicon. As a result, you will not be able to complete this tutorial if your machine runs on an Apple M chipset.

## Set up the environment

Make a directory to store Vagrant's configuration for this tutorial.

```
mkdir consul-getting-started-join
```

Create a new file in the directory called `Vagrantfile` and paste the code below into it. This file will instruct Vagrant to create two virtual machines on your computer with the Consul binary preinstalled.

```
# -_- mode: ruby -_-

# vi: set ft=ruby :

$script = <<SCRIPT
echo "Installing dependencies ..."
sudo apt-get update
sudo apt-get install -y unzip curl jq dnsutils
echo "Determining Consul version to install ..."
CHECKPOINT_URL="https://checkpoint-api.hashicorp.com/v1/check"
if [ -z "$CONSUL*DEMO_VERSION" ]; then
CONSUL_DEMO_VERSION=$(curl -s "${CHECKPOINT_URL}"/consul | jq .current_version | tr -d '"')
fi
echo "Fetching Consul version ${CONSUL_DEMO_VERSION} ..."
cd /tmp/
curl -s https://releases.hashicorp.com/consul/${CONSUL_DEMO_VERSION}/consul*${CONSUL_DEMO_VERSION}\_linux_amd64.zip -o consul.zip
echo "Installing Consul version ${CONSUL_DEMO_VERSION} ..."
unzip consul.zip
sudo chmod +x consul
sudo mv consul /usr/bin/consul
sudo mkdir /etc/consul.d
sudo chmod a+w /etc/consul.d
SCRIPT

# Specify a Consul version

CONSUL_DEMO_VERSION = ENV['CONSUL_DEMO_VERSION']

# Specify a custom Vagrant box for the demo

DEMO_BOX_NAME = ENV['DEMO_BOX_NAME'] || "debian/stretch64"

# Vagrantfile API/syntax version.

# NB: Don't touch unless you know what you're doing!

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
config.vm.box = DEMO_BOX_NAME

config.vm.provision "shell",
inline: $script,
env: {'CONSUL_DEMO_VERSION' => CONSUL_DEMO_VERSION}

config.vm.define "n1" do |n1|
n1.vm.hostname = "n1"
n1.vm.network "private_network", ip: "172.20.20.10"
end

config.vm.define "n2" do |n2|
n2.vm.hostname = "n2"
n2.vm.network "private_network", ip: "172.20.20.11"
end
end
```

Boot your two virtual machines. This may take a moment to download everything needed for the environment to spin up.

```
vagrant up
```

Output

```
Bringing machine 'n1' up with 'virtualbox' provider...
Bringing machine 'n2' up with 'virtualbox' provider...
...
```

## Start the agents

In previous tutorials, you used a single agent in development mode to test Consul's functionality. However, you should never run development agents in production. In this tutorial, you will configure your first Consul agent to run in server mode instead, via the following command line flags. (In production you would provide these settings to consul in a configuration file.)

server- Providing this flag specifies that you want the agent to start in server mode.

-bootstrap-expect - This tells the Consul server how many servers the datacenter should have in total. All the servers will wait for this number to join before bootstrapping the replicated log, which keeps data consistent across all the servers. Because you are setting up a one-server datacenter, you'll set this value to 1.

-node - Each node in a datacenter must have a unique name. By default, Consul uses the hostname of the machine, but you'll manually override it, and set it to agent-one.

-bind - This is the address that this agent will listen on for communication from other Consul members. It must be accessible by all other nodes in the datacenter. If you don't set a bind address Consul will try to listen on all IPv4 interfaces and will fail to start if it finds multiple private IPs. Since production servers often have multiple interfaces, you should always provide a bind address. In this case it is 172.20.20.10, which you specified as the address of the first VM in your Vagrantfile.

data-dir - This flag tells Consul agents where they should store their state, which can include sensitive data like ACL tokens for both servers and clients. In production deployments you should be careful about the permissions for this directory.

config-dir - This flag tells consul where to look for its configuration. You will set it to a standard location: /etc/consul.d.

## Start Consul server

Once the environment is up, ssh into the first node, n1, to begin the configuration of your datacenter.

```
vagrant ssh n1

Linux n1 4.9.0-12-amd64 #1 SMP Debian 4.9.210-1 (2020-01-20) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

vagrant@n1:~$
```

Start your first Consul agent by running the following command. Consul will start up in the foreground of your terminal window.

Note: Do not copy the vagrant@n1:~
when copying the command. This special prompt reminds you that you are ssh-ed into the first virtual machine.

vagrant@n1:~

```
consul agent \
 -server \
 -bootstrap-expect=1 \
 -node=agent-one \
 -bind=172.20.20.10 \
 -data-dir=/tmp/consul \
 -config-dir=/etc/consul.d

...
```

## Start Consul client

Open a new terminal window and move into consul-getting-started-join directory. Then ssh into your second virtual machine.

```

vagrant ssh n2

```

Now start up your second Consul agent in client mode. You'll set the bind address to the IP address of the second VM (172.20.20.11, specified in the Vagrantfile) and the name to agent-two. Don't include the -server flag and the agent will start in client mode. Consul will run in the foreground of your terminal.

Note: Do not copy the vagrant@n2:~
when copying the command. This special prompt reminds you that you are ssh-ed into the second virtual machine.

vagrant@n2:~

```

consul agent \
 -node=agent-two \
 -bind=172.20.20.11 \
 -enable-script-checks=true \
 -data-dir=/tmp/consul \
 -config-dir=/etc/consul.d

```

## Check datacenter membership

Now you have two Consul agents running: one server and one client. The two agents still don't know about each other and each comprise their own single-node datacenters.

Verify this by ssh-ing into each VM and checking each agent's membership information. You'll need to open a new terminal window and change into the consul-getting-started-join directory.

Check the membership of agent-two.

```

vagrant ssh n2

Linux n2 4.9.0-9-amd64 #1 SMP Debian 4.9.168-1+deb9u2 (2019-05-13) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
You have new mail.
Last login: Fri Aug 2 23:42:33 2019 from 10.0.2.2

vagrant@n2:~$

```

Note: Do not copy the vagrant@n2:~
when copying the command. This special prompt reminds you that you are ssh-ed into the second virtual machine.

vagrant@n2:~

```

consul members

Node Address Status Type Build Protocol DC Segment
agent-two 172.20.20.11:8301 alive client 1.9.3 2 dc1 <default>
Open a new terminal window and change directories into consul-getting-started-join.

Check the membership of agent-one.

```

vagrant ssh n1

Linux n1 4.9.0-9-amd64 #1 SMP Debian 4.9.168-1+deb9u2 (2019-05-13) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
You have new mail.
Last login: Fri Aug 2 20:37:46 2019 from 10.0.2.2

vagrant@n1:~$

```

Note: Do not copy the vagrant@n1:~
when copying the command. This special prompt reminds you that you are ssh-ed into the first virtual machine.

vagrant@n1:~

```

consul members

Node Address Status Type Build Protocol DC Segment
agent-one 172.20.20.10:8301 alive server 1.9.3 2 dc1 <all>

## Join the agents

You're now ready to create your multi-agent datacenter. Open the terminal window where you are ssh-ed into the second VM, and run the consul join command on the Consul client, giving it the bind address of the Consul server.

Note: Do not copy the vagrant@n2:~
when copying the command. This special prompt reminds you that you are ssh-ed into the second virtual machine.

vagrant@n2:~

consul join 172.20.20.10

Successfully joined cluster by contacting 1 nodes.

In the same window, run consul members again and you should get both agents listed in the output.

vagrant@n2:~

```

consul members

Node Address Status Type Build Protocol DC Segment
agent-one 172.20.20.10:8301 alive server 1.9.3 2 dc1 <all>
agent-two 172.20.20.11:8301 alive client 1.9.3 2 dc1 <default>

```

Switch to the terminal window where your Consul server is running on the first VM, and you'll notice some log output indicating that agent two joined it.

Now switch to the terminal where your client is running on the second VM. You'll notice that the client had been throwing warnings and errors indicating that no servers were available. When the client learned about the server, it stopped throwing errors and synced its node information.

```

...
[WARN] agent.router.manager: No servers available
[ERROR] agent.anti_entropy: failed to sync remote state: error="No known Consul servers"
[WARN] agent.router.manager: No servers available
[ERROR] agent.anti_entropy: failed to sync remote state: error="No known Consul servers"
[INFO] agent: (LAN) joining: lan_addresses=[172.20.20.10]
[INFO] agent.client.serf.lan: serf: EventMemberJoin: agent-one 172.20.20.10
[INFO] agent: (LAN) joined: number_of_nodes=1
[INFO] agent.client: adding server: server="agent-one (Addr: tcp/172.20.20.10:8300) (DC: dc1)"
[INFO] agent: Synced node info
...

```

Consul clients can not function without a server. All datacenters must have at least one agent running in server mode for Consul to function correctly.

In datacenters with more than one server, more than half of the servers must be in communication with each other at all times for the datacenter to function correctly. This is called maintaining quorum. You can learn more about the quorum requirements of servers in the architecture documentation.

Switch to the window where you are ssh-ed onto the second VM and run consul members on the client. The client will also list both agents as members.

vagrant@n2:~

```

consul members

Node Address Status Type Build Protocol DC Segment
agent-one 172.20.20.10:8301 alive server 1.9.3 2 dc1 <all>
agent-two 172.20.20.11:8301 alive client 1.9.3 2 dc1 <default>

```

Tip: To join a datacenter, a Consul agent only needs to learn about one other existing member, which can be a client or a server. After joining the datacenter, the agents automatically gossip with each other to propagate full membership information.

## Notes on auto-join

In production, new Consul agents should automatically join the datacenter without human intervention. You can configure Consul to automatically discover new agents in AWS, Google Cloud or Azure by adding the relevant cloud auto join object to your Consul configuration file. This will allow a new node to join the datacenter without any hard-coded configuration.

Alternatively, you can provide hard-coded addresses of known Consul agents to new agents using the -join flag or -retry-join flag.

## Query a node

You can query Consul agents using the DNS interface or HTTP API.

For the DNS API, the structure of the names is NAME.node.consul or NAME.node.DATACENTER.consul. If the datacenter is omitted, Consul will only search the local datacenter.

From the terminal window where you are ssh-ed into agent-one, query the DNS interface for the address of agent-two.

vagrant@n1:~

```

dig @127.0.0.1 -p 8600 agent-two.node.consul

...

;; QUESTION SECTION:
;agent-two.node.consul. IN A

;; ANSWER SECTION:
agent-two.node.consul. 0 IN A 172.20.20.11

```

The ability to look up nodes in addition to services is useful for system administration, in addition to service discovery. For example, knowing the address of the node to SSH into is as easy as making the node a part of the Consul datacenter and querying it.

## Stop the agents

Stop both of your agents gracefully by either typing Ctrl-c in the terminal windows where they are running, or issuing the consul leave command.

## Clean up the environment

Vagrant will automatically stop and power down the virtual machines it created, remove their hard disks from your machine, and free up all of the disk space and RAM they consume.

It will not get rid of the directory you created or the Vagrant file it contains, so if you would like to re-run this tutorial, all you need to do is issue vagrant up again from inside the consul-getting-started-join directory.

Clean up your virtual environment by running the following command from within the consul-getting-started-join directory.

```

vagrant destroy

```

```

n2: Are you sure you want to destroy the 'n2' VM? [y/N] y
==> n2: Forcing shutdown of VM...
==> n2: Destroying VM and associated drives...
n1: Are you sure you want to destroy the 'n1' VM? [y/N] y
==> n1: Forcing shutdown of VM...
==> n1: Destroying VM and associated drives...

```

## Next steps

In this tutorial, you set up a multi-agent Consul datacenter by joining two Consul agents, a server and a client. Get more hands-on experience with Consul's features with the following tutorials:

- Get Started with Consul Service Mesh
- Consul on Kubernetes
- Consul and Nomad

```

```
