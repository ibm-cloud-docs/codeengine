---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-23"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying application workloads from images in a private registry
{: #deploy-app-private}

Deploy your app with {{site.data.keyword.codeengineshort}} that uses an image in a private registry such as private Docker Hub. You can create an app from the console or with the CLI. 
{: shortdesc}

Before you begin

To pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

## Deploying an app that references an image in private registry with the console
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

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Deploying an app with an image from a private registry with CLI
{: #deploy-app-private-cli}

Deploy an application that uses an image in a container registry with the CLI with the **`ibmcloud ce app create`** command. 
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} application that references an image in a private registry, you must first add access to the registry, pull the image, and then deploy it. 

1. To pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private registry to pull images. To add access to a private registry with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a Docker Hub registry called `privatedocker` that is at `'https://index.docker.io/v1/'` and uses your username and password.

    ```txt
    ibmcloud ce registry create --name privatedocker --server 'https://index.docker.io/v1/' --username <Docker_User_Name> --password <Password>
    ```
    {: pre}

    **Example output**

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

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

## Next steps for apps
{: #nextsteps-appdeploypriv}

For more information about apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Now that you have deployed your app, you can use event subscriptions to make your apps event-driven, so that your apps are triggered by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) or react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}
