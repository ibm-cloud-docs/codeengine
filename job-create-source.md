---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-30"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, job run, environment variables

subcollection: codeengine

---

# Creating a job from source code
{: #run-job-source-code}

You can create your job from source code. Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
{: shortdesc}

Before you begin, [plan for your build](/docs/codeengine?topic=codeengine-plan-build). You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile). Each time you run the job, the most current version of the dependent build artifacts, including the buildpacks and container image, are used during the build process and are included in the resulting container image.

{{site.data.keyword.codeengineshort}} can automatically push images to {{site.data.keyword.registryshort}} namespaces in your account and even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private DockerHub account, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start from source code**.
3. Select **Job**.
5. Enter a name for the job. Use a name for your job that is unique within the project. 
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select a source repository and Branch name, for example, `https://github.com/IBM/CodeEngine` and `Main`.  Click **Next**.
9. Select a strategy for your build and resources for your build. For more information about build options, see [Planning your build](/docs/codeengine?topic=codeengine-plan-build). Click **Next**.
10. Select a container registry location, such as `IBM Registry, Dallas`. If your registry is private, you must [set up access](/docs/codeengine?topic=codeengine-add-registry) to it.
11. Select your **Registry access**. If you are building your image to a {{site.data.keyword.registryshort}} instance that is in your account, you can select `Automatic`.
12. Select a namespace, name, and a tag for your image.
13. Click **Done**.
14. Modify any default values for environment variables or runtime settings. For more information about these options, see [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options).
15. Click **Create**.

Need help? Check out [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).
