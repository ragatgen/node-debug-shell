# kubectl-node-debug-shell

A `kubectl` plugin that simplifies node-level troubleshooting in Kubernetes clusters.

The plugin discovers cluster nodes, lets you select a node interactively, lets you choose a debug image, and starts an interactive `kubectl debug` session on the selected node.

It works with AKS and any Kubernetes cluster where `kubectl debug` is supported.

## Features

- Lists available cluster nodes interactively
- Allows node selection from a menu
- Supports multiple debug images:
  - Wolfi
  - Netshoot
  - Azure Linux BusyBox
  - Custom image
- Creates a debug pod on the selected node
- Opens an interactive shell using `chroot /host`
- Simplifies the standard `kubectl debug node/<node-name>` workflow
- Works with any Kubernetes cluster where `kubectl debug` is available

## Prerequisites

- `kubectl` installed and available in your `PATH`
- `kubectl` configured for a Kubernetes cluster
- A current Kubernetes context selected
- A Kubernetes cluster that supports `kubectl debug`
- Sufficient RBAC permissions to:
  - List nodes
  - Create debug pods

## Installation

### Manual Installation

Clone the repository:

```bash
git clone https://github.com/ragatgen/kubectl-node-debug-shell.git
