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

To pass additional options as documented [here](https://rancher.com/docs/k3s/latest/en/installation/install-options/agent-config/) (kubelet options [here](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)):
```sh
curl -sfL https://get.k3s.io | K3S_URL=https://<CONTROL PLANE IP>:6443 K3S_TOKEN=<TOKEN> sh -s - --kubelet-arg="max-pods=3"
```

## Label Nodes
### Gigabit Nodes

If one or more nodes have gigabit network access, label them as such:
```sh
kubectl label nodes <NODE NAME> network-bandwidth=gigabit
```

## Troubleshooting

#### `Failed to find memory cgroup, you may need to add \"cgroup_memory=1 cgroup_enable=memory\" to your linux cmdline (/boot/cmdline.txt on a Raspberry Pi)`

Append the following to `/boot/cmdline.txt`:
```
cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1
```
