# Telegraf-DS (DaemonSet) Helm chart for K3s.

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/telegraf-ds-k3s)](https://artifacthub.io/packages/search?repo=telegraf-ds-k3s)

[Telegraf](https://github.com/influxdata/telegraf) is a plugin-driven server agent used for collecting and reporting metrics. This chart runs a DaemonSet of Telegraf instances to collect host-level metrics for your cluster. To poll individual instances of infrastructure or APIs, use the [Telegraf chart](https://github.com/influxdata/helm-charts/tree/master/charts/telegraf).

The Telegraf-DS Helm chart uses the [Helm](https://helm.sh) package manager to bootstrap a Telegraf-DS (DaemonSet) on a [Kubernetes](http://kubernetes.io) cluster. You cannot customize Telegraf inputs for this chart being the goal is to provide an opinionated configuration for monitoring Kubernetes nodes and global Kubernetes monitoring.

This Helm Chart is based on the Oficial [Telegraf DaemonSet Helm Chart](https://github.com/influxdata/helm-charts). The main difference with the original Helm chart is the no support of docker-engine. This Helm Chart was personalized to run in K3s or other Kubernetes distros that don't use Docker as engine.

## Prerequisites

- Helm v2 or later
- Kubernetes 1.11+ with Beta APIs enabled

## QuickStart

```console
$ helm repo add awesome-helm-charts https://xe-nvdk.github.io/awesome-helm-charts/
$ helm install telegraf-ds-k3s awesome-helm-charts/telegraf-ds-k3s
```

> **Tip**: `helm upgrade --install [RELEASE] [CHART] [FLAGS]` is idempotent and can be run multiple times. If chart hasn't been installed, Helm installs it. If chart is installed, Helm redeploys the same version or upgrades the chart if a new version is available.

## Install the chart

To install the chart with the release name `my-release`:

```console
helm upgrade --install my-release awesome-helm-charts/telegraf-ds-k3s
```

The command deploys a Telegraf DaemonSet on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section as well as the [values.yaml](/values.yaml) file lists the parameters that can be configured during installation.

> **Tip**: To view all Helm chart releases, run `helm list`.

## Uninstall the chart

To uninstall/delete the `my-release` deployment:

```console
helm uninstall my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configure the chart

The default configuration parameters are listed in `values.yaml`. To change the defaults, specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```console
helm upgrade --install my-release \
  --set config.outputs.influxdb.url=http://foo.bar:8086 \
    influxdata/telegraf-ds
```

This command lets the chart deploy by setting the InfluxDB URL for Telegraf to write to.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm upgrade --install my-release -f values.yaml awesome-helm-charts/telegraf-ds-k3s
```

> **Tip**: `helm upgrade --install [RELEASE] [CHART] [FLAGS]` can be shortened : `helm upgrade -i [RELEASE] [CHART] [FLAGS]`

## Telegraf configuration

This chart deploys the following by default:

- `telegraf` running as a DaemonSet (`telegraf-ds`) with the following plugins enabled
  * [`cpu`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/cpu)
  * [`disk`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/disk)
  * [`diskio`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/diskio)
  * [`kernel`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/kernel)
  * [`kubernetes`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/kubernetes)
  * [`mem`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/mem)
  * [`net`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/net)
  * [`processes`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/processes)
  * [`swap`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/swap)
  * [`system`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/system)

The following plugin can be enable through the configuration:

- [`internal`](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/internal)
