---
layout: "aws"
page_title: "AWS: aws_api_gateway_domain_name"
sidebar_current: "docs-aws-resource-api-gateway-domain-name"
description: |-
  Registers a custom domain name for use with AWS API Gateway.
---

# aws\_api\_gateway\_domain\_name

Registers a custom domain name for use with AWS API Gateway.

This resource just establishes ownership of and the TLS settings for
a particular domain name. An API can be attached to a particular path
under the registered domain name using
[the `aws_api_gateway_base_path_mapping` resource](api_gateway_base_path_mapping.html).

## Example Usage

```
resource "aws_api_gateway_domain_name" "example" {
  domain_name = "example.com"

  certificate_name        = "example-api"
  certificate_body        = "${file("${path.module}/example.com/example.crt")}"
  certificate_chain       = "${file("${path.module}/example.com/ca.crt")}"
  certificate_private_key = "${file("${path.module}/example.com/example.key")}"
}
```

## Argument Reference

The following arguments are supported:

* `domain_name` - (Required) The fully-qualified domain name to register
* `certificate_name` - (Required) The unique name to use when registering this
  cert as an IAM server certificate
* `certificate_body` - (Required) The certificate issued for the domain name
  being registered, in PEM format
* `certificate_chain` - (Required) The certificate for the CA that issued the
  certificate, along with any intermediate CA certificates required to
  create an unbroken chain to a certificate trusted by the intended API clients.
* `certificate_private_key` - (Required) The private key associated with the
  domain certificate given in `certificate_body`.

## Attributes Reference

The following attributes are exported:

* `id` - The internal id assigned to this domain name by API Gateway
