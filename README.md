# aks-node-debug

A `kubectl` plugin that simplifies node-level troubleshooting in Azure Kubernetes Service (AKS).

The plugin automatically discovers nodes in your AKS cluster, allows you to select a node interactively, and launches a debug session using `kubectl debug`.

## Features

* Lists available AKS nodes interactively
* Allows node selection from a menu
* Creates a debug pod on the selected node
* Opens a shell directly on the node for troubleshooting
* Simplifies the standard `kubectl debug node/<node-name>` workflow

## Prerequisites

* Kubernetes cluster running on Azure Kubernetes Service (AKS)
* `kubectl` installed and configured
* Sufficient RBAC permissions to create debug pods and access nodes
* Kubernetes version that supports `kubectl debug`

## Installation

### Manual Installation

```bash
git clone https://github.com/ragatgen/kubectl-aks-node-debug.git

cd kubectl-aks-node-debug

chmod +x kubectl-aks-node-debug

sudo mv kubectl-aks-node-debug /usr/local/bin/
```

### Verify Installation

```bash
kubectl plugin list
```

Expected output:

```text
/usr/local/bin/kubectl-aks-node-debug
```

## Usage

Launch the plugin:

```bash
kubectl aks-node-debug
```

Example:

```text
Available nodes in your AKS cluster:

1) aks-default-99999999-vmss000000
2) aks-default-99999999-vmss000001
3) aks-default-99999999-vmss000002

Choose one node by number: 2

You selected: aks-default-99999999-vmss000001

Debugging node: aks-default-99999999-vmss000001...

Creating debugging pod node-debugger-aks-default-99999999-vmss000001-njktc with container debugger on node aks-default-99999999-vmss000001.

If you don't see a command prompt, try pressing Enter.

root@aks-default-99999999-vmss000001:/#
```

## How It Works

The plugin:

1. Retrieves the list of cluster nodes.
2. Presents an interactive node selection menu.
3. Executes a `kubectl debug` session against the selected node.
4. Opens a shell for node-level investigation and troubleshooting.

## Common Use Cases

* Investigating node health issues
* Troubleshooting networking problems
* Inspecting host filesystem contents
* Verifying node configuration
* Collecting diagnostics during incident response

## License

MIT License
