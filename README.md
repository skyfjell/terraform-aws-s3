# Terraform AWS S3 Module

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0.5 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 4.0.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 4.0.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_iam_group_policy_attachment.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_group_policy_attachment) | resource |
| [aws_iam_policy.this_ro](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_policy.this_rw](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_role_policy_attachment.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_kms_alias.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/kms_alias) | resource |
| [aws_kms_key.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/kms_key) | resource |
| [aws_s3_bucket.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_s3_bucket_acl.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_acl) | resource |
| [aws_s3_bucket_cors_configuration.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_cors_configuration) | resource |
| [aws_s3_bucket_logging.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_logging) | resource |
| [aws_s3_bucket_policy.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy) | resource |
| [aws_s3_bucket_public_access_block.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_public_access_block) | resource |
| [aws_s3_bucket_server_side_encryption_configuration.this_aes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_server_side_encryption_configuration) | resource |
| [aws_s3_bucket_server_side_encryption_configuration.this_kms](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_server_side_encryption_configuration) | resource |
| [aws_s3_bucket_versioning.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_versioning) | resource |
| [aws_iam_policy_document.this_ro](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.this_rw](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_kms_key.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/kms_key) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_acl"></a> [acl](#input\_acl) | Bucket ACL | `string` | `"private"` | no |
| <a name="input_bucket_policy"></a> [bucket\_policy](#input\_bucket\_policy) | The policy document directly on the bucket. Use `data.aws_iam_policy_document.<name>.json` here. | `any` | `null` | no |
| <a name="input_cors_rule"></a> [cors\_rule](#input\_cors\_rule) | value | <pre>map(object({<br>    allowed_headers = optional(list(string))<br>    allowed_methods = optional(list(string))<br>    allowed_origins = optional(list(string))<br>    expose_headers  = optional(list(string))<br>  }))</pre> | `{}` | no |
| <a name="input_force_destroy"></a> [force\_destroy](#input\_force\_destroy) | Force destroy variable passed through to s3 resource | `bool` | `false` | no |
| <a name="input_groups"></a> [groups](#input\_groups) | Group names to attach | <pre>list(object({<br>    name = string<br>    mode = string<br>  }))</pre> | `[]` | no |
| <a name="input_labels"></a> [labels](#input\_labels) | Instance of labels module | <pre>object(<br>    {<br>      id   = string<br>      tags = any<br>    }<br>  )</pre> | <pre>{<br>  "id": "",<br>  "tags": {}<br>}</pre> | no |
| <a name="input_logging"></a> [logging](#input\_logging) | Pass null to disable logging or pass the logging bucket id | `string` | `null` | no |
| <a name="input_logging_prefix"></a> [logging\_prefix](#input\_logging\_prefix) | Will default to /{name} | `string` | `null` | no |
| <a name="input_name"></a> [name](#input\_name) | The name of the s3 bucket | `string` | n/a | yes |
| <a name="input_name_override"></a> [name\_override](#input\_name\_override) | Name override the opinionated name variable | `bool` | `false` | no |
| <a name="input_policy_conditions"></a> [policy\_conditions](#input\_policy\_conditions) | Conditions on RO and RW policy | <pre>object({<br>    RW = optional(map(object({<br>      test     = string<br>      variable = string<br>      values   = list(string)<br>    })))<br>    RO = optional(map(object({<br>      test     = string<br>      variable = string<br>      values   = list(string)<br>    })))<br>  })</pre> | `{}` | no |
| <a name="input_public_access_block"></a> [public\_access\_block](#input\_public\_access\_block) | n/a | <pre>object({<br>    block_public_policy     = optional(bool)<br>    block_public_acls       = optional(bool)<br>    restrict_public_buckets = optional(bool)<br>    ignore_public_acls      = optional(bool)<br>  })</pre> | `{}` | no |
| <a name="input_roles"></a> [roles](#input\_roles) | Roles to attach | <pre>list(object({<br>    name = string<br>    mode = string<br>  }))</pre> | `[]` | no |
| <a name="input_server_side_encryption_configuration"></a> [server\_side\_encryption\_configuration](#input\_server\_side\_encryption\_configuration) | Pass through to server\_side\_encryption\_configuration. If null is passed for kms\_master\_key\_id, will autocreate.<br>  An alias can also be passed to be created on the key. | <pre>object({<br>    type              = string<br>    kms_master_key_id = optional(string)<br>    alias             = optional(string)<br>  })</pre> | <pre>{<br>  "alias": null,<br>  "kms_master_key_id": null,<br>  "type": "aws:kms"<br>}</pre> | no |
| <a name="input_suppress_iam"></a> [suppress\_iam](#input\_suppress\_iam) | Supresses the module creating iam resources if none are needed | `bool` | `false` | no |
| <a name="input_use_prefix"></a> [use\_prefix](#input\_use\_prefix) | Use var.name as name prefix instead | `bool` | `true` | no |
| <a name="input_versioning"></a> [versioning](#input\_versioning) | Use bucket versioning | `bool` | `true` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_kms_arn"></a> [kms\_arn](#output\_kms\_arn) | Arn of the kms created |
| <a name="output_ro_arn"></a> [ro\_arn](#output\_ro\_arn) | Read Only S3 policy ARN. Deprecated use rw\_policy output |
| <a name="output_ro_policy"></a> [ro\_policy](#output\_ro\_policy) | Read Only S3 policy object |
| <a name="output_rw_arn"></a> [rw\_arn](#output\_rw\_arn) | Read/Write S3 policy ARN. Deprecated use rw\_policy output |
| <a name="output_rw_policy"></a> [rw\_policy](#output\_rw\_policy) | Read/Write S3 policy object |
| <a name="output_s3_arn"></a> [s3\_arn](#output\_s3\_arn) | ARN of created S3 bucket |
| <a name="output_s3_id"></a> [s3\_id](#output\_s3\_id) | ID of created S3 bucket |
<!-- END_TF_DOCS -->
