---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-29"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying application workloads from a public registry
{: #deploy-app}

Deploy your app with {{site.data.keyword.codeengineshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deploying an app from the console
{: #deploy-app-console}

Deploy an application with an image from public Docker Hub with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

This example references an image in public Docker Hub. You can also reference an [image in {{site.data.keyword.registrylong}}](/docs/codeengine?topic=codeengine-deploy-app-crimage) or an [image in a private registry](/docs/codeengine?topic=codeengine-deploy-app-private). 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Application**.
4. Enter a name for the application. Use a name for your application that is unique within the project.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to deploy an app. 
6. Specify a container image, for example, `docker.io/ibmcom/helloworld`. 
6. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
7. Click **Create**. 
8. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  



## Deploying an app with the CLI
{: #deploy-app-cli}

To create and deploy your app with the CLI, use the **`app create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.
{: shortdesc}

The following **`application create`** command creates and deploys an app that is named `myapp` and uses the container image `docker.io/ibmcom/hello`. 

```
ibmcloud ce application create --name myapp --image docker.io/ibmcom/hello
```
{: pre}

**Example output**

```
Creating application 'myapp'...
OK
[...]
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.4idmmq6xpss.us-south.codeengine.appdomain.cloud
```
{: screen}

The following table summarizes the options that are used with the **`app create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

<table>
<caption><code>application create</code> command components</caption>
<thead>
<col width="25%">
<col width="75%">
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
</thead>
<tbody>
<tr>
<td><code>--name</code></td>
<td>The name of the application. Use a name that is unique within the project. This value is required.
<ul>
<li>The name must begin with a lowercase letter.</li>
<li>The name must end with a lowercase alphanumeric character.</li>
<li>The name must be 55 characters or fewer and can contain letters, numbers, and hyphens (-).</li>
</ul>
</td>
</tr>
<tr>
<td><code>--image</code></td>
<td>The name of the image that is used for this application. This value is required. The format is <code>REGISTRY/NAMESPACE/REPOSITORY:TAG</code> where <code>REGISTRY</code> and <code>TAG</code> are optional. If <code>TAG</code> is not specified, the default is <code>latest</code>. For images in <a href="https://hub.docker.com/">Docker Hub</a>, you can specify the image with <code>NAMESPACE/REPOSITORY</code>, as the default for <code>Registry</code> is <code>docker.io</code>. For other registries, use <code>REGISTRY/NAMESPACE/REPOSITORY</code> or <code>REGISTRY/NAMESPACE/REPOSITORY:TAG</code>. 
</td>
</tr>
</tbody>
</table>



