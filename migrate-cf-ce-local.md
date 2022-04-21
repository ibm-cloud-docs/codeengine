---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-21"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Deploying your application code from a local source
{: #migrate-local-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Let's deploy a simple `hello world` app to see how {{site.data.keyword.codeengineshort}} works. First, set up your account and install the CLI. Then, follow the steps to create a project, prepare your code, and deploy your app.
{: shortdesc}

Review [Cloud Foundry and {{site.data.keyword.codeengineshort}} terms](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms) before starting this tutorial.

## Objectives
{: #cf-objectives}

- Learn the similarities between {{site.data.keyword.codeengineshort}} and Cloud Foundry.
- Learn the general process of deploying apps in {{site.data.keyword.codeengineshort}}.
- Deploy an application from code on your local system with {{site.data.keyword.codeengineshort}}.

## Prerequisites
{: #cf-prereqs}

Before you can get started with {{site.data.keyword.codeengineshort}}, you need to set up your account and install the CLI.

- All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account.

- While you can use {{site.data.keyword.codeengineshort}} through the console, the examples in this documentation focus on the command line. Therefore, you must install the {{site.data.keyword.codeengineshort}} CLI.

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}

    For more information, see [setting up the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli). For more information about the CLI, see [{{site.data.keyword.codeengineshort}} CLI reference](/docs/codeengine?topic=codeengine-cli).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}}pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}


