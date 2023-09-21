---

copyright:
  years: 2023
lastupdated: "2023-09-21"

keywords: api reference, api, Kubernetes configuration and code engine, CRD for code engine, CRD, custom resource definition, guid, kubernetes, authenticate, code engine api

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with the {{site.data.keyword.codeengineshort}} CLI 
{: #cecli-getstart}

You can use the {{site.data.keyword.codeenginefull}} API to create and manage your {{site.data.keyword.codeengineshort}} entities. 
{: shortdesc}


- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).


## Setting up your CLI environment 
{: #cecli-getstart-setup}

To work with the CLI to create and manage {{site.data.keyword.codeengineshort}} entities, set up your CLI environment. Make sure you have the latest version of the {{site.data.keyword.cloud_notm}} CLI installed.

Before you begin

You must create an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.


1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

2. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    1. Log in to the {{site.data.keyword.cloud_notm}} CLI.

        ```txt
        ibmcloud login
        ```
        {: pre}
        
    2. If you have more than one account, you are prompted to select which account to use. Follow the prompts or use the **`target`** command to select your {{site.data.keyword.cloud_notm}} account.

        ```txt
        ibmcloud target -c <account_id>
        ```
        {: pre}

    3. Specify a region. Use the **`target`** command to target or change regions.

        ```txt
        ibmcloud target -r <region>
        ```
        {: pre}

    4. Specify a resource group. To get a list of your resource groups, run the following command.

        ```txt
        ibmcloud resource groups
        ```
        {: pre}

        Example output

        ```txt
        Retrieving all resource groups under account <account_name> as email@ibm.com...
        OK
        Name      ID                                 Default Group   State   
        default   a8a12accd63b437bbd6d58fb8b462ca7   true            ACTIVE
        test      a8a12abbbd63b437cca6d58fb8b462ca7  false           ACTIVE
        ```
        {: screen}

    5. Target a resource group by running the following command.

        ```txt
        ibmcloud target -g <resource_group>
        ```
        {: pre}

        Example output

        ```txt 
        Targeted resource group default
        ```
        {: screen}


3. Install the {{site.data.keyword.codeengineshort}} CLI plug-in. 

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}


4. Verify that the {{site.data.keyword.codeengineshort}} CLI plug-in is installed. You can use the **`ibmcloud plugin show code-engine`** command or the  **`ibmcloud plugin list`** command to confirm that the plug-in is installed.

    ```txt
    ibmcloud plugin show code-engine
    ```
    {: pre}

    Example output

    ```txt
    Plugin Name                              code-engine[ce]
    Plugin Version                           1.31.0
    Plugin SDK Version                       0.9.0
    Minimal IBM Cloud CLI version required   1.0.0
    Private endpoints supported              true

    Commands:
    code-engine,ce                    Manage Code Engine components.
    [...]
    ```
    {: screen}


5. Run the **`ibmcloud ce help`** command to view the commands for the {{site.data.keyword.codeengineshort}} CLI. For example, 

    ```txt
    ibmcloud ce help
    ```
    {: pre}


## Working with the {{site.data.keyword.codeengineshort}} CLI 
{: #cecli-getstart-workcecli}

Now that your {{site.data.keyword.codeengineshort}} CLI environment is set up, you are ready to work with {{site.data.keyword.codeengineshort}} resources, such as applications, functions, or jobs with the CLI. 

Before you can work with {{site.data.keyword.codeengineshort}} resources, you must work within the context of a project. 

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. 

A project provides the following items. 

- Provides a unique namespace for entity names.
- Manages access to project resources (inbound access).
- Manages access to backing services, registries, and repositories (outbound access).
- Has an automatically generated certificate for Transport Layer Service (TLS).

For more information about {{site.data.keyword.codeengineshort}} projects, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project). 


1. Create a project with the [**`project create`**](/docs/codeengine?topic=codeengine-cli#cli-project-create) command. Use a project name that is unique to your region. 

    ```txt
    ibmcloud ce project create --name PROJECT_NAME 
    ```
    {: pre}

    Example output

    ```txt
    Creating project 'myproject'...
    OK
    ```
    {: screen}

2. View details about the project with the [**`project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command. 

    ```txt
    ibmcloud ce project get --name PROJECT_NAME
    ```
    {: pre}

    Example output

    ```txt
    Getting project 'myproject'...
    OK
    Name:                       myproject
    ID:                         01234567-abcd-abcd-abcd-abcdabcd1111
    Status:                     active
    Selected:                   true
    Region:                     us-south
    Resource Group:             default
    Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
    Age:                        52d
    Created:                    Fri, 15 Jan 2021 13:32:30 -0500
    Updated:                    Fri, 15 Jan 2021 13:32:45 -0500

    Quotas:
    Category                                  Used      Limit
    App revisions                             1         100
    Apps                                      1         100
    Build runs                                0         100
    Builds                                    0         100
    Configmaps                                2         100
    CPU                                       1.025     64
    Ephemeral storage                         902625Ki  256G
    Instances (active)                        1         250
    Instances (total)                         2         2500
    Job runs                                  1         100
    Jobs                                      1         100
    Memory                                    4400M     256G
    Secrets                                   5         100
    Subscriptions (cron)                      0         100
    Subscriptions (IBM Cloud Object Storage)  0         100
    ```
    {: screen}


Alternatively, you can use the [**`project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command to display a list of your created projects. 

To work with a project with the CLI, the project must be selected as the current context. A project is automatically selected as the current context when it is created, unless you specify the `--no-select` option. To select a project that is not currently targeted, use the [**`project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command.
{: note}

For more information about working with projects, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).


## Next steps
{: #cecli-getstart-next}

Now that you have setup your CLI environment, and have taken the first steps to ensure that you are working within the context of a {{site.data.keyword.codeengineshort}}  project, you can use the {{site.data.keyword.codeengineshort}} CLI to work with apps, functions, and jobs. 


To start working with {{site.data.keyword.codeengineshort}} components with the CLI, see the following topics.

* [Working with apps](/docs/codeengine?topic=codeengine-application-workloads).
* [Working with functions](/docs/codeengine?topic=codeengine-fun-work) 
* [Working with jobs](/docs/codeengine?topic=codeengine-job-plan)


For more information about the {{site.data.keyword.codeengineshort}} CLI, see the [Setting up the CLI environment](/docs/codeengine?topic=codeengine-cli). **FMO think about renaming to "Working with the CLI"**

For more information about working in the {{site.data.keyword.codeengineshort}} CLI environment, see [{{site.data.keyword.codeengineshort}} CLI Command Reference documentation](/docs/codeengine?topic=codeengine-cli). 

For a summary of changes for each version of the CLI, see [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).  Be sure to keep your CLI up-to-date so that you can use all the available commands and their options. 




