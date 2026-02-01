# Jetpath Helm Chart

High-performance eBPF/XDP load balancer and traffic routing platform for Kubernetes.

**Jetpath is a proprietary product by [EdgeNEXUS Limited](https://edgenexus.io).**

## 🚀 Why Jetpath?

With [NGINX Ingress Controller retiring in March 2026](https://kubernetes.io/blog/2025/11/11/ingress-nginx-retirement/), Jetpath offers a modern, high-performance alternative built on eBPF/XDP technology.

### Key Features

- **L4 Load Balancing**: Round robin, weighted, least connection, source persistence
- **L7 HTTP Routing**: Host and path-based routing at kernel speed
- **eBPF/XDP Performance**: Process packets at the earliest point in the network stack
- **Traffic Defense**: IP blocking and DDoS protection at kernel level
- **Kubernetes Native**: Automatic Service/Endpoint synchronization

## Prerequisites

- Kubernetes 1.23+
- Helm 3.0+
- Linux kernel 5.10+ with BPF support
- Nodes with privileged container support

## Installation

### Add the Helm repository

```bash
helm repo add jetpath https://helm.edgenexus.io
helm repo update
```

### Install the chart

```bash
helm install jetpath jetpath/jetpath --namespace jetpath-system --create-namespace
```

## Configuration

See [values.yaml](values.yaml) for the full list of configurable parameters.

### Common configurations

#### DaemonSet mode (default, recommended for production)

```yaml
deploymentMode: daemonset
```

#### Deployment mode (for testing)

```yaml
deploymentMode: deployment
replicaCount: 3
```

#### Enable Prometheus metrics

```yaml
metrics:
  enabled: true
  serviceMonitor:
    enabled: true
```

#### Custom network interface

```yaml
config:
  interface: "ens192"
```

## Migrating from NGINX Ingress

See our [Migration Guide](https://github.com/edgeNEXUS/jetpath/blob/main/docs/MIGRATION_FROM_NGINX_INGRESS.md) for step-by-step instructions.

### Quick comparison

| Feature | NGINX Ingress | Jetpath |
|---------|---------------|---------|
| Technology | User-space proxy | eBPF/XDP kernel |
| L4 Load Balancing | ✅ | ✅ |
| L7 HTTP Routing | ✅ | ✅ |
| Performance | Good | Excellent |
| DDoS Protection | Limited | Built-in XDP |
| Maintenance | Retiring March 2026 | Active |

## Service Annotations

Enable Jetpath for your services using annotations:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
  annotations:
    jetpath.io/enabled: "true"
    jetpath.io/lb-policy: "round_robin"
    jetpath.io/persistence: "source"
    jetpath.io/persistence-timeout: "3600"
spec:
  # ...
```

### Available annotations

| Annotation | Values | Default |
|------------|--------|---------|
| `jetpath.io/enabled` | `true`, `false` | `true` |
| `jetpath.io/lb-policy` | `round_robin`, `weighted_round_robin`, `least_connection`, `source_persistent` | `round_robin` |
| `jetpath.io/persistence` | `source`, `cookie` | none |
| `jetpath.io/persistence-timeout` | seconds | `3600` |
| `jetpath.io/forwarding-mode` | `proxy`, `dsr` | `proxy` |

## Uninstallation

```bash
helm uninstall jetpath --namespace jetpath-system
```

## Support

Jetpath is a proprietary product by EdgeNEXUS Limited.

- **Community Support**: [community.edgenexus.io](https://community.edgenexus.io)
- **Commercial Support**: [edgenexus.io/support](https://edgenexus.io/support)
- **Sales Enquiries**: sales@edgenexus.io

## Links

- [Product Website](https://edgenexus.io/jetpath)
- [Documentation](https://edgenexus.io/jetpath/docs)
- [API Reference](https://app.swaggerhub.com/apis/Edgenexus/Jetpath/1.0.0)
- [Migration from NGINX Ingress](https://edgenexus.io/jetpath/migrate-from-nginx)

## License

Proprietary - EdgeNEXUS Limited. All rights reserved.

Free for evaluation and non-commercial use. Commercial use requires a license from EdgeNEXUS Limited.

