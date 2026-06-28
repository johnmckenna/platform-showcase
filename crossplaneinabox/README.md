# Crossplane-in-a-Box Project

A localised, project-level encapsulation of a production-grade Internal Developer Platform (IDP) control plane. This project leverages the Nx build system to trigger localised Kubernetes cluster creation, eBPF container networking, infrastructure control planes, and GitOps engines.

## Project Architecture Stack

When executed, this project spins up an integrated local cloud-native stack:

* **Cluster Management:** Powered by `kind` utilising host container engines.
* **Networking & Security:** Orchestrated via **Cilium CNI** in full `kube-proxy` replacement mode with native **Kubernetes Gateway API** hooks.
* **Infrastructure Control Plane:** Handled by **Crossplane v2** to reconcile cloud-native manifests.
* **GitOps Engine:** Driven by **ArgoCD** to automatically sync infrastructure states.

---

## Execution and Lifecycle Management

This project uses Nx to coordinate execution tasks, wrapping the underlying configuration scripts and command runners.

### Starting the Platform

To bootstrap the entire stack—initialise the cluster, deploy the Cilium CNI, inject Gateway API resources, apply Crossplane specifications, and open ArgoCD—run the following command from the workspace root:

```shell
nx run crossplaneinabox:start
```

On a successful bootstrap sequence:

1. Your default Kubernetes context will automatically target `kind-control-plane`.
2. The initial admin password for ArgoCD is automatically decoded and injected directly into your system clipboard.
3. Your default web browser will automatically open to the dynamic LoadBalancer IP address allocated to the ArgoCD Gateway.

### Stopping the Platform

To destroy the project's local cluster instances and cleanly release background networking load balancers, run:

```shell
nx run crossplaneinabox:stop
```

---

## Prerequisites

Ensure your local host machine has the following tools installed globally:

* **Container Engine:** Docker Desktop, Podman Desktop, or Containerd (`nerdctl`).
* **CLI Client Binaries:** These are automatically installed in devbox.

---

## Observability & Debugging

The deployed resources are configured to communicate directly with standard cloud-native diagnostic tools:

* **Cilium CLI:** For auditing eBPF engine maps and node properties.
* **Hubble CLI:** To observe network traffic flows and localised application dependencies.
* **ArgoCD CLI:** For monitoring application synchronisation states outside the web browser.

---

## Licence

This project directory contains custom orchestration logic and reference patterns. All usage, reproduction, and modification permissions are proprietary and restricted to authorised colleagues under the guidelines specified in the root **`LICENSE.md`** file.
