---

copyright:
  years: 2020
lastupdated: "2020-09-10"

keywords: getting started, code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



{[css-tiles.md]}

# Getting started with {{site.data.keyword.codeenginefull_notm}} (Beta) 
{: #getting-started}

{{site.data.keyword.codeenginefull}} (or "{{site.data.keyword.codeengineshort}}") provides a platform to unify the deployment of all of your container-based applications. Whether those applications are functions, traditional 12-factor apps, batch workloads or any other container-based workloads, if they can be bundled into a container image, then {{site.data.keyword.codeengineshort}} can host and manage them for you - all on a Kubernetes-based infrastructure. And {{site.data.keyword.codeengineshort}} does this without the need for you to learn, or even know about, Kubernetes. The {{site.data.keyword.codeengineshort}} experience is designed so that you can focus on writing code and not on the infrastructure that is needed to host it.
{: shortdesc}

{{site.data.keyword.codeengineshort}} is available as a beta service. Beta runtimes and services might be unstable or change frequently. Be aware of [beta limitations](/docs/codeengine?topic=codeengine-limits).
{: beta}

Using the console or the CLI, you can [create your project](/docs/codeengine?topic=codeengine-manage-project) and then begin [deploying apps](/docs/codeengine?topic=codeengine-application-workloads) and [running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy).  You can even [build an image](/docs/codeengine?topic=codeengine-build-image) from source code.



<div class=solutionBoxContainer>
  <div class="solutionBox">
    <a href = "#app-hello">
      <div>
        <p><strong>Create an application</p></strong>
        <p class="bx--type-caption">Applications run your code to serve HTTP requests.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#first-job">
      <div>
         <p><strong>Create a job</p></strong>
         <p class="bx--type-caption">Jobs run your code to complete tasks.</p>
      </div>
    </a>
  </div>
  <div class="solutionBox">
    <a href = "#build-image">
      <div>
         <p><strong>Build a container image</p></strong>
         <p class="bx--type-caption">Build a container image from your source code and run it.</p>
      </div>
    </a>
  </div>
</div>

## What are {{site.data.keyword.codeengineshort}} projects, applications, and jobs?
{: #kn-term-summary}

Before you get started, become familiar with some key terms for {{site.data.keyword.codeengineshort}}. 

| Term | Description |
| --------- | ------------------- |
| Project | A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs and builds. Projects are used to manage resources and provide access to its entities.|
| Application | An application, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.|
| Build | A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports Dockerfiles and buildpacks. |
| Job | A job is a stand-alone executable for batch jobs and runs one or more containers. Unlike applications, jobs are meant to be used for running container images that contain an executable that is designed to run one time and then exit. When you create a job, you can specify workload configuration information that is used each time the job is run. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}

## Creating your first {{site.data.keyword.codeengineshort}} app
{: #app-hello}

Create your first {{site.data.keyword.codeengineshort}} app by using the [`Hello`](https://hub.docker.com/r/ibmcom/hello) image in public Docker Hub. When you send a request to your sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned.
{: shortdesc}

1. Access [{{site.data.keyword.codeengineshort}}](https://cloud.ibm.com/codeengine/overview){: external}.
2. Select **Start creating** from **Run your container image**.
3. Select **Application**.
4. Select a project from the list of available projects. You can also [create a new one](/docs/codeengine?topic=codeengine-manage-project#create-a-project). Note that provisioning your project can take a few minutes. Wait until the project status is `Active` before continuing to the next step.
3. After your project is created and the project is in `Active` status, you can create a {{site.data.keyword.codeengineshort}} application. Click the name of your project to open your project page.
4. From the project overview page, click **Application**.
5. Enter a name for the application and specify `ibmcom/hello` for the container image. Use a name for your application that is unique within the project. For this example, you do not need to modify the default values for environment variables or runtime settings.
6. Click **Deploy**. 
7. After the application status changes to **Ready**, you can test the application by clicking **Test application**. To see the running application, click **Application URL**.  

Now that our application is running, let's create a revision by adding an environment variable. From the configuration page for your application: 

1. Click **Env. variables**.
2. Click **Add environment variable**.
3. Enter `TARGET` for name and `Stranger` for value. 
4. Click **Save and deploy** to deploy the application revision. 
5. After the application status changes to **Ready**, you can test the application revision by clicking **Test application**. To see the running application, click **Application URL**. `Hello Stranger` is displayed.
6. You can see the revisions for the application by clicking **Revisions and Traffic** from the navigation. 

Congratulations, you deployed your first application to {{site.data.keyword.codeengineshort}} and tested it out. You then created a revision by adding an environment variable and ran that revision. 

## Running your first {{site.data.keyword.codeengineshort}} job
{: #first-job}

Create your first {{site.data.keyword.codeengineshort}} job by using the [`ibmcom/testjob`](https://hub.docker.com/r/ibmcom/testjob) image in Docker Hub. This job prints `"Hello World"`. 
{: shortdesc}

### Creating the job definition
{: #kn-first-jobdef}

Before you run a job, you can create a job definition. A job definition is a template for how to run your container, so you can specify most runtime configuration settings before you run your job. After you create the job definition, you can then create a job to perform your task.  When you run your job, you can specify the number of instances of that specific job that you want to run as part of your job run.

1. Access your project from the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. Click the name of your project on the Projects page. 
2. From the Components page, click **Job definition** to create the job definition. 
3. From the Create job definition page, provide a name for your job definition name and a container image reference. For this example, let's use the `ibmcom/testjob` container image. 
4. Click **Create**. 

### Running the job 
{: #kn-first-jobrun}

You are now ready to run your job that is based on your job definition.

1. From the job definition page, in the Jobs pane, click **Submit job**. 
2. From the Submit job pane, review and optionally change configuration values such as array indices, CPU, memory, number of job retries, and job timeout. The **Array indices** field specifies how many instances of the job to run by using a list or range of indices. For example, to run 10 instances of the job, specify `1-10` or `0-9`, or use a comma-separated list of indices such as `0-8,10`.
3. Click **Submit job** to run your job. The system displays the status of the instances of your job on the job details page. 
4. If any of the instances of your job failed to run, click **Submit job for failed indices** to run the job again for indices that failed.  From the Submit job pane, review and optionally change the configuration values, including **Array indices**. The Array indices field automatically lists the indices of the failed job run instances. 

When logging is enabled, the expected output of `Hello World` is displayed in the logs. To learn about running jobs with logging enabled, see [Running a job](/docs/codeengine?topic=codeengine-kn-job-deploy). 
{: tip}

Congratulations, you created a job definition and ran your job from the console. 

## Building your source code
{: #build-image}

## Next steps
{: #kn-next}

Learn more about performing these {{site.data.keyword.codeengineshort}} tasks from the console or with the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli):
- [Managing projects](/docs/codeengine?topic=codeengine-manage-project)
- [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads)
- [Running jobs](/docs/codeengine?topic=codeengine-kn-job-deploy)
