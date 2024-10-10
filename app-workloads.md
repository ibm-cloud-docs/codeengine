---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-09"

keywords: jobs in code engine, batch jobs in code engine, running jobs with code engine, creating jobs with code engine, images for jobs in code engine, jobs, batch jobs, batch job workloads, job run, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Application workloads
{: #ceapplications}


{{site.data.keyword.codeenginefull}} is designed to address the needs of developers who want their code to run. {{site.data.keyword.codeengineshort}} abstracts the operational burden of building, deploying, and managing workloads in Kubernetes so that developers can focus on what matters most to them: the source code. Developers can deploy and scale their applications, which are written in any framework or language, by delegating the complexity of building and managing their workloads to {{site.data.keyword.codeengineshort}}. Learn about working with applications in {{site.data.keyword.codeenginefull}}.
{: shortdesc}

## What are application workloads?
{: #ceapp-workloads}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming requests and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

## How do apps compare to jobs and functions?
{: #ceapp-workloads-compare}

| Characteristic | App | Job | Function |
| --------- | --------- | --------- | --------- |
| Execution time (duration) | Long-running (10 minutes per request) | Long-running (up to 24 hours) | Short-running (2 minutes or less) |
| Startup latency | Medium | Scheduled start | Low  | 
| Termination | Run-continuously | Run-to-completion | Run-to-completion |
| Invocation | On request or permanently running | Scheduled | On request, instant |
| Programming Model | Container-based build and execution | Container-based build and execution | Language-specific source code files and dependency metadata |
| Parallelism | Parallel execution, flexible | Low to medium parallel execution | High parallel execution |
| Scale-out | Based on number of requests | Based on job workload definition | Based on events or direct invocations |
| Optimized for | Long running, highly complex workload and on-demand scale-out | Scheduled or planned workloads with high resource demands | Startup time and rapid scale-out |
{: caption="Comparing {{site.data.keyword.codeengineshort}} apps, jobs, and functions" caption-side="bottom"}

For more information, see [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

## What are the key features of working with {{site.data.keyword.codeengineshort}} applications?
{: #ceapp-features}

Review the following topics to learn more about working with applications in {{site.data.keyword.codeengineshort}}.

* [Isolation](#ceapp-isolation)
* [Logging](#ceapp-logging)
* [Running applications](#ceapp-runapp)
* [Scaling](#ceapp-scaling)
* [Security](#ceapp-security)
* [Triggering applications with events](#ceapp-eventing)
* [Visibility](#ceapp-visibility)


### Isolation
{: #ceapp-isolation}

{{site.data.keyword.codeengineshort}} is a multi-tenant, regional service where tenants share the same network and compute infrastructure. In particular, the network and compute infrastructure are shared resources and some management components are common to all tenants. However, tenants and their workloads are isolated from each other by using {{site.data.keyword.codeengineshort}} projects. {{site.data.keyword.codeengineshort}} prevents communication between projects, providing isolation to your applications inside a multi-tenant environment. In addition, there are access controls that are performed on a resource level to only allow authorized users to perform certain operations on project resources, such as applications or other {{site.data.keyword.codeengineshort}} workloads.

For more information about workload isolation, see [{{site.data.keyword.codeengineshort}} workload isolation](/docs/codeengine?topic=codeengine-architecture#workload-isolation).

### Logging
{: #ceapp-logging}

When you work with {{site.data.keyword.codeengineshort}} applications with the console and with logging enabled, logs are forwarded to an {{site.data.keyword.la_full_notm}} service instance that is associated with your {{site.data.keyword.codeengineshort}} project. In the {{site.data.keyword.la_short}} service instance, the logs are indexed, enabling full-text search through all generated messages and convenient querying based on specific fields. See [Getting logs for applications](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettinglogs).

System event information can also be helpful to troubleshoot problems when you run jobs. You can view system event information with the CLI. See [Getting system event information for applications](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent).

For more information about logging, see [Viewing logs](/docs/codeengine?topic=codeengine-logging).

### Running applications
{: #ceapp-runapp}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you with a streamlined way to run your code as an app.

You can deploy and run applications in {{site.data.keyword.codeengineshort}} in the following ways:

* Run from an existing container image. Create an application and provide a reference to your image to use when you deploy your app with {{site.data.keyword.codeengineshort}}.

* Run from existing source code without any container image. If you are starting with source code that is located in a Git repository or on your local workstation, you can point to the location of your source and {{site.data.keyword.codeengineshort}} takes care of building the image for you. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks, which inspects your source code to determine how it must be built and packaged as a container image.

For more information about deploying and running applications, see [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads).

### Scaling
{: #ceapp-scaling}

{{site.data.keyword.codeengineshort}} applications scale up or down depending on the incoming requests. Applications follow the *scale-to-zero* model, where no instances are created in the absence of traffic, leading to cost optimization. When there is an incoming request, an app automatically scales up from zero to accommodate the workload.

With {{site.data.keyword.codeengineshort}}, you can control autoscaling by setting the minimum and maximum number of instances. You can also specify the concurrency of the application by specifying the number of requests to run in parallel for a specific application instance to help determine when a new instance is provisioned.

For more information about scaling your app, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).


### Security
{: #ceapp-security}

{{site.data.keyword.codeengineshort}} provides immediate DDOS protection for your application. {{site.data.keyword.codeengineshort}}'s DDOS protection is provided by {{site.data.keyword.cis_short}} at no additional cost to you. DDoS protection covers System Interconnection (OSI) Layer 3 and Layer 4 (TCP/IP) protocol attacks, but not Layer 7 (HTTP) attacks. See [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos).

{{site.data.keyword.codeengineshort}} also provides a service mesh to use its networking layer, which enables mutual Transport Layer Security (TLS) traffic on applications, thus securing *service-to-service* and *user-to-service* communication.

For more information about security, see [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).

### Triggering applications with events
{: #ceapp-eventing}

You can configure your {{site.data.keyword.codeengineshort}} applications to receive cron events, {{site.data.keyword.cos_full_notm}} events, or Kafka topics. When you subscribe to an event producer, you must specify the name of your destination application to receive the events.

For more information about working with event producers, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events).

### Visibility
{: #ceapp-visibility}

With {{site.data.keyword.codeengineshort}}, you can determine the right level of visibility for your application by defining the endpoints, or system domain mappings that are available for receiving requests. An application can be exposed to the internet, to the {{site.data.keyword.cloud_notm}} private network or scoped only to other resources in the same {{site.data.keyword.codeengineshort}} project.

By default, every running application gets its own TLS secured endpoint, which you can map to your own domain.

In addition, you can map your own custom domain to a {{site.data.keyword.codeengineshort}} application to route requests from your custom URL to your application. If you want to target your application with a domain that you own, you can use a custom domain mapping. When you set a custom domain mapping in {{site.data.keyword.codeengineshort}}, you define a 1-to-1 mapping between your fully qualified domain name (FQDN) and a {{site.data.keyword.codeengineshort}} application in your project.

For more information about visibility, see [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility) and [Configuring custom domain mappings for your application](/docs/codeengine?topic=codeengine-domain-mappings).

## How can I get started with applications?
{: #ceapp-getstart}

To deploy a simple {{site.data.keyword.codeengineshort}} application with the `icr.io/codeengine/helloworld` sample image, see [Creating your first {{site.data.keyword.codeengineshort}} app](/docs/codeengine?topic=codeengine-getting-started#app-hello).

Also, you can try an application tutorial, see [Deploying and scaling applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial).

To dive deeper into working with applications, see [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads).
