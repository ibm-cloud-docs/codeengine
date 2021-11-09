---

copyright:
  years: 2020, 2021
lastupdated: "2021-11-09"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with apps in {{site.data.keyword.codeengineshort}}  
{: #application-workloads}

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

**Before you begin**

* If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
* If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
* Plan a container image for {{site.data.keyword.codeengineshort}} applications. 

{{site.data.keyword.codeengineshort}} provides custom resource definition (CRD) methods. For more information, see [{{site.data.keyword.codeengineshort}} API reference - Serving CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-serving).

## Plan a container image for {{site.data.keyword.codeengineshort}} applications
{: #deploy-app-containerimage}

To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application needs in order to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-build-image) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

Note that when you deploy your application, the most current version of your referenced container image is downloaded and deployed.

By default, {{site.data.keyword.codeengineshort}} assumes that apps listen for incoming connections on port `8080`. In addition, Code Engine sets the PORT environment variable to the port value that the application is expected to be listening on. If your app needs to listen on a port other than port `8080`, either deploy your app from the console and specify the correct port or use the `--port` option on the `app create` command. For more information about environment variables that are set by {{site.data.keyword.codeengineshort}}, see [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).
{: important} 

## Options for visibility for a {{site.data.keyword.codeengineshort}} application
{: #optionsvisibility}

With {{site.data.keyword.codeengineshort}}, you can determine the right choice of visibility for your application by defining the endpoints that are available for receiving requests.  
{: shortdesc}

You can deploy your application with one of the following visibility choices: 


| Setting | Description |
| --------- | ------------------- |
| [`visibility=public`](#app-endpoint-public) | An app with this setting is exposed to the internet and your {{site.data.keyword.codeengineshort}} project. Setting a public endpoint means that your app can receive requests from the public internet or from components within your {{site.data.keyword.codeengineshort}} project.  This is the default setting.|
| [`visibility=private`](#app-endpoint-private) | An app with this setting is exposed to the {{site.data.keyword.cloud_notm}} private network and your {{site.data.keyword.codeengineshort}} project. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} Services using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).|
| [`visibility=project`](#app-endpoint-projectonly) | An app with this setting is exposed to the {{site.data.keyword.codeengineshort}} project only (cluster-local). Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the {{site.data.keyword.codeengineshort}} environment. |
{: caption="Table 1. Visibility for applications" caption-side="bottom"}

### Deploying your app with public endpoint
{: #app-endpoint-public}

When you deploy an app, by default, the application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. In this case, the app is deployed with a public endpoint.


### Deploying your app with a private endpoint
{: #app-endpoint-private}

You can set the endpoint visibility for your app such that it is deployed with a private endpoint. Setting a private endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} services from virtual private endpoints (VPC) or {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local).

For example, if your solution consists of a component that is running on an {{site.data.keyword.containerfull_notm}} Kubernetes cluster within your own virtual private endpoint and you want to access the {{site.data.keyword.codeengineshort}} application from the {{site.data.keyword.cloud_notm}} private network, you can set the visibility of the application to private. When the visibility of the app is set to private, the app is not accessible though the public internet. The application is still accessible from other applications within the project.

You can [deploy your application with a private endpoint](/docs/codeengine?topic=codeengine-vpe#using-vpes-app) so that the app is only exposed through the {{site.data.keyword.cloud_notm}} private network and not exposed to the external internet. The application is still reachable through shared components from within the internal network and the application endpoint needs to be secured.

### Deploying your app with project endpoint
{: #app-endpoint-projectonly}

When you deploy an app, by default, the application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. In this case, the app is deployed with a public endpoint. 
{: shortdesc}

You can also set the endpoint visibility for your app such that it is deployed with a project-only endpoint. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running within the {{site.data.keyword.codeengineshort}} environment. Applications are still accessible through shared components and therefore need to be secured. 

For example, if your solution consists of several applications within a project, you might set up your solution such that only one of those applications is visible from the internet so that it handles incoming traffic. This public-facing application can delegate work to other applications in your solution so that they do not need to be visible from the internet.

You can set the endpoint settings for visibility of an application from the console or with the CLI when you create and deploy, or update your app. 

For example, to create an application with a project-only endpoint with the CLI, add the `--cluster-local` option to your [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command.

```sh
ibmcloud ce app create --name myapp --image ibmcom/hello --cluster-local
```
{: pre}

If you want to obtain the cluster local URL for the application, use the `--output project-url` option with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update), or [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command. For example, 

```sh
ibmcloud ce app get -name myapp --output project-url
```
{: pre}

#### Example output
{: #appget-endpoint-projectonly-example1}

```sh
http://myapp.abcdabcdabc.svc.cluster.local
```
{: screen}

Or, you can also use the [**`app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get details about your app, including the cluster local URL. When you use the cluster local URL, network access from other {{site.data.keyword.codeengineshort}} apps and jobs within the same project to this application remains within the project. For example, when you use the `http://myapp.abcdabcdabc.svc.cluster.local` URL of this `myapp` application, only apps and jobs within the same project can access the app. 

#### Example output
{: #appget-endpoint-projectonly-example2}

```sh
[...]
Name:          myapp
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:                31m
Created:            2021-09-09T14:01:02-04:00
URL:                https://myapp.abcdabcdabc.us-south.codeengine.appdomain.cloud
Cluster Local URL:  http://myapp.abcdabcdabc.svc.cluster.local
Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
Status Summary:     Application deployed successfully

Image:                  ibmcom/hello
[...]
```
{: screen}

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

```sh
ibmcloud ce app create --name myapp --image ibmcom/hello --cmd /myapp --arg --debug
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


