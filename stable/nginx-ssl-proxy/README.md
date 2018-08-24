# nginx-ssl-proxy

[nginx-ssl-proxy](https://github.com/GoogleCloudPlatform/nginx-ssl-proxy) is a docker image that acts as an HTTP reverse proxy with optional but strongly encouraged support for acting as an SSL termination proxy.

## Introduction

This chart uses nginx-ssl-proxy docker image to deploy an HTTP reverse proxy. This deployment is useful to expose kubernetes services lacking SSL termination support.

## Prerequisites

A secret named `nginx-ssl-proxy-secret` should exist with the following fields:

* proxycert
* proxykey
* dhparam
* htpasswd

Refer to [nginx-ssl-proxy](https://github.com/GoogleCloudPlatform/nginx-ssl-proxy) documentation for the values.

## Installing the chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release .
```

This command deploys an HTTP reverse proxy using the default configuration.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

## Configuration

The following table lists the configurable parameters of the MySQL chart and their default values.

| Parameter               | Description                                | Default                    |
| ----------------------- | ------------------------------------------ | -------------------------- |
| `image.repository`      | `nginx-ssl-proxy` image repository         | `albertom/nginx-ssl-proxy` |
| `image.tag`             | `nginx-ssl-proxy` release tag              | `latest`                   |
| `image.pullPolicy`      | Image pull policy                          | `IfNotPresentsql`          |
| `service.type`          | Kubernetes service type                    | `LoadBalancer`             |
| `proxy.targetService`   | Kubernetes target service                  | `jenkins:8080`             |
| `proxy.enableSSL`       | Enables SSL reverse proxy                  | `true`                     |
| `proxy.enableBasicAuth` | Enable basic authentication                | `false`                    |
| `proxy.secretName`      | Kubernetes secret holding the certificates | `nginx-ssl-proxy-secret`   |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set proxy.targetService=jenkins:8080,proxy.enableBasicAuth=true \
  .
```

The above command deploys an HTTPS reverse proxy for jenkins service located at `jenkins:8080` in the Kubernetes cluster and adds basic authentication.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml .
```

> **Tip**: You can use the default [values.yaml](values.yaml)
