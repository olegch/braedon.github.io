[Prometheus Elasticsearch Exporter](https://github.com/braedon/prometheus-es-exporter)
====
This Prometheus exporter collects metrics from queries run on an Elasticsearch cluster's data, and metrics about the cluster itself.

[Source Code](https://github.com/braedon/prometheus-es-exporter) | [Python Package](https://pypi.org/project/prometheus-es-exporter) | [Docker Image](https://hub.docker.com/r/braedon/prometheus-es-exporter) | [Helm Chart](https://braedon.github.io/helm/prometheus-es-exporter)

# Installation
Deploy prometheus-es-exporter on a Kubernetes cluster with the default configuration:
```bash
helm repo add braedon https://braedon.github.io/helm
helm repo update

helm install braedon/prometheus-es-exporter --name <release name> \
                                            --set elasticsearch.cluster=<elasticsearch nodes> \
                                            --set image.tag=<image tag>
```

Specify configuration via a YAML file:
```bash
helm install braedon/prometheus-es-exporter --name <release name> -f <config file>.yaml
```

# Configuration
Available configurable parameters and their default values.

Parameter                   | Description                                         | Default
---                         | ---                                                 | ---
`elasticsearch.cluster`     | addresses of elasticsearch nodes to run queries on  | none
`elasticsearch.queries`     | elasticsearch queries to run                        | see values.yaml
`deployment.replicas`       | exporter pod replicas to deploy                     | `1`
`pod.annotations`           | annotations to add to the exporter pods             | `{}`
`pod.extraVolumes`          | extra volumes to pass to the exporter pod           | `[]`
`image.repository`          | exporter docker image repository                    | `braedon/prometheus-es-exporter`
`image.tag`                 | exporter docker image tag                           | none
`image.pullPolicy`          | exporter docker image pull policy                   | `IfNotPresent`
`container.port`            | exporter container metrics port                     | `9206`
`container.portName`        | exporter container metrics port name                | `prometheus`
`container.extraArgs`       | extra arguments to pass to the exporter container   | `[]`
`container.extraEnv`        | extra env vars to pass to the exporter container    | `[]`
`container.extraVolumeMounts` | extra volume mounts to pass to the exporter container | `[]`
`container.resources`       | exporter container resource requests & limits       | `{}`
`nodeSelector`              | node labels for exporter pod assignment             | `{}`
`tolerations`               | node taints to tolerate (requires Kubernetes >=1.6) | `[]`
`affinity`                  | node/pod affinities (requires Kubernetes >=1.6)     | `{}`
`service.port`              | exporter service port                               | `9206`
`service.portName`          | exporter service port name                          | `prometheus`
`service.annotations`       | annotations to add to the exporter service          | `{}`

See the [exporter README](https://github.com/braedon/prometheus-es-exporter#usage) for details on the format of exporter options like `elasticsearch.cluster`.

See the [example query config file](https://github.com/braedon/prometheus-es-exporter/blob/master/exporter.cfg) for examples and explanations of query configurations for `elasticsearch.queries`.
