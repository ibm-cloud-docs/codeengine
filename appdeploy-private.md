---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying app workloads from images in a private registry
{: #deploy-app-private}

Deploy your app with {{site.data.keyword.codeengineshort}} that uses an image in a private registry such as private Docker Hub. You can create an app from the console or with the CLI. 
{: shortdesc}

Before you begin

* To pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. 
* After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. 
* You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

## Deploying an app that references an image in a private registry with the console
{: #deploy-app-private-console}

Deploy an application that uses an image in a private registry with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in a private registry, you must first add access to the registry, pull the image, and then deploy it. 

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Application**.
4. Enter a name for the application; for example, `helloapp`. Use a name for your application that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You must have a selected project to deploy an app. 
6. Select **Container image** and click **Configure image**.
7. Enter `docker.io` for **Registry server**.
8. For **Registry access secret**, select **Create registry access secret**. 
9. From the Create registry access secret page, choose your registry source. For example, **Docker Hub**.
10. Enter a username. For Docker Hub, it is your Docker ID.
11. Enter the password. For Docker Hub, you can use your Docker Hub password or an access token. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.
12. Click **Create** to add a registry access secret for {{site.data.keyword.codeengineshort}}.
13. From the Configure image page, the registry access secret that was added is listed. Select the registry access secret for your image.
14. Select the namespace and name of the image in Docker Hub for the {{site.data.keyword.codeengineshort}} app to reference. For example, select `mynamespace` and select the image `hello_repo` in that namespace.
15. Select a value for **Tag**; for example, `latest`.
16. Click **Done**. You selected your image in the registry to reference from your app. 
17. Modify any runtime settings or environment variables for your app. For more information about these options, see [Options for endpoint visibility of apps](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy) and [Options for deploying an app](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy).
18. From the Create application page, click **Create**. 
19. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  



If you want to add registry access before you create an app, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry). 

## Deploying an app with an image from a private registry with CLI
{: #deploy-app-private-cli}

Deploy an application that uses an image in a container registry with the CLI with the **`ibmcloud ce app create`** command. 
{: shortdesc}

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in a private registry, you must first add access to the registry, pull the image, and then deploy it. 

1. To pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private registry to pull images. To add access to a private registry with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a Docker Hub registry called `privatedocker` that is at `'https://index.docker.io/v1/'` and uses your username and password.

    ```txt
    ibmcloud ce registry create --name privatedocker --server 'https://index.docker.io/v1/' --username <Docker_User_Name> --password <Password>
    ```
    {: pre}

    Example output

    ```txt
    Creating image registry access secret 'privatedocker'...
    OK
    ```
    {: screen}

3. Create your app and reference the image in your private Docker Hub registry. For example, create the `myhelloapp` app to reference the `docker.io/privaterepo/helloworld` by using the `privatedocker` access information. 

    ```txt
    ibmcloud ce app create --name myhelloapp --image docker.io/privaterepo/helloworld --registry-secret privatedocker
    ```
    {: pre}

    The format of the name of the image for this application is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
    {: important}

4. After your app deploys, you can access the app. To obtain the URL of your app, run `ibmcloud ce app get --name myhelloapp --output url`. When you curl the `myhelloapp` app, `Hello World` is returned.

    ```txt
    curl https://myhelloapp.abcdabcdhye.us-south.codeengine.appdomain.cloud
    ```
    {: pre}


## Next steps
{: #nextsteps-appdeploypriv}

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
