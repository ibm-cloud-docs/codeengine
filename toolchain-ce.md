---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-09"

keywords: code engine, toolchain and code engine, continuous deliver and code engine, toolchain, code engine cicd

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Integrating {{site.data.keyword.codeengineshort}} workloads with {{site.data.keyword.contdelivery_short}}
{: #toolchain-ce}

You can automate the build and deployment of your {{site.data.keyword.codeenginefull}} workloads by creating a toolchain with {{site.data.keyword.contdelivery_short}}. You can create a toolchain that pulls your source code from a repository and then builds and deploys your app or job. Whenever you update the source code in the repository, the toolchain automatically pulls your updated code and then builds and re-deploys your app or job. 
{: shortdesc}
  
## Before you begin
{: #toolchain-begin}
  
Before you get started with toolchains, 

- Create or identify a [{{site.data.keyword.codeengineshort}} project](/docs/codeengine?topic=codeengine-manage-project#create-a-project). You can create these resources by using either the console or the CLI. For more information, see [{{site.data.keyword.codeengineshort}} projects](/docs/codeengine?topic=codeengine-manage-project#create-a-project).

- Create or identify an instance of the [{{site.data.keyword.contdelivery_short}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started) service.

- Create or identify an {{site.data.keyword.registrylong_notm}} namespace. For more information about creating a namespace, see [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started#getting-started) service.


## Configuring access for your toolchain
{: #permissions-toolchain}

If you want to build and deploy an app or job with a toolchain, set the following permissions in IAM.
  
{{site.data.keyword.registrylong_notm}}
- Reader: To pull the image from Container registry.
- Writer: To push the created image to the target namespace.
- Manager: To create the specified namespace if it does not exist.
- Administrator: To create a service ID, policies, and an API key needed to set up a {{site.data.keyword.codeengineshort}} registry secret to use for the app or job.
  
{{site.data.keyword.codeengineshort}}
- Editor: To access a {{site.data.keyword.codeengineshort}} project or to create one, if it does not exist.
- Writer: To manage apps, jobs, and secrets within the {{site.data.keyword.codeengineshort}} project.
  
Resource Group:
- Viewer: To view the resource group that the {{site.data.keyword.codeengineshort}} project is located in.
  
If you want to your app to bind another {{site.data.keyword.cloud_notm}} service, you must set the following additional permissions.
  
All Identity and Access enabled services
- Administrator: To create a service ID, policies, and API key to set up a {{site.data.keyword.codeengineshort}} service access secret, which is used to maintain service credentials to connect individual services to a {{site.data.keyword.codeengineshort}} app or job.
  
## Creating a toolchain
{: #create-toolchain}  
  
You can create a toolchain from the [Toolchain page](https://cloud.ibm.com/devops/toolchains){: external} by selecting **Create toolchain** and then choosing the {{site.data.keyword.codeengineshort}} template. Want to try a tutorial? See [Develop and deploy an app by using {{site.data.keyword.codeengineshort}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-tutorial-cd-code-engine).

## {{site.data.keyword.codeengineshort}} options in your toolchain
{: #toolchain-options}
  
You can set the following options for your {{site.data.keyword.codeengineshort}} toolchain by editing your `ci-pipeline Configuration` and selecting **Environment properties**.

| Option | Description |
| --------- | ------------------- |
| `apikey` | The {{site.data.keyword.cloud_notm}} API key that is used for this toolchain.  |
| `app-concurrency` | The maximum number of requests that can be processed concurrently per instance. The default value is `100`.  |
| `app-deployment-timeout` | The amount of time, in seconds, that can pass before the build must succeed or fail. |
| `app-health-endpoint` | The app health endpoint; for example, `/health`. |
| `app-max-scale` | The maximum number of instances that can be used for this application. If you set this value to `0`, the application scales as needed. The application scaling is limited only by the instances per the resource quota for the project of your application. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). The default value is `10`.  |
| `app-min-scale` | The minimum number of instances that can be used for this application. This option is useful to ensure that no instances are running when not needed. This value is optional. The default value is `0`.  |
| `app-name` | The name of the application. Use a name that is unique within the project.  |
| `app-port` | The port where the application listens for incoming connections. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c` or `http1`. By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port 8080. |
| `app-visibility` | The visibility for the application. Valid values are `public`, `private`, and `project`. Setting a visibility of `public` means that your app can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. See [Options for visibility for a Code Engine application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility). |
| `branch` | The branch in the repository that contains the buildpacks file or the Dockerfile. The default value is `main`.  |
| `build-size` | The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`, and `xxlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). |
| `build-strategy` | The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. |
| `build-timeout` | The amount of time, in seconds, that can pass before the build run must succeed or fail. The default is `1200` seconds. |
| `build-use-native-docker` | Optional property to opt-in for using native Docker build capabilities instead of the {{site.data.keyword.codeengineshort}} build to containerize the source. You can select this value only if the `build-strategy` is set to `dockerfile`. Valid values are `true` and `false`. |
| `code-engine-project` | The project that contains this application.  |
| `cpu` | The amount of CPU set for the instance of the application. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). The default value is `1`. |
| `deployment-type` | Specifies the type of deployment. Valid values are `application` and `job`.  |
| `ephemeral-storage` | The amount of ephemeral storage to set for the instance of the application. Use `M` for megabytes or `G` for gigabytes. |
| `git-token` | The access token for the Git repository.  |
| `image-name` | The name of the image that is used for this application. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. |
| `memory` | The amount of memory set for the instance of the application. Use M for megabytes or G for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). The default value is `4G`.  |
| `path-to-context` |  The directory in the repository that contains the buildpacks file or the Dockerfile. |
| `path-to-dockerfile` |  The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. |
| `pipeline-debug` | The pipeline debug mode. Value can be `0` or `1`. Default to `0`.  |
| `region` | The region where the {{site.data.keyword.codeengineshort}} project is located.  |
| `registry-namespace` |  The Container registry namespace that stores the built image. |
| `registry-region` | The Container registry region.  |
| `resource-group` | The resource group that contains the {{site.data.keyword.codeengineshort}} project. |
| `service-bindings` | The service binding that binds an {{site.data.keyword.cloud_notm}} service instance to an application. This value is in the format `"{\"<SERVICE_INSTANCE_NAME>\": \"<BINDING_PREFIX>\"}"`. For example, `"{\"object-store-rg-e\": \"CLOUD_OBJECT_STORAGE\"}`. This value must be in base64.  |
{: caption="Table 1. Code Engine options in toolchain" caption-side="bottom"}

For more options, see the **Environment properties** for your pipeline in your toolchain settings.
{: note}


## Troubleshooting toolchain issues
{: #ts-toolchain}

Troubleshoot your {{site.data.keyword.codeengineshort}} toolchain with the following topics.
  
- [Debugging your {{site.data.keyword.codeengineshort}} toolchain](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce).
- [Troubleshooting for toolchains](/docs/ContinuousDelivery?topic=ContinuousDelivery-troubleshoot-toolchains).

  



