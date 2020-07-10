---

copyright:
  years: 2020
lastupdated: "2020-07-10"

keywords: code engine, project

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}
{:preview: .preview}

# Managing projects 
{: #manage-project}

Learn how to create and work with projects.
{: shortdesc} 

## What is a project?
In {{site.data.keyword.codeengineshort}}, a project is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you. When you have components that are related, such as components that are part of a larger application, you can put these components within one project to manage access control more easily. By grouping runtime components in the same project, these components share the same private network, enabling them to talk to each other securely. 
See [Managing user access](/docs/codeengine?topic=codeengine-knative-iam) for information about using IAM to manage access control of projects.

Projects incur no costs, but instead serve as folders for your applications and jobs.

### How can I see what projects I can access?

You can see a list of your projects in the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/knative/overview){: external}.

You can also run the [`project list`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-list) command. 

```
ibmcloud coligo project list
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

From the {{site.data.keyword.codeengineshort}} console, you can see details of a project by clicking on the name of a project from the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}.

You can also run the [`project get`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-get) command. Replace `PROJECT_NAME` with the name of your project.

```
ibmcloud coligo project get --name PROJECT_NAME
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

See information about [managing user access](/docs/codeengine?topic=codeengine-knative-iam) to learn about setting IAM policies so others can work with your {{site.data.keyword.codeengineshort}} project. 

## Create a project
{: #create-a-project}
You can create a project through the console or with the CLI.
{: shortdesc} 

Please wait for several minutes after creating your project before you proceed to the next step as it will take some time for your project to provision.
{: important}

### Create a project through the console
{: #create-project-console}

1. From the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/knative/overview){: external} project menu, select **Create Project**.
2. Enter a name for the project. The name must be unique for all your projects within the specified location.
3. Choose the resource group where you want to create the project and a location to deploy the project.
4. Click **Create**.

To view the service instance for the project resource, go to your [{{site.data.keyword.cloud_notm}} dashboard](https://cloud.ibm.com/resources){: external} and find your project name in **{{site.data.keyword.codeengineshort}} Projects**.

### Create a project with the CLI
{: #create-project-cli}

1. Install the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli). Target the resource group that you want to use for the project. 

2. Create a project with the [`project create`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-create) command. Use a project name that is unique to your region. 

  ```
  ibmcloud coligo project create --name PROJECT_NAME 
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
  ibmcloud coligo project get --name PROJECT_NAME
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
  ibmcloud coligo project list
  ```
  {: pre}

## Work with a project
{: #target-a-project}

After you create a project, you can work with the project by using the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc} 

### Work with a project from the console
{: #target-project-console}

To work with a project, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}, click the name of the project from the list.

From the context of your project, you can create and work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [job definitions](/docs/codeengine?topic=codeengine-kn-job-deploy).

### Work with a project with the CLI
{: #target-project-cli}

To work with a project with the CLI, you must target the project with the CLI. Use the  [`target`](/docs/codeengine?topic=codeengine-kn-cli#cli-target) command to target the project that you want to work with.  

```
ibmcloud coligo target --name PROJECT_NAME
```
{: pre}

**Example output**

```
Now targeting environment 'myproject' (42642513-8805-4da8-8dbf-bc4f409g7456). Set the KUBECONFIG environment variable to use kubectl with your project:
export KUBECONFIG=/users/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-bc4f409g9089.yaml
```
{: screen}



From the context of the targeted project, you can work with {{site.data.keyword.codeengineshort}} components, such as [applications](/docs/codeengine?topic=codeengine-application-workloads) or [job definitions](/docs/codeengine?topic=codeengine-kn-job-deploy).

## Delete a project
{: #delete-project}

When you no longer need a project, you can delete it. Deleting a project deletes all of the components that it contains. You can use the console or the CLI.
{: #shortdesc} 

### Delete a project through the console
{: #delete-project-console}

To delete a project from the console, go to the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/knative/projects){: external}, select the project you want to delete, and click **Delete**.  

### Delete a project through the CLI
{: #delete-project-cli}

To delete a project with the CLI, use the [`project delete`](/docs/codeengine?topic=codeengine-kn-cli#cli-project-delete) command. 

```
ibmcloud coligo project delete --name PROJECT_NAME 
```
{: pre}

**Example output**

```
Deleting project 'myproject'...

Deleted project  myproject
```
{: screen}
