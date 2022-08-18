---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying your app from repository source code
{: #app-source-code}

You can deploy your application directly from source code that is located in a Git repository with the {{site.data.keyword.codeenginefull}} console and CLI. Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
{: shortdesc}


## Deploying your app from repository source code from the console
{: #deploy-app-source-code}

You can deploy your application directly from source code with the console.
{: shortdesc}

Before you begin, [plan for your build](/docs/codeengine?topic=codeengine-plan-build). You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile).

{{site.data.keyword.codeengineshort}} can automatically push (upload) images to {{site.data.keyword.registrylong}} namespaces in your account and even create a namespace for you. To upload images to a different {{site.data.keyword.registryshort}} account or to a private Docker Hub account, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start from source code**.
3. Select **Application**.
4. Enter a name for the application. Use a name for your application that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to deploy an app.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select a source repository, for example, `https://github.com/IBM/CodeEngine`. Because we are using sample source that does not require credentials, select `None` for the Code repo access. You can optionally provide a branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. Click **Next**.  
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Select a container registry location, such as `IBM Registry, Dallas` to specify where to store the image of your build output. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Provide registry information about where to store the image of your build output. Select an existing **Registry access secret** or create a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you.
12. Select a namespace, name, and a tag for your image. If you are building your image to an {{site.data.keyword.registrylong_notm}} instance that is in your account, you can select an existing namespace or let {{site.data.keyword.codeengineshort}} create and manage the namespace for you.
13. Click **Done**.
14. Modify any runtime settings or environment variables for your app. For more information about these options, see [Options for endpoint visibility of apps](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy) and [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
15. Click **Create**.
16. After your build run is submitted, the built container image is sent to {{site.data.keyword.registryshort}} and then your application pulls the image and deploys for you. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Build runs that complete are ultimately automatically deleted. When your build run is based on build configuration, this build run is deleted after 3 hours if the build run is successful. If the build run is not successful, this build run is deleted after 48 hours.  
{: note}

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  




## Deploying your app from repository source code with the CLI
{: #deploy-app-source-code-cli}

You can deploy your application directly from repository source code with the CLI. Use the **`app create`** command to both build an image from your Git repository source, and deploy your application to reference this built image.
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

In this scenario, {{site.data.keyword.codeengineshort}} builds an image from your Git repository source, automatically uploads the image to your container registry, and then creates and deploys your app to reference this built image. You need to provide only a name for the app and the URL to the Git repository if the image is to be located in an {{site.data.keyword.registrylong}} account. In this case, {{site.data.keyword.codeengineshort}} manages the namespace for you. However, if you want to use a different container registry, then you must specify the image and a registry access secret for that container registry. For a complete listing of options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.  

For information about required permissions for accessing image registries, see [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

The following example **`application create`** command creates and deploys the `myapp` app, which references an image that is built from the `https://github.com/IBM/CodeEngine` build source. This command automatically builds the image and uploads the image to an {{site.data.keyword.registrylong}} namespace in your account and the application references this built image. By specifying the `--build-context-dir` option, the build uses the source in the `helloworld` directory. This example command uses the default `dockerfile` strategy, and the default `medium` build size. Because the branch name of the repository is not specified with the `--build-commit` option, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository.  

```txt
ibmcloud ce application create --name myapp --build-source https://github.com/IBM/CodeEngine --build-context-dir helloworld
```
{: pre}

Example output

```txt
Creating application 'myapp'...
Submitting build run 'myapp-run-220411-13abcdefg'...
Creating image 'private.us.icr.io/ce--abcde-4svg40kna19/app-myapp:220411-1756-if8jv'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myapp-run-220411-13abcdefg' to check the build run status.
Waiting for application 'myapp' to become ready.
Configuration 'myapp' is waiting for a Revision to become ready.
Ingress has not yet been reconciled.
Waiting for load balancer to be ready.
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}

Notice the output of the **`application create`** command provides information on the progression of the build run before the app is created and deployed. 
{: tip}

In this example, the built image is uploaded to the `ce--abcde-4svg40kna19` namespace in {{site.data.keyword.registryshort}}. 

The following table summarizes the options that are used with the **`app create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

| Option | Description |
| -------------- | -------------- |
| `--name` | The name of the application. Use a name that is unique within the project. This value is required. \n - The name must begin with a lowercase letter. \n - The name must end with a lowercase alphanumeric character. \n - The name must be 63 characters or fewer and can contain letters, numbers, and hyphens (-). | 
| `--build-source` | The URL of the Git repository that contains your source code; for example, `https://github.com/IBM/CodeEngine`. |
| `--build-context-dir` | The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. |
{: caption="Table 1. Command description" caption-side="bottom"}

The following output shows the result of the **`application get`** command for this example, including information about the build.

Example output

```txt
[...]
Name:          myapp  
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f  
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111 
Age:           2d15h
Created:       2022-04-14T16:10:11-04:00
URL:                https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
Cluster Local URL:  http://myapp.4svg40kna19.svc.cluster.local
Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
Status Summary:  Application deployed successfully

Environment Variables:
  Type     Name          Value
  Literal  CE_APP        myapp
  Literal  CE_DOMAIN     us-south.codeengine.appdomain.cloud
  Literal  CE_SUBDOMAIN  4svg40kna19
Image:                  private.us.icr.io/ce--27fe9-4svg40kna19/app-myapp:220414-2010-sqsoj
Resource Allocation:
  CPU:                1
  Ephemeral Storage:  400M
  Memory:             4G
Registry Secrets:
  ce-auto-icr-private-us-south

Revisions:
  myapp-00001:
    Age:                23m
    Latest:             true
    Traffic:            100%
    Image:              private.us.icr.io/ce--27fe9-4svg40kna19/app-myapp:220414-2010-sqsoj (pinned to 86944c)  
    Running Instances:  0

Runtime:
  Concurrency:    100
  Maximum Scale:  10
  Minimum Scale:  0
  Timeout:        300

Build Information:
  Build Run Name:     myapp-run-220414-161009244
  Build Type:         git
  Build Strategy:     dockerfile-medium
  Timeout:            600
  Source:             https://github.com/IBM/CodeEngine
  Context Directory:  helloworld
  Dockerfile:         Dockerfile

  Build Run Summary:  Succeeded
  Build Run Status:   Succeeded
  Build Run Reason:   All Steps have completed executing
  Run 'ibmcloud ce buildrun get -n myapp-run-220414-161009244' for details.
[...]
```
{: screen}

Now that your app is created and deployed from repository source code, you can update the app to meet your needs by using the [**`ibmcloud ce app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. For more information about updating apps, see [Updating your app](/docs/codeengine?topic=codeengine-update-app). If you want to update your source to use with your app, you must provide the `--build-source` option on the **`application update`** command.

When your app is deployed from repository source code or from [local source](/docs/codeengine?topic=codeengine-app-local-source-code) with the CLI, the resulting build run is not based on a build configuration. Build runs that complete are ultimately automatically deleted. Build runs that are not based on a build configuration are deleted after 1 hour if the build run is successful. If the build run is not successful, this build run is deleted after 24 hours. You can only display information about this build run with the CLI. You cannot view this build run in the console.
{: note}



## Next steps
{: #nextsteps-appdeploysource}

* After your app deploys, [access your app](/docs/codeengine?topic=codeengine-access-service) through a URL. 
    * You can create a custom domain and assign it to your app. For information about deploying an app with a custom domain through Cloudflare, see the [Configuring a Custom Domain for Your {{site.data.keyword.codeengineshort}} Application](https://www.ibm.com/cloud/blog/configuring-a-custom-domain-for-your-ibm-cloud-code-engine-application){: external}  blog. For more information about deploying apps across multiple regions with a custom domain name, see [Deploying an application across multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions). 

* Now that you app is deployed, consider making your apps event-driven. By using event subscriptions, you can trigger your apps by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) or set your app to react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).

* After your app is deployed, you can [update your deployed app](/docs/codeengine?topic=codeengine-update-app) and its referenced code by using *any* of the following ways, independent of how you created or previously updated your app:

    - If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you deploy your app. You can deploy your app with an image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private).

        If you created your app by using the **`app create`** command and you specified the `--build-source` option to build the container image from local or repository source, and you want to change your app to point to a different container image, you must first remove the association of the build from your app. For example, run `ibmcloud ce application update -n APP_NAME --build-clear`. After you remove the association of the build from your app, you can update the app to reference a different image. 
        {: important}

    - If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

    - If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you deploy your app. 

    For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the app. Then, after the image is matured, you can update the deployed app to reference the specific image that you want. You can repeat this process as needed.

    When you deploy your updated app, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment. 




Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
