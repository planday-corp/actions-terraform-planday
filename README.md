# Actions Terraform Planday
This repository contains a Github action reusable workflow to lint, format, init, validate, plan and apply a Terraform codebase.


## Inputs

| Name | Type | Required | Description |
| :---: | :---: | :---: |  --- |
| `terraform_version` | `string` | `false` | Version of Terraform that will be used. If left empty, the version set in the `required_version` setting will be used. Semver ranges are allowed. Example: `1.2.4`, `latest`, `~1.1.0` |
| `terraform_workspace` | `string` | `false` | Terraform workspace to select, if any |
| `terraform_init_extra_args` | `string` | `false` | Extra arguments to pass to Terraform `init` command |
| `terraform_fmt_extra_args` | `string` | `false` | Extra arguments to pass to Terraform `fmt` command |
| `terraform_validate_extra_args` | `string` | `false` | Extra arguments to pass to Terraform `validate` command |
| `terraform_plan_extra_args` | `string` | `false` | Extra arguments to pass to Terraform `plan` command |
| `terraform_apply_extra_args` | `string` | `false` | Extra arguments to pass to Terraform `apply` command |
| `tflint_version` | `string` | `false` | Version of TFLint that will be used. Default is `v0.41.0` |

## Secrets
| Name | Required | Description |
| :---: | :---: |  --- |
| `azure_client_id` | `true` | The Client ID which should be used |
| `azure_tenant_id` | `true` | The Tenant ID which should be used |
| `azure_subscription_id` | `true` | The Subscription ID which should be used |


## Usage

```yaml
jobs:
  terraform:
    uses: planday-corp/actions-terraform-planday/.github/workflows/terraform.yaml@v1
    with:
      terraform_version: "1.2.0"
      terraform_workspace: "prod-westeurope"
      terraform_plan_extra_args: "-parallelism=50"
      terraform_apply_extra_args: "-parallelism=50"
      tflint_version: "v0.40.0"
    secrets:
      azure_client_id: "${{ secrets.AZURE_CLIENT_ID }}"
      azure_tenant_id: "${{ secrets.AZURE_TENANT_ID }}"
      azure_subscription_id: "${{ secrets.AZURE_SUBSCRIPTION_ID }}"
```