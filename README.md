# Introduction

`kube-bench` is a helpful tool to check whether Kubernetes is deployed
securely. Details are available on the [kube-bench][] website.

This repository contains configuration that allows `kube-bench` to accurately
report benchmark results against snap-based components.

## Usage

`kube-bench` is designed to run against master and worker nodes. There are
two methods for using the configuration from this repository with `kube-bench`:

### Charm action

The [layer-cis-benchmark][] base layer is included in in `kubernetes-master`,
`kubernetes-worker`, and `etcd` charms. This layer provides a `cis-benchmark`
action to facilitate the installation and execution of `kube-bench`.

By default, the action will use the contents of this repository as the source
of the `kube-bench` configuration. Simply run the `cis-benchmark` action on
desired charms as described in the [layer README][layer-cis-benchmark-readme].

### Manual

Follow the `kube-bench` installation procedure from the [kube-bench][] website.
Once installed, clone this repository:

```bash
git clone https://github.com/charmed-kubernetes/kube-bench-config.git
```

Specify the configuration directory, version, and component for each node you
wish to test:

#### kubernetes-master

```bash
kube-bench -D /path/to/kube-bench-config --version 1.13-snap-k8s master
```

#### kubernetes-worker

```bash
kube-bench -D /path/to/kube-bench-config --version 1.13-snap-k8s node
```

#### etcd

```bash
kube-bench -D /path/to/kube-bench-config --version 1.13-snap-etcd master
```

<!-- LINKS -->

[kube-bench]: https://github.com/aquasecurity/kube-bench
[layer-cis-benchmark]: https://github.com/charmed-kubernetes/layer-cis-benchmark
[layer-cis-benchmark-readme]: https://github.com/charmed-kubernetes/layer-cis-benchmark/blob/master/README.md
