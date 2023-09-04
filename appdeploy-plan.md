---

copyright:
  years: 2020, 2023
lastupdated: "2023-08-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with apps in {{site.data.keyword.codeengineshort}}  
{: #application-workloads}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming requests and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

Before you begin

* If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
* If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} application component.
* Ensure that your app follows the [12-factor app methodology](https://12factor.net/){: external}.

For security features provided with {{site.data.keyword.codeengineshort}}, see [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).

{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Serving CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-serving).

Not sure what type of {{site.data.keyword.codeengineshort}} workload to create? See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
{: tip}

## How do I make my code run as a {{site.data.keyword.codeengineshort}} application component?
{: #deploy-app-containerimage}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you with a streamlined way to run your code as an app. 


- If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create and deploy your app. You can deploy your app with an image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private).

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create and deploy your app. 

- If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code) If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create and deploy your app. 

After your app is deployed, you can also [update your deployed app](/docs/codeengine?topic=codeengine-update-app) by using *any* of the preceding ways, independent of how you created or previously updated your app.

When you deploy your application, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment.


The image that is associated with your specific application revision has a unique container registry digest, and {{site.data.keyword.codeengineshort}} uses this digest for the life of your application revision. If you create a newer version of an image with the same tag as the original image, the original image is overwritten in the container registry and becomes untagged. The newer image is tagged, and this newer image has a different digest. Your {{site.data.keyword.codeengineshort}} application does not use this newer image, because the newer image has a different digest than the  image that is referenced by the application revision. {{site.data.keyword.codeengineshort}} can still create new instances of the application revision as long as the untagged image, which was referenced originally, still exists. For more information, see [Why can't {{site.data.keyword.codeengineshort}} pull an image?](/docs/codeengine?topic=codeengine-image-cannot-pull)
{: important}


The default URL for applications is of the format `https://<appname>.<uuid>.<region>.codeengine.appdomain.cloud` where `appname` is the name of your app, `uuid` is the automatically generated unique identifier, and `region` is the region in which your {{site.data.keyword.codeengineshort}} project resides. The UUID portion of the URL of an application is of the format `aaaabbbbccc`. The automatically generated application URL persists for the lifecycle of the project for your application. 


For more information about endpoints to access applications by region, see [{{site.data.keyword.codeengineshort}} endpoints for accessing applications](/docs/codeengine?topic=codeengine-regions#endpoints-app).


## What do I need to know about ports for apps in {{site.data.keyword.codeengineshort}}?
{: #deploy-app-ports}

By default, {{site.data.keyword.codeengineshort}} assumes that apps listen for incoming connections on port `8080`. In addition, Code Engine sets the `PORT` environment variable to the port value that the application is expected to be listening on. If your app needs to listen on a port other than port `8080`, either deploy your app from the console and specify the correct port or use the `--port` option on the **`app create`** command. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars). The following ports are reserved by {{site.data.keyword.codeengineshort}}:  `8022`, `8008`, `8012`, `9090`, `9091`, and `15090`. Only one port can be exposed as the listening port.


Inbound connections to {{site.data.keyword.codeengineshort}} over HTTP on the Internet use port `80`. Inbound connections to {{site.data.keyword.codeengineshort}} over HTTPS on the Internet use port `443`

If a port scan shows more open ports, see [Why does my port scan show more open ports than expected](/docs/codeengine?topic=codeengine-ts-app-toomanyports)?

## Considerations for HTTP handling
{: #considerationshttphandlingapp}

When you are working with applications (or jobs), it is helpful to be aware of basic HTTP handling in {{site.data.keyword.codeengineshort}}.

- For incoming application connections that use HTTP, the transport layer security (TLS) aspects are managed automatically by {{site.data.keyword.codeengineshort}} outside of the application code. The HTTP Server for the application needs to be concerned about only HTTP connectivity and not HTTPS connectivity. In particular, {{site.data.keyword.codeengineshort}} uses {{site.data.keyword.cis_short}} in {{site.data.keyword.cloud_notm}}, which is based on Cloudflare, as the intrusion prevention system (IPS) for DNS and DDOS protection on layer 4. In other words, the TCP/IP connection that is established on the IPS is owned and managed by Cloudflare. For more information, see [Cloudflare documentation](https://developers.cloudflare.com/fundamentals/get-started/reference/network-ports/#how-to-block-traffic-on-additional-ports){: external}. 

- Internet connections that are bound for {{site.data.keyword.codeengineshort}} applications are automatically redirected to use HTTPS.

- Outbound connections from applications to other {{site.data.keyword.codeengineshort}} applications are automatically protected by TLS. {{site.data.keyword.codeengineshort}} automatically manages this connectivity, so the protocol (or URL) that is used is `HTTP` and not `HTTPS`.

- Outbound connections from applications to non-{{site.data.keyword.codeengineshort}} applications, such as the internet, use `HTTP` or `HTTPS` depending on the protocol that is specified in the app code or URL.  

- Outbound connections from batch jobs use the `HTTP` or `HTTPS` protocol that is specified in the job code or URL. This behavior includes connections from batch jobs to {{site.data.keyword.codeengineshort}} apps. 

## Options for visibility for a {{site.data.keyword.codeengineshort}} application
{: #optionsvisibility}

With {{site.data.keyword.codeengineshort}}, you can determine the right level of visibility for your application by defining the endpoints, or system domain mappings that are available for receiving requests.  
{: shortdesc}

Every application has an *internal* system domain mapping that is visible to all components within the same {{site.data.keyword.codeengineshort}} project, but not outside of the project. In addition to the internal system domain mapping, you choose to make the application visible to either the *public* internet or the {{site.data.keyword.cloud_notm}} *private* network.

You can deploy your application with the following visibility levels:

| Setting | Description |
| --------- | ------------------- |
| [internal (project)](#app-endpoint-projectonly) | An app with this setting can receive requests from components in the same {{site.data.keyword.codeengineshort}} project. Setting an internal (project) endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the same {{site.data.keyword.codeengineshort}} project. This endpoint is always enabled. |
| [public](#app-endpoint-public) | An app with this setting is exposed to the internet and your {{site.data.keyword.codeengineshort}} project. Setting a public endpoint means that your app can receive requests from the public internet or from components within your {{site.data.keyword.codeengineshort}} project. This setting is the default. |
| [private](#app-endpoint-private) | An app with this setting is exposed to the {{site.data.keyword.cloud_notm}} private network and your {{site.data.keyword.codeengineshort}} project. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services by using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project.|
{: caption="Table 1. Visibility for applications" caption-side="bottom"}

You can set the endpoint settings for visibility of an application from the console or with the CLI when you create and deploy, or update your app. 

### Deploying your app with a public endpoint
{: #app-endpoint-public}

When you deploy an app, by default, the application deploys such that it can receive requests from the public internet or from components within the same {{site.data.keyword.codeengineshort}} project. In this case, the app is deployed with a public endpoint.

### Deploying your app with a private endpoint
{: #app-endpoint-private}

You can set the endpoint visibility for your app such that it is deployed with a private endpoint. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services from virtual private endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).

For example, if your solution consists of a component that is running on an {{site.data.keyword.containerfull_notm}} Kubernetes cluster within your own virtual private endpoint and you want to access the {{site.data.keyword.codeengineshort}} application from the {{site.data.keyword.cloud_notm}} private network, you can set the visibility of the application to private. When the visibility of the app is set to private, the app is not accessible through the public internet. The application is still accessible from other applications within the project.

You can [deploy your application with a private endpoint](/docs/codeengine?topic=codeengine-vpe#using-vpes-app) so that the app is only exposed through the {{site.data.keyword.cloud_notm}} private network and not exposed to the external internet. The application is still reachable through shared components from within the internal network and the application endpoint needs to be secured.

With the CLI, set the endpoint visibility for your app so that it is deployed with a private endpoint by using the `--visibility=private` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. You can obtain the available URLs for your app that reflect your endpoint definition by using the [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command.

From the console, set the visibility of endpoints for your app by using the **Endpoints** setting when you create your app. After your app is deployed, you can view and modify these system domain mapping settings on the **Domain mappings** tab on your application page.

For more information about connecting over private networks, see [Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe).

### Deploying your app with a project endpoint
{: #app-endpoint-projectonly}

You can set the endpoint visibility for your app such that it is deployed with an internal (project) endpoint. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the same {{site.data.keyword.codeengineshort}} project. This endpoint is always enabled. Applications are still accessible through shared components and therefore need to be secured.

For example, if your solution consists of several applications within a project, you might set up your solution such that only one of those applications is visible from the internet so that it handles incoming traffic. This public-facing application can delegate work to other applications in your solution so that they do not need to be visible from the internet.

With the CLI, set the endpoint visibility for your app so that it is deployed with a project endpoint by using the `--visibility=project` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. You can obtain the available URLs for your app that reflect your endpoint definition by using the [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command.

From the console, set the visibility of endpoints for your app by using the **Endpoints** setting when you create your app. After your app is deployed, you can view and modify these system domain mapping settings on the **Domain mappings** tab on your application page.

## Options for deploying a {{site.data.keyword.codeengineshort}} application
{: #optionsdeploy}

Learn about the options that you can specify when you deploy your app. Note that options can vary between the console and the CLI.
{: shortdesc}


### Memory and CPU
{: #deploy-app-combo}

When you deploy your app, you can specify the amount of memory and CPU that your app can consume. These amounts can vary, depending on if your app is compute-intensive, memory-intensive, or balanced.
{: shortdesc}

By default, your application is assigned 4 G of memory and 1 vCPU. For more information about selecting memory and CPU, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

### Deploying your app with commands and arguments
{: #deploy-app-cmd-args}

You can define commands and arguments for your application to use at run time.
{: shortdesc}


Define commands and arguments for your application by adding the `--cmd` and `--arg` options to your [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

```txt
ibmcloud ce app create --name myapp --image icr.io/codeengine/hello --cmd /myapp --arg --debug
```
{: pre}

For more information about using `cmd` and `arg`, see [Defining commands and arguments for your {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-cmd-args).

### Creating and running your app with environment variables 
{: #app-option-envvar}

You can define and set environment variables as key-value pairs that can be used by your application at run time. 
{: shortdesc}

You can define environment variables when you create your application, or when you update an existing application from the console or with the CLI. 

For more information about defining environment variables, see [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

{{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the app. For more information about automatically injected environment variables, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

### Creating and running your app when using secrets and configmaps 
{: #app-option-secconfigmap}

In {{site.data.keyword.codeengineshort}}, secrets and configmaps can be consumed by your application by using environment variables. 
{: shortdesc}

Both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

Your application can use environment variables to fully reference a configmap (or secret) or reference individual keys in a configmap (or secret).

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap#configmap-ref).

## Considerations for application quotas
{: #app-quotas}

When you work with applications, functions, and batch jobs, these resources run within the context of a {{site.data.keyword.codeengineshort}} project. Resource quotas are defined on a per project basis, and limits apply for applications, functions, and batch jobs. 

For more information about {{site.data.keyword.codeengineshort}} limits, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Next steps
{: #app-nextsteps}

Now that you are familiar with key concepts of working with {{site.data.keyword.codeengineshort}} applications, are you ready to deploy and work with apps? See

* [Deploying app workloads from images in a public registry](/docs/codeengine?topic=codeengine-deploy-app).
* [Deploying app workloads from images in {{site.data.keyword.registrylong_notm}}](/docs/codeengine?topic=codeengine-deploy-app-crimage).
* [Deploying app workloads from images in a private registry](/docs/codeengine?topic=codeengine-deploy-app-private).
* [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code).
* [Deploying your app from local source code](/docs/codeengine?topic=codeengine-app-local-source-code). 

For more information about working with apps, see

* [Application workloads](/docs/codeengine?topic=codeengine-ceapplications).
* [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).
* [Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-domain-mappings).
* [Integrating {{site.data.keyword.cloud_notm}} services with service bindings](/docs/codeengine?topic=codeengine-service-binding).
* Working with [environment variables](/docs/codeengine?topic=codeengine-envvar), [configmaps](/docs/codeengine?topic=codeengine-configmap), and [secrets](/docs/codeengine?topic=codeengine-secret).
* [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events).
* [Troubleshooting apps](/docs/codeengine?topic=codeengine-troubleshoot-apps).



