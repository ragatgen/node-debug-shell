# node-debug-shell

A `kubectl` plugin that simplifies node-level troubleshooting by launching an interactive debug shell on Kubernetes nodes.

The plugin automatically discovers cluster nodes, allows you to select a node interactively, lets you choose a debug image, and launches a `kubectl debug` session on the selected node.

## Features

* Interactive node selection
* Multiple debug image options:

  * **Wolfi** – Secure default image
  * **Netshoot** – Network diagnostics
  * **Azure Linux BusyBox** – Minimal image optimized for AKS
  * **Custom Image** – Any container image available in your cluster
* Creates a debug pod on the selected node
* Opens an interactive shell directly on the node using `chroot /host`
* Simplifies the standard `kubectl debug node/<node-name>` workflow
* Works with any Kubernetes cluster that supports `kubectl debug`

---

# Prerequisites

* Kubernetes cluster with node debugging enabled
* `kubectl` installed and configured
* A valid Kubernetes context
* RBAC permissions to:

  * List nodes
  * Create debug pods
* Kubernetes version that supports `kubectl debug`

---

# Installation

## Manual Installation

Clone the repository:

```bash
git clone https://github.com/ragatgen/node-debug-shell.git
```

Enter the project directory:

```bash
cd node-debug-shell
```

Make the plugin executable:

```bash
chmod +x kubectl-node-debug-shell
```

Install the plugin:

```bash
sudo install -m 755 kubectl-node-debug-shell /usr/local/bin/
```

---

## Verify Installation

Run:

```bash
kubectl plugin list
```

Expected output:

```text
/usr/local/bin/kubectl-node-debug-shell
```

---

# Usage

## Manual Installation

When installed manually, execute the plugin directly:

```bash
kubectl-node-debug-shell
```

Display help:

```bash
kubectl-node-debug-shell --help
```

Display the version:

```bash
kubectl-node-debug-shell --version
```

---

## Krew Installation

When installed through **Krew**, the plugin is available as:

```bash
kubectl node-debug-shell
```

Depending on your local `kubectl` plugin resolution, it may also be invoked as:

```bash
kubectl node debug shell
```

---

# Example

```text
------------------------------------------------------
kubectl-node-debug-shell 0.2.0
Interactive Kubernetes Node Troubleshooting
------------------------------------------------------

Using Kubernetes context: production

Available cluster nodes:

1) worker-01
2) worker-02
3) worker-03

Choose one node by number: 2

Select debug image:

1) Wolfi (Secure default)
2) Netshoot (Network diagnostics)
3) Azure Linux BusyBox (AKS-friendly minimal image)
4) Custom image

Choose image [1]: 2

Selected node: worker-02
Selected image: Netshoot
Image: nicolaka/netshoot

Starting debug session...

Creating debugging pod node-debugger-worker-02-xxxxx with container debugger on node worker-02.

If you don't see a command prompt, try pressing Enter.

root@worker-02:/#
```

---

# Debug Images

## Wolfi (Default)

```
cgr.dev/chainguard/wolfi-base
```

A secure, minimal image maintained by Chainguard.

Recommended for:

* General node troubleshooting
* Security-conscious environments
* Host inspection

---

## Netshoot

```
nicolaka/netshoot
```

Designed for advanced networking diagnostics.

Includes tools such as:

* tcpdump
* dig
* nslookup
* curl
* ping
* traceroute
* ss
* ip
* netcat
* mtr

---

## Azure Linux BusyBox

```
mcr.microsoft.com/cbl-mariner/busybox:2.0
```

A lightweight Microsoft-maintained image optimized for Azure Kubernetes Service (AKS).

---

## Custom Image

Use any container image that is accessible from your Kubernetes cluster.

Examples:

```
ubuntu:24.04
busybox:latest
myregistry.example.com/debug-tools:latest
```

---

# How It Works

The plugin:

1. Verifies that `kubectl` is installed.
2. Retrieves the current Kubernetes context.
3. Verifies that `kubectl debug` is available.
4. Validates permissions to list nodes and create debug pods.
5. Retrieves the list of cluster nodes.
6. Prompts you to select a node.
7. Prompts you to select a debug image.
8. Starts a `kubectl debug` session using the selected image.
9. Executes `chroot /host` to provide direct access to the node filesystem.

---

# Supported Kubernetes Platforms

This plugin works with any Kubernetes cluster that supports `kubectl debug`, including:

* Azure Kubernetes Service (AKS)
* Amazon Elastic Kubernetes Service (EKS)
* Google Kubernetes Engine (GKE)
* Red Hat OpenShift
* Rancher Kubernetes
* Self-managed Kubernetes clusters
* Any CNCF-conformant Kubernetes distribution

---

# Common Use Cases

* Node health investigations
* Networking diagnostics
* DNS troubleshooting
* Storage troubleshooting
* Host filesystem inspection
* Incident response
* Kubernetes node debugging
* General infrastructure troubleshooting

---

# Version

For manual installations:

```bash
kubectl-node-debug-shell --version
```

For Krew installations:

```bash
kubectl node-debug-shell --version
```

Example output:

```text
kubectl-node-debug-shell 0.2.0
```

---

# License

MIT License
