---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-10"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Create a job from images in a private registry
{: #create-job-private}

Create your job that uses an image in a private registry such as private Docker Hub. You can create a job from the console or with the CLI. 
{: shortdesc}

Before you begin

In order to pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

## Creating a job that references an image in private registry with the console
{: #create-job-private-console}

Create a job configuration that uses an image in a private registry with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private registry, you must first add access to the registry, pull the image, and then create your job configuration.

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run your container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Container image** and click **Configure image**.
7. Enter `docker.io` for **Registry server**.
8. From **Registry access**, select **Create registry access**.
9. From the Add Registry Access page, choose your registry source. For example, **DockerHub**.
10. Enter a username. For Docker Hub, it is your Docker ID.
11. Enter the password. For Docker Hub, you can use your Docker Hub password or an access token. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.
12. Click **Create** to add the registry access for {{site.data.keyword.codeengineshort}}.
13. From the Select image page, the registry that was added is listed. Select the registry of your image.
14. Select the namespace and name of the image in Docker Hub for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `testjob` in that namespace.
15. Select a value for **Tag**; for example, `latest`.
16. Click **Done**. You selected your image in the registry to reference from your job.
17. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
18. From the Create job page, click **Create**.
19. After your job is created, the job page for your specific job opens. Run your job by clicking `Submit job` from the Job runs pane. Note that you might need to scroll to find the Job runs pane.

If you want to add registry access before you create a job configuration, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

## Creating a job with an image from a private registry with CLI
{: #create-job-private-cli}

To create a job configuration with an image from a private registry with CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in a private registry, you must first add access to the registry, pull the image, and then create your job configuration.

1. In order to pull images from a private registry, you must first create a private registry. For example, to create a private Docker Hub registry, see [Docker Hub documentation](https://docs.docker.com/docker-hub/repos/){: external}. After you create a private registry, [push an image to it](https://docs.docker.com/docker-hub/repos/#pushing-a-docker-container-image-to-docker-hub){: external}. You can also set up an access token. By using an access token, you can more easily grant and revoke access to your Docker Hub account without requiring a password change. For more information about access tokens and Docker Hub, see [Managing access tokens](https://docs.docker.com/docker-hub/access-tokens/){: external}.

2. Add access to your private registry in order to pull images. To add access to a private registry with the CLI, use the [**`ibmcloud ce registry create`**](/docs/codeengine?topic=codeengine-cli#cli-registry-create) command to create an image registry access secret. For example, the following **`registry create`** command creates registry access to a Docker Hub registry called `privatedocker` that is at ``https://index.docker.io/v1/`` and uses your username and password.

    ```txt
    ibmcloud ce registry create --name privatedocker --server https://index.docker.io/v1/ --username <Docker_User_Name> --password <Password>
    ```
    {: pre}

    **Example output**

    ```txt
    Creating image registry access secret 'privatedocker'...
    OK
    ```
    {: screen}

3. Create your job configuration and reference the image in your private Docker Hub registry. For example, create the `mytestjob` job configuration to reference the `docker.io/privaterepo/testjob` by using the `privatedocker` access information. 

    ```txt
    ibmcloud ce job create --name mytestjob --image docker.io/privaterepo/testjob --registry-secret privatedocker
    ```
    {: pre}

The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
{: note}


