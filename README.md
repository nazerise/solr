<!--- app-name: Apache Solr -->

when solr pod is running in Kubernetes and you want to restart it, an error like this will be shown and solr will fail to start again:
```console
Port 8983 is already being used by another process (pid: 88)
```
[solr bitnami issue](https://github.com/bitnami/containers/issues/986)

According to this problem, I Add [kill-solr.yaml](https://github.com/nazerise/solr/blob/main/templates/kill-solr.yaml) to helm chart of bitnami/solr which is mounted to /opt/bitnami/scripts/solr/kill-solr.sh .
The main helm chart can be download by these command:
```console
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-solr bitnami/solr --version 8.5.0
```
kill-solr.sh is added in preStop. So, when solr pods terminate, kill-solr.sh runs and kills solr gracefully.

# Bitnami package for Apache Solr

Apache Solr is an extremely powerful, open source enterprise search platform built on Apache Lucene. It is highly reliable and flexible, scalable, and designed to add value very quickly after launch.

[Overview of Apache Solr](http://lucene.apache.org/solr/)

Trademarks: This software listing is packaged by Bitnami. The respective trademarks mentioned in the offering are owned by the respective companies, and use of them does not imply any affiliation or endorsement.

## Prerequisites

- Kubernetes 1.23+
- Helm 3.8.0+
- PV provisioner support in the underlying infrastructure
- ReadWriteMany volumes for deployment scaling

## Installing the Chart

To install the chart with the release name `my-release`:

```console
git clone https://github.com/nazerise/solr.git
helm install my-release ./solr -n my-namespace
```
