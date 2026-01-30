---

copyright:
  years: 2023, 2026
lastupdated: "2026-01-27"


subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Terraform for {{site.data.keyword.codeengineshort}}
{: #terraform-setup-ce}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multitiered cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.codeengineshort}} workloads by using HashiCorp Configuration Language (HCL).
{: shortdesc}


Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}
  

## Installing Terraform and configuring resources for {{site.data.keyword.codeengineshort}}
{: #install-terraform}

Before you can create workloads with Terraform, make sure that you have completed the following prerequisites.

- Make sure that you have the [required access](/docs/codeengine?topic=codeengine-iam) to create and work with {{site.data.keyword.codeengineshort}} resources.
- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

1. Create a {{site.data.keyword.codeengineshort}} project by using the `code_engine_project` resource argument in your `main.tf` file.

   ```terraform
   data "ibm_resource_group" "resource_group" {
      name = "<your_resource_group_name>"
   }

   resource "ibm_code_engine_project" "code_engine_project_instance" {
      name = "<your_project_name>"
      resource_group_id = data.ibm_resource_group.resource_group.id
   }
   ```
   {: codeblock}


2. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

3. Provision the project from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}


      ```terraform
      data.ibm_resource_group.resource_group: Reading...
      data.ibm_resource_group.resource_group: Read complete after 1s [id=<your_resource_group_id>]
      
      Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
         + create

      Terraform will perform the following actions:

         # ibm_code_engine_project.code_engine_project_instance will be created
         + resource "ibm_code_engine_project" "code_engine_project_instance" {
            + account_id        = (known after apply)
            + created_at        = (known after apply)
            + crn               = (known after apply)
            + href              = (known after apply)
            + id                = (known after apply)
            + name              = "<your_project_name>"
            + project_id        = (known after apply)
            + region            = (known after apply)
            + resource_group_id = "<your_resource_group_id>"
            + resource_type     = (known after apply)
            + status            = (known after apply)
         }

      Plan: 1 to add, 0 to change, 0 to destroy.
      ```
      {: screen}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

      ```terraform
      data.ibm_resource_group.resource_group: Reading...
      data.ibm_resource_group.resource_group: Read complete after 1s [id=<your_resource_group_id>]
      
      Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
         + create

      Terraform will perform the following actions:

         # ibm_code_engine_project.code_engine_project_instance will be created
         + resource "ibm_code_engine_project" "code_engine_project_instance" {
            + account_id        = (known after apply)
            + created_at        = (known after apply)
            + crn               = (known after apply)
            + href              = (known after apply)
            + id                = (known after apply)
            + name              = "my-project"
            + project_id        = (known after apply)
            + region            = (known after apply)
            + resource_group_id = "5218b5c8c749454b9fc8be28f32e458e"
            + resource_type     = (known after apply)
            + status            = (known after apply)
         }

      Plan: 1 to add, 0 to change, 0 to destroy.

      Changes to Outputs:
         + ibm_code_engine_project = {
            + account_id        = (known after apply)
            + created_at        = (known after apply)
            + crn               = (known after apply)
            + href              = (known after apply)
            + id                = (known after apply)
            + name              = "my-project"
            + project_id        = (known after apply)
            + region            = (known after apply)
            + resource_group_id = "5218b5c8c749454b9fc8be28f32e458e"
            + resource_type     = (known after apply)
            + status            = (known after apply)
            + timeouts          = null
         }

      Do you want to perform these actions?
         Terraform will perform the actions described above.
         Only 'yes' will be accepted to approve.

         Enter a value: yes

      ibm_code_engine_project.code_engine_project_instance: Creating...
      ibm_code_engine_project.code_engine_project_instance: Still creating... [10s elapsed]
      ibm_code_engine_project.code_engine_project_instance: Still creating... [20s elapsed]
      ibm_code_engine_project.code_engine_project_instance: Still creating... [30s elapsed]
      ibm_code_engine_project.code_engine_project_instance: Creation complete after 30s [id=13468527-84sa-619g-gr99-168fe364w98f]

      Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

      Outputs:

      ibm_code_engine_project = {
         "account_id" = "<your_account_id>"
         "created_at" = "2023-03-16T10:44:24.150838188Z"
         "crn" = "crn:v1:bluemix:public:codeengine:eu-de:a/dc5e6392e5d14021846031b83e95f190:13468527-84sa-619g-gr99-168fe364w98f::"
         "href" = "https://api.eu-de.codeengine.cloud.ibm.com/v2/projects/13468527-84sa-619g-gr99-168fe364w98f"
         "id" = "13468527-84sa-619g-gr99-168fe364w98f"
         "name" = "my-project"
         "project_id" = "<your_project_id>"
         "region" = "eu-de"
         "resource_group_id" = "<your_resource_group_id>"
         "resource_type" = "project_v2"
         "status" = "active"
         "timeouts" = null /* object */
      }
      ```
      {: screen}

      

6. You can see your project in the list of projects in the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}. Alternatively you can see your project in the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, by expanding the category `Containers` and looking for your project name.

## What's next?
{: #terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.codeengineshort}} project with Terraform on {{site.data.keyword.cloud_notm}}, you can create additional resources.

### Resources 
{: #terraform-supported-resources}

* [`ibm_code_engine_allowed_outbound_destination`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_allowed_outbound_destination){: external}
* [`ibm_code_engine_app`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_app){: external}
* [`ibm_code_engine_binding`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_binding){: external}
* [`ibm_code_engine_build`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_build){: external}
* [`ibm_code_engine_config_map`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_config_map){: external}
* [`ibm_code_engine_domain_mapping`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_domain_mapping){: external}
* [`ibm_code_engine_function`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_function){: external}
* [`ibm_code_engine_job`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_job){: external}
* [`ibm_code_engine_project`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_project){: external}
* [`ibm_code_engine_secret`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/code_engine_secret){: external}

### Data Sources
{: #terraform-supported-data-sources}

* [`ibm_code_engine_allowed_outbound_destination`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_allowed_outbound_destination){: external}
* [`ibm_code_engine_app`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_app){: external}
* [`ibm_code_engine_binding`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_binding){: external}
* [`ibm_code_engine_build`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_build){: external}
* [`ibm_code_engine_config_map`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_config_map){: external}
* [`ibm_code_engine_domain_mapping`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_domain_mapping){: external}
* [`ibm_code_engine_function`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_function){: external}
* [`ibm_code_engine_job`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_job){: external}
* [`ibm_code_engine_project`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_project){: external}
* [`ibm_code_engine_secret`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/code_engine_secret){: external}

For more information about {{site.data.keyword.cloud_notm}} and Terraform, see [IBM Cloud Provider](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}.
