---

copyright:
  years: 2020, 2022
lastupdated: "2022-03-19"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

# Creating a job from source code
{: #run-job-source-code}

You can create your job from source code. Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
{: shortdesc}

Before you begin, [plan for your build](/docs/codeengine?topic=codeengine-plan-build). You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile). Each time you run the job, the most current version of the dependent build artifacts, including the buildpacks and container image, are used during the build process and are included in the resulting container image.

{{site.data.keyword.codeengineshort}} can automatically push images to {{site.data.keyword.registryshort}} namespaces in your account and even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private Docker Hub account, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start from source code**.
3. Select **Job**.
4. Enter a name for the job. Use a name for your job that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select a source repository, for example, `https://github.com/IBM/CodeEngine`. You can optionally provide a branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. Click **Next**. 
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Provide registry information about where to store the image of your build output. Select a container registry location, such as `IBM Registry, Dallas`. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Select an existing **Registry access secret** or create a new one. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage the secret for you.
12. Select a namespace, name, and a tag for your image.
13. Click **Done**.
14. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
15. Click **Create**.

Need help? Check out [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

## Next steps for jobs
{: #nextsteps-jobcreatesource}

After you create your job, you can submit it to [run the job](/docs/codeengine?topic=codeengine-run-job). For more information about jobs, see [Working with jobs](/docs/codeengine?topic=codeengine-job-plan).

Now that you have created your job, you can use event subscriptions to make your jobs event-driven, so that your jobs are triggered by [periodic schedules](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job) or react to events like [file uploads](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job).


Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}

