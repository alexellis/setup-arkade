# setup-arkade

## Your favourite developer CLIs for GitHub Actions

This is a GitHub action to make it a bit quicker to use [arkade](https://arkade.dev) from GitHub Actions.

What's arkade?

arkade is a cross-platform tool for downloading the latest (or pinned) versions of your favourite CLIs, for installing Helm charts and Kubernetes apps, and system-level packages like Go, containerd and Firecracker.

That means you don't need a lot of curl statements in your builds, and when you support Arm, you don't need if statements for the architecture. When you support multiple operating systems, you don't need if statements for Linux/Darwin, etc.

How is it different to apt-get, brew and spending hours trawling README files?

[Learn more](https://arkade.dev)

## You may also like "alexellis/arkade-get"

Whilst `alexellis/setup-arkade` installs the arkade binary, `alexellis/arkade-get` is all about making the `arkade get` command seamless.

```yaml
    - uses: alexellis/arkade-get@master
      with:
        kubectl: v1.25.0
        faas-cli: 0.14.10
        helm: latest
        terraform: latest
        inletsctl: latest
        docker-compose: latest
        flyctl: latest
    - name: check for faas-cli
      run: |
        faas-cli version
```

Binaries are placed in `$HOME/.arkade/bin/` and this path is added to the runner's PATH, so there's no need to prefix any binaries that you then go on to use.

See also: ["alexellis/arkade-get"](https://github.com/alexellis/arkade-get)

## Install arkade

Install arkade in a GitHub Action

```yaml
- name: Install arkade
  uses: alexellis/setup-arkade@v2
```

Use the latest version in master:

```yaml
  - name: Setup arkade
    uses: alexellis/setup-arkade@master
```

## Use arkade to download a CLI

Install arkade in a GitHub Action and get the latest version of kubectl

```yaml
  - name: Setup arkade
    uses: alexellis/setup-arkade@v2
  - name: Get kubectl
    run: |
        arkade get kubectl
  - name: Run kubectl
    run: |
      kubectl version
```

Install a specific version of a tool

```yaml
  - name: Setup arkade
    uses: alexellis/setup-arkade@v2
  - name: Get faas-cli 0.14.10
    run: |
      arkade get faas-cli@0.14.10
  - name: Run kubectl
    run: |
      faas-cli version
```


Install multiple tools

```yaml
  - name: Setup arkade
    uses: alexellis/setup-arkade@v2
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
    uses: alexellis/setup-arkade@v2
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
    uses: alexellis/setup-arkade@v2
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
    uses: alexellis/setup-arkade@v2
  - name: Get containerd
    run: |
      arkade system install containerd
      /usr/local/bin/containerd version
  - name: Run go
    run: |
       arkade system install go
       /usr/local/bin/go version
```

