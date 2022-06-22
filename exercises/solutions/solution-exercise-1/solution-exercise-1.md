# Solution - Exercise 1

**[Return to k8s topics list](/docs/kubernetes/kubernetes.md)**

I'll install **kind** to create a K8s cluster locally.

First we have to install it:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64
chmod +x ./kind
```

Creating a Kubernetes cluster is as simple as `kind create cluster`.

By default, the cluster will be given the name `kind`, and it'll have just 1 node. 

You can use the `--name` flag to assign the cluster a different context name.

To see all the clusters you have created, you can use the `get clusters` command.

For example, let's say you create two clusters:

```bash
kind create cluster # Default cluster context name is `kind`.
...
kind create cluster --name kind-2
```
When you list your kind clusters, you will see something like the following:

```
kind get clusters
kind
kind-2
```

The exercise asks to create a cluster with 2 Master Nodes, 3 Worker nodes and `multi-node-cluster-exc-1` as the cluster name.

Let's create a `.yml` called `kind-multi-node.yml` (the name doesn't matter) with those configurations:

```yml
# a cluster with 2 control-plane nodes (2 Master nodes) and 3 workers
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: control-plane
- role: worker
- role: worker
- role: worker
```

Now run this command to create the cluster from the `.yml` file:

```
~/kind create cluster --name multi-node-cluster-exc-1 --config kind-multi-node.yml
```

In this [link](https://kind.sigs.k8s.io/docs/user/quick-start/#advanced) you'll find more examples of `.yml` files.

If you want to delete a cluster created with `kind create cluster` run this command:

```
~/kind delete cluster
```

If the flag `--name` is not specified, kind will use the default cluster context name `kind` and delete that cluster.

If you want to interact with your cluster in a more advanced way, you should use `kubectl`.


For example, to show the cluster information, run this command:

```bash
kubectl cluster-info --context multi-node-cluster-exc-1 # in the context flag you have to put your cluster's name

# The output will be something like this:
Kubernetes control plane is running at https://127.0.0.1:33481
CoreDNS is running at https://127.0.0.1:33481/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

Also you can get the cluster nodes:

```bash
kubectl get nodes --context multi-node-cluster-exc-1

# output
NAME                          STATUS   ROLES           AGE     VERSION
multi-node-cluster-exc-1-control-plane    Ready    control-plane   10m     v1.24.0
multi-node-cluster-exc-1-control-plane2   Ready    control-plane   9m47s   v1.24.0
multi-node-cluster-exc-1-worker           Ready    <none>          8m52s   v1.24.0
multi-node-cluster-exc-1-worker2          Ready    <none>          8m52s   v1.24.0
multi-node-cluster-exc-1-worker3          Ready    <none>          8m52s   v1.24.0
```




