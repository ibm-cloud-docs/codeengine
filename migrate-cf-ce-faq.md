---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-11"

keywords: code engine, tutorial, build, source, application, buildpack, access, build run, image, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ
{: #migrate-cf-ce-faq}

Answers to common questions about migrating your Cloud Foundry applications to {{site.data.keyword.codeengineshort}}.

## Can I use a custom URL with {{site.data.keyword.codeengineshort}}?
{: #customurl}

Yes! You can map your own custom URL to a {{site.data.keyword.codeengineshort}} application by creating a [custom domain mapping](/docs/codeengine?topic=codeengine-domain-mappings) from the {{site.data.keyword.codeengineshort}} console. You can also assign a custom URL through an internet service provider, such as [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-getting-started). For more information about deploying an app with a custom domain through {{site.data.keyword.cis_full_notm}}, see [Configuring a highly available application](/docs/codeengine?topic=codeengine-deploy-multiple-regions). For more information about deploying an app with a custom domain through {{site.data.keyword.cis_short}}, see [Obtaining a custom domain and its TLS certificate and private key](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain).

## My app contains a specific route, Can I use the same route?
{: #sameroute}

You can use the same custom route or domain as long as you control it. If the route is from another source, for example, an IBM-provided route such as  `mybluemix.net`, then you must use the domain that is provided by {{site.data.keyword.codeengineshort}} or else map a new custom domain to your app.

## Can I stop my app?
{: #app_stop}

You cannot stop your app directly, but you can prevent your app from receiving traffic by setting its visibility to `project` and allowing it to scale to 0. For more information, see [How can I stop my app from receiving traffic](/docs/codeengine?topic=codeengine-ts-app-stop-traffic)?

## Why do I have so many app instances?
{: #app_more}

When you update your app, {{site.data.keyword.codeengineshort}} automatically creates a new revision. When the revision is available, traffic is routed to the new instances. While the revision scales up and traffic is transferred to it, the original app instance continues to handle traffic. When the revision is scaled up and all traffic is routed to it, the original app is scaled down. Your app also automatically scales up and down as traffic requires. Check back later to be sure that your app is running the correct number of instances. For more information, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

## Why are my apps slow to respond?
{: #app_response}

Your application scales to zero by default and thus can be slower to respond while it scales back up. You can change this behavior by updating your application and setting the minimum scale to `1` in either the console or from the CLI.

For example, to set the minimum scale to `1` for an application called `myapp` from the CLI,

```txt
ibmcloud ce app update --name myapp --min-scale 1
```
{: pre}

After the application updates, a single instance is always running. Be aware that charges might apply. For more information, see [Pricing for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-pricing).


## Can I route requests to a specific application instance?
{: #specific-app-instance}

No, this functionality is not currently supported. You can approximate this functionality by using [Knative traffic splitting](https://knative.dev/docs/getting-started/first-traffic-split/){: external}. For more information about using Knative with {{site.data.keyword.codeengineshort}}, see [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

## I use a global load balancer with my Cloud Foundry app. Can I migrate it to {{site.data.keyword.codeengineshort}}?
{: #app_glb}

Yes, you can update your global load balancer to point to your {{site.data.keyword.codeengineshort}} app, if you can access the certificate chain and the corresponding private key. The following steps assume that you are using {{site.data.keyword.cis_short}}; however, you can adapt these steps for your own global load balancer.

These steps use the console.

1. Create a domain mapping for your app. When you create your domain mapping, provide your private key and the full certificate chain of the domain(s). For more information, see [Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-domain-mappings). Wait until the domain mappings in all projects are showing a `Ready` state.

2. Open the details of each domain mapping and record the `CNAME` value, for example, `custom.<your-random-id>.us-south.codeengine.appdomain.cloud` or `custom.<your-other-random-id>.us-east.codeengine.appdomain.cloud`.

3. Navigate to the details page for each application and select **Domain mappings** tab and then, select `No external system domain mapping` in the system domain mappings section. This step ensures that your applications are only accessible through the custom domains when called from outside of this project.

4. In your {{site.data.keyword.cis_short}} instance, navigate to **Reliability. > Global load balancers > Origin pools** and edit the existing origin pools by changing the Origin address to the `CNAME` that you recorded earlier.

Your global load balancer is now pointing to your {{site.data.keyword.codeengineshort}} app.

## Does my app need to follow any specifications?
{: #12factor}

Your app must follow the [12-factor app methodology](https://12factor.net/){: external}.

## What types of workloads are available with {{site.data.keyword.codeengineshort}}?
{: #workloads}

{{site.data.keyword.codeengineshort}} supports two types of workloads: Applications and Batch Jobs.

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming requests and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 

A job runs one or more instances of your executable code in parallel. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run.

### Determining the type of workloads that you want
{: #determine-type}

Most Cloud Foundry applications can migrate to {{site.data.keyword.codeengineshort}}. However, if your Cloud Foundry application does not wait for an incoming HTTP request, then jobs are probably the better choice. For more discussion and examples, see [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

## I use manifest files. Are there similar options available with {{site.data.keyword.codeengineshort}}?
{: #manifest}

If you use manifest files for your Cloud Foundry applications, map your manifest attributes to the corresponding {{site.data.keyword.codeengineshort}} features or CLI option.

| Manifest attribute | {{site.data.keyword.codeengineshort}} equivalent on the `ibmcloud ce app create` or `app update` commands |
| -------------- | -------------- |
| `command` | `--command` option |
| `disk_quota` | Implicitly set by {{site.data.keyword.codeengineshort}}. |
| `docker` | Not needed in {{site.data.keyword.codeengineshort}}. |
| `health-check-http-endpoint` | Not needed in {{site.data.keyword.codeengineshort}}. By default a TCP probe is used to know when the application is healthy and ready. |
| `health-check-invocation-timeout` | Not needed in {{site.data.keyword.codeengineshort}}. |
| `instances` | `--min-scale` and `--max-scale` options |
| `memory` | `--memory` option |
| `metadata` | Not currently supported. |
| `no-route` | With the `--cluster-local` option, the application is still accessible from other workloads within the project, but does not include an internet-facing accessible URL that associated with the application. |
| `path` | Not currently applicable. |
| `processes` | Not needed in {{site.data.keyword.codeengineshort}}. The application can create additional processes at run time. |
| `random-route` | Not needed in {{site.data.keyword.codeengineshort}}. Each project has a unique subdomain and since the application name is part of the URL, the URL is guaranteed to be unique. |
| `routes` | Custom routes are not currently supported, but you can use [IBM Cloud Internet Service (CIS) or Cloudflare](#customurl) to front end your application with a custom domain. |
| `sidecars` | Not currently supported. |
| `stack` | Implicitly managed by {{site.data.keyword.codeengineshort}}. |
| `timeout` | Not needed in {{site.data.keyword.codeengineshort}}. |
| Environment variables | `-env` option |
| Services | See the [**`ibmcloud ce app bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. |
{: caption="Markdown coding for tables" caption-side="bottom"}

{{site.data.keyword.codeengineshort}} supports many options that are not available in Cloud Foundry, such as how autoscaling is managed. See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads) and [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

## I know how to deploy an app with Cloud Foundry. What do I need to know to deploy an app in {{site.data.keyword.codeengineshort}}?
{: #deployment}

If you know how to deploy an app with Cloud Foundry, find what you need to know to deploy an app in {{site.data.keyword.codeengineshort}}.

### Push code
{: #push}

With {{site.data.keyword.codeengineshort}}, you can build your code that is sourced in a Git repository or from a local system (CLI-only). Additionally, as with Cloud Foundry (`cf push`), you can build and deploy your app in a single step with both the CLI and the {{site.data.keyword.codeengineshort}} console. For more information, see [How do I make my code run as a {{site.data.keyword.codeengineshort}} application component?](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-containerimage).

### Deployment context
{: #deploy-context}

Cloud Foundry requires an `Org` and a `Space` to push your code into an application. All Cloud Foundry users, by default receive an `Org` and `Space` that are created for them. However, to add new ones, you must set up an `Org` and `Space` target similar to the following example.

```txt
ibmcloud cf create-org MyOrg
ibmcloud target -o <ORGNAME>
ibmcloud target -s dev
```
{: codeblock}

When you then deploy an app with Cloud Foundry, that `Org` and `Space` is targeted for the deployment.

{{site.data.keyword.codeengineshort}} uses the concept of an IBM Cloud resource group and a {{site.data.keyword.codeengineshort}} project.

```txt
ibmcloud target -g <RESOURCE-GROUP>
ibmcloud ce project create --name <PROJECTNAME>
```
{: codeblock}

These commands not only create a project, but "targets" it as well. All subsequent {{site.data.keyword.codeengineshort}} commands run in the context of this project until a different project is targeted by using the **`project select`** command. For more information, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).

### Logs
{: #logs}

{{site.data.keyword.codeengineshort}} provides logs for apps, jobs, and builds to help you determine what happened when deployments do not run properly. You can find logs by running commands similar to the following examples.

```txt
ibmcloud ce app logs -n <APPNAME>
ibmcloud ce jobrun logs -n <JOBRUN-NAME>
ibmcloud ce buildrun logs -n <BUILDRUN_NAME>
```
{: codeblock}

You can also use the {{site.data.keyword.logs_full_notm}} service, which is available for more long-term persistence of log messages. For more information, see [Viewing logs](/docs/codeengine?topic=codeengine-logging).

### Creating a service
{: #create-service}

Creating an instance of a managed service is similar in Cloud Foundry and {{site.data.keyword.codeengineshort}}.

To create a new service to use with your Cloud Foundry application, use the following command.

```txt
ibmcloud cf create-service cloudantNoSQLDB lite myNameCloudant
```
{: codeblock}

To create a new service to use with {{site.data.keyword.codeengineshort}} applications,

```txt
ibmcloud resource service-instance-create myNameCOS cloud-object-storage lite global
```
{: codeblock}

### Service binding
{: #service-binding-cfce}

After you create your application, you can then "bind" your application to the service.

With Cloud Foundry, run the following command.

```txt
ibmcloud cf bind-service appName instanceName
```
{: codeblock}

With {{site.data.keyword.codeengineshort}},

```txt
ibmcloud ce app bind --name appName --service-instance instanceName
```
{: codeblock}

The service instance credentials (coordinates) are injected into the app (or job) by using environment variables. The Cloud Foundry equivalent of `VCAP_SERVICES` in {{site.data.keyword.codeengineshort}} is `CE_SERVICES`. For more information, see [Integrating IBM Cloud service with service binding](/docs/codeengine?topic=codeengine-service-binding).

### Updating an app or job
{: #update-app-job}

After you create your application or job, you can update properties of your workload by using the update command. For example, to update an application in {{site.data.keyword.codeengineshort}},

```txt
ibmcloud ce app update --name <APPNAME> ...
```
{: codeblock}

You can update any of the properties that are available when you create an application or job. For more information, see the following topics.

- [Working with applications](/docs/codeengine?topic=codeengine-application-workloads)
- [Updating an app](/docs/codeengine?topic=codeengine-update-app)
- [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan)
- [Updating a job](/docs/codeengine?topic=codeengine-update-job)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) command


### Runtime support
{: #runtime}

{{site.data.keyword.codeengineshort}} supports many of the runtimes that Cloud Foundry supports. For a list of runtimes that are supported by {{site.data.keyword.codeengineshort}}, see [Cloud Native buildpacks](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat). If you want to use a runtime that is not supported, for example, Swift or Liberty, you can package your app as a container image yourself and [deploy that image in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-deploy-app) without building the image directly from {{site.data.keyword.codeengineshort}}.




## Next steps
{: #migrate-cf-ce-next-faq}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. [Try out {{site.data.keyword.codeengineshort}} with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. Does your application use service bindings? Check out [Migrating your service bindings](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind).
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. **Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ (current page)**

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).
