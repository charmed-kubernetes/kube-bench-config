# Introduction

kube-bench is a helpful tool to check whether Kubernetes is deployed
securely. Learn more at:

https://github.com/aquasecurity/kube-bench

## Installation

kube-bench is designed to run against master and worker nodes. Installation is
the same across all node types. Perform the following steps on
`kubernetes-master`, `kubernetes-worker`, and `etcd` units as needed:

If go is not installed, install and setup `$GOPATH` with the following:

```bash
sudo snap install go --classic
mkdir ~/go
export GOPATH=~/go
```

Install kube-bench from source:

```bash
go get github.com/aquasecurity/kube-bench
go get github.com/golang/dep/cmd/dep
cd $GOPATH/src/github.com/aquasecurity/kube-bench
$GOPATH/bin/dep ensure -vendor-only
go build -o kube-bench .
```

Fetch the configuration files specific to Charmed Kubernetes into a `cfg-ck`
subdirectory:

```bash
cd $GOPATH/src/github.com/aquasecurity/kube-bench
git clone https://github.com/charmed-kubernetes/kube-bench-config.git cfg-ck
```

## Running kube-bench

Specify the configuration directory and component for each node type you wish
to test.

### kubernetes-master

```bash
cd $GOPATH/src/github.com/aquasecurity/kube-bench
./kube-bench master -D cfg-ck
```

### kubernetes-worker

```bash
cd $GOPATH/src/github.com/aquasecurity/kube-bench
./kube-bench node -D cfg-ck
```

### etcd

kube-bench considers `etcd` to be a master component. Charmed Kubernetes uses
standalone etcd units, so kube-bench must be setup with `etcd` tests in a
specific location. You will also need to specify a version string, as there
are no `kubelet` or `kubectl` binaries for kube-bench to derive a version
string.

```bash
cd $GOPATH/src/github.com/aquasecurity/kube-bench
cp cfg-ck/1.13/etcd.yaml cfg-ck/1.13/master.yaml
./kube-bench master -D cfg-ck --config cfg-ck/config-etcd.yaml --version 1.13
```
