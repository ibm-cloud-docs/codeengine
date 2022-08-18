---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with apps in {{site.data.keyword.codeengineshort}}  
{: #application-workloads}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

Before you begin

* If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
* If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} application component.


{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Serving CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-serving).

## How do I make my code run as a {{site.data.keyword.codeengineshort}} application component?
{: #deploy-app-containerimage}

Whether your code exists as source in a local file or in a Git repository, or your code is a container image that exists in a public or private registry, {{site.data.keyword.codeengineshort}} provides you a streamlined way to run your code as an app. 


- If you have a container image, per the [Open Container Initiative (OCI) standard](https://opencontainers.org/){: external}, then you need to provide only a reference to the image, which points to the location of your container registry when you create and deploy your app. You can deploy your app with an image in a [public registry](/docs/codeengine?topic=codeengine-deploy-app) or [private registry](/docs/codeengine?topic=codeengine-deploy-app-private).

- If you are starting with source code that resides in a Git repository, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** operation. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code). If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create and deploy your app. 

- If you are starting with source code that resides on a local workstation, you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image from your source and deploying the app with a **single** CLI command. In this scenario, {{site.data.keyword.codeengineshort}} uploads your image to {{site.data.keyword.registrylong}}. To learn more, see [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code) If you want more control over the build of your image, then you can choose to [build the image](/docs/codeengine?topic=codeengine-build-image) with {{site.data.keyword.codeengineshort}} before you create and deploy your app. 

After your app is deployed, you can also [update your deployed app](/docs/codeengine?topic=codeengine-update-app) by using *any* of the preceding ways, independent of how you created or previously updated your app.

When you deploy your application, the latest version of your referenced container image is downloaded and deployed, unless a tag is specified for the image. If a tag is specified for the image, then the tagged image is used for the deployment.

By default, {{site.data.keyword.codeengineshort}} assumes that apps listen for incoming connections on port `8080`. In addition, Code Engine sets the PORT environment variable to the port value that the application is expected to be listening on. If your app needs to listen on a port other than port `8080`, either deploy your app from the console and specify the correct port or use the `--port` option on the `app create` command. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars). The following ports are reserved by {{site.data.keyword.codeengineshort}}:  `8022`, `8008`, `8012`, `9090`, `9091`, and `15090`. Only one port can be exposed as the listening port.
{: important} 


## Considerations for HTTP handling
{: #considerationshttphandlingapp}

When you are working with applications (or jobs), it is helpful to be aware of basic HTTP handling in {{site.data.keyword.codeengineshort}}.

- For incoming application connections that use HTTP, the transport layer security (TLS) aspects are managed automatically by {{site.data.keyword.codeengineshort}} outside of the application code. The HTTP server for the application needs to be concerned about only HTTP connectivity and not HTTPS connectivity. 

- Internet connections that are bound for {{site.data.keyword.codeengineshort}} applications are automatically redirected to use HTTPS.

- Outbound connections from applications to other {{site.data.keyword.codeengineshort}} applications are automatically protected by TLS. {{site.data.keyword.codeengineshort}} automatically manages this connectivity, so the protocol (or URL) that is used is `HTTP` and not `HTTPS`.

- Outbound connections from applications to non-{{site.data.keyword.codeengineshort}} applications, such as the internet, use `HTTP` or `HTTPS` depending on the protocol that is specified in the app code or URL.  

- Outbound connections from batch jobs use the `HTTP` or `HTTPS` protocol that is specified in the job code or URL. This behavior includes connections from batch jobs to {{site.data.keyword.codeengineshort}} apps. 

## Options for visibility for a {{site.data.keyword.codeengineshort}} application
{: #optionsvisibility}

With {{site.data.keyword.codeengineshort}}, you can determine the right choice of visibility for your application by defining the endpoints that are available for receiving requests.  
{: shortdesc}

You can deploy your application with one of the following visibility choices: 

| Setting | Description |
| --------- | ------------------- |
| [`visibility=public`](#app-endpoint-public) | An app with this setting is exposed to the internet and your {{site.data.keyword.codeengineshort}} project. Setting a public endpoint means that your app can receive requests from the public internet or from components within your {{site.data.keyword.codeengineshort}} project. This setting is the default. |
| [`visibility=private`](#app-endpoint-private) | An app with this setting is exposed to the {{site.data.keyword.cloud_notm}} private network and your {{site.data.keyword.codeengineshort}} project. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} Services by using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).|
| [`visibility=project`](#app-endpoint-projectonly) | An app with this setting is exposed to the {{site.data.keyword.codeengineshort}} project only (cluster-local). Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the {{site.data.keyword.codeengineshort}} environment. |
{: caption="Table 1. Visibility for applications" caption-side="bottom"}

You can set the endpoint settings for visibility of an application from the console or with the CLI when you create and deploy, or update your app. 

### Deploying your app with a public endpoint
{: #app-endpoint-public}

When you deploy an app, by default, the application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. In this case, the app is deployed with a public endpoint.


### Deploying your app with a private endpoint
{: #app-endpoint-private}

You can set the endpoint visibility for your app such that it is deployed with a private endpoint. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services from virtual private endpoints (VPC) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).

For example, if your solution consists of a component that is running on an {{site.data.keyword.containerfull_notm}} Kubernetes cluster within your own virtual private endpoint and you want to access the {{site.data.keyword.codeengineshort}} application from the {{site.data.keyword.cloud_notm}} private network, you can set the visibility of the application to private. When the visibility of the app is set to private, the app is not accessible though the public internet. The application is still accessible from other applications within the project.

You can [deploy your application with a private endpoint](/docs/codeengine?topic=codeengine-vpe#using-vpes-app) so that the app is only exposed through the {{site.data.keyword.cloud_notm}} private network and not exposed to the external internet. The application is still reachable through shared components from within the internal network and the application endpoint needs to be secured.

With the CLI, set the endpoint visibility for your app so that it is deployed with a private endpoint by using the `--visibility=private` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. You can obtain the available URLs for your app that reflect your endpoint definition by using the  [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command.

From the console, set the visibility for your app by using the **Endpoints** setting when you create or update your app. You can view or modify the visibility of your app, and obtain available URLs for your app that reflect your endpoint definition by navigating to your application page and use the **Endpoints** tab.

For more information about connecting over private networks, see [Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe).

### Deploying your app with a project endpoint
{: #app-endpoint-projectonly}

When you deploy an app, by default, the application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. In this case, the app is deployed with a public endpoint. 
{: shortdesc}

You can also set the endpoint visibility for your app such that it is deployed with a project-only endpoint. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the {{site.data.keyword.codeengineshort}} environment. Applications are still accessible through shared components and therefore need to be secured. 

For example, if your solution consists of several applications within a project, you might set up your solution such that only one of those applications is visible from the internet so that it handles incoming traffic. This public-facing application can delegate work to other applications in your solution so that they do not need to be visible from the internet.

With the CLI, set the endpoint visibility for your app so that it is deployed with a project endpoint by using the `--visibility=project` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. You can obtain the available URLs for your app that reflect your endpoint definition by using the  [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command.

From the console set the visibility by using the **Endpoints** setting when you create or update your app. You can view or modify the visibility of your app, and obtain available URLs for your app that reflect your endpoint definition by navigating to your application page and use the **Endpoints** tab.

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

For more information, see [referencing secrets by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#secret-ref) and [referencing configmaps by using environment variables](/docs/codeengine?topic=codeengine-configmap-secret#configmap-ref).


