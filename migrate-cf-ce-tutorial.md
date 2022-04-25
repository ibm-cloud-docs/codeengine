---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-25"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

content-type: tutorial
completion-time: 30m 

---

{{site.data.keyword.attribute-definition-list}}

# Deploying Cloud Foundry applications in {{site.data.keyword.codeengineshort}}: Getting started
{: #migrate-cf-ce-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}


{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads. {{site.data.keyword.codeengineshort}} even builds container images for you from your source code. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on **writing code** and not on the infrastructure that is needed to host it.
{: shortdesc}

{{site.data.keyword.codeengineshort}} was designed with the following key goals in mind.

- **Focus on your code**. {{site.data.keyword.codeengineshort}} provides a simplified developer experience. No need to learn about or manage the underlying infrastructure.
- **Support the modern runtime characteristics**, such as autoscaling, scaling to zero when idle, and seamless integration with managed services and security.
- **Support all your Cloud-native based applications**, whether they are 12-factor apps, event-driven functions, or run-to-completion batch-jobs. If it can be containerized, {{site.data.keyword.codeengineshort}} can run it.
- **Pay for only the resources** that you actually use.

If you are coming from a Cloud Foundry background, many of these features sound familiar. However, {{site.data.keyword.codeengineshort}} also includes some new capabilities that allow you to go beyond even what Cloud Foundry offers, including applications that can scale to zero and incur no charges. So, after you're past the syntactical difference of the user experience, you and your applications will feel right at home in {{site.data.keyword.codeengineshort}}.

Let's deploy a simple `hello world` app to see how {{site.data.keyword.codeengineshort}} works. First, set up your account and install the CLI. Then, follow the steps to create a project, build your code, and deploy your app.

Review [Cloud Foundry and {{site.data.keyword.codeengineshort}} terms](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms) before starting this tutorial.

## Objectives
{: #cftut-objectives}

- Learn the similarities between {{site.data.keyword.codeengineshort}} and Cloud Foundry.
- Learn the general process of deploying apps in {{site.data.keyword.codeengineshort}}.
- Deploy an application from code on your local system with {{site.data.keyword.codeengineshort}}.

## Prerequisites
{: #cftut-prereqs}

Before you can get started with {{site.data.keyword.codeengineshort}}, you need to set up your account and install the CLI.

- All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account.

- While you can use {{site.data.keyword.codeengineshort}} through the console, the examples in this documentation focus on the command line. Therefore, you must install the {{site.data.keyword.codeengineshort}} CLI.

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}

    For more information, see [setting up the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli). For more information about the CLI, see [{{site.data.keyword.codeengineshort}} CLI reference](/docs/codeengine?topic=codeengine-cli).
    

## Log in to {{site.data.keyword.cloud_notm}}
{: #cftut-log-cloud}
{: step}

Follow these steps to log in to your {{site.data.keyword.cloud_notm}} account and target a resource group.

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```txt
    ibmcloud login
    ```
    {: pre}
    
2. Target a resource group by running the following command. To get a list of your resource groups, run **`ibmcloud resource groups`**.

    ```txt
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    **Example output**

    ```txt 
    Targeted resource group default
    ```
    {: screen}

## Creating a project
{: #cftut-create-project}
{: step}

A {{site.data.keyword.codeengineshort}} "project" is similar to a Cloud Foundry "space" in that it groups related workloads into a logical collection that is meaningful to the developer. You can group workloads into different projects based on whatever criteria that makes sense to you, for example, company organization structure, dependencies between the workloads, or development versus test versus production environments. Keep in mind that workloads within a single project share a private network and are isolated within the security boundary of the project. All workloads within a project can talk to each other freely without concern of being seen by workloads outside of the cluster. If workloads in different projects want to communicate with each other, then the communication must either use the internet or an internal IBM private network. For more information, see [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).

    
Create a project in {{site.data.keyword.codeengineshort}} called `sample`.

```txt
ibmcloud ce project create --name sample
```
{: pre}
    
**Example output**
    
```txt
Creating project 'sample'...
ID for project 'sample' is 'abcdabcd-abcd-abcd-abcd-abcd12e3456f7'.
Waiting for project 'sample' to be active...
Now selecting project 'sample'.
OK
```
{: screen}
   
Notice that your project is also selected for context, so all subsequent application-related commands are within the scope of this new `sample` project.

## Creating a directory and source code
{: #cftut-create-dir}
{: step}

1. Create a directory on your local workstation that is named `myapp` and navigate into it. In this directory, save all the files that are required to build the image and to run your app.
        
    ```txt
    mkdir myapp && cd myapp
    ```
    {: pre}
        
2. Create a file called `server.js` and copy the following source code into it.

    ```javascript
    const http = require('http');


    http.createServer(function (request, response) {
      response.writeHead(200, {'Content-Type': 'text/plain'});
      response.end( "Hello world\n" );
    }).listen(8080);
    ```
    {: pre}
    
    This example uses Node.js. You can substitute code from any [supported runtime](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat).
    {: note}


## Building and deploying your application
{: #cftut-build2-application}
{: step}

Push your code to {{site.data.keyword.codeengineshort}} by using the **`application create`** command. You must provide a name for your application, the location of the code source, and the build strategy that you want to use (`buildpacks` or `Dockerfile`). The following example creates an application called `myapp` that uses the buildpack strategy and provides the location for the source code for this specific build in the current directory (`.`).

```txt
ibmcloud ce app create --name myapp --build-source . --strategy buildpacks
```
{: pre}

**Example output**

```txt
Creating application 'myapp'...
Creating build 'myapp-build-220000-210706331'...
Packaging files to upload from source path '.'...
Submitting build run 'myapp-run-220999-210706331'...
Creating image 'private.us.icr.io/ce--6ef04-khxrbwa0lci/app-myapp:220418-0207-askql'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myapp-run-220000-210706331' to check the build run status.
Waiting for application 'myapp' to become ready.
Configuration 'myapp' is waiting for a Revision to become ready.
Ingress has not yet been reconciled.
Waiting for load balancer to be ready.
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.abcdbwa0lci.us-south.codeengine.appdomain.cloud
```
{: screen}

And that's it. You now have an internet-facing application. The code in the application itself is the same as what is used for a Cloud Foundry application, it's just the {{site.data.keyword.codeengineshort}} commands that are slightly different.

Let's take a deeper look at the previous **`app create`** command. 

1. {{site.data.keyword.codeengineshort}} receives a request to create an application from source code (instead of pulling directly from an image). 
2. {{site.data.keyword.codeengineshort}} checks for an IAM service ID and APIkey that is associated with the selected project. This service ID must be authorized to read and write to {{site.data.keyword.registrylong}}. If no service ID exists, {{site.data.keyword.codeengineshort}} creates one for you. Note that this service ID is used for subsequent {{site.data.keyword.codeengineshort}} build requests that are run from the same project.
3. This example builds code from a local source (`--build-source .`). The source code is packed into an archive file and uploaded to a managed namespace within the {{site.data.keyword.registrylong}} instance in your account. Note that you can target only {{site.data.keyword.registrylong}} for your local builds. 
4. {{site.data.keyword.codeengineshort}} builds your source code into an image. The source image is created in the same namespace as your build image.
5. After the build completes, your application is deployed. You can access your application from the provided URL.

With {{site.data.keyword.codeengineshort}}, you automatically get many of the same features as Cloud Foundry, such as autoscaling and blue-green roll-out of updates, but you'll also enjoy the benefits of newer features such as scaling down-to-zero, ensuring that you are not charged if your application is not active.

Now that you've deployed a sample application to {{site.data.keyword.codeengineshort}}, learn more details about how to migrate your existing workloads from Cloud Foundry to {{site.data.keyword.codeengineshort}}. Or, continue to the next in the series, [Migrating Cloud Foundry applications to Code Engine: Service binding](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial2).

## Clean up
{: #cftut-clean-up}

After you finish this tutorial, you can clean up the resources that you created with the following commands.

Delete your application

```txt
ibmcloud ce app delete --name myapp
```
{: pre}

When you delete your app, the associated build files are also deleted.

Lastly, delete the images that the build created from {{site.data.keyword.registrylong_notm}}. 

1. Navigate to [**Registry**](https://cloud.ibm.com/registry/start){: external} in the {{site.data.keyword.cloud_notm}} console.
2. Find the archive and the image that are associated with your application by searching for your application name.
3. Select the archive and image and delete.

## Next steps
{: #cftut-migrate-next}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. **Deploying Cloud Foundry applications in {{site.data.keyword.codeengineshort}}: Getting started**
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).


