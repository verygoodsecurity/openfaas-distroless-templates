# Openfaas Distroless Templates
This repository contains distroless alternatives for OpenFaaS [classic templates](https://github.com/openfaas/templates).
Currently the following languages are supported
* Python3
* Go
* Rust
* Node

Each supported language comes with the standard image and the debug image option. The debug image provides a busybox shell that facilitates debugging in development, and should not be used in production. 

To create your own function:
```shell
# Pull templates
$ faas-cli template pull https://github.com/verygoodsecurity/openfaas-distroless-templates

# List available languages
$ faas-cli new --list
Languages available as templates:
- go-distroless
- go-distroless-debug
- node-distroless
- node-distroless-debug
- python3-distroless
- python3-distroless-debug
- rust-distroless
- rust-distroless-debug

# Create a new function
$ faas-cli new my-function --lang [go/node/python3/rust]-distroless
```
