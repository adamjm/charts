# InfluxDB

##  An Open-Source Time Series Database

[InfluxDB](https://github.com/influxdata/influxdb) is an open source time series database built by the folks over at [InfluxData](https://influxdata.com) with no external dependencies. It's useful for recording metrics, events, and performing analytics.

## Note
The original work for this helm chart is present @ [Helm Charts]( https://github.com/helm/charts) Based on the [influxdb]( https://github.com/helm/charts/tree/master/stable/influxdb) chart 

## QuickStart

```bash
$ helm install stable/ibm-influxdb --name foo --namespace bar
```

## Introduction

This chart bootstraps an InfluxDB deployment and service on a Kubernetes cluster using the Helm Package manager.

## Chart Details
This chart bootstraps an InfluxDB deployment and service on a Kubernetes cluster. 

## Resources Required
The chart deploys pods consuming minimum resources as specified in the resources configuration parameter (default: Memory: 200Mi, CPU: 100m)
 
## Prerequisites

- Kubernetes 1.7+
- PV provisioner support in the underlying infrastructure (optional)
- Tiller 2.7.2 or later

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release stable/ibm-influxdb
```

The command deploys InfluxDB on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The default configuration values for this chart are listed in `values.yaml`. 

The [full image documentation](https://hub.docker.com/_/influxdb/) contains more information about running InfluxDB in docker.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set persistence.enabled=true,persistence.size=200Gi \
    stable/ibm-influxdb
```

The above command enables persistence and changes the size of the requested data volume to 200GB.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/ibm-influxdb
```

> **Tip**: You can use the default `values.yaml`

## Persistence

The [InfluxDB](https://hub.docker.com/_/influxdb/) image stores data in the `/var/lib/influxdb` directory in the container.

The chart mounts a [Persistent Volume](http://kubernetes.io/docs/user-guide/persistent-volumes/) at this location. The volume is created using dynamic volume provisioning.

## Starting with authentication

In `values.yaml` change `.Values.config.http.auth_enabled` to `true`.

Influxdb requires also a user to be set in order for authentication to be enforced. See more details [here](https://docs.influxdata.com/influxdb/v1.2/query_language/authentication_and_authorization/#set-up-authentication).

To handle this setup on startup, a job can be enabled in `values.yaml` by setting `.Values.setDefaultUser.enabled` to `true`.

Make sure to uncomment or configure the job settings after enabling it. If a password is not set, a random password will be generated.

## Limitations

## NOTE
This chart has been validated on ppc64le.
