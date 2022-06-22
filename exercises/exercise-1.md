## Exercise 1 - Local Setup

**[Return to k8s topics list](/README.md)**

**[Proposed solution](./solutions/solution-exercise-1/solution-exercise-1.md)**

Usually in the Kubernetes world when you are setting up a production cluster you could have multiple masters and worker nodes. 

If you want to test something on your local environment, setting up a cluster with those components will be pretty difficult or maybe even impossible if you don't have enough resources like memory, CPU, etc. 

For this exact use case there are some options to run K8s locally:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [k3d](https://k3d.io/v5.4.3/)
- [Kind](https://kind.sigs.k8s.io/)
- [MicroK8s](https://microk8s.io/)

No matter what option you choose, you can run k8s locally for testing purposes. 

Choose any of those, and install it on your pc.

Also, you need to install the command-line tool [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) to interact with your cluster.

After the installation, create a Kubernetes cluster with these requirements:

- 2 Master Nodes
- 3 Worker nodes
- Cluster Name: multi-node-cluster-exc-1

Test your cluster with kubectl running some commands like `kubectl cluster-info`, `kubectl get nodes`, etc.