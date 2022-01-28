<staging-internal>---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-28"

keywords: code engine, getting started, cli, get help, internal adopters

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.codeenginefull_notm}} for Internal adopters
{: #getting-started-internal}

Review internal only information to get access to {{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}") 
{: shortdesc}

## Where can I find the {{site.data.keyword.codeengineshort}} console?
{: #ce-console}

Access to {{site.data.keyword.codeengineshort}} console is available at [{{site.data.keyword.codeengineshort}} test](https://test.cloud.ibm.com/codeengine/overview){: external}. Log in with your IBM ID. 

## How do I get the CLI?
{: #ce-cli}

You must create an [{{site.data.keyword.cloud_notm}} account on TEST](https://test.cloud.ibm.com/){: external}. If you do not have one, you can create one by accessing the URL. If you cannot create one, ask on the #bss-account-issues channel in the IBM Cloud Platform slack.

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started) 

2. Install the {{site.data.keyword.codeengineshort}} CLI plug-in

    ```sh
    ibmcloud plugin repo-add staging https://plugins.test.cloud.ibm.com
    ibmcloud plugin install code-engine -r staging
    ```
    {: pre}

3. Log into Test IBM Cloud

    ```sh
    ibmcloud login -a https://test.cloud.ibm.com --sso
    ```
    {: pre}

4. If you have more than one account, select one from the list. 

5. Select `us-south` as the target region.

6. List your resource groups and select one to target.

    ```sh
    ibmcloud resource groups
    ```
    {: pre}

7. Target a resource group.

    ```sh
    ibmcloud target -g <GROUP_NAME>
    ```
    {: pre}        

You can now proceed to [Managing projects](/docs/codeengine?topic=codeengine-manage-project)!

## Where can I get help?
{: #ce-help}

You can get help from Code Engine #code-engine-users slack channel.

</staging-internal>


