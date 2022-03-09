---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-09"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Creating a job from images in {{site.data.keyword.registryshort}}
{: #create-job-crimage}

Create your job configuration that uses an image in {{site.data.keyword.registryshort}}. You can create a job from the console or with the CLI. 
{: shortdesc}

Before you begin

- You must have an image in {{site.data.keyword.registryshort}}. For more information, see [Getting started with {{site.data.keyword.registryshort}}](/docs/Registry?topic=Registry-getting-started#getting-started). Or, you can [build one from source](/docs/codeengine?topic=codeengine-run-job-source-code).
- Verify that you can access the registry. See [Setting up authorities for container registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).

## Creating a job that references an image in {{site.data.keyword.registryshort}} with the console
{: #create-job-crimage-console}

Create a job configuration that uses an image in {{site.data.keyword.registryshort}} by using the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically pull images from {{site.data.keyword.registryshort}} namespaces in your account. To pull images from a different {{site.data.keyword.registryshort}} account or from a private Docker Hub account, see [Create a job from images in a private registry](/docs/codeengine?topic=codeengine-create-job-private).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Job**.
4. Enter a name for the job; for example, `myjob`.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Container image** and click **Configure image**. 
7. Select a container registry location, such as `IBM Registry, Dallas`.
8. Select `{{site.data.keyword.codeengineshort}} managed secret` for **Registry access secret**. Because this example uses an image in a {{site.data.keyword.registryshort}} namespace in your account, {{site.data.keyword.codeengineshort}} can create and manage the registry access secret for you.
9. Select an existing namespace and name of the image in the registry for the {{site.data.keyword.codeengineshort}} job to reference. For example, select `mynamespace` and select the image `hello_repo` in that namespace.
10. Select a value for **Tag**; for example, `latest`.
11. Click **Done**.
12. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
13. From the Create job page, click **Create**. 
14. From your job page, click **Submit job** to submit a job based on the current configuration.  

If you want to add registry access before you create a job, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

## Creating a job with an image in {{site.data.keyword.registryshort}} with the CLI
{: #create-job-crimage-cli}

Create a job configuration that uses an image in a {{site.data.keyword.registryshort}} with the CLI, use the **`job create`** command. This command requires a name and an image and also allows other optional arguments. For a complete listing of options, see the [**`ibmcloud ce job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) command.
{: shortdesc}

Before you can work with a {{site.data.keyword.codeengineshort}} job that references an image in {{site.data.keyword.registryshort}}, you must first add access to the registry, pull the image, and then create your job configuration.

1. To add access to {{site.data.keyword.registryshort_notm}}, [create an IAM API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key). To create an {{site.data.keyword.cloud_notm}} IAM API key from the CLI, run the [**`iam api-key-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_api_key_create) command. For example, to create an API key called `cliapikey` with a description of "My CLI APIkey" and save it to a file called `key_file`, run the following command:

    ```txt
    ibmcloud iam api-key-create cliapikey -d "My CLI APIkey" --file key_file
    ```
    {: pre}

    If you choose to not save your key to a file, you must record the APIkey that is displayed when you create it. You cannot retrieve it later.
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

3. Create your job configuration and reference the `hello_repo` image in {{site.data.keyword.registryshort}}. For example, the following **`job create`** command creates the `myhellojob` job to reference the `us.icr.io/mynamespace/hello_repo` by using the `myregistry` access information. 

    ```txt
    ibmcloud ce job create --name myhellojob --image us.icr.io/mynamespace/hello_repo --registry-secret myregistry
    ```
    {: pre}

    The format of the name of the image for this job is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`.
    {: note}

After you create your job, you can submit it. See [Run a job](/docs/codeengine?topic=codeengine-run-job).

## Next steps for jobs
{: #nextsteps-jobcreatecr}

After you create your job, you can submit it to [run the job](/docs/codeengine?topic=codeengine-run-job). For more information about jobs, see [Working with jobs](/docs/codeengine?topic=codeengine-job-plan).

Now that you have created your job, you can use event subscriptions to make your jobs event-driven, so that your jobs are triggered by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


