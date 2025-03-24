# openapi-codegen-example
Demonstrate how to use openapi-codegen to generate separate model vs server packages.

Requires Go 1.24+

# Commands
```sh
go get -tool github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest
```
```sh
go run github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest --config=openapi_gen_model.yaml  openapi_spec_components.yaml
go run github.com/oapi-codegen/oapi-codegen/v2/cmd/oapi-codegen@latest --config=openapi_gen_server.yaml openapi_spec_paths.yaml
```

# Problem

Below are excerpts from the generated  `openapi_gen_server.go` file. There is a mix of  `externalRef0` and  `ExternalRef0` qualifiers; only the lowercase one works.

## Import

https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/internal/openapi/server/openapi_gen_server.go#L16

## Correct

https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/internal/openapi/server/openapi_gen_server.go#L129
https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/internal/openapi/server/openapi_gen_server.go#L218

## Incorrect

https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/internal/openapi/server/openapi_gen_server.go#L138
https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/internal/openapi/server/openapi_gen_server.go#L227

## Thoughts

oapi-codegen seems to handle external references differently for the API responses in openapi_spec_paths.yaml.

HTTP 200 responses for both APIs are OK. HTTP error responses for both APIs don't compile.

https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/openapi_spec_paths.yaml#L19-L41
https://github.com/justincranford/openapi-codegen-example/blob/16c6aba2896d2cb83b976efdb2844e7ad25669d0/openapi_spec_paths.yaml#L48-L72
