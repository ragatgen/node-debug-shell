# kubectl-node-debug-shell

A `kubectl` plugin that simplifies node-level troubleshooting by launching an interactive debug shell on Kubernetes nodes.

The plugin automatically discovers cluster nodes, allows you to select a node interactively, lets you choose a debug image, and starts a `kubectl debug` session on the selected node.

## Features

* Lists available cluster nodes interactively
* Allows node selection from a menu
* Provides multiple debug image options:

  * Wolfi — secure default
  * Netshoot — network diagnostics
  * Azure Linux BusyBox — AKS-friendly minimal image
  * Custom image
* Creates a debug pod on the selected node
* Opens a shell directly on the node for troubleshooting
* Simplifies the standard `kubectl debug node/<node-name>` workflow
* Supports any Kubernetes cluster where `kubectl debug` is available

## Prerequisites

* Kubernetes cluster with node debugging enabled
* `kubectl` installed and configured
* A current Kubernetes context selected
* Sufficient RBAC permissions to:

  * List nodes
  * Create debug pods
* Kubernetes version that supports `kubectl debug`

## Installation

### Manual Installation

```bash
git clone https://github.com/ragatgen/kubectl-node-debug-shell.git

cd kubectl-node-debug-shell

chmod +x kubectl-node-debug-shell

sudo install -m 755 kubectl-node-debug-shell /usr/local/bin/

Verify Installation
kubectl plugin list
Expected output:
/usr/local/bin/kubectl-node-debug-shell
Usage
Launch the plugin:
kubectl node-debug-shell
Display help:
kubectl node-debug-shell --help
Display version:
kubectl node-debug-shell --version
Example
------------------------------------------------------
kubectl-node-debug-shell 0.2.0
Interactive Kubernetes Node Troubleshooting
------------------------------------------------------
''''

Using Kubernetes context: production

'''bash
Available cluster nodes:

1) worker-01
2) worker-02
3) worker-03

Choose one node by number: 2

Select debug image:

1) Wolfi (secure default)
2) Netshoot (network diagnostics)
3) Azure Linux BusyBox (AKS-friendly minimal image)
4) Custom image
''''

Choose image [1]: 2

'''bash
Selected node:  worker-02
Selected image: Netshoot
Image:          nicolaka/netshoot

Starting debug session...
'''
Creating debugging pod node-debugger-worker-02-xxxxx with container debugger on node worker-02.

If you don't see a command prompt, try pressing Enter.

'''bash
root@worker-02:/#
Debug Image Options
Wolfi
cgr.dev/chainguard/wolfi-base
Recommended as the secure default image for general node inspection.
Netshoot
nicolaka/netshoot
Recommended for networking diagnostics such as DNS, routing, TCP connectivity, packet capture, and socket inspection.
Azure Linux BusyBox
mcr.microsoft.com/cbl-mariner/busybox:2.0
Recommended as a minimal AKS-friendly image for lightweight troubleshooting.
Custom Image
Allows you to provide any image available to your cluster, for example:
ubuntu:24.04
myregistry.example.com/debug-tools:latest
'''

## How It Works

The plugin:

Verifies that kubectl is installed.
Retrieves the current Kubernetes context.
Validates permissions to list nodes and create pods.
Checks that kubectl debug is available.
Retrieves the list of cluster nodes.
Presents an interactive node selection menu.
Presents an interactive debug image selection menu.
Executes a kubectl debug session against the selected node.
Starts chroot /host inside the debug container for node-level investigation and troubleshooting.


## Supported Environments

This plugin is Kubernetes-generic and works with clusters that support kubectl debug, including:

'''bash
Azure Kubernetes Service (AKS)
Amazon Elastic Kubernetes Service (EKS)
Google Kubernetes Engine (GKE)
Self-managed Kubernetes clusters
Other Kubernetes distributions with node debugging enabled
''''
## Common Use Cases

Investigating node health issues

Troubleshooting networking problems

Inspecting the host filesystem

Verifying node configuration

Collecting diagnostics during incident response

Analyzing node-level Kubernetes issues

Launching network-focused diagnostics with Netshoot

Using secure minimal debug environments with Wolfi

## Version

Display the installed plugin version:
'''bash
kubectl node-debug-shell --version

## Example output:
kubectl-node-debug-shell 0.2.0
''''

License
MIT License

