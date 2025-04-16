---
description: This section guides you through setting up Kerno on a local Kubernetes cluster
---

# Install Kerno Locally

{% hint style="warning" %}
We're currently aware of issues with Docker on Apple M4 chips. If you're installing Kerno using Docker, please use a Mac with an earlier chip version (M1/M2/M3) for now. We're looking into a resolution and will provide updates soon.
{% endhint %}

Installing Kerno locally is a quick way to experience eBPF-powered observability in your Kubernetes cluster. In just a few steps, you’ll be collecting invaluable insights into your workloads and cluster behavior without complex configurations.

{% hint style="info" %}
Local installations do not include the Kerno dashboard, but we’re actively working on it.
{% endhint %}

### **Prerequisites**

1. [Kind](https://kind.sigs.k8s.io/), [minikube](https://minikube.sigs.k8s.io/docs/start), or [k3d](https://k3d.io/) installed on your machine.
2. A local Kubernetes cluster up and tunning
3. The kubectl CLI tool installed and configured to access your cluster.
4. Docker installed locally to run the installer image.
5. Minimum [system requirements](system-requirements.md#hardware-and-resource-requirements).

{% hint style="info" %}
If you are using minikube please execute this command when creating the cluster:\
`minikube start --embed-certs`
{% endhint %}

### Installing Kerno

Ensure your `kubectl` context is set to the cluster where you want to install Kerno:

```markup
kubectl config use-context <kubernetes-context>
```

Run the Kerno installer via Docker, mounting your local `~/.kube/config`:

```markup
docker run -it --pull always --network host \
  -e ENVIRONMENT=local \
  -v ~/.kube/config:/root/.kube/config \
  public.ecr.aws/fyck.io/installer:main
```

The installation automatically creates the necessary deployments and daemon sets in your cluster.

### **Verifying the Installation**

Kerno installs the following Kubernetes resources in the `kerno` namespace:

* **Nanobe** (Deployment)
* **Preon** (DaemonSet)
* **Vector** (DaemonSet)

You can learn more about Kerno's architecture [here](../concepts-and-references/architecture.md).

To verify that these resources are running correctly, run:

```markup
kubectl get pods -n kerno
```

Ensure that all pods have a `Running` or `Completed` status. If any pods are in a `CrashLoopBackOff` or `Error` state, check their logs for more details.

{% hint style="info" %}
After the installation is completed, the installer will output a unique Kerno key (`K4_KEY`). This key identifies your local installation.

**Important**: For any subsequent operations (updates or uninstalls), you must provide the same `K4_KEY`. Not using or using an incorrect key can result in unexpected behavior.
{% endhint %}

### **Exploring the Data**

To inspect the data Kerno collects, replace `<pod-name>` with the name of a running `nanobe` pod:

```markup
kubectl logs <pod-name> -n kerno
```

### Updating Kerno

To update Kerno with the latest release, rerun the installer command but include your `K4_KEY`:

```markup
kubectl config use-context <kubernetes-context>
```

```markup
docker run -it --pull always --network host \
  -e ENVIRONMENT=local \
  -e K4_KEY=<K4_KEY> \
  -v ~/.kube/config:/root/.kube/config \
  public.ecr.aws/fyck.io/installer:main
```

### Uninstalling Kerno

If you need to remove Kerno and its components entirely from your cluster, set the `UNINSTALL` environment variable to `true`, along with your `K4_KEY`:

```markup
kubectl config use-context <kubernetes-context>
```

```markup
docker run -it --pull always --network host \
  -e ENVIRONMENT=local \
  -e K4_KEY=<K4_KEY> \
  -e UNINSTALL=true \
  -v ~/.kube/config:/root/.kube/config \
  public.ecr.aws/fyck.io/installer:main
```

{% hint style="warning" %}
Always confirm you are using the correct Kubernetes context before performing installation, updates, or uninstallation.
{% endhint %}

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
