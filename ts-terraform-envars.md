---

copyright:
  years: 2024
lastupdated: "2024-04-18"

keywords: troubleshooting for code engine terraform, terraform, tips for terraform, terraform environment variables

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does Terraform show environment variables discrepancies during app or job creation?
{: #ts-terraform-envirobment-variables}
{: troubleshoot}

When you create an app or job in Terraform and run the `terraform apply` command without making any changes, Terraform shows that the app or job contains six extra environment variables and that you need to replace them to resolve the discrepancy.
{: tsSymptoms}

These environment variables are default ones that {{site.data.keyword.codeengineshort}} creates, and they are not specified in your `.tf` file.
{: tsCauses}

Edit your `.tf` file to include the following six `run_env_variables` settings for {{site.data.keyword.codeengineshort}} resources:
{: tsResolve}

```txt
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
