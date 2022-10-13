# setup-arkade

This is a GitHub action to make it a bit quicker to use [arkade](https://arkade.dev) from GitHub Actions.

What's arkade?

arkade is a cross-platform tool for downloading the latest (or pinned) versions of your favourite CLIs, for installing Helm charts and Kubernetes apps, and system-level packages like Go, containerd and Firecracker.

[Learn more](https://arkade.dev)

## Install arkade

Install arkade in a GitHub Action

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
```

## Use arkade to download a CLI

Install arkade in a GitHub Action and get the latest version of kubectl

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get kubectl
    run: |
        arkade get kubectl
  - name: Run kubectl
    run: |
        $HOME/.arkade/bin/kubectl version
```

Install a specific version of a tool

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get faas-cli 0.14.10
    run: |
        arkade get faas-cli@0.14.10
  - name: Run kubectl
    run: |
        $HOME/.arkade/bin/faas-cli version
```


Install multiple tools

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get tools for CI
    run: |
        arkade get kubectl \
            faas-cli \
            inletsctl \
            helm
```

Or install to /usr/local/bin

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get kubectl
    run: |
        arkade get kubectl
        sudo mv .arkade/bin/kubectl /usr/local/bin
  - name: Run kubectl
    run: |
        kubectl version
```

## System apps

Did you know that arkade contains system-level apps for Linux servers and desktops?

```bash
$ arkade system install --help
Install system apps for Linux hosts

Usage:
  arkade system install [command]

Examples:
  arkade system install [APP]
  arkade system install --help

Available Commands:
  actions-runner  Install GitHub Actions Runner
  cni             Install CNI plugins
  containerd      Install containerd
  firecracker     Install Firecracker
  go              Install Go
  node            Install Node.js
  prometheus      Install Prometheus
  tc-redirect-tap Install tc-redirect-tap
```

Install firecracker:

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get kubectl
    run: |
        arkade system install firecracker
  - name: Run firecracker
    run: |
        firecracker --version
```

Install containerd and go (latest):

```yaml
  - name: Setup arkade
    uses: alexellis/arkade@master
  - name: Get containerd
    run: |
        arkade system install containerd
        /usr/local/bin/containerd version
  - name: Run go
    run: |
         arkade system install go
         /usr/local/bin/go version
```

