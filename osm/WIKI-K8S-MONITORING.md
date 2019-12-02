# Feature 7898: Fault and Performance Management of OSM Modules

## Introduction
This is an utility to monitor the components of the OSM platform (RO, NBI, KAFKA, MySQL, etc...) with prometheus and
grafana dashboards

## Requirements
It must be installed the OSM platform using kubernetes 15.0. The OSM installer with the "-c k8s" option.

## Test 1: Install the feature

To install the utility you must use the instalation script.

```sh
$ cd <devops_download>/devops/installers/k8s
$ ./install_osm_k8s_monitoring.sh
```

It will install the kubernetes components of the feature within default namespace "monitoring"

To test if the instalation is correct, it must be installed the following components:

```sh
$ kubectl get all -n monitoring
NAME                                                                  READY   STATUS    RESTARTS   AGE
pod/alertmanager-osm-monitoring-prometheus-alertmanager-0             2/2     Running   0          3m17s
pod/osm-kafka-exporter-deployment-5bbdbb5696-sjhpz                    1/1     Running   0          2m42s
pod/osm-mongodb-exporter-prometheus-mongodb-exporter-555747db8nx6zw   1/1     Running   0          2m46s
pod/osm-monitoring-grafana-7869d6469c-949p7                           2/2     Running   0          2m40s
pod/osm-monitoring-kube-state-metrics-5d54cbf799-kp767                1/1     Running   0          3m24s
pod/osm-monitoring-prometheus-node-exporter-xlrhx                     1/1     Running   0          3m24s
pod/osm-monitoring-prometheus-operator-675c978bfb-cnjdm               2/2     Running   0          3m24s
pod/osm-mysql-exporter-prometheus-mysql-exporter-5688c46c65-kvfrm     1/1     Running   0          2m43s
pod/prometheus-osm-monitoring-prometheus-prometheus-0                 3/3     Running   1          3m7s


NAME                                                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
service/alertmanager-operated                              ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP   3m17s
service/osm-kafka-exporter-service                         ClusterIP   10.102.18.230    <none>        9092/TCP                     2m43s
service/osm-mongodb-exporter-prometheus-mongodb-exporter   ClusterIP   10.111.130.38    <none>        9216/TCP                     2m46s
service/osm-monitoring-grafana                             NodePort    10.97.106.171    <none>        80:18660/TCP                 3m24s
service/osm-monitoring-kube-state-metrics                  ClusterIP   10.101.134.16    <none>        8080/TCP                     3m24s
service/osm-monitoring-prometheus-alertmanager             NodePort    10.109.79.119    <none>        9093:14503/TCP               3m24s
service/osm-monitoring-prometheus-node-exporter            ClusterIP   10.111.14.25     <none>        9100/TCP                     3m24s
service/osm-monitoring-prometheus-operator                 ClusterIP   10.99.252.11     <none>        8080/TCP,443/TCP             3m24s
service/osm-monitoring-prometheus-prometheus               NodePort    10.100.133.205   <none>        9090:7569/TCP                3m24s
service/osm-mysql-exporter-prometheus-mysql-exporter       ClusterIP   10.107.104.205   <none>        9104/TCP                     2m43s
service/prometheus-operated                                ClusterIP   None             <none>        9090/TCP                     3m7s

NAME                                                     DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
daemonset.apps/osm-monitoring-prometheus-node-exporter   1         1         1       1            1           <none>          3m24s

NAME                                                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/osm-kafka-exporter-deployment                      1/1     1            1           2m43s
deployment.apps/osm-mongodb-exporter-prometheus-mongodb-exporter   1/1     1            1           2m46s
deployment.apps/osm-monitoring-grafana                             1/1     1            1           3m24s
deployment.apps/osm-monitoring-kube-state-metrics                  1/1     1            1           3m24s
deployment.apps/osm-monitoring-prometheus-operator                 1/1     1            1           3m24s
deployment.apps/osm-mysql-exporter-prometheus-mysql-exporter       1/1     1            1           2m43s

NAME                                                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/osm-kafka-exporter-deployment-5bbdbb5696                      1         1         1       2m42s
replicaset.apps/osm-mongodb-exporter-prometheus-mongodb-exporter-555747db8b   1         1         1       2m46s
replicaset.apps/osm-monitoring-grafana-7869d6469c                             1         1         1       3m24s
replicaset.apps/osm-monitoring-kube-state-metrics-5d54cbf799                  1         1         1       3m24s
replicaset.apps/osm-monitoring-prometheus-operator-675c978bfb                 1         1         1       3m24s
replicaset.apps/osm-mysql-exporter-prometheus-mysql-exporter-5688c46c65       1         1         1       2m43s

NAME                                                                   READY   AGE
statefulset.apps/alertmanager-osm-monitoring-prometheus-alertmanager   1/1     3m17s
statefulset.apps/prometheus-osm-monitoring-prometheus-prometheus       1/1     3m7s
```

After this command it is possible access to the grafical browser with the NodePort exported by the service grafana

```sh
service/osm-monitoring-grafana                             NodePort    10.97.106.171    <none>        80:18660/TCP                 3m24s
```
In the above results this NodePort will be 18660

```sh
  http://<ip_your_osm_host>:<nodeport>
```
  
* Username: admin
* Password: prom-operator

Inside the grafana WEB you must have the charts in diferent foders:

* Kubernetes Cluster: this folder will have diferents charts of the diferent components of kubernetes cluster such as PODs, 
API Server, etcd, etc.... The following list show some of this
  - CoreDNS
  - API server
  - Namespace (Pods)
  - Pod
  - Controller Manager
  - Kubelet
  - Persistent Volumes
  - Pods
  - ....

* OSM Third Party Modules: this folder have the three charts of third party modules in OSM
  - Kafka Exporter Overview
  - MongoDB
  - Mysql - Prometheus

* Summary: this folder will have a unique chart with teh summary of all components of OSM
  - Summary Kubernetes Cluster and OSM Modules

## Test 2: Uninstall the feature

To uninstall the utility you must use the uninstalation script.

```sh
$ cd <devops_download>/devops/installers/k8s
$ ./uninstall_osm_k8s_monitoring.sh
```

It will uninstall the kubernetes components of the feature within default namespace "monitoring"

To test if the instalation is correct, it must be installed the following components:

```sh
$ kubectl get all -n monitoring
No resources found.
```