## Log into {{site.data.keyword.cloud_notm}}
{: #local-log-cloud}
{: step}

Follow these steps to log into your {{site.data.keyword.cloud_notm}} account and target a resource group.

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
{: #local-create-project}
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
{: #local-create-dir}
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
    


## Creating a container registry namespace
{: #local-create-cr-namespace}
{: step}

In Cloud Foundry, your application is packaged and provided to the hosting environment automatically. In {{site.data.keyword.codeengineshort}}, you must build or package your source code into a container image and then store that container image in a namespace, or folder, in a registry that {{site.data.keyword.codeengineshort}} can access. This example uses {{site.data.keyword.registryshort}}. 

1. Set your {{site.data.keyword.registryshort}} to the same region that you created your project in. For example, to set your region to `us-south`, run the following command.

    ```txt
    ibmcloud cr region-set us-south
    ```
    {: pre}
    
    **Example output**
        
    ```txt
    The region is set to 'us-south', the registry is 'us.icr.io'.
    ```
    {: screen}
    

2. Create your registry namespace. The following command creates a namespace called `myapp-images`. However, as namespace names must be globally unique, add your name or initials to it. 

    ```txt
    ibmcloud cr namespace-add myapp-images<INITIALS>
    ```
    {: pre}
        
    **Example output**
        
    ```txt
    Adding namespace 'myapp-images' in resource group 'default' for account John Doe's Account in registry us.icr.io...
    Successfully added namespace 'myapp-images'
    OK
    ```
    {: screen}
    
For more information, see [add registry access documentation](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).    
 
## Creating an API key
{: #local-create-apikey}
{: step}

Set up access to your namespace by creating an API key. 

```txt
ibmcloud iam api-key-create myapp-icr-apikey
```
{: pre}

**Example output**

```txt
Creating API key myapp-icr-apikey under 7f9dc5344476457f2c0f53244a246d44 as johndoe@example.com...
Please preserve the API key! It cannot be retrieved after it's created.
OK
API key myapp-icr-apikey was created


                 
ID            ApiKey-d688eb25-2b35-4641-a75f-079d8f627b8a   
Name          myapp-icr-apikey   
Description      
Created At    2022-02-04T15:02+0000   
API Key       LAzmpcrTc6OCIgiqxuwH5-frnTFiDth6bkiuGN19X9hP   
Locked        false  
```
{: screen}

## Storing access to your registry in {{site.data.keyword.codeengineshort}}
{: #local-store-registry-access}
{: step}

Store access to your registry in {{site.data.keyword.codeengineshort}}. Registry access is used to store access credentials for container registries. Replace the `password` value of `LAzmpcrTc6OCIgiqxuwH5-frnTFiDth6bkiuGN19X9hP` with the `API Key` value returned in the previous command.

```txt
ibmcloud ce registry create --name icr --password LAzmpcrTc6OCIgiqxuwH5-frnTFiDth6bkiuGN19X9hP --server us.icr.io
```
{: pre}

**Example output**

```txt
Creating image registry access secret 'icr'...
OK
```
{: screen}

For more information, see [add registry access documentation](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce).

## Creating a build definition for your application
{: #local-create-build-def}
{: step}

Create a build, which defines how you want the source code to be built and where to store the image.

```txt
ibmcloud ce build create --name myapp-build --image us.icr.io/myapp-images<INITIAL>/myapp --registry-secret icr --strategy buildpacks --build-type local
```
{: pre}

**Example output**

```txt
Creating build 'myapp-build'...
OK
```
{: screen}

Let's briefly discuss the options.

`--name` 
:    Specifies the name of the build definition. You can use this name to refer back to the build definition when you want to run the build.

`--image`
:    Specifies the location in {{site.data.keyword.registryshort}} to store the resulting image.

`--registry-secret` 
:    The registry access credentials that you created in the previous step.

`--strategy`
:    Defines the method that Code Engine uses to build the image. This build uses ` buildpack`, a method similar to Cloud Foundry. Another valid type is `dockerfile`. For more information, see [Choose a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

`--build-type`
:    Indicates whether the source code can be found locally or in a Git repository. In this example, use `local`. For more information, see [Prepare your source location](/docs/codeengine?topic=codeengine-plan-build#build-plan-repo).

## Running your build
{: #local-run-build-submit}
{: step}

After your create your build definition, submit your build run. This example references the previously created build definition and provides the location for the source code for this specific build in the current directory (`.`). The `--wait` option indicates for build run to wait for the build to finish rather than running the command in the background.

```txt
ibmcloud ce buildrun submit --build myapp-build --source . --wait
```
{: pre}

**Example output**

```txt
Getting build 'myapp-build'
Packaging files to upload from source path '.'...
Submitting build run 'myapp-build-run-220204-150228492'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myapp-build-run-220204-150228492' to check the build run status.
OK
```
{: screen}


## Deploying your application
{: #local-deploy-application}
{: step}

Now that you created your container image, you can deploy our application. Notice that since the registry that you are using is {{site.data.keyword.registryshort}}, which is a private registry, you must pass in the registry credentials so that {{site.data.keyword.codeengineshort}} can access and download your image.

```txt
ibmcloud ce app create --name myapp --image us.icr.io/myapp-images/myapp --registry-secret icr
```
{: pre}

**Example output**

```txt
Creating application 'myapp'...
The Route is still working to reflect the latest desired specification.
Configuration 'myapp' is waiting for a Revision to become ready.
Ingress has not yet been reconciled.
Waiting for load balancer to be ready.
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK


https://myapp.bqos0nxl0jo.us-south.codeengine.appdomain.cloud
```
{: screen}

The `--name` option specifies the name for the application.  At the end of the output is the URL that you can use to connect to your app.

And that's it. You now have an internet-facing application. The code in the application itself is the same as what is used for a Cloud Foundry application, it's just the {{site.data.keyword.codeengineshort}} commands that are slightly different.

With {{site.data.keyword.codeengineshort}}, you automatically get many of the same features as Cloud Foundry, such as autoscaling and blue-green roll-out of updates, but you'll also enjoy the benefits of newer features such as scaling down-to-zero, ensuring that you are not charged if your application is not active.

Now that you've deployed a sample application to {{site.data.keyword.codeengineshort}}, learn more details about how to migrate your existing workloads from Cloud Foundry to {{site.data.keyword.codeengineshort}}. Or, continue to the next in the series, [Migrating Cloud Foundry applications to Code Engine: Service binding](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial2).



## Clean up
{: #local-clean-up}

After you finish this tutorial, you can clean up the resources that you created with the following commands.

Delete your application

```txt
ibmcloud ce app delete --name myapp
```
{: pre}

When you delete your app, the associated build files are also deleted.

Lastly, delete the images that the build created from {{site.data.keyword.registrylong_notm}}. 

1. Navigate to **Registry** in the {{site.data.keyword.cloud_notm}} console.
2. Find the archive and the image that are associated with your application by searching for your application name.
3. Select the archive and image and delete.

## Next steps
{: #migrate-cf-ce-next-local}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with Code Engine](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. **Deploying your application code from a local source**
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [Code Engine equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to Code Engine FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).


