---
description: >-
  Before you get started with the installation, make sure you meet the
  requirements below
---

# System Requirements

{% hint style="info" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}

### **Kubernetes RBAC Permissions**

To install Kerno, you need permission to deploy the following Kubernetes objects.

* **Namespace**
* **Deployment**&#x20;
* **DaemonSet**
* **ConfigMap**
* **Secret**&#x20;
* **Service**
* **ServiceAccount**
* **ClusterRole**
* **ClusterRoleBinding**

### **AWS Permissions**

The following AWS permissions are required to deploy Kenro:

* **IAM Role**
* **Role Policy**
* **Bucket**
* **Bucket Policy**

### **Kubernetes**

Kubernetes `v1.23.0` or higher is required.

The following tables list Kubernetes environments that have been tested with Kerno.

#### **Environments**

| Kubernetes environment | Supported     |
| ---------------------- | ------------- |
| EKS                    | Supported     |
| EKS Fargate            | Not Supported |

### **Kernel Version**

Kerno supports Linux kernel version 5.3 or higher (released after 2020).

Run `uname -r` on your Linux system to check your kernel version.

#### **Supported Linux Distributions**

| Distribution            | Supported Versions |
| ----------------------- | ------------------ |
| Debian                  | 11+                |
| RedHat Enterprise Linux | 8.2+               |
| Ubuntu                  | 20.10+             |
| CentOS                  | 7.3+               |
| Fedora                  | 31+                |
| BottlerockOS            | 1.10+              |
| Amazon Linux            | All official AMIs  |
| Google COS              | All official AMIs  |
| Azure Linux             | All official AMIs  |
| Talos                   | 1.7.3+             |

**Note:** Kerno might work on other Linux kernels that are not listed here.

If your distribution isn't listed, please drop us a note on [Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA).

#### **Permissions**

* Loading the eBPF code requires running **privileged containers**.

**Note:** [eBPF is entirely safe to run](https://docs.ebpf.io/linux/concepts/verifier/). It uses a Verifier to ensure that BPF programs are safe to run, won’t break the kernel in any way, and won’t violate the system's security model.

#### **CO:RE support**

Kerno leverages eBPF’s [CO-RE (Compile Once - Run Everywhere)](https://nakryiko.com/posts/bpf-portability-and-co-re/) capability to ensure compatibility across various Linux kernels and distributions. This requires the kernel to be compiled with BTF (BPF Type Format) information, enabled by setting the `CONFIG_DEBUG_INFO_BTF=y` flag during kernel compilation. Most modern [Linux distributions](https://github.com/libbpf/libbpf#bpf-co-re-compile-once--run-everywhere) now include this by default.

To verify if your kernel supports CO-RE, look for the presence of the BTF file:

```
$ ls -la /sys/kernel/btf/vmlinux

- r--r--r--. 1 root root 3541561 Jun 2 18:16 /sys/kernel/btf/vmlinux
```

If the `vmlinux` file is listed, and your kernel has CO-RE support enabled.

#### **What if My Kernel Is Not Supported?**

* If your system does not meet these requirements, Kerno's eBPF agent cannot run in your environment.

### **Hardware and Resource Requirements**

* **CPU Architectures**: Kerno fully supports **x86** and **ARM** processors.
* **Resources**: Kerno's services have resource requests and limits optimized for low overhead. Actual usage depends on cluster activity; more active clusters may require more resources.

#### **Memory Requirements**

Kerno requires the following memory per node:

<table><thead><tr><th width="204">Minimum</th><th>Note</th></tr></thead><tbody><tr><td>256MB per node</td><td>We install two daemonsets, each using at least 128MB</td></tr><tr><td>768MB</td><td>One replica of a Deployment also uses 768MB</td></tr></tbody></table>
