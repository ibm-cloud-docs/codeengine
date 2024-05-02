copyright:
  years: 2024
lastupdated: "2024-05-02"

keywords: troubleshooting for code engine terraform, terraform, tips for terraform, terraform environment variables

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does Terraform show environment variables discrepancies during app or job creation?
{: #ts-terraform-environment-variables}
{: troubleshoot}

When you create an app or job with Terraform, and then rerun the `terraform apply` or `terraform plan` commands without changing your `.tf` file, you see changes related to environment variables.
{: tsSymptoms}

When a {{site.data.keyword.codeengineshort}} app or job is created, the service creates some default environment variables:

* For apps: `CE_SUBDOMAIN`, `CE_APP`, `CE_REGION`, `CE_DOMAIN`, `CE_API_BASE_URL`, and `CE_PROJECT_ID`
* For jobs: `CE_REGION`, `CE_API_BASE_URL`, and `CE_PROJECT_ID`

For more information about additional environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

When you rerun the `terraform apply` or `terraform plan`, Terraform sees these default environment variables in your existing app or job as discrepancies because they are not listed in your `.tf` file.
{: tsCauses}

Edit your `.tf` file to include the default `run_env_variables` entries for {{site.data.keyword.codeengineshort}} resources. For example, if you are working with an app, you can edit as follows:
{: tsResolve}

```txt
  data "ibm_code_engine_project" "my-project" {
    project_id = var.ibmcloud_code_engine_project_id
  }

  resource "ibm_code_engine_app" "my-app-instance" {
    project_id      = data.ibm_code_engine_project.my-project.project_id
    name            = "my-app"
    image_reference = "icr.io/codeengine/helloworld"
  }

  run_env_variables {
    name  = "CE_SUBDOMAIN"
    type  = "literal"
    value = "-"
  }
  run_env_variables {
    name  = "CE_APP"
    type  = "literal"
    value = "${var.basename}-app"
  }
  run_env_variables {
    name  = "CE_REGION"
    type  = "literal"
    value = var.ibmcloud_region
  }
  run_env_variables {
    name  = "CE_DOMAIN"
    type  = "literal"
    value = "${var.ibmcloud_region}.codeengine.appdomain.cloud"
  }
  run_env_variables {
    name  = "CE_API_BASE_URL"
    type  = "literal"
    value = "https://api.${var.ibmcloud_region}.codeengine.cloud.ibm.com"
  }
  run_env_variables {
    name  = "CE_PROJECT_ID"
    type  = "literal"
    value = ibm_code_engine_project.project.project_id
  }
```
{: screen}
