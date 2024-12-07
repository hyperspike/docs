+++
date = '2024-12-06T09:50:15-05:00'
draft = false
title = 'Getting Started'
+++

# Quick Start

Deploy kubernetes locally using minikube, and install the controller:
```sh
git clone https://github.com/hyperspike/valkey-operator
cd valkey-operator
make quickstart
```

and optionally, turn on TLS and Prometheus:
```sh
make quickstart TLS=1 PROMETHEUS=1
```


### To Uninstall

```sh
make minikube-delete
```
