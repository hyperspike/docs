+++
date = '2025-01-30T18:19:08-05:00'
draft = false
title = 'Configuration Options'
+++

# Configuration Options

This page describes the configuration options available for instatiating a new Valkey Cluster.

```yaml
apiVersion: hyperspike.io/v1
kind: Valkey
metadata:
  labels:
    app.kubernetes.io/name: keyval
  name: keyval
spec:
  # the number of master nodes in the cluster
  nodes: 3
  # the number of replicas per master node
  replicas: 0
  # the resource requests and limits for the Valkey Container
  resources:
    limits:
      cpu: 100m
      memory: 128Mi
    requests:
      cpu: 100m
      memory: 128Mi
  # boolean value to enable or disable TLS, cert-manager is required for TLS
  tls: true
  # the cert issuer to use for the Valkey Container
  certIssuer: selfsigned
  # the cert issuer type to use for the Valkey Container (ClusterIssuer or Issuer)
  certIssuerType: ClusterIssuer
  # Enalbe or disable external access to the Valkey Container
  externalAccess:
    # boolean value to enable or disable external access
    enabled: false
    # the type of service to use for external access (LoadBalancer or Proxy)
    type: LoadBalancer
    certIssuer: selfsigned
    certIssuerType: ClusterIssuer
    type: LoadBalancer
    loadBalancer:
      annotations:
        cert-manager.io/cluster-issuer: selfsigned
    proxy:
      annotations:
        cert-manager.io/cluster-issuer: selfsigned
      extraConfig: |
        proxy_buffer_size 128k;
        proxy_buffers 4 256k;
        proxy_busy_buffers_size 256k;
      hostname: valkey.example.com
      image: envoyproxy/envoy:v1.19-latest
      replicas: 1
      resources:
        limits:
          cpu: 100m
          memory: 128Mi
        requests:
          cpu: 100m
          memory: 128Mi
  # Volume Permissions ensures that the PVC volume ownership is set to the correct user
  volumePermissions: true
  # the image to use for the Valkey Sidecar Container/Exporter image
  exporterImage: ghcr.io/hyperspike/valkey-sidecar:latest
  # the image to use for the Valkey Container
  image: ghcr.io/hyperspike/valkey:latest
  # Enable or disable the Prometheus metrics endpoint requires servicemonitor crd (proetheus-operator|alloy) to be installed
  prometheus: true
  # the Prometheus metric labels to be used to target the correct prometheus instance
  prometheusLabels:
    prometheus: prometheus
  # the PVC object template to use for the Valkey Containers (corev1.PersistentVolumeClaim is used)
  storage:
    labels:
      custome: label
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
      storageClassName: standard
```
