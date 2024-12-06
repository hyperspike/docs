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


## Project Distribution

### Vanilla Kubernetes Manifests

To install the valkey-operator, all you need to do is run the following command:

```sh
LATEST=$(curl -s https://api.github.com/repos/hyperspike/valkey-operator/releases/latest | jq -cr .tag_name)
curl -sL https://github.com/hyperspike/valkey-operator/releases/download/$LATEST/install.yaml | kubectl create -f -
```

### Helm

```sh
LATEST=$(curl -s https://api.github.com/repos/hyperspike/valkey-operator/releases/latest | jq -cr .tag_name)
helm install valkey-operator --namespace valkey-operator-system --create-namespace oci://ghcr.io/hyperspike/valkey-operator --version ${LATEST}-chart
```

### Verifying the container image

```sh
LATEST=$(curl -s https://api.github.com/repos/hyperspike/valkey-operator/releases/latest | jq -cr .tag_name)
cosign verify ghcr.io/hyperspike/valkey-operator:$LATEST  --certificate-oidc-issuer https://token.actions.githubusercontent.com --certificate-identity https://github.com/hyperspike/valkey-operator/.github/workflows/image.yaml@refs/tags/$LATEST
```
