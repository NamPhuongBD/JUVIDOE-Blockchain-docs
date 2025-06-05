# Installation

Please refer to the installation method more applicable to you.

Our recommendation is to use the pre-built releases and verify the provided checksums.

***

## Building from source

Prior to using `go install` make sure that you have Go `>=1.17` installed and properly configured.

The stable branch is `develop`.

```
git clone https://github.com/0xEVMBuilder/JUVIDOE-edge.git
cd JUVIDOE-edge/
go build main.go -o JUVIDOE-edge
sudo mv JUVIDOE-edge /usr/local/bin
```

***

## Using `go install`

Prior to using `go install` make sure that you have Go `>=1.17` installed and properly configured.

`go install github.com/0xEVMBuilder/JUVIDOE-edge@develop`

The binary will be available in your `GOBIN` environment variable, and will include the latest changes from the mainline `develop` branch.
