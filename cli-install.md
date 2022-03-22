---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-19"

keywords: command-line interface for code engine, cli, cli for code engine, install cli for code engine, configuring code engine cli, kubernetes and code engine cli, knative and code engine cli, kubectl and code engine cli

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Setting up the CLI 
{: #install-cli}

Install, update, and delete the required CLIs and set up your environment to use {{site.data.keyword.codeenginefull}}. 
{: shortdesc}

## Installing the {{site.data.keyword.cloud_notm}} CLI 
{: #cli-setup}

Install the latest version of the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

Before you begin

You must create an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

    This installation includes the following files: 
    
    * IBM Cloud Functions plug-in
    * IBM Cloud Object Storage plug-in
    * IBM Cloud Container Registry plug-in
    * IBM Cloud Kubernetes Service plug-in

    For more information, see [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

2. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```txt
    ibmcloud login
    ```
    {: pre}

3. If you have more than one account, you are prompted to select which account to use. Follow the prompts or use the **`target`** command to select your {{site.data.keyword.cloud_notm}} account.

    ```txt
    ibmcloud target -c <account_id>
    ```
    {: pre}

4. You must also specify a region. You can use the **`target`** command to target or change regions.

    ```txt
    ibmcloud target -r <region>
    ```
    {: pre}

5. You must specify a resource group. To get a list of your resource groups, run the following command.

    ```txt
    ibmcloud resource groups
    ```
    {: pre}

    **Example output**

    ```txt
    Retrieving all resource groups under account <account_name> as email@ibm.com...
    OK
    Name      ID                                 Default Group   State   
    default   a8a12accd63b437bbd6d58fb8b462ca7   true            ACTIVE
    test      a8a12abbbd63b437cca6d58fb8b462ca7  false           ACTIVE
    ```
    {: screen}

6. Target a resource group by running the following command.

    ```txt
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    **Example output**

    ```txt 
    Targeted resource group default
    ```
    {: screen}

## Installing the {{site.data.keyword.codeengineshort}} CLI plug-in
{: #install-cli-plugin}

Install the latest version of the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

Be sure that you installed the latest version of the {{site.data.keyword.cloud_notm}} CLI. Otherwise, your {{site.data.keyword.codeengineshort}} CLI installation might fail with a message similar to `Could not find compatible binary to install for plug-in code-engine`.
{: tip}



1. Install the {{site.data.keyword.codeengineshort}} plug-in.

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}

2. Use the **`ibmcloud plugin show code-engine`** command to verify that the plug-in is installed.

    ```txt
    ibmcloud plugin show code-engine
    ```
    {: pre}

    **Example output**

    ```txt
    Plugin Name                              code-engine/ce
    Plugin Version                           0.5.16
    Plugin SDK Version                       0.5.0
    Minimal IBM Cloud CLI version required   1.0.0
    Private endpoints supported              false

    Commands:
    code-engine,ce                    Manage Code Engine components.
    [...]
    ```
    {: screen}

3. To run {{site.data.keyword.codeengineshort}}} commands, use **`ibmcloud code-engine`** or **`ibmcloud ce`**. To see everything that you can do with the {{site.data.keyword.codeengineshort}} plug-in, run **`ibmcloud ce`** with no arguments.

    ```txt
    ibmcloud ce
    ```
    {: pre}

Optionally, you can install the [`jq` package](https://stedolan.github.io/jq){: external}. Many {{site.data.keyword.codeengineshort}} commands include an option (`--output JSON`) to create JSON output. With this package, you can view and parse JSON responses from the command line.
{: tip}

For more information about {{site.data.keyword.codeengineshort}} commands, see the [**`ibmcloud ce`** commands](/docs/codeengine?topic=codeengine-cli).

## Updating the {{site.data.keyword.codeengineshort}} CLI
{: #update-cli}

Update the CLI periodically to take advantage of new features.

1. View your current plug-in list by running the **`ibmcloud plugin list`** command.

    ```txt
    ibmcloud plugin list
    ```
    {: pre}

    **Example output**

    ```txt
    Listing installed plug-ins...

    Plugin Name                            Version    Status             Private endpoints supported
    code-engine/ce                         0.5.16                        false
    container-registry                     0.1.497                       false
    container-service/kubernetes-service   1.0.118    Update Available   false
    ```
    {: screen}

2. If an update is available, run the **`ibmcloud plugin update`** command.

    ```txt
    ibmcloud plugin update code-engine
    ```
    {: pre}


## Uninstalling the CLI
{: #uninstall-cli}

If you no longer need the CLI, you can uninstall it.

1. List the plug-ins that are installed.

    ```txt
    ibmcloud plugin list
    ```
    {: pre}

2. Uninstall the plug-ins. For example, to uninstall the {{site.data.keyword.codeengineshort}} CLI plug-in:

    ```txt
    ibmcloud plugin uninstall code-engine
    ```
    {: pre}

3. Verify the plug-ins were uninstalled by running the following command and checking the list of the plug-ins that are installed.

    ```txt
    ibmcloud plugin list
    ```
    {: pre}

The plug-ins that you deleted are not displayed in the results.


