# setup-arkade

Install arkade in a GitHub Action

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
