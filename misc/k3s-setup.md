# K3s Setup

Links:
* https://rancher.com/docs/k3s/latest/en/installation/install-options/

## Setup Control Plane
### Install K3s
```sh
curl -sfL https://get.k3s.io | sh -
```

### Get K3s Token For Worker Nodes To Join
```sh
sudo cat /var/lib/rancher/k3s/server/node-token
```

## Add Worker Nodes
### Install K3s
```sh
curl -sfL https://get.k3s.io | K3S_URL=https://<CONTROL PLANE IP>:6443 K3S_TOKEN=<TOKEN> sh -
```

You can pass additional options as documented [here](https://rancher.com/docs/k3s/latest/en/installation/install-options/agent-config/).

**Example:**

You might have a node with special capabilities. You want to limit the total amount of pods and only use it for certain deployments. For example, it should only schedule pods requiring gigabit network.

You can limit the total number of pods by instructuring [kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/) like this:
```sh
curl -sfL https://get.k3s.io | K3S_URL=https://<CONTROL PLANE IP>:6443 K3S_TOKEN=<TOKEN> sh -s - --kubelet-arg="max-pods=3"
```

You can then use node [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) and [taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) to schedule some pods exclusively on a given node. See [Gigabit Nodes](#gigabit-nodes) below.

## Label Nodes
### Gigabit Nodes

If one or more nodes have gigabit network access, label them as such:
```sh
kubectl label nodes <NODE NAME> network-bandwidth=gigabit
```

In case the number of pods (or resources in general) is limited on that node, add a [taint](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) to repel (not schedule) any unwanted pods:

```sh

```

## Troubleshooting

#### `Failed to find memory cgroup, you may need to add \"cgroup_memory=1 cgroup_enable=memory\" to your linux cmdline (/boot/cmdline.txt on a Raspberry Pi)`

Append the following to `/boot/cmdline.txt`:
```
cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1
```
