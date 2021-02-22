# Introduction
With the growth of micro-service based architectures, the points of failures have distributed across multiple applications and servers. This raises a need for an active monitoring solution that helps the administrators and the application developers to know the failures before even the users of the systems notice it. In this blog we briefly introduce the responsibilities of the monitoring system followed by a brief guidance to Prometheus and Loki based monitoring infrastructure.


## Motivation

 What is the importance of distributed monitoring?
Monitoring infrastructure can help in the following aspects:
### 1. Identification of faults: 
    Faults such as network failures, unavailability, application exceptions resource overload are unpreventable while running a complex IT infrastructure. Monitoring helps in identifying the faults so that they are addressed on time. sometimes, it is not just about the faults that has occured already, rather it may be about the faults that are about to occur. The monitoring system should facilitate the identification of possible faults by providing interactive dashboards and by providing timely alerts. The fault identification involves indication of existence of a fault and sometimes showing the exact point of failure. 
### 2. Debugging
    Debugging an identified problems need a deep investigation with respect to the occured fault or an event. This sometimes needs different factors which revolve around the deployed service viz. CPU usage, internal logs, network transmissions, memory usage  and exceptions. Monitoring dashboards makes such information available to the debuggers without much efforts of manual extraction. Monitoring the logs accelerate the debugging provided there is a provision for visualization and filtering of logs.
### 3. Data Driven Insights
    Analyzing the long term and short term data collected for a running service add multitude of strategical benefits. Historical data showing the resource usage of a service over time assists in the decision related to acquision of the software, comparing the alternatives, scaling up/down the infrastructure. 

Now that we listed out the overall purpose of the monitoring, a typical monitoring tool would provide mainly monitoring and reporting functinalities. Monitoring involves the gathering of various metrics and logs. Reporting involves the visualization and alerting based on the collected metrics. 
Optionally monitoring tools can also perform certain administrative actions such as resource optimization (e.g. [Amazon Cloudwatch](https://aws.amazon.com/cloudwatch/)), providing remote management tooling ([NinjaRMM](https://www.ninjarmm.com/)) to the services and IT workflow automation ([OpManager](https://www.manageengine.com/network-monitoring/)).
## Overview
After reading this blog, you should be able to perform the following:
1. **Runtime Metrics:** Collection of run time metrics of running containers at different hosts. This mainly includes the resource and network bandwidth usage of the running containers. We shall achieve this using Prometheus, cAdvisor and Grafana.
2. **Alerting:** Alerting helps the administrators or the maintainers to know the service status without manually following the service status visualizations. The administrators can create different alerting rules and get notifications through different channels. We shall achieve alerting using Alertmanager and Prometheus. 
3. **Distributed Logging:** Logging gives an insight to the running applications and their behaviour. This can be used by the service providers to deduce the causes for malfunctioning and to get an overview of the client behavior. In the current document, we visualize the logs exported by NGINX. We shall achieve the logging using Loki and Grafana.
   
# Existing Monitoring solutions
# Prometheus and Loki
# Deployment and the Data Flow
The figure below shows a possible deployment where both metrics (collected by Prometheus and derived from Loki logs) and logs (collected by loki) are visualized using Grafana. Monitoring target hosts are being monitored by the monitoring infrastructure running on monitoring server. Vector and cAdvisors running on the target hosts help in exporting the metrics and logs to the monitoring server. Vector is used to publish the logs to Loki and cAdvisor is used to expose the metrics of the monitoring targets so that Prometheus can pull from them using cAdvisor APIs.

![The deployment and data flow](./resources/2020-01-29-Monitoring-Prometheus-Loki-Grafana/monitoring.png)



## Setting up the Monitoring Server
## Open ID provider

Monitoring server is composed of Grafana, Prometheus, Loki and Alertmanager. Optionally one can run vector and cAdvisor in case you want to monitor the monitoring server itself.

download the docker compose file and the configuration files:
```
# Download Docker compose
$wget  https://raw.githubusercontent.com/linksmart/blog/master/_posts\resources\2020-01-29-Monitoring-Prometheus-Loki-Grafana/docker-compose-monitoring_server.yml -O docker-compose.yml

# create a conf directory
$mkdir conf

# Download alertmanager conf
$wget https://raw.githubusercontent.com/linksmart/blog/master/_posts\resources\2020-01-29-Monitoring-Prometheus-Loki-Grafana/prometheus_conf_alertmanager.yml -O conf/alertmanager.yml

# Download prometheus configuration
$wget https://raw.githubusercontent.com/linksmart/blog/master/_posts\resources\2020-01-29-Monitoring-Prometheus-Loki-Grafana/prometheus_conf_prometheus.yml -O conf/prometheus.yml

# Download loki configuration
$wget https://raw.githubusercontent.com/linksmart/blog/master/_posts\resources\2020-01-29-Monitoring-Prometheus-Loki-Grafana/loki_loki-config.yaml -O conf/loki-config.yaml

```

## Setting Up the Monitoring Clients


# Use Case (EFPF)
Introduction to efpf and its infrastructure
- Composite applications failing of containers: monitoring at a central location.
- System administration to know RAM usage etc
- 

Multiple clients located at different locations sending the logs
Example client(s)




