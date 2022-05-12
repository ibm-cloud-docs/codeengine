---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-12"

keywords: getting started with ibm cloud code engine, code engine, ibm cloud code engine, jobs in code engine, apps in code engine, builds with code engine, {{site.data.keyword.codeenginefull_notm}}, building container image, source code

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.codeenginefull_notm}}
{: #getting-started}

{{site.data.keyword.codeenginefull}} is a fully managed, serverless platform that runs your containerized workloads, including web apps, micro-services, event-driven functions, or batch jobs. {{site.data.keyword.codeengineshort}} even builds container images for you from your source code. All these workloads can seamlessly work together because they are all hosted within the same Kubernetes infrastructure. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on writing code and not on the infrastructure that is needed to host it. 
{: shortdesc}



First, learn about some [key terms](#term-summary) for {{site.data.keyword.codeengineshort}} and then get started with one of the following options.

- [Deploy an application](#app-hello)
- [Create and run a job](#first-job)
- [Build a container image from source code](#build-image-gs)



## What are {{site.data.keyword.codeengineshort}} projects, applications, jobs, and builds?
{: #term-summary}

Before you get started, become familiar with some key terms for {{site.data.keyword.codeengineshort}}. Afterward, you can test your knowledge and [take a quiz!](https://ibm.biz/BdfFxR){: external}

| Term | Description |
| --------- | ------------------- |
| Project | A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. Projects are used to manage resources and provide access to its entities.|
| Application | An application, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. |
| Build | A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile or Cloud Native Buildpacks. |
| Job | A job runs one or more instances of your executable code. Unlike applications, which include an HTTP Server to handle incoming requests, jobs are designed to run one time and exit. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}

For more information about terms, see [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology).

## Creating your first {{site.data.keyword.codeengineshort}} app
{: #app-hello}

Create your first {{site.data.keyword.codeengineshort}} app by using the `icr.io/codeengine/helloworld` image.  
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Application**.
4. Enter a name for the application. Use a name for your application that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to deploy an app.
6. Select to run a **Container image** and specify `icr.io/codeengine/helloworld` for the image reference. For this example, you do not need to modify the default values for endpoint or runtime settings. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.
7. Click **Create**. 
8. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Example output

```txt
Hello World from:
     ___  __  ____  ____             
    / __)/  \(    \(  __)            
   ( (__(  O )) D ( ) _)             
    \___)\__/(____/(____)            
 ____  __ _   ___  __  __ _  ____ 
(  __)(  ( \ / __)(  )(  ( \(  __)
 ) _) /    /( (_ \ )( /    / ) _) 
(____)\_)__) \___/(__)\_)__)(____)
Some Env Vars:
--------------
CE_APP=myapp
CE_DOMAIN=us-south.codeengine.appdomain.cloud
CE_SUBDOMAIN=abcdabcdab
HOME=/root
HOSTNAME=myapp-00001-deployment-6db6d89dc7-k6qc7
K_REVISION=myapp-00001
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PORT=8080
PWD=/
SHLVL=1
```
{: screen}

You deployed your first application to {{site.data.keyword.codeengineshort}} and tested it out. Go to the [Tutorial: Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) to try out more options for applications.

## Running your first {{site.data.keyword.codeengineshort}} job
{: #first-job}

Create and run your first {{site.data.keyword.codeengineshort}} job by using the `icr.io/codeengine/firstjob` image. This job prints `Hi from a batch job! My index is: <index>`. 
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Run a container image**.
3. Select **Job**.
4. Enter a name for the job. Use a name for your job that is unique within the project.
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
6. Specify `icr.io/codeengine/firstjob` for the image reference. For this example, you do not need to modify the default values for environment variables or runtime settings. For more information about the code that is used for this example, see [`firstjob`](https://github.com/IBM/CodeEngine/tree/main/job){: external}. 
7. Click **Create**.
8. From your job page, click **Submit job** to submit a job based on the current configuration.  
9. From the Submit job pane, accept all the default values, and click **Submit job** again to run your job.

When logging is enabled, the expected output of `Hi from a batch job! My index is: 0` is displayed in the logs. To learn about running jobs with logging enabled, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs). 
{: tip}

You created and ran your job from the console. Go to the [Tutorial: Running jobs](/docs/codeengine?topic=codeengine-run-job-tutorial) or [Running jobs in Code Engine](/docs/codeengine?topic=codeengine-job-plan) to try out more options for jobs.

## Building your first container image from source code
{: #build-image-gs}

Create and run your first {{site.data.keyword.codeengineshort}} build and then deploy the container image in an application.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically push images to a {{site.data.keyword.registryshort}} namespace in your account. It can even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private Docker Hub account, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating** from **Start with source code**.
3. Select **Application**.
4. Enter a name for the application. Use a name for your application that is unique within the project. 
5. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to deploy an app.
6. Select **Source code**.
7. Click **Specify build details**.
8. Select `https://github.com/IBM/CodeEngine` for Source repository and `main` for Branch name. If you do not provide a branch name and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically uses the default branch of the specified repository. Click **Next**.
9. Select `Dockerfile` for Strategy, `Dockerfile` for Dockerfile, `10m` for Timeout, and `Medium` for Build resources. Click **Next**.
10. Select a container registry location, such as `IBM Registry, Dallas` to specify where to store the image of your build output
11. For **Registry access secret**, select `{{site.data.keyword.codeengineshort}} managed secret` and let {{site.data.keyword.codeengineshort}} create and manage this secret for you.
12. Select an existing namespace or enter a name for a new one, for example, `newnamespace`.
13. Enter a name for your image and optionally a tag.
14. Click **Done**. 
15. Click **Create**.

After your build run is submitted, the built container image is sent to {{site.data.keyword.registryshort}} and then your application pulls the image and deploys for you. After the application status changes to **Ready**, you can try it out. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. 

Example output

```txt
Hello World from:
     ___  __  ____  ____             
    / __)/  \(    \(  __)            
   ( (__(  O )) D ( ) _)             
    \___)\__/(____/(____)            
 ____  __ _   ___  __  __ _  ____ 
(  __)(  ( \ / __)(  )(  ( \(  __)
 ) _) /    /( (_ \ )( /    / ) _) 
(____)\_)__) \___/(__)\_)__)(____)
Some Env Vars:
--------------
CE_APP=myapp
CE_DOMAIN=us-south.codeengine.appdomain.cloud
CE_SUBDOMAIN=abcdabcdab
HOME=/root
HOSTNAME=myapp-00001-deployment-6db6d89dc7-k6qc7
K_REVISION=myapp-00001
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PORT=8080
PWD=/
SHLVL=1
```
{: screen}

You submitted source code to {{site.data.keyword.codeengineshort}} and created a container image that you then deployed in an application - all from one interface.

Go to [Building a container image](/docs/codeengine?topic=codeengine-plan-build) to explore and try out more options for builds.

## Next steps for {{site.data.keyword.codeengineshort}}
{: #nextsteps-getstart}

Learn more about performing these {{site.data.keyword.codeengineshort}} tasks from the console or with the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli).
- [Managing projects](/docs/codeengine?topic=codeengine-manage-project)
- [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads)
- [Running jobs](/docs/codeengine?topic=codeengine-job-plan)
- [Building container images](/docs/codeengine?topic=codeengine-build-image)

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


