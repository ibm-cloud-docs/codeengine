---

copyright:
  years: 2020, 2023
lastupdated: "2023-07-06"

keywords: getting started with ibm cloud code engine, code engine, ibm cloud code engine, jobs in code engine, apps in code engine, builds with code engine, {{site.data.keyword.codeenginefull_notm}}, building container image, source code, functions in code engine

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
- [Run Function code](#first-function)
- [Building your first container image from source code](#build-image-gs)


## What are {{site.data.keyword.codeengineshort}} projects, applications, jobs, and functions?
{: #term-summary}

Before you get started, become familiar with some key terms for {{site.data.keyword.codeengineshort}}. Afterward, you can test your knowledge and [take a quiz!](https://ibm.biz/BdfFxR){: external}

| Term | Description |
| --------- | ------------------- |
| Project | A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. Projects are used to manage resources and provide access to its entities.|
| Application | An application, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. |
| Build | A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile or Cloud Native Buildpacks. |
| Function | A Function is a stateless code snippet that performs tasks in response to an HTTP request. |
| Job | A job runs one or more instances of your executable code. Unlike applications, which include an HTTP Server to handle incoming requests, jobs are designed to run one time and exit. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}

For more information about terms, see [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology).

Not sure what to choose? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}

## Deploying your first {{site.data.keyword.codeengineshort}} app
{: #app-hello}

Create your first {{site.data.keyword.codeengineshort}} app by using the `icr.io/codeengine/helloworld` image.  
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating**.
3. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to deploy an app.
4. Select **Application**.
5. Enter a name for the application, for example, `myapp`. Use a name for your application that is unique within the project. 
6. Select to run a **Container image** and specify `icr.io/codeengine/helloworld` for the image reference. For this example, you do not need to modify the default values. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.
7. Click **Create**. 
8. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  

Example output

```txt
Hello World from:
. ___  __  ____  ____
./ __)/  \(    \(  __)
( (__(  O )) D ( ) _)
.\___)\__/(____/(____)
.____  __ _   ___  __  __ _  ____
(  __)(  ( \ / __)(  )(  ( \(  __)
.) _) /    /( (_ \ )( /    / ) _)
(____)\_)__) \___/(__)\_)__)(____)

Some Env Vars:
--------------
CE_APP=myapp
CE_DOMAIN=us-east.codeengine.appdomain.cloud
CE_SUBDOMAIN=14juxb5nb96g
HOME=/root
HOSTNAME=myapp-00001-deployment-5b5895fdf7-44fnv
K_REVISION=myapp-00001
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PORT=8080
PWD=/
SHLVL=1
z=Set env var 'SHOW' to see all variables
```
{: screen}

You deployed your first application to {{site.data.keyword.codeengineshort}} and tested it out. Go to the [Tutorial: Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) or [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads) to try out more options for applications.

## Running your first {{site.data.keyword.codeengineshort}} job
{: #first-job}

Create and run your first {{site.data.keyword.codeengineshort}} job by using the `icr.io/codeengine/helloworld` image. 
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating**.
3. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a job.
4. Select **Job**.
5. Enter a name for the job, for example, `myjob`. Use a name for your job that is unique within the project.
6. Specify `icr.io/codeengine/helloworld` for the image reference. For this example, you do not need to modify the default values. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}. 
7. Click **Create**.
8. From your job page, click **Submit job** to submit a job based on the current configuration.  
9. From the Submit job pane, accept all the default values, and click **Submit job** again to run your job.

When logging is enabled, the following example is displayed in the logs. To learn about running jobs with logging enabled, see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).
{: tip}

Example output from logging instance

```txt
Hello World from:
. ___  __  ____  ____
./ __)/  \(    \(  __)
( (__(  O )) D ( ) _)
.\___)\__/(____/(____)
.____  __ _   ___  __  __ _  ____
(  __)(  ( \ / __)(  )(  ( \(  __)
.) _) /    /( (_ \ )( /    / ) _)
(____)\_)__) \___/(__)\_)__)(____)

Some Env Vars:
--------------
CE_DOMAIN=us-east.codeengine.appdomain.cloud 
CE_JOB=myjob
CE_JOBRUN=myjob-jobrun-xgpmz
CE_SUBDOMAIN=14juxb5nb96g
HOME=/root
HOSTNAME=myjob-jobrun-xgpmz-0-0 
JOB_INDEX=0
...
z=Set env var 'SHOW' to see all variables
```
{: screen}

You created and ran your job from the console. Go to the [Tutorial: Running jobs](/docs/codeengine?topic=codeengine-run-job-tutorial) or [Running jobs in Code Engine](/docs/codeengine?topic=codeengine-job-plan) to try out more options for jobs.

## Running your first function
{: #first-function}

Create and run your first {{site.data.keyword.codeengineshort}} function with sample function code.
{: shortdesc}

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating**.
3. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to create a function.
4. Select **Function**.
5. Enter a name for the function. Use a name for your function that is unique within the project.
6. Select **Node.js 18**
7. Click **Create**. Your function is created with sample code. You can edit this code on the **Function -> Configuration** page.
8. Click **Test function** and then click **Send request** in the Test function pane. To open the function in a web page, click **Function URL**. 

Example output

```txt
{"args":{"__ce_headers":{"Accept-Encoding":"gzip, deflate, br","User-Agent":"got (https://github.com/sindresorhus/got)","X-Request-Id":"72940b7c-82d0-4fb3-b16b-a6cce27f4146"},"__ce_method":"GET","__ce_path":"/"},"env":{"HOME":"/root","PATH":"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/lib/nodejs/bin","PWD":"/nodejsAction","SHLVL":"1","_":"/usr/local/lib/nodejs/bin/node","__OW_ALLOW_CONCURRENT":"true","container":"oci"}}
```
{: screen}

You deployed your first function to {{site.data.keyword.codeengineshort}} and tested it out. Go to the [Running a function from local source](/docs/codeengine?topic=codeengine-fun-tutorial) or [Working with functions](/docs/codeengine?topic=codeengine-fun-work) to try out more options for functions.

You can [migrate your IBM Cloud Functions to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-migrate).
{: tip}

## Building your first container image from source code
{: #build-image-gs}

Create and run your first {{site.data.keyword.codeengineshort}} build and then deploy the container image in an application.
{: shortdesc}

{{site.data.keyword.codeengineshort}} can automatically push images to a {{site.data.keyword.registryshort}} namespace in your account. It can even create a namespace for you. To push images to a different {{site.data.keyword.registryshort}} account or to a private Docker Hub account, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

1. Open the [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external} console.
2. Select **Start creating**.
3. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that you must have a selected project to deploy an app.
4. Select **Application**.
5. Enter a name for the application. Use a name for your application that is unique within the project. 
6. Select to run a **Container image** and specify `icr.io/codeengine/helloworld` for the image reference. For this example, you do not need to modify the default values. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.
7. Select **Source code**.
8. Click **Specify build details**.
9. Accept the default for each page, clicking **Next** and then **Done**. 
16. Click **Create**.

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
- [Running Functions](/docs/codeengine?topic=codeengine-fun-work)
- [Building container images](/docs/codeengine?topic=codeengine-build-image)

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}


