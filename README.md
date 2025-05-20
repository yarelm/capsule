
<p align="left">
  <a href="https://bestpractices.coreinfrastructure.org/projects/5601"><img src="https://bestpractices.coreinfrastructure.org/projects/5601/badge.svg" alt="OpenSSF Best Practices"/></a>
  <a href="https://github.com/clastix/capsule/blob/master/LICENSE"><img src="https://img.shields.io/github/license/clastix/capsule" alt="License"/></a>
  <a href="https://github.com/clastix/capsule/blob/master/go.mod"><img src="https://img.shields.io/github/go-mod/go-version/clastix/capsule" alt="Go Mod Version"/></a>
  <a href="https://github.com/clastix/capsule/releases"><img src="https://img.shields.io/github/v/release/clastix/capsule" alt="Release"/></a>
  <a href="https://charmhub.io/capsule-k8s"><img src="https://charmhub.io/capsule-k8s/badge.svg" alt="Charmhub"/></a>
  <a href="https://slack.k8s.io/"><img src="https://img.shields.io/badge/slack-%23capsule-blue.svg?logo=slack" alt="Slack"/></a>
</p>

<p align="center">
  <img src="assets/logo/capsule_medium.png" />
</p>

---

# Kubernetes multi-tenancy made easy

**Capsule** implements a multi-tenant and policy-based environment in your Kubernetes cluster. It is designed as a microservice-based ecosystem with the minimalist approach, leveraging only on upstream Kubernetes.

# Addressing Multi-Tenancy Challenges in Kubernetes

While Kubernetes Namespaces offer a way to create logical partitions, advanced multi-tenancy scenarios become complex due to their flat structure and inability to share resources effectively across namespaces of the same tenant. This often leads to "cluster sprawl" – an operational nightmare of managing numerous dedicated clusters.

Capsule offers a solution by introducing the "Tenant" concept, a grouping of Kubernetes Namespaces. Within a single cluster, Capsule allows users to create their namespaces and share resources within their Tenant. The Capsule Policy Engine ensures isolation between Tenants, automatically inheriting policies like Network and Security Policies, Resource Quotas, and RBAC to all namespaces within a Tenant. This empowers users to manage their Tenants autonomously, reducing the need for cluster administrator intervention.

# Features

- **Self-Service**: Empowers developers to self-provision cluster resources within defined boundaries.
- **Preventing Clusters Sprawl**: Enables sharing a single cluster across multiple teams or departments, saving operational effort.
- **Governance**: Leverages Kubernetes Admission Controllers to enforce security best practices and policy requirements.
- **Resource Control**: Provides control over resource consumption by users, preventing overuse.
- **Native Experience**: Delivers multi-tenancy with a native Kubernetes experience, avoiding extra management layers or custom binaries.
- **GitOps ready**: Capsule is fully declarative and compatible with GitOps workflows.
- **Bring your own device (BYOD)**: Enables administrators to assign dedicated sets of cluster resources (such as compute, storage, and network) directly to tenants. This helps prevent the 'noisy neighbor' problem, ensuring that each tenant has access to their allocated resources without interference from others.

# Quick Start

This section provides a brief guide to get Capsule up and running on your Kubernetes cluster.

**Prerequisites:**

*   A running Kubernetes cluster (v1.16+).
*   `helm` CLI installed.
*   `kubectl` CLI installed and configured to communicate with your cluster.

**Installation:**

Capsule is typically installed using Helm. Please refer to the official Capsule documentation or [ArtifactHub](https://artifacthub.io/packages/helm/projectcapsule/capsule) for the latest Helm chart repository URL and detailed installation instructions.

**Creating a Tenant:**

1.  Create a file named `tenant-oil.yaml` with the following content:
    ```yaml
    apiVersion: capsule.clastix.io/v1beta2
    kind: Tenant
    metadata:
      name: oil
    spec:
      owners:
      - kind: User
        name: alice
      - kind: Group
        name: engineering
    ```
2.  Apply the Tenant manifest:
    ```bash
    kubectl apply -f tenant-oil.yaml
    ```

This creates a Tenant named `oil` managed by user `alice` and group `engineering`. User `alice` and members of the `engineering` group can now create namespaces and other resources within this Tenant, subject to policies defined by the administrator.

For more advanced configurations and detailed information, please refer to the full documentation.

# Documentation

Please check the project [documentation](https://capsule.clastix.io) for the cool things you can do with Capsule. Key topics covered include:

*   **Overview**: In-depth explanation of Capsule's architecture, core concepts, and benchmarks.
*   **Operating Capsule**: Guides for installation (including quickstart and upgrades), authentication, monitoring, backup/restore, Pod Security, and troubleshooting.
*   **Tenants**: Detailed information on managing Tenants, including permissions, namespace management, resource quotas, policy enforcement, and replications.
*   **Capsule Proxy**: Instructions for installing and configuring the Capsule Proxy, integrations with tools like Kubernetes Dashboard and Lens, and API reference.
*   **Guides**: Practical tutorials for common use cases, such as migrating namespaces across tenants and using Capsule with Flux for GitOps.
*   **API Reference**: Comprehensive reference for the Capsule API.

# Contributions

Capsule is Open Source with Apache 2 license and any contribution is welcome.

## Chart Development

### Chart Linting

The Helm chart is linted with [ct](https://github.com/helm/chart-testing). You can run the linter locally with this command:

```
make helm-lint
```

### Chart Documentation

The documentation for the Helm chart is generated using [helm-docs](https://github.com/norwoodj/helm-docs). This ensures that the `values.yaml` file is consistent with the chart's documentation. Run this command whenever you make changes to a `values.yaml` file:

```
make helm-docs
```

## Community

Join the community, share and learn from it. You can find all the resources to how to contribute code and docs, connect with people in the [community repository](https://github.com/clastix/capsule-community).

## Adopters

See the [ADOPTERS.md](ADOPTERS.md) file for a list of companies that are using Capsule.

# Governance

You can find how the Capsule project is governed [here](https://capsule.clastix.io/docs/contributing/governance).

## Maintainers

Please refer to the maintainers file available [here](.github/maintainers.yaml).

# FAQ

- Q. How to pronounce Capsule?

  A. It is pronounced as `/ˈkæpsjuːl/`.

- Q. Is it production grade?

  A. Although Capsule is under active development with frequent improvements, it is production-ready. Many organizations are using it in public and private deployments. Check out the [release](https://github.com/clastix/capsule/releases) page for a detailed list of available versions.

- Q. Does it work with my Kubernetes XYZ distribution?

  A. Capsule has been tested with vanilla Kubernetes 1.16+ on both private and public cloud environments. We expect it to work smoothly on any other Kubernetes distribution. Please let us know if you encounter any compatibility issues.

- Q. Do you provide commercial support?

  A. Yes, Clastix, the company behind Capsule, offers commercial support. Please contact us for a quote. 
