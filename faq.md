---

copyright:
  years: 2020
lastupdated: "2020-08-13"

keywords: code engine, faq

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
{:faq: data-hd-content-type='faq'}

# FAQs 
{: #kn-faqs}

Answers to common questions about the {{site.data.keyword.codeenginefull_notm}} service. 
{:shortdesc}


## What is {{site.data.keyword.codeenginefull_notm}}? 
{: #what-is-codeengine}
{: faq}
{: support}

{{site.data.keyword.codeengineshort}} is an open source platform that was developed by IBM. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps on top of your Kubernetes cluster. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. For more information, see [About {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kn-about).

## What is a Project? 
{: #what-is-project}
{: faq}
{: support}

A project is a grouping of runtime components such as applications and job definitions. The grouping of components is up to you, but typically runtime components that are part of a larger application are grouped. Projects are used to manage resources and provide access to components in the project.

For more information, see [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-kn-about#code-engine-terminology).

## What is an Application?  
{: #what-is-app}
{: faq}
{: support}

An *Application* in a {{site.data.keyword.codeengineshort}} service that runs your code to serve HTTP requests. Applications are organized and run within a defined [Project](#what-is-project).

Build your code in any language, by using your favorite libraries, dependencies, and tools. When you create your Application, you specify where your code resides. The Application has a URL for incoming requests.  

The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. 

An Application contains one or more *revisions* (revision entities). A revision represents an immutable version of the configuration properties of the Application. Each update of an application configuration property creates a new revision of the Application.

## What is a Job?   
{: #what-is-job}
{: faq}
{: support}

A *Job* runs your code in a {{site.data.keyword.codeengineshort}} service to complete a task. 

A job is submitted based on a [Job definition](#what-is-jobdef). After a job definition is created, which contains the workload configuration, you can then run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. The Job runs within a defined [Project](#what-is-project). 

A job can run a large number of instances, which enables work on large volumes of input data in parallel.

## What is a Job definition?   
{: #what-is-jobdef}
{: faq}
{: support}

A *Job definition* is a template that is used to run a [job](#what-is-job), and the template contains workload configuration information. After you create a job definition, you can submit one or more jobs based on the job definition, optionally overwriting values of the job definition.

 ## What is the relationship between a Job and a Job definition?   
{: #what-is-jobvsjobdef}
{: faq}
{: support}

A [job definition](#what-is-jobdef) defines the workload configuration and can be used as a template for a *Job*. 

A [job](#what-is-job) can run one or more containers in a {{site.data.keyword.codeengineshort}} service. Multiple jobs can refer to the same job definition.

While a job definition serves as a template for configuring a job, a functional connection between a job and the job definition does not otherwise exist.

 ## How can I review the {{site.data.keyword.codeengineshort}} service terms?  
{: #review-service-terms}
{: faq}
{: support}
For the latest service level agreement terms, see the [terms of service](/docs/overview/terms-of-use?topic=overview-terms).
