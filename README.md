# openapi-codegen-example
Demonstrate how to use openapi-codegen to generate separate model vs server packages.

Requires Go 1.24+

# Commands
```sh
go get -tool github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest
```
```sh
go mod tidy
```
```sh
go run github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest --config=openapi_gen_model.yaml  openapi_spec_components.yaml
```
```sh
go run github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest --config=openapi_gen_server.yaml openapi_spec_paths.yaml
```

# Problem

The contents of openapi_gen_server.go don't compile due to Fiber strict-server responses containing a mix of `externalRef0` vs `ExternalRef0`.