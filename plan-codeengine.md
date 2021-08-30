---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-30"

keywords: planning for code engine, scenarios for code engine, workloads, computation, concurrency, events, latency, app, job, application, use cases

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Planning for {{site.data.keyword.codeengineshort}}
{: #plan-codeengine}

{{site.data.keyword.codeenginefull}} supports two basic workloads: Applications and Jobs.

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.

## {{site.data.keyword.codeengineshort}} use cases
{: #ce-use-cases}

While the use cases for {{site.data.keyword.codeengineshort}} widely vary, here are some examples to get you started.

**Experienced with containers, but no skill or budget for managing clusters**

You are a developer who is knowledgeable about containers. However, you don't want the complexity or time consumption of managing a cluster. With {{site.data.keyword.codeengineshort}}, you do not need to worry about the skills that are required to manage a cluster or the time it takes to do so. Instead, {{site.data.keyword.codeengineshort}} takes these complexities away and the IBM team manages your infrastructure as part of the {{site.data.keyword.cloud_notm}} service. 

**Workloads with intermittent spikes**

Your website is busy on the weekends, but experiences less traffic during the week. Because this website experiences bursts of activity followed by periods of inactivity, {{site.data.keyword.codeengineshort}} is a good solution. With {{site.data.keyword.codeengineshort}}, the website application automatically scales up the application instances for the increase in traffic, and then back down again for the periods of inactivity (even down to zero).

**Batch workloads integrated with storage**

Your batch job processes employee salaries at the end of every month. Because this job runs monthly, it is idle most of the time, but consumes a high amount of CPU and memory when it does runs. The batch job needs to integrate with storage in order to store the results. By using {{site.data.keyword.codeengineshort}}, you can integrate the batch job with {{site.data.keyword.cos_full_notm}} and are charged only for the resources that the job uses when it is running. When the job is idle, it isn't consuming any resources and therefore is not incurring charges. However, the job might incur costs with the {{site.data.keyword.cos_full_notm}} instance.

**Bring your workload**

Part of your job is to create images and deploy them. You are experienced with creating container images and with deploying them, but you want to simplify this process so that you can concentrate on other tasks. With {{site.data.keyword.codeengineshort}}, you can build images and deploy them directly from the same interface, thus simplifying daily tasks and freeing up time to develop more code.

**Testing, proof-of-concepts, or "tire-kicking”**

You are interested in learning more about container-based architecture. Your team developed an application, but wants to test it out before the application is presented to stakeholders. This application is small, so they do not want to pay for even a small, dedicated cluster. In this case, you can test the application and then provide a proof-of-concept of the design to the stakeholders without the cost that a dedicated cluster might require.

## When to use an application or a job
{: #when-app-job}

Applications and jobs are very similar, in the end, they both simply run code. However, there are some key aspects to consider when you decide to structure your code as an app or job,

**Does your code need to respond to an event?**

In the context of {{site.data.keyword.codeengineshort}}, any incoming HTTP request (even the request to load a web page) or a REST API call is considered an event. The concept of being event-driven is often the key factor when you choose between an app or a job because, by definition, apps are run as a result of an HTTP request while jobs are run as of result of an invocation. 

If you know that your workload responds to incoming HTTP requests, then app is the right choice. However, if your workload is run and then done, a job is a better fit.

**How does your code scale?**

Both apps and jobs are scalable. Apps are scaled in response to measurable real-time criteria such as the number of active incoming requests because each instance of your app might be able to process only a certain number of concurrent requests at one time. Jobs are scaled based on how many instances are specified when the job is created. 

If you know that you want a specific number of instances of your code to run, and each instance can be run without an incoming HTTP request, then a job is the right choice. However, if the number of instances must scale dynamically based on the incoming HTTP load, apps are a better fit.

## Common scenarios for {{site.data.keyword.codeengineshort}}
{: #common-scenarios}

Read through some of these common scenarios to gain understanding of when to choose an app and when to choose a job.

### Does your workload require low latency or is it interactive? 
{: #low-latency}

<img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Applications.

If your workload requires a client or user to wait synchronously for the response of the request, and the response must be available within a few milliseconds, use an application. Applications provide an externally-reachable endpoint and respond synchronously to the request. Examples of such workloads are websites, chatbots, and mobile applications.


### Is your computation lightweight and does it require low CPU, memory, and I/O? 
{: #lightweight-computation}

<img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Applications.

If your workload is lightweight and requires low CPU, memory, and I/O, then the concurrent option, available from an application might be helpful. A typical example is an API Server that provides basic operations and is backed with a NoSQL database. These types of requests typically have a small amount of data and require low memory or fewer CPU cycles. With higher concurrency, the application can process the data of a first request while the second request is waiting for I/O. Because the CPU and memory requirements are low, many requests can be run concurrently. 

### Is your computation bound to CPU, memory, or I/O?
{: #bound-computation}

<img src="images/job.svg" alt="Job icon." width="15" style="width:15px; border-style: none"/> <img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Jobs or Applications. 

To process a specific amount of data, where each chunk of the data is large and requires a large amount of CPU and memory, jobs are typically the better choice. However, if the workload requires a request-response pattern, it's also possible to use apps. In both cases, the computation task runs with single concurrency. Each application instance or job task processes only one request or chunk of data concurrently in order to fully leverage the resources that are configured for the instance. Parallelism is achieved by the number of instances or tasks, where the cost of creating an additional task is negligible due to the high resource constraints. A typical example is the processing of image data in a {{site.data.keyword.cos_short}} bucket or serving machine learning models.

### Does your computation run for a long time?
{: #time-intensive}

<img src="images/job.svg" alt="Job icon." width="15" style="width:15px; border-style: none"/> Use Jobs.

If the computation runs for longer durations, jobs are the better choice because of their asynchronous nature. The maximum duration of applications is always limited because maintaining an open connection at scale is expensive. Typical workloads are training machine learning models or hyper-parameter optimization.

### Can you specify the concurrency of your computation upfront? 
{: #known-concurrency}

<img src="images/job.svg" alt="Job icon." width="15" style="width:15px; border-style: none"/> Use Jobs. 

If you know how much computation you need to perform, you can run a job with the exact number of instances until it completes. Typical examples are hyper-parameter tuning or training a neural network.

### Does your workload react to some event?
{: #reactive-workload}

<img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Applications.

If your workload is required to react to an event, such as a Git commit that is pushed to your repository, an object that is uploaded into a {{site.data.keyword.cos_short}} bucket, or a document that is modified within your database, use applications. Applications provide an endpoint that can be configured to receive events from the event source.

### Do you need to process a large amount of data in a short time in response to events or requests? 
{: #large-data}

<img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Applications.

If your workload requires a fast response to unpredicted requests or events, then applications are typically a better fit because applications are scaled dynamically, even from zero.

## Combining apps and jobs 
{: #combine-app-job}

<img src="images/job.svg" alt="Job icon." width="15" style="width:15px; border-style: none"/> <img src="images/application.svg" alt="Application icon." width="15" style="width:15px; border-style: none"/> Use Jobs and Applications.

You can even combine apps and jobs, where an application can start a job to outsource specific computations. Jobs can also query an application. A typical example of a combination of both jobs and apps is training and serving of machine learning models. Jobs are typically used to train the models and applications are used to serve the models.
