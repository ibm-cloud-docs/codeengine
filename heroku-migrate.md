---

copyright:
  years: 2022, 2026
lastupdated: "2026-01-27"

keywords: migrate, migration, heroku, terms, code engine

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with your migration from Heroku to {{site.data.keyword.codeengineshort}}
{: #heroku-migrate}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

Welcome Heroku users to {{site.data.keyword.codeenginefull}}.
{: shortdesc}

{{site.data.keyword.codeengineshort}} is a fully managed, serverless platform that runs your containerized workloads. {{site.data.keyword.codeengineshort}} even builds container images for you from your source code. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on **writing code** and not on the infrastructure that is needed to host it.

{{site.data.keyword.codeengineshort}} was designed with the following key goals in mind.

- **Focus on your code**. {{site.data.keyword.codeengineshort}} provides a simplified developer experience. No need to learn about or manage the underlying infrastructure.
- **Support the modern runtime characteristics**, such as autoscaling, scaling to zero when idle, and seamless integration with managed services and security.
- **Support all your Cloud-native based applications**, whether they are 12-factor apps, event-driven functions, or run-to-completion batch-jobs. If it can be containerized, {{site.data.keyword.codeengineshort}} can run it.
- **Pay for only the resources** that you actually use.

If you are coming from a Heroku background, many of these features sound familiar. However, {{site.data.keyword.codeengineshort}} also includes some new capabilities that allow you to go beyond even what Heroku offers, including applications that can scale to zero and incur no charges. In addition, {{site.data.keyword.codeengineshort}} requires a Pay-as-you-Go account that includes a [free tier](https://cloud.ibm.com/codeengine/overview){: external}. So, after you're past the syntactical difference of the user experience, you and your applications will feel right at home in {{site.data.keyword.codeengineshort}}. 

## Objectives
{: #heroku-objectives}

- Learn the similarities between {{site.data.keyword.codeengineshort}} and Heroku.
- Learn the general process of deploying apps in {{site.data.keyword.codeengineshort}}.
- Deploy an application from code on your local system with {{site.data.keyword.codeengineshort}}.

Watch the tutorial on YouTube. [Deploy Heroku app in IBM Cloud Code Engine](https://www.youtube.com/watch?v=01g1QSjYDa0){: external}.
{: tip}

## Prerequisites
{: #heroku-prereqs}

Before you can get started with {{site.data.keyword.codeengineshort}}, you need to set up your account and install the CLI.

- All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account.

- While you can use {{site.data.keyword.codeengineshort}} through the console, the examples in this documentation focus on the command line. Therefore, you must install the {{site.data.keyword.codeengineshort}} CLI.

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}

    For more information, see [setting up the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli). For more information about the CLI, see [{{site.data.keyword.codeengineshort}} CLI reference](/docs/codeengine?topic=codeengine-cli).

## Comparing Heroku and {{site.data.keyword.codeengineshort}} terminology
{: #heroku-migrate-terms}

Before you get started with deploying apps in {{site.data.keyword.codeengineshort}}, learn the basics about {{site.data.keyword.codeengineshort}}. The following table describes some high-level terminology differences between Cloud Foundry and {{site.data.keyword.codeengineshort}}.


| Heroku| {{site.data.keyword.codeengineshort}} | Description |
| -------------- | -------------- | -------------- |
| N/A | Resource group and projects | A grouping of workloads. The specific choice of which workload goes into each grouping is defined by the user. "Resource groups" are an {{site.data.keyword.cloud_notm}} concept, while "projects" are {{site.data.keyword.codeengineshort}} specific. Projects provide a level of isolation between workloads. See [Managing projects](/docs/codeengine?topic=codeengine-manage-project). |
| Dynos | Containers | A dyno is a light-weight container that runs your Heroku code and is managed for you. In {{site.data.keyword.codeengineshort}}, the underlying containers are based on Kubernetes and are automatically managed for you. |
| Application | Application (app) | A workload that responds to HTTP requests from a REST API, a web page request, or an event, for example. {{site.data.keyword.codeengineshort}} requires that applications include the HTTP server as part of the code. {{site.data.keyword.codeengineshort}} applications automatically scale (up and down) based on the incoming load. You can configure the minimum and maximum scale if needed. By default, the application listens on port 8080. You can override this behavior by using the console or with the CLI `--port` flag. See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads). |
| N/A | Job or batch job | A job runs one or more instances of your executable code in parallel. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. See [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan). |
| `heroku create` and `git push heroku main` or `heroku container:push web` | `app create` | The process of creating an application. With Heroku, you create an app and then push your code to it. Your code is build and deployed in that single step. With {{site.data.keyword.codeengineshort}}, you can pull a container image from an image repository, build your source code from a repository such as GitHub, or pull your code from a local file on your system, all from a single command. You can build code based on a Dockerfile or that use a Paketo buildpack. You can build from a single step in the CLI as well as from the {{site.data.keyword.codeengineshort}} console. See [Planning your build](/docs/codeengine?topic=codeengine-plan-build). |
| Custom domains | Custom domain mapping | Both services allow you to define and manage external URLs to your workloads. {{site.data.keyword.codeengineshort}} provides support for [custom domains mappings](/docs/codeengine?topic=codeengine-domain-mappings) from the console. You can also add [custom domains](/docs/codeengine?topic=codeengine-deploy-multiple-regions) through {{site.data.keyword.cis_full_notm}} or any other domain provider of your choice. |
{: caption="Terminology" caption-side="bottom"}

For more terms and capabilities for {{site.data.keyword.codeengineshort}}, see [Learn about {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about).

## Log in to {{site.data.keyword.cloud_notm}}
{: #heroku-log-cloud}
{: step}

Follow these steps to log in to your {{site.data.keyword.cloud_notm}} account and target a resource group.

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```txt
    ibmcloud login
    ```
    {: pre}
    
2. Target a resource group by running the following command. To get a list of your resource groups, run **`ibmcloud resource groups`**.

    ```txt
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    Example output

    ```txt 
    Targeted resource group default
    ```
    {: screen}

## Creating a project
{: #heroku-create-project}
{: step}

A [{{site.data.keyword.codeengineshort}} "project"](/docs/codeengine?topic=codeengine-manage-project) groups related workloads into a logical collection. You can group workloads into different projects based on whatever criteria that makes sense to you, for example, company organization structure, dependencies between the workloads, or development versus test versus production environments. You can then [configure access to these projects](/docs/codeengine?topic=codeengine-iam). Keep in mind that workloads within a single project share a private network and are isolated within the security boundary of the project. All workloads within a project can talk to each other freely without concern of being seen by workloads outside of the cluster. If workloads in different projects want to communicate with each other, then the communication must either use the internet or an internal IBM private network. For more information, see [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility). 

    
Create a project in {{site.data.keyword.codeengineshort}} called `sample-proj`.

```txt
ibmcloud ce project create --name sample-proj
```
{: pre}
    
Example output
    
```txt
Creating project 'sample-proj'...
ID for project 'sample-proj' is 'abcdabcd-abcd-abcd-abcd-abcd12e3456f7'.
Waiting for project 'sample-proj' to be active...
Now selecting project 'sample-proj'.
OK
```
{: screen}
   
Notice that your project is also selected for context, so all subsequent application-related commands are within the scope of this new `sample-proj` project.


## Deploying your application
{: #heroku-build2-application}
{: step}

This sample application pulls code from the [sample GitHub repository](https://github.com/IBM/heroku-to-code-engine){: external}. This code is a simple Push your code to {{site.data.keyword.codeengineshort}} by using the **`application create`** command. You must provide a name for your application and the location of the source code. The following example creates an application called `myapp` that uses the `buildpack` strategy and provides the location for the source code in the current directory (`.`). 

```txt
ibmcloud ce app create --name myapp --build-source https://github.com/IBM/heroku-to-code-engine
```
{: pre}

Example output

```txt
Creating application 'myapp'...
Packaging files to upload from source path '.'...
Submitting build run 'myapp-run-220999-210706331'...
Creating image 'private.us.icr.io/ce--6ef04-khxrbwa0lci/app-myapp:220418-0207-askql'...
Waiting for build run to complete...
Build run status: 'Running'
Build run completed successfully.
Run 'ibmcloud ce buildrun get -n myapp-run-220000-210706331' to check the build run status.
Waiting for application 'myapp' to become ready.
Configuration 'myapp' is waiting for a Revision to become ready.
Ingress has not yet been reconciled.
Waiting for load balancer to be ready.
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.abcdbwa0lci.us-south.codeengine.appdomain.cloud
```
{: screen}

And that's it. You now have an internet-facing application. The code in the application itself is the same as what is used for a Heroku application, it's just the {{site.data.keyword.codeengineshort}} commands that are slightly different.

Let's take a deeper look at the previous **`app create`** command. Notice that the output of the **`app create`** command provides information about the progression of the build run before the app is created and deployed.

1. {{site.data.keyword.codeengineshort}} receives a request to create an application from source code (instead of pulling directly from an image). 
2. {{site.data.keyword.codeengineshort}} checks for an IAM service ID and API key that is associated with the selected project. This service ID must be authorized to read and write to {{site.data.keyword.registrylong_notm}}. If no service ID exists, {{site.data.keyword.codeengineshort}} creates one for you. Note that this service ID is used for subsequent {{site.data.keyword.codeengineshort}} build requests that are run from the same project.
3. This example builds code from a public GitHub repository (`--build-source https://github.com/IBM/heroku-to-code-engine`). The source code is packed into an archive file and uploaded to a managed namespace within the {{site.data.keyword.registrylong_notm}} instance in your account. Note that you can target only {{site.data.keyword.registrylong_notm}} for your local builds. For more information about IBM Container Registry, including information about quota limits and access, see [Getting started with IBM Cloud Container Registry](/docs/Registry?topic=Registry-getting-started).
4. {{site.data.keyword.codeengineshort}} builds your source code into an image. The source image is created in the same namespace as your source archive file.
5. After the build completes, your application is deployed. You can access your application from the provided URL.

With {{site.data.keyword.codeengineshort}}, you automatically get many of the same features as Heroku, such as autoscaling and blue-green roll-out of updates, but you'll also enjoy the benefits of newer features such as scaling down-to-zero, ensuring that you are not charged if your application is not active.

Want to learn more about your options for building your source code? See the [**`application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) and the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create) commands.

Want to learn more about applications and jobs? See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads) and [Working with jobs and jobruns](/docs/codeengine?topic=codeengine-job-plan).

## Clean up
{: #heroku-clean-up}

After you finish this tutorial, you can clean up the resources that you created with the following commands.

Delete your application

```txt
ibmcloud ce app delete --name myapp
```
{: pre}

When you delete your app, the associated build files are also deleted.

Lastly, delete the images that the build created from {{site.data.keyword.registrylong_notm}}. 

1. Navigate to [**Registry**](https://cloud.ibm.com/registry/start){: external} in the {{site.data.keyword.cloud_notm}} console.
2. Find the archive and the image that are associated with your application by searching for your application name.
3. Select the archive and image and delete.

## Video transcript
{: #video-transcript-ce}
{: notoc}

Hi, my name is JJ Asghar and I'm a developer advocate for IBM Cloud. Recently, you might have heard about Heroku changing their policy on free -  the free tier. It's causing a challenge for a lot of developers out there so I want to take a handful of moments here to show you how you can migrate from Heroku to Code Engine from IBM Cloud in just a handful of steps. So let's go ahead and start playing around with it and see how quickly you can actually make your system work. 

So first thing first, if you haven't seen it this is the actual line inside the official blog from Heroku, starting on November 28, 2022, we plan to stop free - offering the free product plans and plan on shutting down the free dynos and data services. We'll be sending out a series of email communications to affected users. This is challenging for a lot of beginner beginner web applications. I know for a fact personally I used Heroku when I first started back in the day so this is a pretty large hit for a lot of people and I want to show you how easy it is to convert from Heroku to Code Engine.

So first thing first, let's actually see a nice little application I've created. If I go ahead and start my application here, we have a nice little flask app. If you don't know what python is or flask is, it's a it's a format for python to be able to run an application on a standard port. So let's say we have this application; it says “Hello World!”. I've already deployed it and we can check out right here We have our amazing production app at heroku.com. It says “hello world” and we want to go ahead and change it. We wanted to update it so I'm going to go ahead and quickly update it to “Hello Moving from Heroku to Code Engine”.

Let’s go ahead and come out of it. `git add .` `git commit -m “update hello line”`. Then I'm going to go ahead and push and just like you would normally do to push code to Heroku. I want to show you that this is the exact same process inside of Code Engine. What we'll do is, we'll create a new … we'll log in to IBM Cloud first and then from there we'll create a new project and then we'll go ahead and deploy it to see that it works.

So there we go, we've gone ahead and deployed it to Heroku first ,just to make sure that we all have our working code and I go ahead and reload this and there we go we're moving from Heroku to Code Engine so we know our code works. This is great. 

So now actually let's get Code Engine as part of this, so first thing first, we need to IBM Cloud log in. So I'm going to go ahead and log in to IBM Cloud. If you haven't set up IBM Cloud video or if you haven't set up your IBM Cloud account, if you look above, me you should see a link to it, which I will put into the video.

I'll go ahead and copy my name here and then I'll take my password, log in just fine, which is great to see, perfect. And now what I'll do is `ibmcloud ce project create —name amazing product production app`. So this create our nice, little… Target first. I’ll get my default resource group and then I'll go ahead and create the project. There we go. Should only take a moment - perfect. Now you can change your name to whatever you like. This is just a catch-all for your project, which is useful. Then I will take the next command, which is `ibmcloud ce app create —name pythonbackend — build-source . —strategy build packs`

Now because I already have a requirements.txt, this will be, this application is smart enough to figure out, “hey it's a python application! So let's go ahead and build it!", which is nice. So as you can see, it's taking step one here. It's running the build, which is good. It creates a nice, private image for us too, which is useful. It takes a couple moments. There we go and now we see that if we wanted to do this with no wait, which is the `-nw`, we can actually put this into the background and wait for it to come up and then we can check it via this `build run get` the actual name. Being that we're going to be looking at this live, we'll go ahead and do this here. 

Perfect! So now I go ahead and open up the this URL here and it came over here and as you can see

“hello moving from Heroku to Code Engine”

And that's it. I took the exact same code I did from Heroku. I created a new project and then I created an application and I just pushed it and it just worked so imagine what you can do with that for yourself. This shows the power that is Code Engine and on a free tier it is truly free -  just like Heroku was or will be or was will won't be in the future. Code Engine is free forever, which is great and hopefully, it'll make your life a little easier.

Thanks so much for watching and if you have any questions, my Twitter handle is @jjasghar or you're more than welcome to email me at awesome@ibm.com. My job is to be a personable nerd so never hesitate to reach out.

Thanks so much.

Bye y'all.
