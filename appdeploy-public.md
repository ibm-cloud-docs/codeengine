---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-18"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying application workloads from images in a public registry
{: #deploy-app}

Deploy your app with {{site.data.keyword.codeengineshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deploying an app from the console
{: #deploy-app-console}

Deploy an application with an image from a public registry that does not require credentials with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

This example references an image in [{{site.data.keyword.registrylong}}](/docs/codeengine?topic=codeengine-deploy-app-crimage). You can also reference an image in a public Docker Hub or an [image in a private registry](/docs/codeengine?topic=codeengine-deploy-app-private).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Application**.
4. Enter a name for the application. Use a name for your application that is unique within the project.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to deploy an app. 
6. Specify a container image for your app, for example, `icr.io/codeengine/helloworld`. If you have your own source code that you want to turn into a container image for the app, see [building a container image](/docs/codeengine?topic=codeengine-build-image). For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.  
7. Modify any default values for endpoint or runtime settings. For more information about these options, see [Options for endpoint visibility of apps](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy) and [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
8. Click **Create**. 
9. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  



## Deploying an app with the CLI
{: #deploy-app-cli}

To create and deploy your app with the CLI, use the **`app create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.
{: shortdesc}

The following **`application create`** command creates and deploys an app that is named `myapp` and uses the container image `icr.io/codeengine/hello`. 

```txt
ibmcloud ce application create --name myapp --image icr.io/codeengine/hello
```
{: pre}

**Example output**

```txt
Creating application 'myapp'...
OK
[...]
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.4idmmq6xpss.us-south.codeengine.appdomain.cloud
```
{: screen}

The following table summarizes the options that are used with the **`app create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the application. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 55 characters or fewer and can contain letters, numbers, and hyphens (-). | 
| `--image` | The name of the image that is used for this application. This value is required. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `TAG` is not specified, the default is `latest`. For images in [Docker Hub](https://hub.docker.com/){: external}, you can specify the image with `NAMESPACE/REPOSITORY`, as the default for `Registry` is `docker.io`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. |
{: caption="Table 1. Command description" caption-side="bottom"}
 
## Next steps for apps
{: #nextsteps-appdeploypub}

For more information about apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

After your app is deployed, you can update your application workload in any of the following ways:

* By accessing and referencing your existing built container image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private). For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

* By using the [build container images](/docs/codeengine?topic=codeengine-build-image) feature available in {{site.data.keyword.codeengineshort}} to build your image and then accessing the referenced image from your app.

* You can choose to let {{site.data.keyword.codeengineshort}} handle the build of your [local source](/docs/codeengine?topic=codeengine-app-local-source-code)  or [Git repository source](/docs/codeengine?topic=codeengine-app-source-code) for you. The application can then access the referenced image.

For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the app. Then, after the image is "matured", you can update the deployed app to reference the specific image that you want. You can repeat this process as needed.

When you deploy your updated app, the most current version of your referenced container image is downloaded and deployed.





Now that you have deployed your app, consider making your apps event-driven. By using event subscriptions, you can trigger your apps by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) or set your app to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).



Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

