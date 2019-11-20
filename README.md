# OSM Monitoring
## Introduction
This is an utility to monitor the components of the OSM platform (RO, NBI, KAFKA, MUSQL, etc...) with prometheus and
grafana dashboards

## Requirements
It must be installed the OSM platform using kubernetes 15.0. The OSM installer with the "-c k8s" option.

## Install
To install the utility you must use the instalation script.

```sh
./install_osm_k8s_monitoring.sh
```

It will install the kubernetes components within the default namespace "monitoring", this namespace can be changed with
an option in the instalation script. To see the options type --help.

```sh
usage: ./install_osm_k8s_monitoring.sh [OPTIONS]
Install OSM Monitoring
  OPTIONS
     -n <namespace>   :   use specified kubernetes namespace - default: monitoring
     -s <service_type>:   service type (ClusterIP|NodePort|LoadBalancer) - default: NodePort
     --debug          :   debug script
     --dump           :   dump arguments and versions
     -h / --help      :   print this help
```

## Uninstall
To uninstall the utility you must use the instalation script.

```sh
./uninstall_osm_k8s_monitoring.sh
```

It will uninstall all components of this utility. To see the options type --help.

```sh
usage: ./uninstall_osm_k8s_monitoring.sh [OPTIONS]
Uninstall OSM Monitoring
  OPTIONS
     -n <namespace>:   use specified kubernetes namespace - default: monitoring
     --helm        :   uninstall tiller
     --debug       :   debug script
     -h / --help   :   print this help
```

## Functionality

This feature is based on the Prometheus software that implementets the monitoring of diferent services. This is composed by several
service monitorig servers and this service monitor server exports the data to the prometheus server.

We install three prometheus components:

* Operator (prometheus-operator): this component monitors the kubernetes services of the OSM platform deployed (RO, NBI, KAFKA, ...)
* Mysql (pormetheus-mysql): this component monitors the MySQL database status of the OSM platform
* MongoDB (pormetheus-mongodb): this component monitors the MongoDB database status of the OSM platform

The utility create a kubernetes infrastruture with PODS, SERVICES, etc... into the namespace monitoring.

## Access to Grafana Web Monitoring

To view the WEB with the diferent dashboards it is necesary to connect to the service "grafana" installed with this utility
and view the NodePort that uses. If the utility is installed with the default namespace "monitoring" you must type this:

```sh
kubectl get all --namespace monitoring
```

You must see the NodePort (greater than 30000) that uses the grafana service and type in your WEB broser:

```sh
  http://<ip_your_osm_host>:<nodeport>
```
  
* Username: admin
* Password: prom-operator

