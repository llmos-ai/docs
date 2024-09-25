---
sidebar_position: 1
title: LLMOS Configurations
---

LLMOS provides a set of configuration options that can be set in the `/etc/llmos/config.yaml` file. If the file doesn't exist, you can create it manually.

### Minimum Configuration

```shell
mkdir -p /etc/llmos
cat > /etc/llmos/config.yaml << EOF
role: cluster-init
token: mytoken
EOF
```

### Full Configuration Example

```yaml
################################################################
# The following parameters apply to the cluster-init role only #
################################################################

# LLMOS Operator version to be installed
llmosOperatorVersion: v0.1.0

# LLMOS chart repository, set to "latest" or "dev". Defaults to latest.
chartRepo: latest

# Kubernetes version to be installed. Defaults to a stable k3s version if not specified.
kubernetesVersion: v1.30.5+k3s1

# Custom values for the LLMOS Operator Helm chart.
# See https://github.com/llmos-ai/llmos-operator/blob/main/deploy/charts/llmos-operator/values.yaml
operatorValues:
  # Default values
  operator:
    apiserver:
      replicaCount: 1

# Additional SANs (hostnames) for the TLS certificate generated for port 6443.
tlsSans:
- additionalhostname.example.com

# Commands to run before bootstrapping the node.
preInstructions:
  - name: custom-pre-task
    # Image to extract and set as the current working directory (optional)
    image: custom/image:1.1.1
    # Environment variables to set
    env:
    - FOO=BAR
    # Program arguments
    args:
    - arg1
    - arg2
    # Command to execute
    command: /bin/dosomething
    # Save output to /var/lib/llmos/plan/plan-output.json (optional)
    saveOutput: false

# Commands to run after bootstrapping the node.
postInstructions:
  - name: custom-post-task
    env:
    - FOO=BAR
    args:
    - arg1
    - arg2
    command: /bin/dosomething
    saveOutput: false

# Custom Kubernetes resources to create after the LLMOS operator is bootstrapped.
resources:
  - kind: ConfigMap
    apiVersion: v1
    metadata:
      name: random
    data:
      key: value

# Content for the `registries.yaml` file used by k3s.
# Refer to https://rancher.com/docs/k3s/latest/en/installation/private-registry/ for details.
registries: {}

# Default registry for LLMOS operator container images.
# More details: https://github.com/llmos-ai/llmos-operator/blob/main/deploy/charts/llmos-operator/values.yaml
globalImageRegistry: someprefix.example.com:5000

# Advanced: Override the Kubernetes system agent installer image.
runtimeInstallerImage: ...

# Advanced: Override the LLMOS operator installer image.
llmosInstallerImage: ...

###############################################
# The following parameters apply to all roles #
###############################################

# URL for joining a node to the LLMOS cluster.
server: https://server-url:6443

# Shared secret for joining nodes to the cluster.
token: mytoken

# Role of this node. The cluster must start with one node as `role=cluster-init`.
# Additional nodes can join using `server` for control-plane nodes, or `agent` for worker nodes.
# These roles align with the server/agent terms used by k3s.
role: cluster-init,server,agent

# Set the Kubernetes node name.
nodeName: custom-hostname

# External IP address for the node in Kubernetes.
address: 123.123.123.123

# Internal IP address for the node.
internalAddress: 123.123.123.124

# Taints to apply to the node upon creation.
taints:
- dedicated=special-user:NoSchedule

# Labels to apply to the node upon creation.
labels:
- key=value

# Advanced: Arbitrary configuration to be placed in `/etc/rancher/k3s/config.yaml.d/40-llmos.yaml`.
extraConfig: {}
```
