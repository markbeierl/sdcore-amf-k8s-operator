# SD-Core AMF Operator (k8s)
[![CharmHub Badge](https://charmhub.io/sdcore-amf/badge.svg)](https://charmhub.io/sdcore-amf)

Charmed Operator for SD-Core's Access and Mobility Management Function (AMF).


## Pre-requisites

Juju model on a Kubernetes cluster.

## Usage

```bash
juju deploy sdcore-amf --trust --channel=edge
juju deploy mongodb-k8s --trust --channel=5/edge
juju deploy sdcore-nrf --channel=edge
juju deploy self-signed-certificates --channel=beta
juju integrate sdcore-nrf:database mongodb-k8s
juju integrate sdcore-nrf:certificates self-signed-certificates:certificates
juju integrate sdcore-amf:database mongodb-k8s
juju integrate sdcore-amf:fiveg-nrf sdcore-nrf:fiveg-nrf
juju integrate sdcore-amf:certificates self-signed-certificates:certificates
```

### Overriding external access information for N2 interface

By default, the N2 connection information sent to the RAN will be taken from
the created `LoadBalancer` Kubernetes Service. If this is not appropriate with
your network configuration, you can override that information through
configuration:

```bash
juju config sdcore-amf external-amf-ip=192.168.0.4 external-amf-hostname=amf.example.com
```

## Image

**amf**: ghcr.io/canonical/sdcore-amf:1.3
