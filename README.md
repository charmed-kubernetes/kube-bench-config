# Introduction

`kube-bench` is a helpful tool to check whether Kubernetes is deployed
securely. Details are available on the [kube-bench][] website.

This repository contains configuration that allows `kube-bench` to accurately
report benchmark results against snap-based components.

## Usage

The [layer-cis-benchmark][] base layer is included in in `kubernetes-master`,
`kubernetes-worker`, and `etcd` charms. This layer provides a `cis-benchmark`
action to facilitate the installation and execution of `kube-bench`.

By default, the action will use the contents of this repository as the source
of the `kube-bench` configuration. Simply run the `cis-benchmark` action on
desired charms as described in the [layer README][layer-cis-benchmark-readme].

<!-- LINKS -->

[kube-bench]: https://github.com/aquasecurity/kube-bench
[layer-cis-benchmark]: https://github.com/charmed-kubernetes/layer-cis-benchmark
[layer-cis-benchmark-readme]: https://github.com/charmed-kubernetes/layer-cis-benchmark/blob/master/README.md
