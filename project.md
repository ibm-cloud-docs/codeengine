---

copyright:
  years: 2020
lastupdated: "2020-09-01"

keywords: code engine, project

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:new_window: target="_blank"}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Managing projects 
{: #manage-project}

Learn how to create and work with projects.
{: shortdesc} 

## What is a project?
In {{site.data.keyword.codeengineshort}}, a project is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you. When you have components that are related, such as components that are part of a larger application, you can put these components within one project to manage access control more easily. By grouping runtime components in the same project, these components share a private network, enabling them to talk to each other securely. 
For more information managing access control to projects with IAM, see [Managing user access](/docs/codeengine?topic=codeengine-codeengine-iam).

Projects incur no costs, but instead serve as folders for your applications and jobs.

### How can I see what projects I can access?

You can see a list of your projects in the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external}.

You can also run the [`project list`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-list) command. 

```
ibmcloud ce project list
```
{: pre}

**Example output**

```
Name            ID                                    Status         Tags   Location   Resource Group
myproject       42642513-8805-4da8-8dbf-bc4f409g9089   active               us-south   Default
new_proj        d294c0a3-30d8-49bc-b070-1921692f41d4   active               us-south   Default

Command 'project list' performed successfully
```
{: screen}


### How can I see details about a project? 

From the {{site.data.keyword.codeengineshort}} console, you can see details of a project by clicking the name of a project from the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.

You can also run the [`project get`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-get) command. Replace `PROJECT_NAME` with the name of your project.

```
ibmcloud ce project get --name PROJECT_NAME
```
{: pre}

**Example output**

```
Getting project 'myproject'...

Name: myproject
ID: 42642513-8805-4da8-8dbf-bc4f409g9089
Status: active
Tags: []
Location: us-south
Resource Group: Default
Created: Tue, 28 Apr 2020 09:27:22 -0400
Updated: Tue, 28 Apr 2020 09:27:57 -0400

Command 'project get' performed successfully
```
{: screen}


### How can I set policies so others can work with my project? 

See information about [managing user access](/docs/codeengine?topic=codeengine-codeengine-iam) to learn about setting IAM policies so others can work with your {{site.data.keyword.codeengineshort}} project. 

## Create a project
{: #create-a-project}
You can create a project through the console or with the CLI.
{: shortdesc} 

Wait for several minutes after you create your project before you proceed to the next step as it will take some time for your project to provision.
{: important}

### Creating a project from the console
{: #create-project-console}

1. From the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external} project menu, select **Create Project**.
2. Enter a name for the project. The name must be unique for all your projects within the specified location.
3. Choose the resource group where you want to create the project and a location to deploy the project.
4. Click **Create**.

To view the service instance for the project resource, go to your [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/resources){: external} and find your project name in **{{site.data.keyword.codeengineshort}} Projects**.

### Creating a project with the CLI
{: #create-project-cli}

1. Install the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli). Target the resource group that you want to use for the project. 

2. Create a project with the [`project create`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-create) command. Use a project name that is unique to your region. 

  ```
  ibmcloud ce project create --name PROJECT_NAME 
  ```
  {: pre}

  **Example output**

  ```
  Creating project 'myProject'...
  Successfully created project myProject
  ```
  {: screen}

3. Verify that your new project is created with the [`project get`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-get) command.

  ```
  ibmcloud ce project get --name PROJECT_NAME
  ```
  {: pre}

  **Example output**

  ```
  Getting project 'myProject'...

  Name: myProject
  ID: 42642513-8805-4da8-8dbf-bc4f409g7456
  Status: active
  Tags: []
  Location: us-south
  Resource Group: Default
  Created: Tue, 28 Apr 2020 09:27:22 -0400
  Updated: Tue, 28 Apr 2020 09:27:57 -0400
  ```
  {: screen}

  You can also list all projects:

  ```
  ibmcloud ce project list
  ```
  {: pre}

## Work with a project
{: #target-a-project}

After you create a project, you can work with the project by using the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc} 

### Working with a project from the console
{: #target-project-console}

To work with a project, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external} and click the name of the project from the list.

From the context of your project, you can create and work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [job definitions](/docs/codeengine?topic=codeengine-kn-job-deploy).

### Working with a project with the CLI
{: #target-project-cli}

To work with a project with the CLI, you must target the project. Use the  [`project target`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-target) command to target the project that you want to work with.  

```
ibmcloud ce project target --name PROJECT_NAME
```
{: pre}

**Example output**

```
Now targeting environment 'myproject'.
```
{: screen}

From the context of the targeted project, you can work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [job definitions](/docs/codeengine?topic=codeengine-kn-job-deploy).

## Delete a project
{: #delete-project}

When you no longer need a project, you can delete it. Deleting a project deletes all of the components that it contains. You can use the console or the CLI.
{: #shortdesc} 

### Deleting a project through the console
{: #delete-project-console}

To delete a project from the console, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, select the project that you want to delete, and click **Delete**.  

### Deleting a project through the CLI
{: #delete-project-cli}

To delete a project with the CLI, use the [`project delete`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-delete) command. 

```
ibmcloud ce project delete --name PROJECT_NAME 
```
{: pre}

**Example output**

```
Deleting project 'myproject'...

Deleted project  myproject
```
{: screen}


 
