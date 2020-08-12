---

copyright:
  years: 2020
lastupdated: "2020-08-12"

keywords: about, code engine

subcollection: codeengine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# About {{site.data.keyword.codeenginefull_notm}}
{: #kn-about}

{{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}") was developed by IBM with the goal of helping you create modern, source-centric, containerized, and serverless apps on top of your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. Each type of app requires an open source or proprietary solution that is tailored to these apps: Cloud Foundry for 12-factor apps, Kubernetes for containers, and OpenWhisk and others for functions. In the past, developers had to decide what approach they wanted to follow, which led to inflexibility and complexity when different types of apps had to be combined.

{{site.data.keyword.codeengineshort}} uses a consistent approach across programming languages and frameworks to abstract the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code. By integrating with Istio, {{site.data.keyword.codeengineshort}} ensures that your serverless and containerized workloads can be easily exposed on the internet, monitored, and controlled, and that your data is encrypted during transit.


## {{site.data.keyword.codeengineshort}} terminology

Learn the basics about {{site.data.keyword.codeengineshort}} by reviewing the following key terms.

|Term|Description|
|---------|-------------------|
| Application | An application, or app, runs your code to serve HTTP requests. An application has a URL for incoming requests. The number of running instances of an application are automatically scaled up or down (to zero) based on incoming workload. An application contains one or more revisions. A revision represents an immutable version of the configuration properties of the application. Each update of an application configuration property creates a new revision of the application.|
| Configmap | A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environmental variables, you can decouple specific information from your deployment and keep your app or job portable. A donfigmap contains information in key-value pairs. You can create a configmap from the console or with the CLI.|
| Job | A job is a stand-alone executable for batch jobs and runs one or more containers according to a *job definition*. Unlike applications, which react to incoming HTTP requests, jobs are meant to be used for running container images that contain an executable that is designed to run one time and then exit. Rather than specifying the full configuration of a job each time it is executed, you can create a job definition. The job definition acts as a template for the job and contains the workload configuration.|
| Job definition | A job definition is a template that contains the workload configuration for a job. After a job definition is created, you can then run one or more jobs that refer to the job definition to perform your task.|
| Project | A project is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you, but typically runtime components that are part of a larger application are grouped. Projects are used to manage resources and provide access to components in the project. A project:<ul><li>Provides a unique namespace for entity names.</li><li> Groups entities and allows operations to work on them at once.</li><li> Manages access to project resources (inbound access).</li><li> Manages access to backing services (outbound access).</li><li> Has an automatically generated certificate for TLS.</li><li> Is based on a Kubernetes namespace.</li></ul> |
| Secret | A secret provides a method to include sensitive configuration information, such as passwords or ssh keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Note that anyone who is authorized to your project can also view your secrets so be sure that you know the secret information can be shared with those users. Secrets contain information in key-value pairs. You can create secrets from the console or with the CLI. |
{: caption="Table 1. {{site.data.keyword.codeengineshort}} Terms" caption-side="bottom"}
