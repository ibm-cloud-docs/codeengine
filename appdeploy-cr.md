---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-14"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying application workloads from images in {{site.data.keyword.registryshort}}
{: #deploy-app-crimage}

Deploy your app with {{site.data.keyword.codeengineshort}} that uses an image in {{site.data.keyword.registryshort}}. You can create an app from the console or with the CLI. 
{: shortdesc}

Before you begin

- You must have an image in {{site.data.keyword.registryshort}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started).  Or, you can [build one from source](/docs/codeengine?topic=codeengine-app-source-code).

## Deploying an app that references an image in {{site.data.keyword.registryshort}} with the console
{: #deploy-app-crimage-console}

Deploy an application that uses an image in a container registry by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically pull images from a {{site.data.keyword.registryshort}} namespace in your account. To pull images from a different {{site.data.keyword.registryshort}} account or from a private Docker Hub account, see [Deploy application workloads from images in a private registry](/docs/codeengine?topic=codeengine-deploy-app-private). 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Application**.
4. Enter a name for the application; for example, `helloapp`. Use a name for your application that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to deploy an app. 
6. Select **Container image** and click **Configure image**. 
7. Select a container registry location, such as `IBM Registry, Dallas`.
8. Select `{{site.data.keyword.codeengineshort}} managed secret` for **Registry access secret**. Because this example uses an image in a {{site.data.keyword.registryshort}} namespace in your account, {{site.data.keyword.codeengineshort}} can create and manage the registry access secret for you. 
9. Select an existing namespace and name of the image in the registry for the {{site.data.keyword.codeengineshort}} app to reference. For example, select `mynamespace` and select the image `hello_repo` in that namespace.
10. Select a value for **Tag**; for example, `latest`.
11. Click **Done**.
12. Modify any runtime settings or environment variables for your app. For more information about these options, see [Options for endpoint visibility of apps](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy) and [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
13. Click **Create** to create the application.
14. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  



If you want to add registry access to a {{site.data.keyword.registryshort}} instance that is not in your account, see [Adding access to a {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-add-registry). 

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deploying an app with an image in {{site.data.keyword.registryshort}} with the CLI
{: #deploy-app-crimage-cli}

Deploy an application that uses an image in a container registry with the CLI with the **`ibmcloud ce app create`** command. 
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then deploy it. 

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key). To create an {{site.data.keyword.cloud_notm}} IAM API key with the CLI, run the [**`iam api-key-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

    ```txt
    ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
    ```
    {: pre}

    If you choose to not save your key to a file, you must record the apikey that is displayed when you create it. You cannot retrieve it later.
    {: important}

2. After you create your API key, add registry access to {{site.data.keyword.codeengineshort}}. To add access to {{site.data.keyword.registryshort}} with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a {{site.data.keyword.registryshort}} instance called `myregistry`. Note, even though the `--server` and `--username` options are specified in the example command, the default value for the `--server` option is `us.icr.io` and the `--username` option defaults to `iamapikey` when the server is `us.icr.io`.  

    ```txt
    ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password APIKEY
    ```
    {: pre}

    **Example output**

    ```txt
    Creating image registry access secret 'myregistry'...
    OK
    ```
    {: screen}

3. Create your app and reference the `hello_repo` image in {{site.data.keyword.registryshort}}. For example, use the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command to create the `myhelloapp` app to reference the `us.icr.io/mynamespace/hello_repo` by using the `myregistry` access information. 

    ```txt
    ibmcloud ce app create --name myhelloapp --image us.icr.io/mynamespace/hello_repo --registry-secret myregistry
    ```
    {: pre}

    The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
    {: important}

4. After your app deploys, you can access the app. To obtain the URL of your app, run `ibmcloud ce app get --name myhelloapp --output url`. When you curl the `myhelloapp` app, `Hello World` is returned.  

    ```txt
    curl https://myhelloapp.abcdabcdhye.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Next steps for apps
{: #nextsteps-appdeploycr}

For more information about apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

**For 4/30** To deploy applications in {{site.data.keyword.codeengineshort}}, the application requires a container image that includes the runtime artifacts that your application needs to run. You can begin with your built image in a container registry, or take advantage of {{site.data.keyword.codeengineshort}} functions to build your image before or during the application deployment. 

You can deploy application workloads in any of the following ways: 

* By accessing and referencing your existing built container image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private). For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

* By using the [build container images](/docs/codeengine?topic=codeengine-build-image) feature available in {{site.data.keyword.codeengineshort}} to build your image and then accessing the referenced image from your app.

* You can choose to let {{site.data.keyword.codeengineshort}} handle the build of your [local source](/docs/codeengine?topic=codeengine-app-local-source-code)  or [Git repository source](/docs/codeengine?topic=codeengine-app-source-code) for you. The application can then access the referenced image.

When you deploy your application, the most current version of your referenced container image is downloaded and deployed.

After your application is deployed, you can also update your app in any one of these ways. For example, you might choose to let {{site.data.keyword.codeengineshort}} handle the build of your local source while you evolve the development of your source for the app. Then, after the image is "matured", you can update the deployed app to reference the specific image that you want.



Now that you have deployed your app, you can use event subscriptions to make your apps event-driven, so that your apps are triggered by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) or react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


