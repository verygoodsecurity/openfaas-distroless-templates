# Openfaas Distroless Templates
This repository contains distroless alternatives for OpenFaaS [classic templates](https://github.com/openfaas/templates).
Currently the following languages are supported
* Python3
* Go
* Rust
* Node

To create your own function:
```shell
# Pull templates
$ faas-cli template pull https://github.com/verygoodsecurity/openfaas-distroless-templates

# List available languages
$ faas-cli new --list
Languages available as templates:
- go-distroless
- node-distroless
- python3-distroless
- rust-distroless

# Create a new function
$ faas-cli new my-function --lang [go/node/python3/rust]-distroless
```