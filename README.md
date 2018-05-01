# OSB Stub

[![Build Status](https://travis-ci.org/jboyd01/osb-stub.svg?branch=master)](https://travis-ci.org/jboyd01/osb-stub "Travis") [![Docker Repository on Quay](https://quay.io/repository/jboyd01/osb-stub/status "Docker Repository on Quay")](https://quay.io/repository/jboyd01/osb-stub)

A go Open Service Broker stub implementation based on [`osb-starter-pack`](https://github.com/pmorie/osb-starter-pack) utilizing [`osb-broker-lib`](https://github.com/pmorie/osb-broker-lib) and [`go-open-service-broker-client`](https://github.com/pmorie/go-open-service-broker-client).  This is a No-Op Broker.  That is, it contains a single Service and it maintains minimal state in memory and does not actually provision any service.  It is used to exercise the Service Catalog and verify end to end infrastructure functionality.

## Who should use this project?

You should use this project if you're looking for a Open Service Broker you can use to verify your Kubernetes based Service Catalog deployment.

## Prerequisites

You'll need:

- [`go`](https://golang.org/dl/)
- A running [Kubernetes](https://github.com/kubernetes/kubernetes) (or [openshift](https://github.com/openshift/origin/)) cluster
- The [service-catalog](https://github.com/kubernetes-incubator/service-catalog)
  [installed](https://github.com/kubernetes-incubator/service-catalog/blob/master/docs/install.md)
  in that cluster

If you're using [Helm](https://helm.sh) to deploy this project, you'll need to
have it [installed](https://docs.helm.sh/using_helm/#quickstart) in the cluster.
Make sure [RBAC is correctly configured](https://docs.helm.sh/using_helm/#rbac)
for helm.

## Getting started

You can `go get` this repo or `git clone` it to start poking around right away.


### Get the project

```console
$ go get github.com/jboyd01/osb-stub/cmd/servicebroker
```

Or clone the repo:

```console
$ cd $GOPATH/src && mkdir -p github.com/jboyd01 && cd github.com/jboyd01 && git clone git://github.com/jboyd01/osb-stub
```

Change into the project directory:

```console
$ cd $GOPATH/src/github.com/jboyd01/osb-stub
```

### Deploy broker using Helm

Deploy with Helm and pass custom image and tag name.
Note: This also pushes the generated image with docker.

```console
$ IMAGE=myimage TAG=latest make push deploy-helm
```

### Deploy broker using Openshift

Deploy to OpenShift cluster by passing a custom image and tag name.
Note: You must already be logged into an OpenShift cluster. 
This also pushes the generated image with docker.

```console
$ IMAGE=myimage TAG=latest make push deploy-openshift
```

Running either of these flavors of deploy targets will build the broker binary,
build the image, deploy the broker into your Kubernetes, and add a
`ClusterServiceBroker` to the service-catalog.

## Goals of this project

- Provide a Service Broker that can be used for testing Service Catalog
