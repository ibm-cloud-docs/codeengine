---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-30"

keywords: projects in code engine, project context in code engine, providing access with projects in code engine, access control in code engine, iam access for projects in code engine, projects, code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note .note}
{:note: .note}
{:note:.deprecated}
{:objectc data-hd-programlang="objectc"}
{:objectc: .ph data-hd-programlang='Objective C'}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:right: .ph data-hd-position='right'}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Managing projects 
{: #manage-project}

Learn how to create and work with projects.
{: shortdesc} 

## What is a project?
{: #project-def}

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. A project provides the following items:<ul><li>Provides a unique namespace for entity names.</li><li> Manages access to project resources (inbound access).</li><li> Manages access to backing services, registries, and repositories (outbound access).</li><li> Has an automatically generated certificate for Transport Layer Service (TLS).</li></ul>

For more information about managing access control to projects with IAM, see [Managing user access](/docs/codeengine?topic=codeengine-iam).

Projects incur no costs, but instead serve as folders for your apps and jobs.

### How can I see what projects I can access?
{: #project-access}

You can see a list of your projects in the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

You can also run the [**`project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command. 

```
ibmcloud ce project list
```
{: pre}

**Example output**

```
Getting projects...
OK

Name             ID                                    Status  Selected  Tags  Region    Resource Group  Age
myproj-eude      01234567-abcd-abcd-abcd-abcdabcd2222  active  false           eu-de     default         27d
myproject        01234567-abcd-abcd-abcd-abcdabcd1111  active  true            us-south  default         52d
```
{: screen}


### How can I see details about a project? 
{: #project-details}

From the {{site.data.keyword.codeengineshort}} console, you can see details of a project by clicking the name of a project from the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.

You can also run the [**`project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to display details of a project. Replace `PROJECT_NAME` with the name of your project. If your project is selected as the current context, the output of this command includes details about limits and quota usage of {{site.data.keyword.codeengineshort}} project resources. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

```
ibmcloud ce project get --name PROJECT_NAME
```
{: pre}

**Example output**

```
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
  Category                                  Used       Limit
  App revisions                             33         100
  Apps                                      10         100
  Build runs                                4          100
  Builds                                    4          100
  Configmaps                                7          100
  CPU                                       6.15       64
  Ephemeral storage                         5415750Ki  256G
  Instances (active)                        6          250
  Instances (total)                         9          2500
  Job runs                                  4          100
  Jobs                                      3          100
  Memory                                    26400M     256G
  Secrets                                   21         100
  Subscriptions (IBM Cloud Object Storage)  0          100
  Subscriptions (ping)                      1          100
```
{: screen}


### How can I set policies so others can work with my project? 
{: #project-policies}

See information about [managing user access](/docs/codeengine?topic=codeengine-iam) to learn about setting IAM policies so others can work with your {{site.data.keyword.codeengineshort}} project. 

### Are there project limits to consider? 
{: #project-limits}

The maximum number of projects that you can create per region is 20. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

## Create a project
{: #create-a-project}

You can create a project through the console or with the CLI.
{: shortdesc} 

### Creating a project from the console
{: #create-project-console}

1. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, click **Create**. Alternatively, from the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}, you can select **Start creating** from either **Run your container image** or **Run your source code**, and then click **Create project** from the Start creating page.
2. Choose a location to deploy the project. 
3. Enter a name for the project. The name must be unique for all your projects within the specified location.
4. Choose the resource group where you want to create the project.
5. Click **Create**.

To view the service instance for the project resource, go to your [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/resources){: external} and find your project name in **{{site.data.keyword.codeengineshort}}**.

### Creating a project with the CLI
{: #create-project-cli}

When you create a project, it is automatically selected as the current context. To create a project that is not automatically selected, use the `--no-select` option.

1. Install the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli). Target the resource group that you want to use for the project. 

2. Create a project with the [**`project create`**](/docs/codeengine?topic=codeengine-cli#cli-project-create) command. Use a project name that is unique to your region. 

  ```
  ibmcloud ce project create --name PROJECT_NAME 
  ```
  {: pre}

  **Example output**

  ```
  Creating project 'myproject'...
  OK
  ```
  {: screen}

3. Verify that your new project is created with the [**`project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command.

  ```
  ibmcloud ce project get --name PROJECT_NAME
  ```
  {: pre}

  **Example output**

  ```
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
  Subscriptions (IBM Cloud Object Storage)  0         100
  Subscriptions (ping)                      0         100
  ```
  {: screen}

  You can also list all projects and this output displays which project is your selected project. In the following example, `myproject` is the project that is selected as the current context.  

  ```
  ibmcloud ce project list
  ```
  {: pre}

  **Example output**

  ```
  Getting projects...
  OK

  Name             ID                                    Status  Selected  Tags  Region    Resource Group  Age
  myproj-eude      01234567-abcd-abcd-abcd-abcdabcd2222  active  false           eu-de     default         27d
  myproject        01234567-abcd-abcd-abcd-abcdabcd1111  active  true            us-south  default         52d
  ```
  {: screen}

## Work with a project
{: #target-a-project}

After you create a project, you can work with the project by using the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc} 

### Working with a project from the console
{: #target-project-console}

To work with a project, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external} and click the name of the project from the list.

To work with {{site.data.keyword.codeengineshort}} components, you must work with the components in the context of a project.  From the context of your project, you can create and work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [jobs](/docs/codeengine?topic=codeengine-job-plan). To determine the project from which you are currently working, see the breadcrumb of your {{site.data.keyword.codeengineshort}} component.

### Working with a project with the CLI
{: #target-project-cli}

To work with a project with the CLI, the project must be selected as the current context. A project is automatically selected as the current context when it is created, unless you specify the `--no-select` option. To select a project that is not currently targeted, use the [**`project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command.

```
ibmcloud ce project select --name PROJECT_NAME
```
{: pre}

**Example output**

```
Selecting project 'myproject'...
```
{: screen}

From within the context of the selected project, you can work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [jobs](/docs/codeengine?topic=codeengine-job-plan).

### Determining which project is selected as the current context
{: #current-project-cli}

You can find details about the project that is selected as the current context by using the [**`project current`**](/docs/codeengine?topic=codeengine-cli#cli-project-current) command. 

## Delete a project
{: #delete-project} 

When you no longer need a project, you can delete it. Deleting a project deletes all of the components that it contains. You can use the console or the CLI.
{: #shortdesc}

When you delete a project from the console or with the CLI, it is soft deleted and can be restored. You must restore your project within 7 days or it is permanently deleted. For more information about restoring projects, see [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project). To permanently delete a project, see [Permanently deleting projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project).

When you delete a project, any projects that are not permanently deleted count toward the maximum of 20 total projects per region that are allowed.
{: tip} 

Project names within a region must be unique. When you soft delete a project (or delete the project with reclamation), you cannot reuse the project name until the project is permanently deleted. 
{: important} 

### Deleting a project from the console
{: #delete-project-console}

To delete a project from the console, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, select the project that you want to delete, and click the delete icon. If you open a specific project, you can also delete the project from the Actions menu. 

When you delete a project from the console, the project is soft deleted and can be restored within 7 days before it is permanently deleted. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, the number of project reclamations is displayed. Click `Project reclamations` to display a list of projects that can be restored or permanently deleted.

### Deleting a project with the CLI
{: #delete-project-cli}

To delete a project with the CLI, use the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command. You can optionally use the `-f` option to force the delete a project without confirmation. The following example soft deletes the `myproject` project,

```
ibmcloud ce project delete --name myproject -f
```
{: pre}

**Example output**

```
Deleting project 'myproject'...
OK
```
{: screen}

To permanently delete a project so that it cannot be restored, specify the `--hard` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command. You can optionally use the `-f` option to force the delete a project without confirmation. The following example permanently deletes the `myproject2` project,

```
ibmcloud ce project delete --name myproject2 --hard -f
```
{: pre}

**Example output**

```
Deleting project 'myproject2'...
OK
```
{: screen}

If you specify the `--hard` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command, the project is immediately deleted and cannot be restored by using {{site.data.keyword.cloud_notm}} resource reclamation. If you do not specify the `--hard` option, the project can be restored within 7 days by using [{{site.data.keyword.cloud_notm}} resource reclamation](/docs/account?topic=account-resource-reclamation).
{: note}

If you previously soft deleted a project (without specifying the `--hard` option), you can specify a subsequent delete only by using the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command with the `--hard` option. This action completely deletes the project so that it cannot be restored.

## Restoring deleted projects
{: #restore-softdelete-project}

### Restoring deleted projects from the console
{: #restore-softdelete-project-ui}

After you soft delete a project (or delete the project with reclamation), you can restore it or permanently delete it from the console. You must restore your project within 7 days or it is permanently deleted.

1. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, view the list of projects in your region. The number of project reclamations is displayed.
2. Click the link for `project reclamations`.
3. From the **Project reclamations** page, you can view the number of days remaining that you can restore your project. 
   * To restore your project, click the restore icon.
   * To permanently delete your project, click the delete icon.

If you take no action on deleted projects that are listed on the **Project reclamations** page, the project is automatically deleted permanently after 7 days.

### Restoring deleted projects with the CLI
{: #restore-softdelete-project-cli}

1.  Discover projects that are soft deleted by using the [**`project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command to list all of your projects. 

  ```
  ibmcloud ce project list 
  ```
  {: pre}

  **Example output**

  ```
  Getting projects...
  OK

  Name           ID                                    Status               Selected  Tags  Region    Resource Group  Age
  myproject      c2909945-fac5-4acd-8dce-ceebdb5c4ede  active               false           jp-tok    default         4d22h
  myproject2     4ff0c4e0-2f13-4ce4-8165-f007f48bafe4  soft deleted         false           us-south  default         67m
  myproject3     bba96f18-1b3c-44f2-8a09-e141e1c905c1  soft deleted         false           us-south  default         65m
  ```
  {: screen} 

2. Use the [**`project restore`**](/docs/codeengine?topic=codeengine-cli#cli-project-restore) command to restore a soft deleted project to an active state. The following example restores the `myproject2` project and its components. 

  ```
  ibmcloud ce project restore --name myproject2 
  ```
  {: pre}

  **Example output**

  ```
  Restoring project 'myproject2'...
  OK
  ```
  {: screen}

## Permanently deleting projects
{: #perm-delete-project}

### Permanently deleting projects from the console
{: #perm-delete-project-ui}

After you soft delete a project (or delete the project with reclamation), you can restore it or permanently delete it from the console. When a project is permanently deleted, it cannot be restored. 

1. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, view the list of projects in your region. The number of project reclamations is displayed.
2. Click the link for `project reclamations`.
3. From the **Project reclamations** page, you can view the number of days remaining that you can restore your project. To permanently delete your project, click `Delete`.

If you take no action on deleted projects that are listed on the **Project reclamations** page, the project is automatically deleted permanently after 7 days.

### Permanently deleting projects with the CLI
{: #perm-delete-project-cli}

To permanently delete a project so that it cannot be restored, use the `--hard` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command to specify to immediately and permanently delete the project. For example, to permanently delete the `myproject` project,  

```
  ibmcloud ce project delete --name myproject --hard 
  ```
  {: pre}

  **Example output**

  ```
  Deleting project 'myproject'...
  OK
  ```
  {: screen}

