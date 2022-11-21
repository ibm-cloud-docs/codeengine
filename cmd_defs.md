---

copyright:
  years: 2022
lastupdated: "2022-11-21"

keywords: cli for code engine, command-line interface for code engine, cli commands for code engine, reference for code engine cli, ibmcloud ce, ibmcloud codeengine, commands, code engine cli, apps, jobs, source code, configmap, build repository, build, secret, image repository, registry, example, example output

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.codeenginefull_notm}} CLI
{: #cli}

Run these commands to manage the entities that make up {{site.data.keyword.codeenginefull}}. For more information about {{site.data.keyword.codeengineshort}}, see [Getting started with {{site.data.keyword.codeengineshort}}](/docs/codeengine).
{: shortdesc}

To run {{site.data.keyword.codeenginefull_notm}} commands, use `ibmcloud code-engine` or `ibmcloud ce`.
{: tip}

## Prerequisites
{: #codeengine-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.codeengineshort}} CLI by running the following command:

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}  
  
## Application commands  
{: #cli-application}  

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `application` commands.

For more information about working with apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

You can use either `application` or `app` in your `application` commands. To see CLI help for the `application` commands, run `ibmcloud ce app -h`.
{: tip}

To manage application revisions, see the [`ibmcloud ce revision`](/docs/codeengine?topic=codeengine-cli#cli-revision) commands.  
  
### `ibmcloud ce application bind`  
{: #cli-application-bind}  

Bind an {{site.data.keyword.cloud_notm}} service instance to an application.  
  
```txt
ibmcloud ce application bind --name APP_NAME (--service-instance SI_NAME | --service-instance-id SI_ID)  [--no-wait] [--prefix PREFIX] [--quiet] [--role ROLE] [--service-credential SERVICE_CREDENTIAL] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-bind} 

`--name`, `-n`
:   The name of the application to bind. This value is *required*. 

`--no-wait`, `--nw`
:   Bind the service instance and do not wait for the service binding to be ready. If you specify the `no-wait` option, the service binding creation is started and the command exits without waiting for it to complete. Use the `app get` command to check the application bind status. This value is *optional*. The default value is `false`.

`--prefix`, `-p`
:   A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--role`, `-r`
:   The name of a service role for the new service credential that is created for this service binding. Valid values include `Reader`, `Writer`, `Manager`, or a service-specific role. The option defaults to `Manager` or the first role provided by the service if `Manager` is not supported. This option is ignored if `--service-credential` is specified. This value is *optional*. 

`--service-credential`, `--sc`
:   The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is *optional*. 

`--service-instance`, `--si`
:   The name of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the application. This value is *optional*. 

`--service-instance-id`, `--siid`
:   The GUID of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the application. This value is *optional*. 

`--wait`, `-w`
:   Bind the service instance and wait for the service binding to be ready. If you specify the `--wait` option, the application bind waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the app bind to complete successfully. If the app bind is not completed successfully or fails within the specified `--wait-timeout` period, the command fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the service binding to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `300`.

 
  
#### Example
{: #application-bind-example}

In this example, bind your {{site.data.keyword.languagetranslationshort}} service instance called `langtranslator` to your application called `myapp`.

```txt
ibmcloud ce application bind --name myapp --service-instance langtranslator
```
{: pre}

#### Example output
{: #application-bind-example-output}

```txt
Binding service instance...
Waiting for service binding to become ready...
Status: Pending (Processing Resource)
Status: Pending (Processing Resource)
Status: Creating service binding
Status: Creating service binding
Status: Ready
Waiting for application revision to become ready...
Traffic is not yet migrated to the latest revision.
Ingress has not yet been reconciled.
Waiting for load balancer to be ready
OK
```
{: screen}  
  
### `ibmcloud ce application create`  
{: #cli-application-create}  

Create an application.  
  
```txt
ibmcloud ce application create --name APP_NAME ((--image IMAGE_REF | (--build-source SOURCE [--image IMAGE_REF])) [--argument ARGUMENT] [--build-commit BUILD_COMMIT] [--build-context-dir BUILD_CONTEXT_DIR] [--build-dockerfile BUILD_DOCKERFILE] [--build-git-repo-secret BUILD_GIT_REPO_SECRET] [--build-size BUILD_SIZE] [--build-strategy BUILD_STRATEGY] [--build-timeout BUILD_TIMEOUT] [--cluster-local] [--command COMMAND] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-secret MOUNT_SECRET] [--no-cluster-local] [--no-wait] [--output OUTPUT] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--request-timeout REQUEST_TIMEOUT] [--revision-name REVISION_NAME] [--service-account SERVICE_ACCOUNT] [--user USER] [--visibility VISIBILITY] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-create} 

`-n`, `--name`
:   The name of the application. Use a name that is unique within the project.

   - The name must begin with a lowercase letter.
   - The name must end with a lowercase alphanumeric character.
   - The name must be 63 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).

   This value is *required*. 

`--argument`, `--arg`, `-a`
:   Set arguments for the application. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value overrides the default values that are specified within the container image. This value is *optional*. 

`--build-commit`, `--commit`, `--bcm`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The build commit option is allowed if the `--build-source` option is set to the URL of a Git repository and **not** allowed if the `--build-source` option is not set to the URL of a Git repository. This value is *optional*. 

`--build-context-dir`, `--context-dir`, `--bcdr`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. The build context directory option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. 

`--build-dockerfile`, `--dockerfile`, `--bdf`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. The build dockerfile option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `Dockerfile`.

`--build-git-repo-secret`, `--git-repo-secret`, `--bgrs`, `--grs`, `--repo`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The build Git repository access secret option is allowed if the `--build-source` option is set to the URL of a Git repository and **not** allowed if the `--build-source` option is not set to the URL of a Git repository. This value is *optional*. 

`--build-size`, `--size`, `--bsz`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). The build size option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `medium`.

`--build-source`, `--source`, `--bsrc`, `--src`
:   The URL of the Git repository or the path to local source that contains your source code; for example `https://github.com/IBM/CodeEngine` or `.`. This value is *optional*. 

`--build-strategy`, `--strategy`, `--bstr`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. The build strategy option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. If not specified, the build strategy is determined by {{site.data.keyword.codeengineshort}} if `--build-source` is specified and the source is on your local machine. This value is *optional*. The default value is `dockerfile`.

`--build-timeout`, `--bto`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. The build timeout option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `600`.

`--cluster-local`, `--cl`
:   Deploy the application with a project-only endpoint. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project. This value is *optional*. The default value is `false`.

`--command`, `--cmd`, `-c`
:   Set commands for the application. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--concurrency`, `--cn`
:   The maximum number of requests that can be processed concurrently per instance. This value is *optional*. The default value is `100`.

`--concurrency-target`, `--ct`
:   The threshold of concurrent requests per instance at which one or more additional instances are created. Use this value to scale up instances based on concurrent number of requests. If `--concurrency-target` is not specified, this option defaults to the value of the `--concurrency` option. This value is *optional*. The default value is `0`.

`--cpu`
:   The amount of CPU set for the instance of the application. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `1`.

`--env`, `-e`
:   Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   - To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage to set for the instance of the application. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` or `--mount-configmap` options. Secret references are specified with the `--env-from-secret`, `--mount-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The name of the image that is used for this application. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. The image option is required if the `--build-source` option is not specified. This value is *optional*. 

`--max-scale`, `--max`, `--maxscale`
:   The maximum number of instances that can be used for this application. If you set this value to `0`, the application scales as needed. The application scaling is limited only by the instances per the resource quota for the project of your application. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). This value is *optional*. The default value is `10`.

`--memory`, `-m`
:   The amount of memory set for the instance of the application. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `4G`.

`--min-scale`, `--min`, `--minscale`
:   The minimum number of instances that can be used for this application. This option is useful to ensure that no instances are running when not needed. This value is *optional*. The default value is `0`.

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of your application container by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of your application container by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`--no-cluster-local`, `--ncl`
:   Deploy the application with a public endpoint. The application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. This value is *optional*. The default value is `true`.

`--no-wait`, `--nw`
:   Create the application and do not wait for the application to be ready. If you specify the `--no-wait` option, the application create begins and does not wait. Use the `app get` command to check the application status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, `jsonpath-as-json=JSONPATH_EXPRESSION`, `url`, and `project-url`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--port`, `-p`
:   The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your application needs to listen on a port other than port `8080`, use `--port` to specify the port. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--request-timeout`, `--rt`, `--timeout`, `-t`
:   The amount of time in seconds that can pass before requests made to the application must succeed or fail. This value is *optional*. The default value is `300`.

`--rn`, `--revision-name`
:   The name of the revision. Use a name that is unique within the application.

   - The name can contain lowercase letters, numbers, and hyphens (-).
   - The name must end with a lowercase alphanumeric character.
   - The fully qualified revision name must be in the format, `Name_of_application`-`Name of revision`.
   - The fully qualified revision name must be 63 characters or fewer.

   This value is *optional*. 

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--user`, `-u`
:   The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is *optional*. The default value is `0`.

`--visibility`, `-v`
:   The visibility for the application. Valid values are `public`, `private` and `project`. Setting a visibility of `public` means that your app can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. Setting a visibility of `private` means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project. Visibility can only be `private` if the project supports application private visibility. Setting a visibility of `project` means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project. This value is *optional*. 

`--wait`, `-w`
:   Create the application and wait for the application to be ready. If you specify the `--wait` option, the application create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become ready. If the application is not ready within the specified `wait-timeout` period, the application create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the application to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #application-create-example}

```txt
ibmcloud ce application create --name myapp --image icr.io/codeengine/hello
```
{: pre}

#### Example output
{: #application-create-example-output}

```txt
Creating application 'myapp'...
[...]
Run `ibmcloud ce application get -n 'myapp'` to check the application status.
OK

https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}

When you run `ibmcloud ce application get -n 'myapp'` to check the application status, the URL for your application is displayed.  
{: tip}  
  
### `ibmcloud ce application delete`  
{: #cli-application-delete}  

Delete an application.  
  
```txt
ibmcloud ce application delete --name APPLICATION_NAME [--force] [--ignore-not-found] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-delete} 

`--name`, `-n`
:   The name of the application. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Delete the application and do not wait for the application to be deleted. If you specify the `no-wait` option, the application delete begins and does not wait. Use the `app get` command to check the application status. This value is *optional*. The default value is `true`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the application and wait for the application to be deleted. If you specify the `--wait` option, the application delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become deleted. If the application is not deleted within the specified `--wait-timeout` period, the application delete fails. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the application to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #application-delete-example}

```txt
ibmcloud ce application delete --name myapp -f
```
{: pre}

#### Example output
{: #application-delete-example-output}

```txt
Deleted application 'myapp'
```
{: screen}  
  
### `ibmcloud ce application events`  
{: #cli-application-events}  

Display the events of application instances.  
  
```txt
ibmcloud ce application events (--instance APP_INSTANCE | --application APP_NAME) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-events} 

`--application`, `--app`, `-a`, `--name`, `-n`
:   Display the events of all the instances of the specified application. This value is required if `--instance` is not specified. 

`--instance`, `-i`
:   The name of a specific application instance. Use the `app get` command to find the instance name. This value is required if `--application` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #application-events-example}

The following example displays the system event information for all the instances of a specified application.   

```txt
ibmcloud ce application events --application myapp 
```
{: pre}

##### Example output
{: #application-events-example-output}

```txt
Getting events for all instances of application 'myapp'...
OK

myapp-atfte-1-deployment-6b49c5fb85-kf4m2:
    Type    Reason     Age  Source                Messages
    Normal  Scheduled  31s  default-scheduler     Successfully assigned 4svg40kna19/myapp-atfte-1-deployment-6b49c5fb85-kf4m2 to 10.240.0.15
    Normal  Pulling    29s  kubelet, 10.240.0.15  Pulling image "icr.io/codeengine/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
    Normal  Pulled     24s  kubelet, 10.240.0.15  Successfully pulled image "icr.io/codeengine/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6" in 4.907426108s
    Normal  Created    24s  kubelet, 10.240.0.15  Created container user-container
    Normal  Started    24s  kubelet, 10.240.0.15  Started container user-container
    Normal  Pulled     24s  kubelet, 10.240.0.15  Container image "icr.io/obs/codeengine/knative-serving/queue-39be6f1d08a095bd076a71d288d295b6:v0.20.0-rc1@sha256:8988bea781130827b3e1006e6e5e7f49094343a5505c1927bb832be3470455f6" already present on machine
    Normal  Created    23s  kubelet, 10.240.0.15  Created container queue-proxy
    Normal  Started    23s  kubelet, 10.240.0.15  Started container queue-proxy
```
{: screen}

#### Example of system event information for specified instance of an app
{: #application-events-example2}

The following example displays the system event information for a specified instance of an app. Use the **`app get`** command to display details about your app, including the running instances of the app.

```txt
ibmcloud ce application events --instance myapp-li17x-1-deployment-69fd57bcb6-sr9tl
```
{: pre}

##### Example output of system event information for specified instance of an app
{: #application-events-example2-output}

```txt
Getting events for application instance 'myapp-li17x-1-deployment-69fd57bcb6-sr9tl'...
OK

myapp-li17x-1-deployment-69fd57bcb6-sr9tl:
    Type     Reason     Age                    Source                Messages
    Normal   Scheduled  6m40s                  default-scheduler     Successfully assigned 4svg40kna19/myapp-li17x-1-deployment-69fd57bcb6-sr9tl to 10.240.64.6
    Normal   Pulling    6m39s                  kubelet, 10.240.64.6  Pulling image "icr.io/codeengine/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
    Normal   Pulled     6m36s                  kubelet, 10.240.64.6  Successfully pulled image "icr.io/codeengine/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
    Normal   Created    6m34s                  kubelet, 10.240.64.6  Created container user-container
    Normal   Started    6m33s                  kubelet, 10.240.64.6  Started container user-container
    Normal   Pulled     6m33s                  kubelet, 10.240.64.6  Container image "icr.io/obs/codeengine/knative-serving/queue-39be6f1d08a095bd076a71d288d295b6:v0.19.0-rc3@sha256:9cb525af53896afa6b5210b5ac56a893cf85b6cd013a61cb6503a005e40c5c6f" already present on machine
    Normal   Created    6m33s                  kubelet, 10.240.64.6  Created container queue-proxy
    Normal   Started    6m32s                  kubelet, 10.240.64.6  Started container queue-proxy
    [...]
```
{: screen}  
  
### `ibmcloud ce application get`  
{: #cli-application-get}  

Display the details of an application.  
  
```txt
ibmcloud ce application get --name APPLICATION_NAME [--output OUTPUT] [--quiet] [--show-all-revisions]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-get} 

`--name`, `-n`
:   The name of the application. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, `jsonpath-as-json=JSONPATH_EXPRESSION`, `url`, and `project-url`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--show-all-revisions`, `-r`
:   Show all revisions for this application. If not specified, only revisions which are configured to receive traffic are shown. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #application-get-example}

```txt
ibmcloud ce application get --name myapp
```
{: pre}

#### Example output
{: #application-get-example-output}

```txt
Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
OK

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

Image:                  icr.io/codeengine/hello

Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

Revisions:
    myapp-atfte-1:
        Age:                3d6h
    Traffic:            100%
    Image:              icr.io/codeengine/hello (pinned to f0dc03)
    Running Instances:  1

Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  0
    Timeout:        300

Conditions:
    Type                 OK    Age   Reason
    ConfigurationsReady  true  3d6h
    Ready                true  3d6h
    RoutesReady          true  3d6h

Events:
    Type    Reason   Age    Source              Messages
    Normal  Created  3m55s  service-controller  Created Configuration "myapp"
    Normal  Created  3m54s  service-controller  Created Route "myapp"

Instances:
    Name                                       Revision       Running  Status   Restarts  Age
    myapp-00002-deployment-8495f8ccb9-kmc57    myapp-00002    3/3      Running  0         27m
```
{: screen}  
  
### `ibmcloud ce application list`  
{: #cli-application-list}  

List all applications in a project.  
  
```txt
ibmcloud ce application list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #application-list-example}

```txt
ibmcloud ce app list --sort-by age
```
{: pre}

#### Example output
{: #application-list-example-output}

```txt
Listing all applications...
OK

Name           Status  URL                                                                    Latest                 Age   Conditions  Reason
myapptestapp2  Ready   https://myapptestapp2.4svg40kna19.us-south.codeengine.appdomain.cloud  myapptestapp2-emy0q-1  52s   3 OK / 3
myapptestapp1  Ready   https://myapptestapp1.4svg40kna19.us-south.codeengine.appdomain.cloud  myapptestapp1-ps4ca-1  104s  3 OK / 3
myapp-e        Ready   https://myapp-e.4svg40kna19.us-south.codeengine.appdomain.cloud        myapp-e-gx6xa-1        12m   3 OK / 3
myappd         Ready   https://myappd.4svg40kna19.us-south.codeengine.appdomain.cloud         myappd-lxjxm-1         13m   3 OK / 3
myappc         Ready   https://myappc.4svg40kna19.us-south.codeengine.appdomain.cloud         myappc-qffan-1         14m   3 OK / 3
myappb         Ready   https://myappb.4svg40kna19.us-south.codeengine.appdomain.cloud         myappb-i3hw3-1         15m   3 OK / 3
myapp          Ready   https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud          myapp-jmxwd-1          17m   3 OK / 3
```
{: screen}  
  
### `ibmcloud ce application logs`  
{: #cli-application-logs}  

Display the logs of application instances.  
  
```txt
ibmcloud ce application logs (--instance APP_INSTANCE | --application APP_NAME) [--all-containers] [--follow] [--output OUTPUT] [--quiet] [--raw] [--tail TAIL] [--timestamps]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-logs} 

`--all-containers`, `--all`
:   Display the logs of all containers of the specified application instances. This value is *optional*. The default value is `false`.

`--application`, `--app`, `-a`, `--name`, `-n`
:   Display the logs of all the instances of the specified application. This value is required if `--instance` is not specified. 

`--follow`, `-f`
:   Follow the logs of application instances. Use this option to stream logs of application instances. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is *optional*. The default value is `false`.

`--instance`, `-i`
:   The name of a specific application instance. Use the `app get` command to find the instance name. This value is required if `--application` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--raw`, `-r`
:   Display logs without instance and container labels. This value is *optional*. The default value is `false`.

`--tail`, `-t`
:   Limit the display of logs of containers of the specified application instances to a maximum number of recent lines per container. For example, to display the last `3` lines of the logs of the containers of the specified application instances, specify `--tail 3`. If this option is not specified, all lines of the logs of the containers of the specified application instances are displayed. This value is *optional*. The default value is `-1`.

`--timestamps`, `--ts`
:   Include timestamps on each line in the log output. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #application-logs-example}

The following example displays the logs of a specific instance of an app. Use the **`app get`** command to obtain the name of the app instances. 

```txt
ibmcloud ce application logs --instance myapp-zhk9x-1-deployment-6f955f5cc5-abcde
```
{: pre}

#### Example output
{: #application-logs-example-output}

```txt
Getting logs for application instance 'myapp-zhk9x-1-deployment-6f955f5cc5-abcde'...
OK

myapp-zhk9x-1-deployment-6f955f5cc5-abcde:
Server running at http://0.0.0.0:8080/
```
{: screen}

#### Example of logs of all instances of an app
{: #application-logs-example2}

The following example displays the logs of all the instances of an app.   

```txt
ibmcloud ce application logs --app myapp
```
{: pre}

##### Example output of logs of all instances of an app
{: #application-logs-example2-output}

```txt
Getting application 'myapp'...
Getting revisions for application 'myapp'...
Getting instances for application 'myapp'...
Getting logs for all instances of application 'myapp'...
OK

myapp-zhk9x-1-deployment-6f955f5cc5-abcde:
Server running at http://0.0.0.0:8080/
```
{: screen}
  
  
### `ibmcloud ce application restart`  
{: #cli-application-restart}  

Restart running application instances.  
  
```txt
ibmcloud ce application restart (--instance APP_INSTANCE | --application APP_NAME) [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-restart} 

`--application`, `--app`, `-a`, `--name`, `-n`
:   Restart all the running instances of the specified application. This value is required if `--instance` is not specified. 

`--instance`, `-i`
:   The name of a specific application instance. Use the `app get` command to find the instance name. This value is required if `--application` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #application-restart-example}

```txt
ibmcloud ce application restart --name myapp 
```
{: pre}

#### Example output
{: #application-restart-example-output}

```txt
Restarting all running instances of application 'myapp'...
OK
```
{: screen}  
  
### `ibmcloud ce application unbind`  
{: #cli-application-unbind}  

Unbind {{site.data.keyword.cloud_notm}} service instances from an application.  
  
```txt
ibmcloud ce application unbind --name APP_NAME (--binding BINDING_NAME | --all) [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-unbind} 

`--name`, `-n`
:   The name of the application to unbind. This value is *required*. 

`--all`, `-A`
:   Unbinds all service instances for this application. This value is required if `--binding` is not specified. The default value is `false`.

`--binding`, `-b`
:   The name of the binding to unbind. Run `ibmcloud ce app get -n APP_NAME` to view binding names. This value is required if `--all` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #application-unbind-example}

In this example, remove all bindings from your application called `myapp`.

```txt
ibmcloud ce application unbind --name myapp --all
```
{: pre}

#### Example output
{: #application-unbind-example-output}

```txt
Removing service bindings...
OK
```
{: screen}  
  
### `ibmcloud ce application update`  
{: #cli-application-update}  

Update an application. Updating your application creates a revision. When calls are made to the application, traffic is routed to the revision.  
  
```txt
ibmcloud ce application update --name APP_NAME [--argument ARGUMENT] [--arguments-clear] [--build-clear] [--build-commit BUILD_COMMIT] [--build-commit-clear] [--build-context-dir BUILD_CONTEXT_DIR] [--build-dockerfile BUILD_DOCKERFILE] [--build-git-repo-secret BUILD_GIT_REPO_SECRET] [--build-git-repo-secret-clear] [--build-size BUILD_SIZE] [--build-source BUILD_SOURCE] [--build-strategy BUILD_STRATEGY] [--build-timeout BUILD_TIMEOUT] [--cluster-local] [--command COMMAND] [--commands-clear] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--image IMAGE] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-rm MOUNT_RM] [--mount-secret MOUNT_SECRET] [--no-cluster-local] [--no-wait] [--output OUTPUT] [--port PORT] [--quiet] [--rebuild] [--registry-secret REGISTRY_SECRET] [--registry-secret-clear] [--request-timeout REQUEST_TIMEOUT] [--revision-name REVISION_NAME] [--service-account SERVICE_ACCOUNT] [--service-account-clear] [--user USER] [--visibility VISIBILITY] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-application-update} 

`--name`, `-n`
:   The name of the application. This value is *required*. 

`--argument`, `--arg`, `-a`
:   Set arguments for the application. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is *optional*. 

`--arguments-clear`, `--ac`
:   Clear application arguments. This value is *optional*. The default value is `false`.

`--build-clear`, `--bc`
:   Remove the association of a build from this application. The build clear option is only allowed if your app currently has an associated build. This value is *optional*. The default value is `false`.

`--build-commit`, `--commit`, `--bcm`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The build commit option is allowed if the `--build-source` option is set to the URL of a Git repository on this `app update` command, or your application currently has an associated build from a Git repository source. This value is *optional*. 

`--build-commit-clear`, `--commit-clear`, `--bcmc`, `--cmc`
:   Clear the commit, tag, or branch in the source repository to pull. The commit clear option is allowed if your application currently has an associated build. This value is *optional*. The default value is `false`.

`--build-context-dir`, `--context-dir`, `--bcdr`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. The build context directory option is allowed if the `--build-source` option is set on this `app update` command, or your application currently has an associated build. This value is *optional*. 

`--build-dockerfile`, `--dockerfile`, `--bdf`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. The build dockerfile option is allowed if the `--build-source` option is set on this `app update` command, or your application currently has an associated build. This value is *optional*. The default value is `Dockerfile`.

`--build-git-repo-secret`, `--git-repo-secret`, `--bgrs`, `--grs`, `--repo`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The build Git repository access secret option is allowed if the `--build-source` option is set to the URL of a Git repository on this `app update` command, or your application currently has an associated build from a Git repository source. This value is *optional*. 

`--build-git-repo-secret-clear`, `--git-repo-secret-clear`, `--bgrsc`, `--grsc`
:   Clear the Git repository access secret. The Git repository access secret clear option is allowed if your application currently has an associated build. This value is *optional*. The default value is `false`.

`--build-size`, `--size`, `--bsz`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). The build size option is allowed if the `--build-source` option is set on this `app update` command, or your application currently has an associated build. This value is *optional*. The default value is `medium`.

`--build-source`, `--source`, `--bsrc`, `--src`
:   The URL of the Git repository or the path to local source that contains your source code; for example `https://github.com/IBM/CodeEngine` or `.`. This value is *optional*. 

`--build-strategy`, `--strategy`, `--bstr`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. The build strategy option is allowed if the `--build-source` option is set on this `app update` command, or your application currently has an associated build. If not specified, the build strategy is determined by {{site.data.keyword.codeengineshort}} if `--build-source` is specified and the source is on your local machine. This value is *optional*. The default value is `dockerfile`.

`--build-timeout`, `--bto`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. The build timeout option is allowed if the `--build-source` option is set on this `app update` command, or your application currently has an associated build. This value is *optional*. The default value is `600`.

`--cluster-local`, `--cl`
:   Deploy the application with a project-only endpoint. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project. This value is *optional*. The default value is `false`.

`--command`, `--cmd`, `-c`
:   Set commands for the application. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--commands-clear`, `--cc`
:   Clear application commands. This value is *optional*. The default value is `false`.

`--concurrency`, `--cn`
:   The maximum number of requests that can be processed concurrently per instance. This value is *optional*. The default value is `0`.

`--concurrency-target`, `--ct`
:   The threshold of concurrent requests per instance at which one or more additional instances are created. Use this value to scale up instances based on concurrent number of requests. If `--concurrency-target` is not specified, this option defaults to the value of the `--concurrency` option. This value is *optional*. The default value is `0`.

`--cpu`
:   The amount of CPU set for the instance of the application. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `0`.

`--env`, `-e`
:   Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   - To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-from-configmap-rm`, `--env-cm-rm`
:   Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This option can be specified multiple times. This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--env-from-secret-rm`, `--env-sec-rm`
:   Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This option can be specified multiple times. This value is *optional*. 

`--env-rm`
:   Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This option can be specified multiple times. This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage to set for the instance of the application. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` or `--mount-configmap` options. Secret references are specified with the `--env-from-secret`, `--mount-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The name of the image that is used for this application. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is *optional*. 

`--max-scale`, `--max`, `--maxscale`
:   The maximum number of instances that can be used for this application. If you set this value to `0`, the application scales as needed. The application scaling is limited only by the instances per the resource quota for the project of your application. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits). This value is *optional*. The default value is `0`.

`--memory`, `-m`
:   The amount of memory set for the instance of the application. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. 

`--min-scale`, `--min`, `--minscale`
:   The minimum number of instances that can be used for this application. This value is *optional*. The default value is `0`.

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of your application container by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-rm`
:   Remove the contents of a configmap or secret from the file system of your application container by specifying the directory where the configmap or secret is mounted. Specify one mount directory per `--mount-rm` option; for example, `--mount-rm /etc/configmap-a --mount-rm /etc/secret-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of your application container by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`--no-cluster-local`, `--ncl`
:   Deploy the application with a public endpoint. The application deploys such that it can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. This value is *optional*. The default value is `true`.

`--no-wait`, `--nw`
:   Update the application and do not wait for the application to be ready. If you specify the `no-wait` option, the application update begins and does not wait. Use the `app get` command to check the application status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, `jsonpath-as-json=JSONPATH_EXPRESSION`, `url`, and `project-url`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--port`, `-p`
:   The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your application needs to listen on a port other than port `8080`, use `--port` to specify the port. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--rebuild`
:   Rebuild image from source. The rebuild option is allowed if your application currently has an associated build. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--registry-secret-clear`, `--rsc`
:   Clear the image registry access secret. This value is *optional*. The default value is `false`.

`--request-timeout`, `--rt`, `--timeout`, `-t`
:   The amount of time in seconds that can pass before requests made to the application must succeed or fail. This value is *optional*. The default value is `0`.

`--rn`, `--revision-name`
:   The name of the revision. Use a name that is unique within the application.

   - The name can contain lowercase letters, numbers, and hyphens (-).
   - The name must end with a lowercase alphanumeric character.
   - The fully qualified revision name must be in the format, `Name_of_application`-`Name of revision`.
   - The fully qualified revision name must be 63 characters or fewer.

   This value is *optional*. 

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--service-account-clear`, `--sac`
:   Clear the service account. This value is *optional*. The default value is `false`.

`--user`, `-u`
:   The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is *optional*. The default value is `0`.

`--visibility`, `-v`
:   The visibility for the application. Valid values are `public`, `private` and `project`. Setting a visibility of `public` means that your app can receive requests from the public internet or from components within the {{site.data.keyword.codeengineshort}} project. Setting a visibility of `private` means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.cloud_notm}} using Virtual Private Endpoints (VPE) or {{site.data.keyword.codeengineshort}} components that are running in the same project. Visibility can only be `private` if the project supports application private visibility. Setting a visibility of `project` means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project. This value is *optional*. 

`--wait`, `-w`
:   Update the application and wait for the application to be ready. If you specify the `--wait` option, the application update waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become ready. If the application is not ready within the specified `--wait-timeout` period, the application create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the application to be updated. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #application-update-example}

```txt
ibmcloud ce application update --name myapp --image icr.io/codeengine/hello
```
{: pre}

#### Example output
{: #application-update-example-output}

```txt
Updating application 'myapp' to latest revision.
[...]
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}  
  
## Build commands  
{: #cli-build}  

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks. Use `build` commands to create, display details, update, and delete build configurations. After you create a build configuration, one or more [`buildrun` commands](#cli-buildrun) can be submitted based on the build configuration.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `build` commands.

For more information about working with builds, see [Building a container image](/docs/codeengine?topic=codeengine-build-image).

You can use either `build` or `bd` in your `build` commands. To see CLI help for the `build` commands, run `ibmcloud ce build -h`.
{: tip}  
  
### `ibmcloud ce build create`  
{: #cli-build-create}  

Create a build.  
  
```txt
ibmcloud ce build create --name BUILD_NAME [--build-type BUILD_TYPE] [--commit COMMIT] [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--force] [--git-repo-secret GIT_REPO_SECRET] [--image IMAGE] [--output OUTPUT] [--quiet] [--registry-secret REGISTRY_SECRET] [--size SIZE] [--source SOURCE] [--strategy STRATEGY] [--timeout TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-build-create} 

`-n`, `--name`
:   The name of the build. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).

   This value is *required*. 

`--build-type`, `--bt`
:   The type of build. Valid values are `git` and `local`. If the type of build is `local`, then the `--source`, `--commit`, and `--git-repo-secret` options are not valid. This value is *optional*. The default value is `git`.

`--commit`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The commit option is allowed if the `--build-type` option is `git` and not allowed if the `--build-type` option is `local`. This value is *optional*. 

`--context-dir`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. This value is *optional*. 

`--dockerfile`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is *optional*. The default value is `Dockerfile`.

`--force`, `-f`
:   Do not verify the existence of specified secret references. Secret references are specified with the `--get-repo-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--git-repo-secret`, `--grs`, `--repo`, `-r`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The git-repo-secret option is allowed if the `--build-type` option is `git` and not allowed if the `--build-type` option is `local`. This value is *optional*. 

`--image`, `-i`
:   The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The image registry access secret that is used to access the registry. You can add the image registry access secret by running the `registry create` command. This value is *optional*. 

`--size`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). This value is *optional*. The default value is `medium`.

`--source`, `--src`
:   The URL of the Git repository that contains your source code; for example `https://github.com/IBM/CodeEngine`. The source option is required if the `--build-type` option is `git` and not allowed if the `--build-type` option is `local`. This value is *optional*. 

`--strategy`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. This value is *optional*. The default value is `dockerfile`.

`--timeout`, `--to`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. This value is *optional*. The default value is `600`.

 
  
#### Example
{: #build-create-example}

The following example creates a build configuration file called `helloworld-build` from a source Dockerfile, that is located in `https://github.com/IBM/CodeEngine` within the `hello` directory in the `main` branch, with `dockerfile` strategy and `medium` size. When this build is submitted, the container image that is built is stored in a {{site.data.keyword.registryshort}} instance at `us.icr.io/mynamespace/codeengine-helloworld` that is accessed by using an image registry secret called `myregistry`.

```txt
ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --commit main --strategy dockerfile --size medium --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry
```
{: pre}

#### Example output
{: #build-create-example-output}

```txt
Creating build helloworld-build...
OK
```
{: screen}  
  
### `ibmcloud ce build delete`  
{: #cli-build-delete}  

Delete a build.  
  
```txt
ibmcloud ce build delete --name BUILD_NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-build-delete} 

`--name`, `-n`
:   The name of the build. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #build-delete-example}

```txt
ibmcloud ce build delete --name helloworld-build
```
{: pre}

#### Example output
{: #build-delete-example-output}

```txt
Are you sure you want to delete build helloworld-build? [y/N]> y
Deleting build 'helloworld-build'...
OK
```
{: screen}  
  
### `ibmcloud ce build get`  
{: #cli-build-get}  

Display the details of a build.  
  
```txt
ibmcloud ce build get --name BUILD_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-build-get} 

`--name`, `-n`
:   The name of the build. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #build-get-example}

```txt
ibmcloud ce build get --name helloworld-build
```
{: pre}

#### Example output
{: #build-get-example-output}

```txt
Getting build 'helloworld-build'
OK

Name:          helloworld-build
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           15s
Created:       2021-03-14T14:48:19-05:00  
Status:        Succeeded 
Reason:        all validations succeeded

Last Build Run:
  Name:     helloworld-build-run
  Age:      39d
  Created:  2021-09-30T15:19:33-04:00

Image:              us.icr.io/mynamespace/codeengine-helloworld
Registry Secret:    myregistry
Build Strategy:     dockerfile-medium
Timeout:            10m0s
Source:             https://github.com/IBM/CodeEngine
Commit:             main
Context Directory:  /hello
Dockerfile:         Dockerfile 

Build Runs:
  Name                  Status                              Image                                        Age
  helloworld-build-run  All Steps have completed executing  us.icr.io/mynamespace/codeengine-helloworld  39d
```
{: screen}  
  
### `ibmcloud ce build list`  
{: #cli-build-list}  

List all builds in a project.  
  
```txt
ibmcloud ce build list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-build-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #build-list-example}

```txt
ibmcloud ce build list
```
{: pre}

#### Example output
{: #build-list-example-output}

```txt
Listing builds...
OK

Name                    Status     Reason                     Image                                               Build Strategy     Age    Last Build Run Name                        Last Build Run Age
myhellobuild           Succeeded  all validations succeeded  us.icr.io/mynamespace/codeengine-codeengine-200      dockerfile-medium  160d   myhellobuild-run-4xdnb                    160d
hello-build-5ckgs      Succeeded  all validations succeeded  us.icr.io/mynamespace/codeengine-codeengine-51       dockerfile-medium  39d    helloapp3-build-5ckgs-run-210803-2129500   39d
hello-build-pmg6v      Succeeded  all validations succeeded  us.icr.io/mynamespace/codeengine-codeengine-4f       dockerfile-medium  40d    hellooapp2-build-pmg6v-run-210802-2112310  40d
helloworld-build       Succeeded  all validations succeeded  us.icr.io/mynamespace/codeengine-helloworld          dockerfile-medium  39d    helloworld-build-run                       39d
```
{: screen}  
  
### `ibmcloud ce build update`  
{: #cli-build-update}  

Update a build.  
  
```txt
ibmcloud ce build update --name BUILD_NAME [--commit COMMIT] [--commit-clear] [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--force] [--git-repo-secret GIT_REPO_SECRET] [--git-repo-secret-clear] [--image IMAGE] [--output OUTPUT] [--quiet] [--registry-secret REGISTRY_SECRET] [--size SIZE] [--source SOURCE] [--strategy STRATEGY] [--timeout TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-build-update} 

`--name`, `-n`
:   The name of the build. This value is *required*. 

`--commit`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. This value is *optional*. 

`--commit-clear`, `--cmc`
:   Clear the commit, tag, or branch in the source repository to pull. This value is *optional*. The default value is `false`.

`--context-dir`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. This value is *optional*. 

`--dockerfile`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is *optional*. The default value is `Dockerfile`.

`--force`, `-f`
:   Do not verify the existence of specified secret references. Secret references are specified with the `--get-repo-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--git-repo-secret`, `--grs`, `--repo`, `-r`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. This value is *optional*. 

`--git-repo-secret-clear`, `--grsc`
:   Clear the Git repository access secret. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--size`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). This value is *optional*. 

`--source`, `--src`
:   The URL of the Git repository that contains your source code; for example `https://github.com/IBM/CodeEngine`. This value is *optional*. 

`--strategy`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. This value is *optional*. 

`--timeout`, `--to`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. This value is *optional*. The default value is `600`.

 
  
#### Example
{: #build-update-example}

```txt
ibmcloud ce build update --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --commit main --timeout 900
```
{: pre}

#### Example output
{: #build-update-example-output}

```txt
Updating build helloworld-build...
OK
```
{: screen}  
  
## Buildrun commands  
{: #cli-buildrun}  

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and Cloud Native Buildpacks. Use `buildrun` commands to submit, display details, and delete build runs.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `buildrun` commands.

For more information about working with builds and build runs, see [Building a container image](/docs/codeengine?topic=codeengine-build-image).

You can use either `buildrun` or `br` in your `buildrun` commands. To see CLI help for the `buildrun` commands, run `ibmcloud ce br -h`.
{: tip}  
  
### `ibmcloud ce buildrun cancel`  
{: #cli-buildrun-cancel}  

Cancel a build run.  
  
```txt
ibmcloud ce buildrun cancel --name BUILDRUN_NAME [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-cancel} 

`--name`, `-n`
:   The name of the build run. This value is *required*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #buildrun-cancel-example}

```txt
ibmcloud ce buildrun cancel --name mybuildrun
```
{: pre}

#### Example output
{: #buildrun-cancel-example-output}

```txt
Cancelling build run 'mybuildrun'...
OK
```
{: screen}  
  
### `ibmcloud ce buildrun delete`  
{: #cli-buildrun-delete}  

Delete a build run.  
  
```txt
ibmcloud ce buildrun delete (--name BUILDRUN_NAME | --build BUILD_NAME) [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-delete} 

`--build`, `-b`
:   Use this option to delete all build runs of the specified build. The `--build` option is required, if you do not specify the `--name` value. This value is *optional*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--name`, `-n`
:   The name of the build run. The `--name` option is required, if you do not specify the `--build` value. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #buildrun-delete-example}

```txt
ibmcloud ce buildrun delete --name mybuildrun
```
{: pre}

#### Example output
{: #buildrun-delete-example-output}

```txt
Are you sure you want to delete build run mybuildrun? [y/N]> y
Deleting build run 'mybuildrun'...
OK
```
{: screen}  
  
### `ibmcloud ce buildrun events`  
{: #cli-buildrun-events}  

Display the events of a build run.  
  
```txt
ibmcloud ce buildrun events --buildrun BUILDRUN_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-events} 

`--buildrun`, `-b`, `--br`, `--name`, `-n`
:   The name of the build run. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #buildrun-events-example}

This example displays the system event information for a build run. 

```txt
ibmcloud ce buildrun events --buildrun mybuildrun
```
{: pre}

#### Example output
{: #buildrun-events-example-output}

```txt
Getting build run 'mybuildrun'...
Getting instances of build run 'mybuildrun'...
Getting events for build run 'mybuildrun'...
OK

mybuildrun-l4mr2-pod-89z4t:
    Type    Reason     Age  Source                  Messages
    Normal  Scheduled  33s  default-scheduler       Successfully assigned 4svg40kna19/mybuildrun-l4mr2-pod-89z4t to 10.240.128.97
    Normal  Pulled     31s  kubelet, 10.240.128.97  Container image "gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e" already present on machine
    Normal  Created    31s  kubelet, 10.240.128.97  Created container working-dir-initializer
    Normal  Started    31s  kubelet, 10.240.128.97  Started container working-dir-initializer
    Normal  Pulled     30s  kubelet, 10.240.128.97  Container image "icr.io/obs/codeengine/tekton-pipeline/entrypoint-bff0a22da108bc2f16c818c97641a296:v0.20.1-rc2@sha256:19ec0672b5e84a4c5939c6ece6fa69efbce0d38479baf35ce894cf1c67f7e435" already present on machine
    Normal  Created    30s  kubelet, 10.240.128.97  Created container place-tools
    Normal  Started    29s  kubelet, 10.240.128.97  Started container place-tools
    Normal  Pulled     28s  kubelet, 10.240.128.97  Container image "gcr.io/distroless/base@sha256:92720b2305d7315b5426aec19f8651e9e04222991f877cae71f40b3141d2f07e" already present on machine
    Normal  Created    28s  kubelet, 10.240.128.97  Created container step-create-dir-image-l7lf2
    Normal  Created    25s  kubelet, 10.240.128.97  Created container step-git-source-source-46fm7
    Normal  Pulled     25s  kubelet, 10.240.128.97  Container image "icr.io/obs/codeengine/tekton-pipeline/git-init-4874978a9786b6625dd8b6ef2a21aa70:v0.20.1-rc2@sha256:5febfb32459a114b7beafdc593770a0f692a09d874ac6b59ce85507844641cdf" already present on machine
    Normal  Started    25s  kubelet, 10.240.128.97  Started container step-create-dir-image-l7lf2
    Normal  Started    24s  kubelet, 10.240.128.97  Started container step-git-source-source-46fm7
    Normal  Pulled     24s  kubelet, 10.240.128.97  Container image "icr.io/obs/codeengine/kaniko/executor:v1.3.0-rc1" already present on machine
    Normal  Created    24s  kubelet, 10.240.128.97  Created container step-build-and-push
    Normal  Started    24s  kubelet, 10.240.128.97  Started container step-build-and-push
    Normal  Pulled     24s  kubelet, 10.240.128.97  Container image "icr.io/obs/codeengine/tekton-pipeline/imagedigestexporter-6e7c518e6125f31761ebe0b96cc63971:v0.20.1-rc2@sha256:21b3120ce9b930b4eb1359eb20a3109e3a6643e9d2777ef9694efb033367e57c" already present on machine
    Normal  Created    24s  kubelet, 10.240.128.97  Created container step-image-digest-exporter-gnbrp
    Normal  Started    23s  kubelet, 10.240.128.97  Started container step-image-digest-exporter-gnbrp
```
{: screen}  
  
### `ibmcloud ce buildrun get`  
{: #cli-buildrun-get}  

Display the details of a build run.  
  
```txt
ibmcloud ce buildrun get --name BUILDRUN_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-get} 

`--name`, `-n`
:   The name of the build run. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #buildrun-get-example}

```txt
ibmcloud ce buildrun get --name mybuildrun
```
{: pre}

#### Example output
{: #buildrun-get-example-output}

```txt
Getting build run 'mybuildrun'...
Run 'ibmcloud ce buildrun events -n mybuildrun' to get the system events of the build run.
Run 'ibmcloud ce buildrun logs -f -n mybuildrun' to follow the logs of the build run.
OK

Name:          mybuildrun
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           21m  
Created:       2021-03-14T14:50:13-05:00  

Summary:       Succeeded  
Status:        Succeeded  
Reason:        All Steps have completed executing  
Source:          
  Commit Branch:  main  
  Commit SHA:     abcdeb88263442e28af6ae26d2082dea1d6abcde  
  Commit Author:  myauthor  
Image Digest:  sha256:522488ca3b54eb65f8c1e609a7b27c08558d08166fe062e7dde6838d4a609d61  

Image:  us.icr.io/mynamespace/test
```
{: screen}  
  
### `ibmcloud ce buildrun list`  
{: #cli-buildrun-list}  

List all build runs in a project.  
  
```txt
ibmcloud ce buildrun list [--build BUILD] [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-list} 

`--build`, `-b`
:   Use this option to only display build runs from the specified build. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #buildrun-list-example}

```txt
ibmcloud ce buildrun list
```
{: pre}

#### Example output
{: #buildrun-list-example-output}

```txt
Listing builds...
OK

Name                                  Status     Build Name        Age
helloworld-build-run                  Succeeded  helloworld-build  5d22h
mybuildrun                            Succeeded  helloworld-build  7m23s
mybuildrun2                           Succeeded  helloworld-build  3m4s
```
{: screen}  
  
### `ibmcloud ce buildrun logs`  
{: #cli-buildrun-logs}  

Display the logs of a build run.  
  
```txt
ibmcloud ce buildrun logs --buildrun BUILDRUN_NAME [--follow] [--output OUTPUT] [--quiet] [--raw] [--tail TAIL] [--timestamps]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-logs} 

`--buildrun`, `-b`, `--br`, `--name`, `-n`
:   The name of the build run. This value is *required*. 

`--follow`, `-f`
:   Follow the logs of the build run. Use this option to stream logs of the build run. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--raw`, `-r`
:   Display logs without instance and container labels. This value is *optional*. The default value is `false`.

`--tail`, `-t`
:   Limit the display of logs of containers of the specified build run to a maximum number of recent lines per container. For example, to display the last `3` lines of the logs of the containers of the specified build run, specify `--tail 3`. If this option is not specified, all lines of the logs of the containers of the specified build run are displayed. This value is *optional*. The default value is `-1`.

`--timestamps`, `--ts`
:   Include timestamps on each line in the log output. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #buildrun-log-example}

```txt
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

#### Example output
{: #buildrun-log-example-output}

```txt
Getting build run 'mybuildrun'...
Getting instances of build run 'mybuildrun'...
Getting logs for build run 'mybuildrun'...
OK

mybuildrun-v2mb8-pod-tlzdx/step-git-source-source-g2kbf:
{"level":"info","ts":1614089507.7123275,"caller":"git/git.go:165","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 433e2b8d6529e4a55f5e0f72d3772a79602a5ee8 (grafted, HEAD, origin/main) in path /workspace/source"}
{"level":"info","ts":1614089509.0128207,"caller":"git/git.go:203","msg":"Successfully initialized and updated submodules in path /workspace/source"}

mybuildrun-v2mb8-pod-tlzdx/step-build-and-push:
INFO[0000] Retrieving image manifest node:12-alpine
INFO[0000] Retrieving image node:12-alpine
INFO[0001] Retrieving image manifest node:12-alpine
INFO[0001] Retrieving image node:12-alpine
INFO[0001] Built cross stage deps: map[]
INFO[0001] Retrieving image manifest node:12-alpine
INFO[0001] Retrieving image node:12-alpine
INFO[0002] Retrieving image manifest node:12-alpine
INFO[0002] Retrieving image node:12-alpine
INFO[0002] Executing 0 build triggers
INFO[0002] Unpacking rootfs as cmd RUN npm install requires it.
INFO[0006] RUN npm install
INFO[0006] Taking snapshot of full filesystem...
INFO[0008] cmd: /bin/sh
INFO[0008] args: [-c npm install]
INFO[0008] Running: [/bin/sh -c npm install]
npm WARN saveError ENOENT: no such file or directory, open '/package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open '/package.json'
npm WARN !invalid#2 No description
npm WARN !invalid#2 No repository field.
npm WARN !invalid#2 No README data
npm WARN !invalid#2 No license field.

up to date in 0.27s
found 0 vulnerabilities

INFO[0010] Taking snapshot of full filesystem...
INFO[0010] COPY server.js .
INFO[0010] Taking snapshot of files...
INFO[0010] EXPOSE 8080
INFO[0010] cmd: EXPOSE
INFO[0010] Adding exposed port: 8080/tcp
INFO[0010] CMD [ "node", "server.js" ]

mybuildrun-v2mb8-pod-tlzdx/step-image-digest-exporter-hcvmf:
2021/02/23 14:11:43 warning: unsuccessful cred copy: ".docker" from "/tekton/creds" to "/tekton/home": unable to open destination: open /tekton/home/.docker/config.json: permission denied
{"severity":"INFO","timestamp":"2021-02-23T14:12:05.65581098Z","caller":"logging/config.go:115","message":"Successfully created the logger.","logging.googleapis.com/labels":{},"logging.googleapis.com/sourceLocation":{"file":"github.com/tektoncd/pipeline/vendor/knative.dev/pkg/logging/config.go","line":"115","function":"github.com/tektoncd/pipeline/vendor/knative.dev/pkg/logging.newLoggerFromConfig"}}
{"severity":"INFO","timestamp":"2021-02-23T14:12:05.655937558Z","caller":"logging/config.go:116","message":"Logging level set to: info","logging.googleapis.com/labels":{},"logging.googleapis.com/sourceLocation":{"file":"github.com/tektoncd/pipeline/vendor/knative.dev/pkg/logging/config.go","line":"116","function":"github.com/tektoncd/pipeline/vendor/knative.dev/pkg/logging.newLoggerFromConfig"}}
```
{: screen}  
  
### `ibmcloud ce buildrun submit`  
{: #cli-buildrun-submit}  

Submit a build run.  
  
```txt
ibmcloud ce buildrun submit (--build BUILD_NAME [--name NAME]) | (--name NAME [--commit COMMIT] [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--git-repo-secret GIT_REPO_SECRET] [--registry-secret REGISTRY_SECRET] [--size SIZE] [--strategy STRATEGY]) [--image IMAGE] [--no-wait] [--output OUTPUT] [--quiet] [--service-account SERVICE_ACCOUNT] [--source SOURCE] [--timeout TIMEOUT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-buildrun-submit} 

`--build`, `-b`, `--bd`
:   The name of the build configuration to use. This value is *optional*. 

`--commit`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The build commit option is allowed if the `--source` option is set to the URL of a Git repository and **not** allowed if the `--source` option is not set to the URL of a Git repository. This value is *optional*. 

`--context-dir`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. The build context directory option is allowed if the `--build` option is not set and **not** allowed if the `--build` option is set. This value is *optional*. 

`--dockerfile`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. The build dockerfile option is allowed if the `--build` option is not set and **not** allowed if the `--build` option is set. This value is *optional*. The default value is `Dockerfile`.

`--git-repo-secret`, `--grs`, `--repo`, `-r`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The build Git repository access secret option is allowed if the `--source` option is set to the URL of a Git repository and **not** allowed if the `--source` option is not set to the URL of a Git repository. This value is *optional*. 

`--image`, `-i`
:   The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is *optional*. 

`-n`, `--name`
:   The name of the build run. Use a name that is unique within the project. If the `--build` option is  set, the name option is optional. If the `--build` option is not set, the name option is required.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).

   This value is *optional*. 

`--no-wait`, `--nw`
:   Submit the build run and do not wait for this build run to complete. If you specify the `--no-wait` option, the build run submit begins and does not wait. Use the `buildrun get` command to check the build run status. This value is *optional*. The default value is `true`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. The image registry access secret option is allowed if the `--build` option is not set and **not** allowed if the `--build` option is set. This value is *optional*. 

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--size`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). The build size option is allowed if the `--build` option is not set and **not** allowed if the `--build` option is set. This value is *optional*. The default value is `medium`.

`--source`, `--src`
:   The URL of the Git repository or the path to local source that contains your source code; for example `https://github.com/IBM/CodeEngine` or `.`. If the `--build` option is set, the source option is required if the `--build-type` option on the related build is `local` and **not** allowed if the `--build-type` option on the related build is `git`. If the `--build` option is not set, the source option is optional. This value is *optional*. The default value is `.`.

`--strategy`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. The build strategy option is allowed if the `--build` option is not set and **not** allowed if the `--build` option is set. If not specified, the build strategy is determined by {{site.data.keyword.codeengineshort}} if `--source` is specified and the source is on your local machine. This value is *optional*. The default value is `dockerfile`.

`--timeout`, `--to`
:   The amount of time, in seconds, that can pass before the build run must succeed or fail. This value is *optional*. The default value is `600`.

`--wait`, `-w`
:   Submit the build run and wait for this build run to complete. If you specify the `--wait` option, the build run submit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the build run to complete. If the build run is not completed within the specified `--wait-timeout` period, the build run submit fails. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for this build run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #buildrun-submit-example}

The following command submits a build run called `mybuildrun` and uses the build configuration file called `helloworld-build`.

```txt
ibmcloud ce buildrun submit --name mybuildrun --build helloworld-build
```
{: pre}

#### Example output
{: #buildrun-submit-example-output}

```txt
Submitting build run 'mybuildrun'...
Run 'ibmcloud ce buildrun get -n mybuildrun' to check the build run status.
OK 
```
{: screen}  
  
## Configmap commands  
{: #cli-configmap}  

A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app or job portable. A configmap contains information in key-value pairs. Use `configmap` commands to create, display details, update, and delete configmaps.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `configmap` commands.

For more information about working with configmaps, see [Setting up and using configmaps and secrets](/docs/codeengine?topic=codeengine-configmap-secret).

You can use either `configmap` or `cm` in your `configmap` commands. To see CLI help for the `configmap` commands, run `ibmcloud ce configmap -h`.
{: tip}  
  
### `ibmcloud ce configmap create`  
{: #cli-configmap-create}  

Create a configmap.  
  
```txt
ibmcloud ce configmap create --name CONFIGMAP_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-configmap-create} 

`-n`, `--name`
:   The name of the configmap. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--from-env-file`, `-e`
:   Create a configmap from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. This value is required if `--from-literal` or `--from-file` is not specified. 

`--from-file`, `-f`
:   Create a configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 

`--from-literal`, `-l`
:   Create a configmap from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. This option can be specified multiple times. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #configmap-create-example}

The following example creates a configmap that is named `configmap-fromliteral` with two key pair values: `color=blue` and `size=large`.

```txt
ibmcloud ce configmap create --name configmap-fromliteral --from-literal color=blue --from-literal size=large
```
{: pre}

#### Example output
{: #configmap-create-example-output}

```txt
Creating Configmap 'configmap-fromliteral'...
OK
Run 'ibmcloud ce configmap get -n configmap-fromliteral' to see more details.
```
{: screen}

#### Example of a configmap with values from multiple files
{: #configmap-create-example2}

The following example creates a configmap that is named `configmap-fromfile` with values from multiple files.

```txt
ibmcloud ce configmap create --name configmap-fromfile  --from-file ./color.txt --from-file ./size.txt
```
{: pre}

##### Example output of a configmap with values from multiple files
{: #configmap-create-example2-output}

```txt
Creating configmap 'configmap-fromfile'...
OK
Run 'ibmcloud ce configmap get -n configmap-fromfile' to see more details.
```
{: screen}  
  
### `ibmcloud ce configmap delete`  
{: #cli-configmap-delete}  

Delete a configmap.  
  
```txt
ibmcloud ce configmap delete --name CONFIGMAP_NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-configmap-delete} 

`--name`, `-n`
:   The name of the configmap. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #configmap-delete-example}

```txt
ibmcloud ce configmap delete --name configmap-fromliteral -f
```
{: pre}

#### Example output
{: #configmap-delete-example-output}

```txt
Deleting Configmap 'configmap-fromliteral'...
OK
```
{: screen}  
  
### `ibmcloud ce configmap get`  
{: #cli-configmap-get}  

Display the details of a configmap.  
  
```txt
ibmcloud ce configmap get --name CONFIGMAP_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-configmap-get} 

`--name`, `-n`
:   The name of the configmap. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #configmap-get-example}

```txt
ibmcloud ce configmap get --name configmap-fromliteral 
```
{: pre}

#### Example output
{: #configmap-get-example-output}

```txt
Getting configmap 'configmap-fromliteral'...
OK

Name:          configmap-fromliteral
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           21s
Created:       2021-03-01T13:50:56-05:00

Data:
---
color: blue
size: large
```
{: screen}  
  
### `ibmcloud ce configmap list`  
{: #cli-configmap-list}  

List all configmaps in a project.  
  
```txt
ibmcloud ce configmap list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-configmap-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #configmap-list-example}

```txt
ibmcloud ce configmap list
```
{: pre}

#### Example output
{: #configmap-list-example-output}

```txt
Listing Configmaps...
Name                    Data   Age
configmap-fromfile      2      19m13s
configmap-fromliteral   2      16m12s
```
{: screen}  
  
### `ibmcloud ce configmap update`  
{: #cli-configmap-update}  

Update a configmap.  
  
```txt
ibmcloud ce configmap update --name CONFIGMAP_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE | --rm KEY) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-configmap-update} 

`--name`, `-n`
:   The name of the configmap. This value is *required*. 

`--from-env-file`, `-e`
:   Update a configmap from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. This value is required if `--from-literal` or `--from-file` is not specified. This option can be specified multiple times. 

`--from-file`, `-f`
:   Update a configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. This option can be specified multiple times. 

`--from-literal`, `-l`
:   Update a configmap from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or  or `--from-env-file`is not specified. This option can be specified multiple times. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--rm`
:   Remove an individual key-value pair in a configmap by specifying the name of the key. This option can be specified multiple times. This value is *optional*. 

 
  
#### Example
{: #configmap-update-example}

The following example updates a configmap that is named `configmap-fromliteral` with a username and password value pair.

```txt
ibmcloud ce configmap update --name configmap-fromliteral --from-literal username=devuser --from-literal password='A!B99c$D1Def'
```
{: pre}

#### Example output
{: #configmap-update-example-output}

```txt
Updating configmap 'configmap-fromliteral'...
OK
Run 'ibmcloud ce configmap get -n configmap-fromliteral' to see more details.
```
{: screen}

#### Example of a configmap with values from a file 
{: #configmap-update-example2}

The following example updates a configmap that is named `configmap-fromfile` with values from a file.

```txt
ibmcloud ce configmap update --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
```
{: pre}

##### Example output of a configmap with values from a file 
{: #configmap-update-example2-output}

```txt
Updating configmap 'configmap-fromfile'...
OK
Run 'ibmcloud ce configmap get -n configmap-fromfile' to see more details.

```
{: screen}  
  
## Job commands  
{: #cli-job}  

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. Use `job` commands to create a configuration for your job.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `job` commands.

For more information about working with jobs, see [Running jobs](/docs/codeengine?topic=codeengine-job-plan).

To see CLI help for the `job` commands, run `ibmcloud ce job -h`.
{: tip}  
  
### `ibmcloud ce job bind`  
{: #cli-job-bind}  

Bind an {{site.data.keyword.cloud_notm}} service instance to a job.  
  
```txt
ibmcloud ce job bind --name JOB_NAME (--service-instance SI_NAME | --service-instance-id SI_ID) [--no-wait] [--prefix PREFIX] [--quiet] [--role ROLE] [--service-credential SERVICE_CREDENTIAL] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-bind} 

`--name`, `-n`
:   The name of the job to bind. This value is *required*. 

`--no-wait`, `--nw`
:   Bind the service instance and do not wait for the service binding to be ready. If you specify the `--no-wait` option, the service binding creation is started and the command exits without waiting for it to complete. Use the `job get` command to check the job bind status. This value is *optional*. The default value is `false`.

`--prefix`, `-p`
:   A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--role`, `-r`
:   The name of a service role for the new service credential that is created for this service binding. Valid values include `Reader`, `Writer`, `Manager`, or a service-specific role. The option defaults to `Manager` or the first role provided by the service if `Manager` is not supported. This option is ignored if `--service-credential` is specified. This value is *optional*. 

`--service-credential`, `--sc`
:   The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is *optional*. 

`--service-instance`, `--si`
:   The name of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the job. This value is *optional*. 

`--service-instance-id`, `--siid`
:   The GUID of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the job. This value is *optional*. 

`--wait`, `-w`
:   Bind the service instance and wait for the service binding to be ready. If you specify the `--wait` option, the job bind waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job bind to complete successfully. If the job bind is not completed successfully or fails within the specified `--wait-timeout` period, the command fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the service binding to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `300`.

 
  
#### Example
{: #job-bind-example}

In this example, bind your service instance called `my-object-storage` to your job that is called `hello`.

```txt
ibmcloud ce job bind --name hello --service-instance my-object-storage
```
{: pre}

#### Example output
{: #job-bind-example-output}

```txt
Binding service instance...
Waiting for service binding to become ready...
Status: Pending (Processing Resource)
Status: Pending (Processing Resource)
Status: Creating service binding
Status: Creating service binding
Status: Ready
OK
```
{: screen}  
  
### `ibmcloud ce job create`  
{: #cli-job-create}  

Create a job.  
  
```txt
ibmcloud ce job create --name JOB_NAME ((--image IMAGE_REF | (--build-source SOURCE [--image IMAGE_REF])) [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--build-commit BUILD_COMMIT] [--build-context-dir BUILD_CONTEXT_DIR] [--build-dockerfile BUILD_DOCKERFILE] [--build-git-repo-secret BUILD_GIT_REPO_SECRET] [--build-size BUILD_SIZE] [--build-strategy BUILD_STRATEGY] [--build-timeout BUILD_TIMEOUT] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--instances INSTANCES] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--mode MODE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-secret MOUNT_SECRET] [--no-wait] [--output OUTPUT] [--quiet] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT] [--service-account SERVICE_ACCOUNT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-create} 

`-n`, `--name`
:   The name of the job. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 63 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).

   This value is *required*. 

`--argument`, `--arg`, `-a`
:   Set arguments for runs of the job. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is *optional*. 

`--array-indices`, `--ai`
:   Specifies the array indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `0,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This option can only be specified if the `--instances` option is not specified. This value is *optional*. The default value is `0`.

`--build-commit`, `--commit`, `--bcm`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The build commit option is allowed if the `--build-source` option is set to the URL of a Git repository and **not** allowed if the `--build-source` option is not set to the URL of a Git repository. This value is *optional*. 

`--build-context-dir`, `--context-dir`, `--bcdr`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. The build context directory option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. 

`--build-dockerfile`, `--dockerfile`, `--bdf`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. The build dockerfile option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `Dockerfile`.

`--build-git-repo-secret`, `--git-repo-secret`, `--bgrs`, `--grs`, `--repo`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The build Git repository access secret option is allowed if the `--build-source` option is set to the URL of a Git repository and **not** allowed if the `--build-source` option is not set to the URL of a Git repository. This value is *optional*. 

`--build-size`, `--size`, `--bsz`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). The build size option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `medium`.

`--build-source`, `--source`, `--bsrc`, `--src`
:   The URL of the Git repository or the path to local source that contains your source code; for example `https://github.com/IBM/CodeEngine` or `.`. This value is *optional*. 

`--build-strategy`, `--strategy`, `--bstr`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. The build strategy option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. If not specified, the build strategy is determined by {{site.data.keyword.codeengineshort}} if `--build-source` is specified and the source is on your local machine. This value is *optional*. The default value is `dockerfile`.

`--build-timeout`, `--bto`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. The build timeout option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `600`.

`--command`, `--cmd`, `-c`
:   Set commands for runs of the job. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--cpu`
:   The amount of CPU to set for runs of the job. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `1`.

`--env`, `-e`
:   Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   - To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage to set for runs of the job. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` option. Secret references are specified with the `--env-from-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The name of the image that is used for runs of the job. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. The image option is required if the `--build-source` option is not specified. This value is *optional*. 

`--instances`, `--is`
:   Specifies the number of instances that are used for runs of the job. When you use this option, the system converts to array indices. For example, if you specify `instances` of `5`, the system converts to `array-indices` of `0 - 4`. This option can only be specified if the `--array-indices` option is not specified. This value is *optional*. The default value is `1`.

`--maxexecutiontime`, `--met`
:   The maximum execution time in seconds for runs of the job. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `7200`.

`--memory`, `-m`
:   The amount of memory that is set for runs of the job. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `4G`.

`--mode`
:   The mode for runs of the job. Valid values are `task` and `daemon`. In `task` mode, the `maxexecutiontime` and `retrylimit` options apply. In `daemon` mode, since there is no timeout and failed instances are restarted indefinitely, the `--maxexecutiontime` and `--retrylimit` options are not allowed. This value is *optional*. The default value is `task`.

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of runs of the job by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of runs of the job by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`--no-wait`, `--nw`
:   Do not wait for the build run to complete. If you specify the `--no-wait` option, the build run begins and does not wait. Use the `buildrun get` command to check the build run status. The no-wait option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `true`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--retrylimit`, `-r`
:   The number of times to rerun an instance of the job before the job is marked as failed. An array index of a job is rerun when it gives an exit code other than zero. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `3`.

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--wait`, `-w`
:   Wait for the build run to complete. If you specify the `--wait` option, the build run waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the build run to complete. If the build run is not completed within the specified `--wait-timeout` period, the build run fails. The wait option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the build run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The wait-timeout option is allowed if the `--build-source` option is set and not allowed if the `--build-source` option is not set. The default value is `600`.

 
  
#### Example
{: #job-create-example}

The following example uses the container image `icr.io/codeengine/firstjob` and assigns 2G MB as memory and 1 CPU to the container. For more information about selecting valid memory and CPU values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

```txt
ibmcloud ce job create --image icr.io/codeengine/firstjob --name hellojob --memory 2G --cpu 1
```
{: pre}

#### Example output
{: #job-create-example-output}

```txt
Creating job 'hellojob'...
OK
```
{: screen}  
  
### `ibmcloud ce job delete`  
{: #cli-job-delete}  

Delete a job and its associated job runs.  
  
```txt
ibmcloud ce job delete --name JOB_NAME [--force] [--ignore-not-found] [--orphan-job-runs] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-delete} 

`--name`, `-n`
:   The name of the job. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--orphan-job-runs`, `-o`
:   Specify to keep any job runs that are associated with this job configuration. These orphaned job runs must then be deleted separately. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #job-delete-example}

```txt
ibmcloud ce job delete --name hello
```
{: pre}

#### Example output
{: #job-delete-example-output}

```txt
Are you sure you want to delete job hello? [y/N]> y
Deleting job 'hello'...
OK
```
{: screen}

When you run the **`ibmcloud ce job delete`** command to delete a job, all the submitted job runs that reference this job are also deleted.  
{: important}  
  
### `ibmcloud ce job get`  
{: #cli-job-get}  

Display the details of a job.  
  
```txt
ibmcloud ce job get --name JOB_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-get} 

`--name`, `-n`
:   The name of the job. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #job-get-example}

```txt
ibmcloud ce job get --name hellojob
```
{: pre}

#### Example output
{: #job-get-example-output}

```txt
Getting job 'hellojob'...
OK

Name:          hellojob
ID:            abcdabcd-abcd-abcd-abcd-abcdabcd1111
Project Name:  myproj
Project ID:    01234567-abcd-abcd-abcd-abcdabcd2222
Age:           59s
Created:       2021-03-01T15:33:30-05:00

Last Job Run:
  Name:     hellojob-jobrun-abcde
  Age:      32d
  Created:  2021-06-06T13:52:42-04:00

Image:                icr.io/codeengine/firstjob
Resource Allocation:
    CPU:     1
    Memory:  4G

Runtime:
    Array Indices:       0
    Max Execution Time:  7200
    Retry Limit:         3
```
{: screen}  
  
### `ibmcloud ce job list`  
{: #cli-job-list}  

List all jobs in a project.  
  
```txt
ibmcloud ce job list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #job-list-example}

```txt
ibmcloud ce job list
```
{: pre}

#### Example output
{: #job-list-example-output}

```txt
Name           Age   Last Job Run Name      Last Job Run Age
demo           110d  demo-jobrun-hkkmx      108d
myjob-envvar   107d
hellojob       7s
myjob          60d   myjob-977v7            58d
testjob        88d   testjob-jobrun-kzxlp   72d
```
{: screen}  
  
### `ibmcloud ce job unbind`  
{: #cli-job-unbind}  

Unbind {{site.data.keyword.cloud_notm}} service instances from a job to remove existing service bindings.  
  
```txt
ibmcloud ce job unbind --name JOB_NAME (--binding BINDING_NAME | --all) [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-unbind} 

`--name`, `-n`
:   The name of the job to unbind. This value is *required*. 

`--all`, `-A`
:   Unbinds all service instances for this job. This value is required if `--binding` is not specified. The default value is `false`.

`--binding`, `-b`
:   The name of the binding to unbind. Run `ibmcloud ce job get -n JOB_NAME` to view binding names. This value is required if `--all` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #job-unbind-example}

In this example, remove all bindings from your job called `hello`.

```txt
ibmcloud ce job unbind --name hello --all
```
{: pre}

#### Example output
{: #job-unbind-example-output}

```txt
Removing service bindings...
OK
```
{: screen}  
  
### `ibmcloud ce job update`  
{: #cli-job-update}  

Update a job.  
  
```txt
ibmcloud ce job update --name JOB_NAME [--argument ARGUMENT] [--arguments-clear] [--array-indices ARRAY_INDICES] [--build-clear] [--build-commit BUILD_COMMIT] [--build-commit-clear] [--build-context-dir BUILD_CONTEXT_DIR] [--build-dockerfile BUILD_DOCKERFILE] [--build-git-repo-secret BUILD_GIT_REPO_SECRET] [--build-git-repo-secret-clear] [--build-size BUILD_SIZE] [--build-source BUILD_SOURCE] [--build-strategy BUILD_STRATEGY] [--build-timeout BUILD_TIMEOUT] [--command COMMAND] [--commands-clear] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--image IMAGE] [--instances INSTANCES] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--mode MODE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-rm MOUNT_RM] [--mount-secret MOUNT_SECRET] [--no-wait] [--output OUTPUT] [--quiet] [--rebuild] [--registry-secret REGISTRY_SECRET] [--registry-secret-clear] [--retrylimit RETRYLIMIT] [--service-account SERVICE_ACCOUNT] [--service-account-clear] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-job-update} 

`--name`, `-n`
:   The name of the job. This value is *required*. 

`--argument`, `--arg`, `-a`
:   Set arguments for runs of the job. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is *optional*. 

`--arguments-clear`, `--ac`
:   Clear job arguments. This value is *optional*. The default value is `false`.

`--array-indices`, `--ai`
:   Specifies the array indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `0,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This option can only be specified if the `--instances` option is not specified. This value is *optional*. 

`--build-clear`, `--bc`
:   Remove the association of a build from this job. The build clear option is only allowed if your job currently has an associated build. This value is *optional*. The default value is `false`.

`--build-commit`, `--commit`, `--bcm`, `--cm`, `--revision`
:   The commit, tag, or branch in the source repository to pull. The build commit option is allowed if the `--build-source` option is set to the URL of a Git repository on this `job update` command, or your job currently has an associated build from a Git repository source. This value is *optional*. 

`--build-commit-clear`, `--commit-clear`, `--bcmc`, `--cmc`
:   Clear the commit, tag, or branch in the source repository to pull. The commit clear option is allowed if your job currently has an associated build. This value is *optional*. The default value is `false`.

`--build-context-dir`, `--context-dir`, `--bcdr`, `--cdr`
:   The directory in the repository that contains the buildpacks file or the Dockerfile. The build context directory option is allowed if the `--build-source` option is set on this `job update` command, or your job currently has an associated build. This value is *optional*. 

`--build-dockerfile`, `--dockerfile`, `--bdf`, `--df`
:   The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. The build dockerfile option is allowed if the `--build-source` option is set on this `job update` command, or your job currently has an associated build. This value is *optional*. The default value is `Dockerfile`.

`--build-git-repo-secret`, `--git-repo-secret`, `--bgrs`, `--grs`, `--repo`
:   The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. The build Git repository access secret option is allowed if the `--build-source` option is set to the URL of a Git repository on this `job update` command, or your job currently has an associated build from a Git repository source. This value is *optional*. 

`--build-git-repo-secret-clear`, `--git-repo-secret-clear`, `--bgrsc`, `--grsc`
:   Clear the Git repository access secret. The Git repository access secret clear option is allowed if your job currently has an associated build. This value is *optional*. The default value is `false`.

`--build-size`, `--size`, `--bsz`, `--sz`
:   The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. For details, see [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size). The build size option is allowed if the `--build-source` option is set on this `job update` command, or your job currently has an associated build. This value is *optional*. The default value is `medium`.

`--build-source`, `--source`, `--bsrc`, `--src`
:   The URL of the Git repository or the path to local source that contains your source code; for example `https://github.com/IBM/CodeEngine` or `.`. This value is *optional*. 

`--build-strategy`, `--strategy`, `--bstr`, `--str`
:   The strategy to use for building the image. Valid values are `dockerfile` and `buildpacks`. The build strategy option is allowed if the `--build-source` option is set on this `job update` command, or your job currently has an associated build. If not specified, the build strategy is determined by {{site.data.keyword.codeengineshort}} if `--build-source` is specified and the source is on your local machine. This value is *optional*. The default value is `dockerfile`.

`--build-timeout`, `--bto`
:   The amount of time, in seconds, that can pass before the build must succeed or fail. The build timeout option is allowed if the `--build-source` option is set on this `job update` command, or your job currently has an associated build. This value is *optional*. The default value is `600`.

`--command`, `--cmd`, `-c`
:   Set commands for runs of the job. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--commands-clear`, `--cc`
:   Clear job commands. This value is *optional*. The default value is `false`.

`--cpu`
:   The amount of CPU to set for runs of the job. This value updates any `--cpu` value that is assigned in the job. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `0`.

`--env`, `-e`
:   Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   -  To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   -  To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-from-configmap-rm`, `--env-cm-rm`
:   Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This option can be specified multiple times. This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--env-from-secret-rm`, `--env-sec-rm`
:   Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This option can be specified multiple times. This value is *optional*. 

`--env-rm`
:   Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This option can be specified multiple times. This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage to set for runs of the job. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` option. Secret references are specified with the `--env-from-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The name of the image that is used for runs of the job. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is *optional*. 

`--instances`, `--is`
:   Specifies the number of instances that are used for runs of the job. When you use this option, the system converts to array indices. For example, if you specify `instances` of `5`, the system converts to `array-indices` of `0 - 4`. This option can only be specified if the `--array-indices` option is not specified. This value is *optional*. The default value is `0`.

`--maxexecutiontime`, `--met`
:   The maximum execution time in seconds for runs of the job. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `7200`.

`--memory`, `-m`
:   The amount of memory that is set for runs of the job. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. 

`--mode`
:   The mode for runs of the job. Valid values are `task` and `daemon`. In `task` mode, the `maxexecutiontime` and `retrylimit` options apply. In `daemon` mode, since there is no timeout and failed instances are restarted indefinitely, the `--maxexecutiontime` and `--retrylimit` options are not allowed. This value is *optional*. 

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of runs of the job by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-rm`
:   Remove the contents of a configmap or secret from the file system of runs of the job by specifying the directory where the configmap or secret is mounted. Specify one mount directory per `--mount-rm` option; for example, `--mount-rm /etc/configmap-a --mount-rm /etc/secret-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of runs of the job by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`--no-wait`, `--nw`
:   Do not wait for the build run to complete. If you specify the `--no-wait` option, the build run begins and does not wait. Use the `buildrun get` command to check the build run status. The no-wait option is allowed if the `--build-source` option is set on this `job update` command or your job currently has an associated build. This value is *optional*. The default value is `true`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--rebuild`
:   Rebuild image from source. The rebuild option is allowed if your job currently has an associated build. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--registry-secret-clear`, `--rsc`
:   Clear the image registry access secret. This value is *optional*. The default value is `false`.

`--retrylimit`, `-r`
:   The number of times to rerun an instance of the job before the job is marked as failed. An array index of a job is rerun when it gives an exit code other than zero. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `3`.

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--service-account-clear`, `--sac`
:   Clear the service account. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Wait for the build run to complete. If you specify the `--wait` option, the build run waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the build run to complete. If the build run is not completed within the specified `--wait-timeout` period, the build run fails. The wait option is allowed if the `--build-source` option is set on this `job update` command or your job currently has an associated build. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the build run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The wait-timeout option is allowed if the `--build-source` option is set on this `job update` command or your job currently has an associated build. The default value is `600`.

 
  
#### Example
{: #job-update-example}

```txt
ibmcloud ce job update --name hellojob --cpu 2
```
{: pre}

#### Example output
{: #job-update-example-output}

```txt
Updating job 'hellojob'...
OK
```
{: screen}  
  
## Jobrun commands  
{: #cli-jobrun}  

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. Use `jobrun` commands to run instances of your job.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `jobrun` commands.

For more information about working with jobs and job runs, see [Running jobs](/docs/codeengine?topic=codeengine-run-job).

To see CLI help for the `jobrun` commands, run `ibmcloud ce jobrun -h`.
{: tip}  
  
### `ibmcloud ce jobrun delete`  
{: #cli-jobrun-delete}  

Delete a job run.  
  
```txt
ibmcloud ce jobrun delete (--name JOBRUN_NAME | --job JOB_NAME) [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-delete} 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--job`, `-j`
:   Use this option to delete all job runs of the specified job. The `--job` option is required, if you do not specify the `--name` value. This value is *optional*. 

`--name`, `-n`
:   The name of the job run to delete. The `--name` option is required, if you do not specify the `--job` value. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #jobrun-delete-example}

```txt
ibmcloud ce jobrun delete --name myjobrun -f
```
{: pre}

#### Example output
{: #jobrun-delete-example-output}

```txt
Deleting job run 'myjobrun'...
OK
```
{: screen}  
  
### `ibmcloud ce jobrun events`  
{: #cli-jobrun-events}  

Display the events of job run instances.  
  
```txt
ibmcloud ce jobrun events (--instance JOBRUN_INSTANCE | --jobrun JOBRUN_NAME) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-events} 

`--instance`, `-i`
:   The name of a specific job run instance. Use the `jobrun get` command to find the instance name. This value is required if `--jobrun` is not specified. 

`--jobrun`, `-j`, `--name`, `-n`
:   Display the events of all the instances of the specified job run. This value is required if `--instance` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #jobrun-events-example}

The following example displays the system event information for all the instances of a specified job run. 
```txt
ibmcloud ce jobrun events --jobrun myjobrun
```
{: pre}

#### Example output
{: #jobrun-events-example-output}

```txt
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
Getting events for all instances of job run 'myjobrun'...
OK

myjobrun-1-0:
    Type     Reason                  Age  Source                  Messages
    Normal   Scheduled               49s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-1-0 to 10.240.64.136
    [...]
    Normal   Pulling                 34s  kubelet, 10.240.64.136  Pulling image "icr.io/codeengine/testjob"

myjobrun-2-0:
    Type    Reason     Age  Source                  Messages
    Normal  Scheduled  50s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-2-0 to 10.240.64.131
    Normal  Pulling    48s  kubelet, 10.240.64.131  Pulling image "icr.io/codeengine/testjob"

```
{: screen}

#### Example of system event information for specified instance of a job run
{: #jobrun-events-example2}

You can also display system event information for a specified instance of a job run by using the `--instance` option with the [**`ibmcloud ce jobrun events`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command. Use the **`jobrun get`** command to display details about your job run, including the running instances of the job run. 

```txt
ibmcloud ce jobrun events --instance myjobrun-2-0
```
{: pre}

##### Example output of system event information for specified instance of a job run
{: #jobrun-events-example2-output}

```txt
Getting events for job run instance 'myjobrun-2-0'...
OK

myjobrun-2-0:
    Type    Reason     Age    Source                  Messages
    Normal  Scheduled  3m39s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-2-0 to 10.240.64.131
    Normal  Pulling    3m37s  kubelet, 10.240.64.131  Pulling image "icr.io/codeengine/testjob"
    Normal  Pulled     2m42s  kubelet, 10.240.64.131  Successfully pulled image "icr.io/codeengine/testjob"
    Normal  Created    2m42s  kubelet, 10.240.64.131  Created container myjobrun
    Normal  Started    2m41s  kubelet, 10.240.64.131  Started container myjobrun
```
{: screen}
  
  
### `ibmcloud ce jobrun get`  
{: #cli-jobrun-get}  

Display the details of a job run.  
  
```txt
ibmcloud ce jobrun get --name JOBRUN_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-get} 

`--name`, `-n`
:   The name of the job run. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #jobrun-get-example}

```txt
ibmcloud ce jobrun get --name myjobrun  
```
{: pre}

#### Example output
{: #jobrun-get-example-output}

```txt
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
Getting events of jobrun 'myjobrun'...
Run 'ibmcloud ce jobrun events -n myjobrun' to get the system events of the job run instances.
Run 'ibmcloud ce jobrun logs -f -n myjobrun' to follow the logs of the job run instances.
OK

Name:          myjobrun
[...]
Created:       2021-03-02T10:31:13-05:00

Image:                icr.io/codeengine/firstjob
Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G

Runtime:
    Array Indices:       1-5
    Max Execution Time:  7200
    Retry Limit:         3

Status:
    Completed:          2m58s
    Instance Statuses:
        Succeeded:  5
    Conditions:
        Type      Status  Last Probe  Last Transition
    Pending   True    3m55s       3m55s
    Running   True    3m51s       3m51s
    Complete  True    2m58s       2m58s

Events:
    Type     Reason         Age                     Source                Messages
    [...]
    Normal   Updated        3m38s (x23 over 3m56s)  batch-job-controller  Updated JobRun "myjobrun"
    Normal   Updated        3m38s (x22 over 3m56s)  batch-job-controller  Updated JobRun "myjobrun"

Instances:
    Name           Running  Status     Restarts  Age
    myjobrun-1-0  0/1      Succeeded  0         3m58s
    myjobrun-2-0  0/1      Succeeded  0         3m58s
    myjobrun-3-0  0/1      Succeeded  0         3m57s
    myjobrun-4-0  0/1      Succeeded  0         3m58s
    myjobrun-5-0  0/1      Succeeded  0         3m58s
```
{: screen}  
  
### `ibmcloud ce jobrun list`  
{: #cli-jobrun-list}  

List all job runs in a project.  
  
```txt
ibmcloud ce jobrun list [--job JOB] [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-list} 

`--job`, `-j`
:   Use this option to only display job runs from the specified job. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #jobrun-list-example}

```txt
ibmcloud ce jobrun list
```
{: pre}

#### Example output
{: #jobrun-list-example-output}

```txt
Listing job runs...
OK

Name                         Failed  Pending  Requested  Running  Succeeded  Unknown  Age
firstjob-jobrun-shnj5        0       0        0          0        1          0        11d
myjob-jobrun-fji48           0       0        0          0        5          0        11d
myjob-jobrun-xeqc8           0       0        0          0        5          0        12d
myjobrun                     0       0        0          0        5          0        7m47s
mytestjob-jobrun-el0o8       0       0        0          0        1          0        11d
testjobrun                   0       0        0          0        5          0        11d
```
{: screen}

The name of the job run listed indicates the name of the job run and the current revision of the job run.  
{: tip}  
  
### `ibmcloud ce jobrun logs`  
{: #cli-jobrun-logs}  

Display the logs of job run instances.  
  
```txt
ibmcloud ce jobrun logs (--instance JOBRUN_INSTANCE | --jobrun JOBRUN_NAME) [--follow] [--output OUTPUT] [--quiet] [--raw] [--tail TAIL] [--timestamps]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-logs} 

`--follow`, `-f`
:   Follow the logs of job run instances. Use this option to stream logs of job run instances. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is *optional*. The default value is `false`.

`--instance`, `-i`
:   The name of a specific job run instance. Use the `jobrun get` command to find the instance name. This value is required if `--jobrun` is not specified. 

`--jobrun`, `-j`, `--name`, `-n`
:   Display the logs of all the instances of the specified job run. This value is required if `--instance` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--raw`, `-r`
:   Display logs without instance and container labels. This value is *optional*. The default value is `false`.

`--tail`, `-t`
:   Limit the display of logs of the specified job run instances to a maximum number of recent lines. For example, to display the last `3` lines of the logs of the specified job run instances, specify `--tail 3`. If this option is not specified, all lines of the logs of the specified job run instances are displayed. This value is *optional*. The default value is `-1`.

`--timestamps`, `--ts`
:   Include timestamps on each line in the log output. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #jobrun-logs-example}

The following example displays the logs of a specific instance of a job run. Use the **`jobrun get`** command to obtain the name of the job run instances. 

```txt
ibmcloud ce jobrun logs --instance myjobrun-3-0
```
{: pre}

#### Example output
{: #jobrun-logs-example-output}

```txt
Getting logs for job run instance 'myjobrun-3-0'...
OK

myjobrun-3-0/myjobrun:
Hi from a batch job! My index is: 3
```
{: screen}

#### Example of logs of all instances of a job run
{: #jobrun-logs-example2}

The following example displays the logs of all the instances of a job run. 

```txt
ibmcloud ce jobrun logs --jobrun myjobrun
```
{: pre}

##### Example output of logs of all instances of a job run
{: #jobrun-logs-example2-output}

```txt
Getting logs for all instances of job run 'myjobrun'...
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
OK

myjobrun-1-0/myjobrun:
Hi from a batch job! My index is: 1

myjobrun-2-0/myjobrun:
Hi from a batch job! My index is: 2

myjobrun-3-0/myjobrun:
Hi from a batch job! My index is: 3

myjobrun-4-0/myjobrun:
Hi from a batch job! My index is: 4

myjobrun-5-0/myjobrun:
Hi from a batch job! My index is: 5
```
{: screen}  
  
### `ibmcloud ce jobrun restart`  
{: #cli-jobrun-restart}  

Restart running job run instances.  
  
```txt
ibmcloud ce jobrun restart (--instance JOBRUN_INSTANCE | --jobrun JOBRUN_NAME) [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-restart} 

`--instance`, `-i`
:   The name of a specific job run instance. Use the `jobrun get` command to find the instance name. This value is required if `--jobrun` is not specified. 

`--jobrun`, `-j`, `--name`, `-n`
:   Restart all the running instances of the specified job run. This value is required if `--instance` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #jobrun-restart-example}

```txt
ibmcloud ce jobrun restart --name myjobrun   
```
{: pre}

#### Example output
{: #jobrun-restart-example-output}

```txt
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
Restarting all running instances of job run 'myjobrun'...
OK
```
{: screen}  
  
### `ibmcloud ce jobrun resubmit`  
{: #cli-jobrun-resubmit}  

Resubmit a job run based on the configuration of a previous job run.  
  
```txt
ibmcloud ce jobrun resubmit --jobrun REFERENCED_JOBRUN_NAME [--argument ARGUMENT] [--arguments-clear] [--array-indices ARRAY_INDICES] [--command COMMAND] [--commands-clear] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--instances INSTANCES] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--mode MODE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-rm MOUNT_RM] [--mount-secret MOUNT_SECRET] [--name NAME] [--no-wait] [--output OUTPUT] [--quiet] [--retrylimit RETRYLIMIT] [--service-account SERVICE_ACCOUNT] [--service-account-clear] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-resubmit} 

`--jobrun`, `-j`
:   The name of the previous job run that this job run is based on. This value is *required*. 

`--argument`, `--arg`, `-a`
:   Set arguments for this job run. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is *optional*. 

`--arguments-clear`, `--ac`
:   Clear job run arguments. This value is *optional*. The default value is `false`.

`--array-indices`, `--ai`
:   Specifies the array indices that are used for this job run. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `0,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This option can only be specified if the `--instances` option is not specified. This value is *optional*. 

`--command`, `--cmd`, `-c`
:   Set commands for this job run. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--commands-clear`, `--cc`
:   Clear job run commands. This value is *optional*. The default value is `false`.

`--cpu`
:   The amount of CPU set for each array index for this job run. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `0`.

`--env`, `-e`
:   Set environment variables for this job run. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `-e envA -e envB`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   - To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-from-configmap-rm`, `--env-cm-rm`
:   Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--env-from-secret-rm`, `--env-sec-rm`
:   Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This option can be specified multiple times. This value is *optional*. 

`--env-rm`
:   Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This option can be specified multiple times. This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage for this job run. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` option. Secret references are specified with the `--env-from-secret` option. This value is *optional*. The default value is `false`.

`--instances`, `--is`
:   Specifies the number of instances that are used for this job run. When you use this option, the system converts to array indices. For example, if you specify `instances` of `5`, the system converts to `array-indices` of `0 - 4`. This option can only be specified if the `--array-indices` option is not specified. This value is *optional*. The default value is `0`.

`--maxexecutiontime`, `--met`
:   The maximum execution time in seconds for this job run. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `7200`.

`--memory`, `-m`
:   The amount of memory to assign to this job run. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. 

`--mode`
:   The mode of the job run. Valid values are `task` and `daemon`. In `task` mode, the `maxexecutiontime` and `retrylimit` options apply. In `daemon` mode, since there is no timeout and failed instances are restarted indefinitely, the `maxexecutiontime` and `retrylimit` options are not allowed. This value is *optional*. 

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of this job run by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-rm`
:   Remove the contents of a configmap or secret from the file system of this job run by specifying the directory where the configmap or secret is mounted. Specify one mount directory per `--mount-rm` option; for example, `--mount-rm /etc/configmap-a --mount-rm /etc/secret-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of this job run by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`-n`, `--name`
:   The name of this job run. This value is required if the referenced job does not have a related job configuration. Use a name that is unique within the project.

   -   The name must begin and end with a lowercase alphanumeric character.
   -   The name must be 53 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).

   This value is *optional*. 

`--no-wait`, `--nw`
:   Resubmit the job run and do not wait for the instances of this job run to complete. If you specify the `--no-wait` option, the job run resubmit begins and does not wait. Use the `jobrun get` command to check the job run status. This value is *optional*. The default value is `true`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--retrylimit`, `-r`
:   The number of times to rerun an instance of this job run before the job run is marked as failed. An array index of a job run is rerun when it gives an exit code other than zero. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `3`.

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--service-account-clear`, `--sac`
:   Clear the service account. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Resubmit the job run and wait for the instances of this job run to complete. If you specify the `--wait` option, the job run resubmit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job run to complete. If the job run is not completed within the specified `--wait-timeout` period, the job run resubmit fails. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the instances of this job run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #jobrun-resubmit-example}

The following example reruns the `myjobrun` job run for instances `4-5`. The name of the resubmitted job run is `myjobresubmit`. 

```txt
ibmcloud ce jobrun resubmit --name myjobresubmit --jobrun myjobrun --array-indices 4-5
```
{: pre}

#### Example output
{: #jobrun-resubmit-example-output}

```txt
Getting job run 'myjobrun'...
Rerunning job run 'myjobresubmit'...
Run 'ibmcloud ce jobrun get -n myjobresubmit' to check the job run status.
OK
```
{: screen}  
  
### `ibmcloud ce jobrun submit`  
{: #cli-jobrun-submit}  

Submit a job run based on a job.  
  
```txt
ibmcloud ce jobrun submit ((--name JOBRUN_NAME --image IMAGE) | (--job JOB_NAME [--name JOBRUN_NAME])) [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--force] [--instances INSTANCES] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--mode MODE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-secret MOUNT_SECRET] [--no-wait] [--output OUTPUT] [--quiet] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT] [--service-account SERVICE_ACCOUNT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-jobrun-submit} 

`--argument`, `--arg`, `-a`
:   Set arguments for this job run. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is *optional*. 

`--array-indices`, `--ai`
:   Specifies the array indices that are used for this job run. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `0,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This option can only be specified if the `--instances` option is not specified. This value is *optional*. The default value is `0`.

`--command`, `--cmd`, `-c`
:   Set commands for this job run. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is *optional*. 

`--cpu`
:   The amount of CPU set for each array index for this job run. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `1`.

`--env`, `-e`
:   Set environment variables for this job run. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `-e envA -e envB`. This value is *optional*. 

`--env-cm`, `--env-from-configmap`
:   Set environment variables from the key-value pairs that are stored in this configmap by using one of the following ways:

   - To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. You can modify the environment variable names by specifying a prefix when referencing the configmap. To specify a prefix, use the value `PREFIX=CONFIGMAP_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_CONFIGMAP>`. For example, to set the prefix for all variable names of keys in configmap `configmapName` to `CUSTOM_`, use the value `CUSTOM_=configmapName`. If the configmap `configmapName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:myKey=key1`.

   This value is *optional*. 

`--env-sec`, `--env-from-secret`
:   Set environment variables from the key-value pairs that are stored in this secret by using one of the following ways:

   - To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. You can modify the environment variable names by specifying a prefix when referencing the secret. To specify a prefix, use the value `PREFIX=SECRET_NAME`. Each resulting environment variable has the format `<PREFIX><NAME_OF_KEY_IN_SECRET>`. For example, to set the prefix for all variable names of keys in secret `secretName` to `CUSTOM_`, use the value `CUSTOM_=secretName`. If the secret `secretName` contains KEY_A, the environment variable name is `CUSTOM_KEY_A`.
   - To add environment variables for individual keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a secret that is named `secretName`, use the value `secretName:key1`. To assign a different name to a referenced key, use the format `NAME:NEW_NAME=KEY_A`. For example, to add an environment variable named `myKey` for a single key `key1` in a secret that is named `secretName`, use the value `secretName:myKey=key1`.

   This value is *optional*. 

`--ephemeral-storage`, `--es`
:   The amount of ephemeral storage for this job run. Use `M` for megabytes or `G` for gigabytes. This value is *optional*. 

`--force`, `-f`
:   Do not verify the existence of specified configmap and secret references. Configmap references are specified with the `--env-from-configmap` option. Secret references are specified with the `--env-from-secret` or `--registry-secret` options. This value is *optional*. The default value is `false`.

`--image`, `-i`
:   The name of the image that is used for this job run. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. If you do not specify the `--job` option, the `--name` and the `--image` values are required. This value is *optional*. 

`--instances`, `--is`
:   Specifies the number of instances that are used for this job run. When you use this option, the system converts to array indices. For example, if you specify `instances` of `5`, the system converts to `array-indices` of `0 - 4`. This option can only be specified if the `--array-indices` option is not specified. This value is *optional*. The default value is `1`.

`--job`, `-j`
:   The name of the job configuration. View job configurations with the `job list` command. If you specify the `--job` value, you can optionally specify the `--name` value. If you don't specify the `--job` value, you must specify the `--name` and `--image` values. This value is *optional*. 

`--maxexecutiontime`, `--met`
:   The maximum execution time in seconds for this job run. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `7200`.

`--memory`, `-m`
:   The amount of memory to assign to this job run. Use `M` for megabytes or `G` for gigabytes. For valid values, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). This value is *optional*. The default value is `4G`.

`--mode`
:   The mode of the job run. Valid values are `task` and `daemon`. In `task` mode, the `maxexecutiontime` and `retrylimit` options apply. In `daemon` mode, since there is no timeout and failed instances are restarted indefinitely, the `maxexecutiontime` and `retrylimit` options are not allowed. This value is *optional*. The default value is `task`.

`--mount-configmap`, `--mount-cm`
:   Add the contents of a configmap to the file system of this job run by providing a mount directory and the name of a configmap, with the format `MOUNT_DIRECTORY=CONFIGMAP_NAME`. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is *optional*. 

`--mount-secret`, `--mount-sec`
:   Add the contents of a secret to the file system of this job run by providing a mount directory and the name of a secret, with the format `MOUNT_DIRECTORY=SECRET_NAME`. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is *optional*. 

`-n`, `--name`
:   The name of this job run. If you do not specify the `--job` value, then the `--name` and the `--image` values are required. Use a name that is unique within the project.

   -   The name must begin and end with a lowercase alphanumeric character.
   -   The name must be 53 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).

   This value is *optional*. 

`--no-wait`, `--nw`
:   Submit the job run and do not wait for the instances of this job run to complete. If you specify the `--no-wait` option, the job run submit begins and does not wait. Use the `jobrun get` command to check the job run status. This value is *optional*. The default value is `true`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--registry-secret`, `--rs`
:   The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is *optional*. 

`--retrylimit`, `-r`
:   The number of times to rerun an instance of this job run before the job run is marked as failed. An array index of a job run is rerun when it gives an exit code other than zero. This option can only be specified if `mode` is `task`. This value is *optional*. The default value is `3`.

`--service-account`, `--sa`
:   The name of the service account. A service account provides an identity for processes that run in an instance. For built-in service accounts, you can use the shortened names `manager`, `none`, `reader`, and `writer`. You can also use the full names that are prefixed with the `Kubernetes Config Context`, which can be determined with the `project current` command. This value is *optional*. 

`--wait`, `-w`
:   Submit the job run and wait for the instances of this job run to complete. If you specify the `--wait` option, the job run submit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job run to complete. If the job run is not completed within the specified `--wait-timeout` period, the job run submit fails. This value is *optional*. The default value is `false`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the instances of this job run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #jobrun-submit-example}

```txt
ibmcloud ce jobrun submit --name myjobrun --image icr.io/codeengine/firstjob --array-indices 1-5
```
{: pre}

#### Example output
{: #jobrun-submit-example-output}

```txt
Submitting job run 'myjobrun'...
Run 'ibmcloud ce jobrun get -n myjobrun' to check the job run status.
OK
```
{: screen}  
  
## Project commands  
{: #cli-project}  

Use `project` commands to create, list, delete, and select a project as the current context.
{: shortdesc}

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. 

A project provides the following items. 

- Provides a unique namespace for entity names.
- Manages access to project resources (inbound access).
- Manages access to backing services, registries, and repositories (outbound access).
- Has an automatically generated certificate for Transport Layer Service (TLS).

For more information about working with projects, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).

You can use either `project` or `proj` in your `project` commands. To see CLI help for the `project` commands, run `ibmcloud ce proj -h`.
{: tip}  
  
### `ibmcloud ce project create`  
{: #cli-project-create}  

Create a project.  
  
```txt
ibmcloud ce project create --name PROJECT_NAME [--endpoint ENDPOINT] [--no-select] [--no-wait] [--output OUTPUT] [--quiet] [--tag TAG] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-create} 

`-n`, `--name`
:   The name of the project. Use a name that is unique to your region. The name must be 128 characters or fewer and can contain:

   - Any Unicode or alphanumeric character.
   - Only these special characters: spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-).

   This value is *required*. 

`--endpoint`, `-e`
:   The endpoint for the project. Valid values are `public` and `private`. If the `--endpoint` option is not explicitly specified, the behavior is determined by the system. If the {{site.data.keyword.cloud_notm}} CLI is connected to `private.cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `private`. If the {{site.data.keyword.cloud_notm}} CLI is connected to `cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `public`. This value is *optional*. 

`--no-select`, `--ns`
:   Do not select the project as the current context after this project is created. If you do not select this option, the project is automatically selected. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Create the project and do not wait for the project to be created. If you specify the `no-wait` option, the project create begins and does not wait. Use the `project get` command to check the project status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--tag`, `-t`
:   A label to assign to your project. The label must be 128 characters or fewer and can contain letters, numbers, spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-). Specify one label per `--tag` option; for example, `--tag tagA --tag tagB`. This value is *optional*. 

`--wait`, `-w`
:   Create the project and wait for the project to be created. If you specify the `--wait` option, the project create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the project to be created. If the project is not created within the specified `--wait-timeout` period, the project create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the project to be created. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #project-create-example}

```txt
ibmcloud ce project create --name myproject  
```
{: pre}

#### Example output
{: #project-create-example-output}

```txt
Creating project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project current`  
{: #cli-project-current}  

Display the details of the project that is currently targeted.  
  
```txt
ibmcloud ce project current [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-current} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #project-current-example}

```txt
ibmcloud ce project current  
```
{: pre}

#### Example output
{: #project-current-example-output}

```txt
Getting the current project context...
OK

Name:       myproject
ID:         01234567-abcd-abcd-abcd-abcdabcd1111
Subdomain:  aabon2dfwa0
Domain:     us-south.codeengine.appdomain.cloud
Region:     us-south
Kubectl Context:  4svg40kna19

Kubernetes Config:
Context:             aabon2dfwa0
Environment Variable: export KUBECONFIG=/user/myusername/.bluemix/plugins/code-engine/myproject-01234567-abcd-abcd-abcd-abcdabcd1111.yaml
```
{: screen}  
  
### `ibmcloud ce project delete`  
{: #cli-project-delete}  

Delete a project.  
  
```txt
ibmcloud ce project delete (--name PROJECT_NAME | --id PROJECT_ID) [--force] [--hard] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-delete} 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--hard`
:   Immediately delete the project. If you do not specify the `--hard` option, the project can be restored within 7 days by using either the `project restore` or the `reclamation restore` command. This value is *optional*. The default value is `false`.

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--no-wait`, `--nw`
:   Delete the project and do not wait for the project to be deleted. If you specify the `no-wait` option, the project delete begins and does not wait. Use the `project get` command to check the project status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the project and wait for the project to be deleted. If you specify the `--wait` option, the project delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the project to become deleted. If the project is not deleted within the specified `--wait-timeout` period, the project delete fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the project to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #project-delete-example}

```txt
ibmcloud ce project delete --name myproject -f
```
{: pre}

#### Example output
{: #project-delete-example-output}

```txt
Deleting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project get`  
{: #cli-project-get}  

Display the details of a single project.  
  
```txt
ibmcloud ce project get (--name PROJECT_NAME | --id PROJECT_ID) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-get} 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #project-get-example}

```txt
ibmcloud ce project get --name myproject
```
{: pre}

#### Example output
{: #project-get-example-output}

```txt
Getting project 'myproject'...
OK

Name:                       myproject
ID:                         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:                     active
Selected:                   true
Tags:                       tag1, tag2
Region:                     us-south
Resource Group:             default
Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
Age:                        52d
Created:                    Fri, 15 Jan 2021 13:32:30 -0500
Updated:                    Fri, 15 Jan 2021 13:32:45 -0500

Quotas:
    Category                                  Used      Limit
    App revisions                             1         100
    Apps                                      1         100
    Build runs                                0         100
    Builds                                    0         100
    Configmaps                                2         100
    CPU                                       1.025     64
    Ephemeral storage                         902625Ki  256G
    Instances (active)                        1         250
    Instances (total)                         2         2500
    Job runs                                  1         100
    Jobs                                      1         100
    Memory                                    4400M     256G
    Secrets                                   5         100
    Subscriptions (cron)                      0         100
    Subscriptions (IBM Cloud Object Storage)  0         100
```
{: screen}  
  
### `ibmcloud ce project list`  
{: #cli-project-list}  

List all projects.  
  
```txt
ibmcloud ce project list [--all-resource-groups] [--output OUTPUT] [--quiet] [--regions REGIONS] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-list} 

`--all-resource-groups`, `--all`
:   Display projects from all resource groups. By default, projects are only displayed from the current resource group. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--regions`, `-r`
:   Limit the display of projects to specified regions. Provide the name of one or more regions; for example, `us-south,eu-de`. This value is *optional*. 

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #project-list-example}

```txt
ibmcloud ce project list
```
{: pre}

#### Example output
{: #project-list-example-output}

```txt
Getting projects...
OK

Name             ID                                    Status  Selected  Tags  Region    Resource Group  Age
myproj-eude      09768af4-abcd-abcd-abcd-24674ba90db0  active  false           eu-de     default         27d
myproject        cd09cfe1-abcd-abcd-abcd-0f8a8a1d0ddf  active  true            us-south  default         52d
```
{: screen}  
  
### `ibmcloud ce project restore`  
{: #cli-project-restore}  

Restore a project.  
  
```txt
ibmcloud ce project restore (--name PROJECT_NAME | --id PROJECT_ID) [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-restore} 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--no-wait`, `--nw`
:   Restore the project and do not wait for the project to be restored. If you specify the `no-wait` option, the project restore begins and does not wait. Use the `project get` command to check the project status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Restore the project and wait for the project to be restored. If you specify the `--wait` option, the project restore waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the project to be restored. If the project is not restored within the specified `--wait-timeout` period, the project restore fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the project to be restored. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #project-restore-example}

This example restores the `myproject` project that is in `soft deleted` status to an active state. Use the **`project list`** command to display a list of all projects with their status. 

```txt
ibmcloud ce project restore --name myproject
```
{: pre}

#### Example output
{: #project-restore-example-output}

```txt
Restoring project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project select`  
{: #cli-project-select}  

Select a project as the current context. The project must be in `active` status before it can be selected.  
  
```txt
ibmcloud ce project select (--name PROJECT_NAME | --id PROJECT_ID) [--endpoint ENDPOINT] [--kubecfg] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-select} 

`--endpoint`, `-e`
:   The endpoint for the project. Valid values are `public` and `private`. If the `--endpoint` option is not explicitly specified, the behavior is determined by the system. If the {{site.data.keyword.cloud_notm}} CLI is connected to `private.cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `private`. If the {{site.data.keyword.cloud_notm}} CLI is connected to `cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `public`. This value is *optional*. 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--kubecfg`, `-k`
:   Append the project to the Kubernetes configuration file. You can override the default Kubernetes configuration file by setting the `KUBECONFIG` environment variable. This value is *optional*. The default value is `false`.

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #project-select-example}

```txt
ibmcloud ce project select --name myproject
```
{: pre}

#### Example output
{: #project-select-example-output}

```txt
Selecting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project tag`  
{: #cli-project-tag}  

Manages the tags of a single project.  
  
```txt
ibmcloud ce project tag (--name PROJECT_NAME | --id PROJECT_ID) [--quiet] [--tag TAG] [--tag-rm TAG_RM]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-tag} 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--tag`, `-t`
:   A label to assign to your project. The label must be 128 characters or fewer and can contain letters, numbers, spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-). Specify one label per `--tag` option; for example, `--tag tagA --tag tagB`. This value is *optional*. 

`--tag-rm`, `--trm`
:   Remove a label assigned to your project. Specify one label per `--tag-rm` option; for example, `--tag-rm tagA --tag-rm tagB`. This value is *optional*. 

 
  
#### Example
{: #project-tag-example}

```txt
ibmcloud ce project tag --name myproject --tag tag1 --tag tag2
```
{: pre}

#### Example output
{: #project-tag-example-output}

```txt
Getting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project update`  
{: #cli-project-update}  

Update the selected project.  
  
```txt
ibmcloud ce project update (--binding-service-id SERVICE_ID_ID | --binding-resource-group RESOURCE_GROUP_NAME | --binding-resource-group-id RESOURCE_GROUP_ID) [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-project-update} 

`--binding-resource-group`, `--brg`
:   The name of a resource group to use for authentication for the service bindings of this project. A service ID is created with `Operator` and `Manager` roles for all services in this resource group. Use `"*"` to specify all resource groups in this account. This value is *optional*. 

`--binding-resource-group-id`, `--brgid`
:   The ID of a resource group to use for authentication for the service bindings of this project. A service ID is created with `Operator` and `Manager` roles for all services in this resource group. This value is *optional*. 

`--binding-service-id`, `--bsid`
:   The ID of a service ID to use for authentication for the service bindings of this project. This service ID must have the `Operator` role and an appropriate service role for one or more service instances, service types, or resource groups. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #project-update-example}

```txt
ibmcloud ce project update --binding-service-id ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
```
{: pre}

#### Example output
{: #project-update-example-output}

```txt
Configuring your project for service bindings...
Creating service binding API key 'my-project-api-key' for service ID 'my-custom-service-id'...
OK
```
{: screen}  
  
## Reclamation commands  
{: #cli-reclamation}  

Manage {{site.data.keyword.codeengineshort}} project reclamations. Projects that are soft-deleted can be restored within 7 days by using the `reclamation restore` command.  
  
### `ibmcloud ce reclamation delete`  
{: #cli-reclamation-delete}  

Delete a project reclamation.  
  
```txt
ibmcloud ce reclamation delete (--name PROJECT_NAME | --id PROJECT_ID) [--force] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-reclamation-delete} 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--no-wait`, `--nw`
:   Delete the project reclamation and do not wait for the project reclamation to be deleted. If you specify the `no-wait` option, the project reclamation delete begins and does not wait. Use the `reclamation get` command to check the project reclamation status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the project reclamation and wait for the project reclamation to be deleted. If you specify the `--wait` option, the project reclamation delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the project reclamation to be deleted. If the project reclamation is not deleted within the specified `--wait-timeout` period, the project reclamation delete fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the project reclamation to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #reclamation-delete-example}

This example permanently deletes the `myproject` project that is in `soft deleted` status. By using the `--force` option with this command, the delete is forced without confirmation. You can use the  [**`reclamation list`**](/docs/codeengine?topic=codeengine-cli#cli-reclamation-list) command to display a list of all projects that are in `soft deleted` status.  

```txt
ibmcloud ce reclamation delete --name myproject --f
```
{: pre}

#### Example output
{: #reclamation-delete-example-output}

```txt
Hard deleting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce reclamation get`  
{: #cli-reclamation-get}  

Display the details of a single project reclamation.  
  
```txt
ibmcloud ce reclamation get (--name PROJECT_NAME | --id PROJECT_ID) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-reclamation-get} 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #reclamation-get-example}

```txt
ibmcloud ce reclamation get --name myproject
```
{: pre}

#### Example output
{: #reclamation-get-example-output}

```txt
Getting project reclamation
OK

Name:                   myproject
Reclamation ID:         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:                 soft deleted
Region:                 us-south
Resource Group:         default
Age:                    27m
Created:                Thu, 09 Sep 2021 13:24:15 -0400
Updated:                Thu, 09 Sep 2021 13:33:45 -0400
Time to Hard Deletion:  6d23h
```
{: screen}  
  
### `ibmcloud ce reclamation list`  
{: #cli-reclamation-list}  

List all project reclamations.  
  
```txt
ibmcloud ce reclamation list [--all-resource-groups] [--output OUTPUT] [--quiet] [--regions REGIONS] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-reclamation-list} 

`--all-resource-groups`, `--all`
:   Display project reclamations from all resource groups. By default, project reclamations are only displayed from the current resource group. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--regions`, `-r`
:   Limit the display of project reclamations to specified regions. Provide the name of one or more regions; for example, `us-south,eu-de`. This value is *optional*. 

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #reclamation-list-example}

```txt
ibmcloud ce reclamation list
```
{: pre}

#### Example output
{: #reclamation-list-example-output}

```txt
Getting project reclamations...
OK
Name          ID                                    Reclamation ID                        Status        Region    Resource Group  Age   Time to Hard Deletion
myproject     def218c5-abcd-abcd-abcd-97854c288d76  48e3d7a2-abcd-abcd-abcd-99db7152b8fe  soft deleted  us-south  default         40h   6d23h
myproject2    01f0bc66-abcd-abcd-abcd-3ef7e99f6f69  af2cd017-abcd-abcd-abcd-d32e2bb79136  soft deleted  jp-osa    default         8m58s 2d11h
```
{: screen}   
  
### `ibmcloud ce reclamation restore`  
{: #cli-reclamation-restore}  

Restore a project reclamation. Projects that are soft-deleted can be restored within 7 days by using the `reclamation restore` command.  
  
```txt
ibmcloud ce reclamation restore (--name PROJECT_NAME | --id PROJECT_ID) [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-reclamation-restore} 

`--id`, `--guid`
:   The ID of the project. This value is required if `--name` is not specified. 

`--name`, `-n`
:   The name of the project. This value is required if `--id` is not specified. 

`--no-wait`, `--nw`
:   Restore the project reclamation and do not wait for the project reclamation to be restored. If you specify the `no-wait` option, the project reclamation restore begins and does not wait. Use the `reclamation get` command to check the project reclamation status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Restore the project reclamation and wait for the project reclamation to be restored. If you specify the `--wait` option, the project reclamation restore waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the project reclamation to be restored. If the project reclamation is not restored within the specified `--wait-timeout` period, the project reclamation restore fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the project reclamation to be restored. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `600`.

 
  
#### Example
{: #reclamation-restore-example}

This example restores the `myproject` project that is in `soft deleted` status to an active state. Use the **`reclamation list`** command to display a list of all projects that are in `soft deleted` status. 

```txt
ibmcloud ce reclamation restore --name myproject
```
{: pre}

#### Example output
{: #reclamation-restore-example-output}

```txt
Restoring project 'myproject'...
OK
```
{: screen}  
  
## Registry commands  
{: #cli-registry}  

A container registry, or registry, is a service that stores container images. For example, {{site.data.keyword.registryfull_notm}} and Docker Hub are container registries. A container registry can be public or private. A container registry that is public does not require credentials to access. In contrast, accessing a private registry does require credentials.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `registry` commands.

For more information about accessing registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

To see CLI help for the `registry` commands, run `ibmcloud ce registry -h`.
{: tip}  
  
### `ibmcloud ce registry create`  
{: #cli-registry-create}  

Create an image registry access secret.  
  
```txt
ibmcloud ce registry create --name NAME (--password PASSWORD | --password-from-file PASSWORD_FILE | --password-from-json-file) [--email EMAIL] [--output OUTPUT] [--quiet] [--server SERVER] [--username USERNAME]
```
{: pre}

#### Command Options  
 {: #cmd-options-registry-create} 

`-n`, `--name`
:   The name of the image registry access secret. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--email`, `-e`
:   The email address to access the registry server. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--password`, `-p`
:   The password to access the registry server. If neither `--password`, nor `--password-from-file`, nor `--password-from-json-file` option is specified, then you are prompted for the password. This value is *optional*. 

`--password-from-file`, `--pf`
:   The path to a file containing the password to access the registry server. The first line of the file is used for the password. If neither `--password`, nor `--password-from-file`, nor `--password-from-json-file` option is specified, then you are prompted for the password. This value is *optional*. 

`--password-from-json-file`, `--pfj`
:   The path to a JSON file containing the password to access the registry server. The `apikey` field is used for the password. If neither `--password`, nor `--password-from-file`, nor `--password-from-json-file` option is specified, then you are prompted for the password. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--server`, `-s`
:   The URL of the registry server. This value is *optional*. The default value is `us.icr.io`.

`--username`, `-u`
:   The username to access the registry server. This value is *optional*. The default value is `iamapikey`.

 
  
#### Example
{: #registry-create-example}

The following example creates image registry access that is called `myregistry` to a {{site.data.keyword.registryshort}} instance that is located at `us.icr.io` and uses a username of `iamapikey` and the IAM API key as a password.

```txt
ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password API_KEY   
```
{: pre}

#### Example output
{: #registry-create-example-output}

```txt
Creating image registry access secret myregistry...

OK
```
{: screen}  
  
### `ibmcloud ce registry delete`  
{: #cli-registry-delete}  

Delete an image registry access secret.  
  
```txt
ibmcloud ce registry delete --name NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-registry-delete} 

`--name`, `-n`
:   The name of the image registry access secret. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #registry-delete-example}

```txt
ibmcloud ce registry delete --name myregistry -f   
```
{: pre}

#### Example output
{: #registry-delete-example-output}

```txt
Deleting image registry access secret myregistry...

OK
```
{: screen}  
  
### `ibmcloud ce registry get`  
{: #cli-registry-get}  

Display the details of an image registry access secret.  
  
```txt
ibmcloud ce registry get --name NAME [--decode] [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-registry-get} 

`--name`, `-n`
:   The name of the image registry access secret. This value is *required*. 

`--decode`, `-d`
:   Show the `Data` output as decoded in the details. If this option is not specified, the `Data` details are base64-encoded. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #registry-get-example}

```txt
ibmcloud ce registry get --name myregistry   
```
{: pre}

#### Example output
{: #registry-get-example-output}

```txt
Getting image registry access secret myregistry...
OK

Name:        myregistry
Project:     myproject
Project ID:  01234567-abcd-abcd-abcd-abcdabcd1111
Created:     2021-02-23T09:10:01-05:00
Data:
---
.dockerconfigjson: abcdabcdabcdabcdabcdnVzZXJuYW1lIjoiaWFtYXBpa2V5IiwicGFzc3dvcmQiOiJoQllTSTc5Uk8yQUIxSDV3RUs2UzhScV9uNzE4NkQ1eWt1M1FOUk85aFpfaCIsImVtYWlsIjoiYUBiLmMiLCabcdabcdabcdabcdabcdT21oQ1dWTkpOemxTVHpKQlFqRklOWGRGU3paVE9GSnhYMjQzTVRnMlJEVjabcdabcdabcdabcdabcdbG9XbDlvIn19fQ==
```
{: screen}  
  
### `ibmcloud ce registry list`  
{: #cli-registry-list}  

List all image registry access secrets in a project.  
  
```txt
ibmcloud ce registry list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-registry-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #registry-list-example}

```txt
ibmcloud ce registry list   
```
{: pre}

#### Example output
{: #registry-list-example-output}

```txt
Listing image registry access secrets...

OK

Name        Age
myregistry  19m22s
```
{: screen}  
  
### `ibmcloud ce registry update`  
{: #cli-registry-update}  

Update an image registry access secret.  
  
```txt
ibmcloud ce registry update --name NAME [--email EMAIL] [--output OUTPUT] [--password PASSWORD] [--password-from-file PASSWORD_FROM_FILE] [--password-from-json-file PASSWORD_FROM_JSON_FILE] [--quiet] [--server SERVER] [--username USERNAME]
```
{: pre}

#### Command Options  
 {: #cmd-options-registry-update} 

`--name`, `-n`
:   The name of the image registry access secret. This value is *required*. 

`--email`, `-e`
:   The email address to access the registry server. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--password`, `-p`
:   The password to access the registry server. This value is *optional*. 

`--password-from-file`, `--pf`
:   The path to a file containing the password to access the registry server. The first line of the file is used for the password. This value is *optional*. 

`--password-from-json-file`, `--pfj`
:   The path to a JSON file containing the password to access the registry server. The `apikey` field is used for the password. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--server`, `-s`
:   The URL of the registry server. This value is *optional*. 

`--username`, `-u`
:   The username to access the registry server. This value is *optional*. 

 
  
#### Example
{: #registry-update-example}

The following example updates a password for the image registry access that is called `myregistry`. 

```txt
ibmcloud ce registry update --name myregistry --password NEW_API_KEY  
```
{: pre}

#### Example output
{: #registry-update-example-output}

```txt
Getting image registry access secret 'myregistry'...
Updating image registry access secret 'myregistry'...

OK
```
{: screen}  
  
## Repo commands  
{: #cli-repo}  

A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `repo` commands.

For more information about accessing repositories, see [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

To see CLI help for the `repo` commands, run `ibmcloud ce repo -h`.
{: tip}  
  
### `ibmcloud ce repo create`  
{: #cli-repo-create}  

Create a Git repository access secret.  
  
```txt
ibmcloud ce repo create --name SECRET_NAME --key-path SSH_KEY_PATH --host HOST_ADDRESS [--known-hosts-path KNOWN_HOSTS_PATH] [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-repo-create} 

`--host`, `--ho`
:   The address of the host; for example `github.com`. This value is *required*. 

`--key-path`, `--kp`
:   The path to your unencrypted SSH private key file. If you use your personal private SSH key, then this file is usually located at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa` (Windows). This value is *required*. 

`-n`, `--name`
:   The name of the Git repository access secret. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--known-hosts-path`, `--khp`
:   The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #repo-create-example}

The following command creates a Git access secret called `github` for host `github.com` and authenticates with an SSH key located at `/<filepath>/.ssh/id_rsa`, where `<filepath>` is the path on your system.

```txt
ibmcloud ce repo create -n github --key-path /<filepath>/.ssh/id_rsa --host github.com  
```
{: pre}

#### Example output
{: #repo-create-example-output}

```txt
Creating Git access secret github...
OK
```
{: screen}  
  
### `ibmcloud ce repo delete`  
{: #cli-repo-delete}  

Delete a Git repository access secret.  
  
```txt
ibmcloud ce repo delete --name NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-repo-delete} 

`--name`, `-n`
:   The name of the Git repository access secret. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #repo-delete-example}

```txt
ibmcloud ce repo delete --name github
```
{: pre}

#### Example output
{: #repo-delete-example-output}

```txt
Are you sure you want to delete the Git access secret github? [y/N]> y
Deleting Git access secret github...
OK

```
{: screen}  
  
### `ibmcloud ce repo get`  
{: #cli-repo-get}  

Display the details of a Git repository access secret.  
  
```txt
ibmcloud ce repo get --name NAME [--decode] [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-repo-get} 

`--name`, `-n`
:   The name of the Git repository access secret. This value is *required*. 

`--decode`, `-d`
:   Show the `Data` output as decoded in the details. If this option is not specified, the `Data` details are base64-encoded. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #repo-get-example}

```txt
ibmcloud ce repo get -n github
```
{: pre}

#### Example output
{: #repo-get-example-output}

```txt
Getting Git access secret github...
OK

Name:        github  
Project:     myproject  
Project ID:  01234567-abcd-abcd-abcd-abcdabcd1111 
Age:         30s  
Created:     2021-03-14T14:05:56-05:00  
Host:        github.com

Data:          
---
ssh-privatekey: 
ABCDABCDABCDABCDABCDU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjABCDABCDABCDABCDhrdGRqRUFBQUFBQ21GbGN6STFOaABCDABCDABCDABCDABCDABCDE
...
```
{: screen}  
  
### `ibmcloud ce repo list`  
{: #cli-repo-list}  

List all Git repository access secrets in a project.  
  
```txt
ibmcloud ce repo list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-repo-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #repo-list-example}

```txt
ibmcloud ce repo list
```
{: pre}

#### Example output
{: #repo-list-example-output}

```txt
Listing Git access secrets...
OK

Name    Age  
github  13m0s  
```
{: screen}  
  
### `ibmcloud ce repo update`  
{: #cli-repo-update}  

Update a Git repository access secret.  
  
```txt
ibmcloud ce repo update --name SECRET_NAME [--host HOST] [--key-path KEY_PATH] [--known-hosts-path KNOWN_HOSTS_PATH] [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-repo-update} 

`--name`, `-n`
:   The name of the Git repository access secret. This value is *required*. 

`--host`, `--ho`
:   The address of the host; for example `github.com`. This value is *optional*. 

`--key-path`, `--kp`
:   The path to your unencrypted SSH private key file. If you use your personal private SSH key, then this file is usually located at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa` (Windows). This value is *optional*. 

`--known-hosts-path`, `--khp`
:   The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #repo-update-example}

The following command updates a Git access secret that is called `github` to use a new host.

```txt
ibmcloud ce repo update  -n github --host NEW_HOST  
```
{: pre}

#### Example output
{: #repo-update-example-output}

```txt
Getting Git access secret 'github'...
Updating Git access secret 'github'...
OK
```
{: screen}  
  
## Revision commands  
{: #cli-revision}  

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeenginefull}} also supports applications that use WebSockets as their communications protocol.  An app contains one or more *revisions*. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

Use `revision` commands to manage application revisions.

You must be within the context of a [project](#cli-project) before you use `revision` commands.

For more information about working with revisions for apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

You can use either `revision` or `rev` in your `revision` commands. To see CLI help for the `revision` commands, run `ibmcloud ce revision -h`.
{: tip}  
  
### `ibmcloud ce revision delete`  
{: #cli-revision-delete}  

Delete an application revision.  
  
```txt
ibmcloud ce revision delete --name REVISION_NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-revision-delete} 

`--name`, `-n`
:   The name of the application revision. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #revision-delete-example}

```txt
ibmcloud ce revision delete -n newapp-mytest-00004 -f
```
{: pre}

#### Example output
{: #revision-delete-example-output}

```txt
Deleting application revision 'newapp-mytest-00004'...
OK
```
{: screen}  
  
### `ibmcloud ce revision events`  
{: #cli-revision-events}  

Display the events of application revision instances.  
  
```txt
ibmcloud ce revision events (--instance REVISION_INSTANCE | --revision REVISION_NAME) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-revision-events} 

`--instance`, `-i`
:   The name of a specific application instance. Use the `rev get` command to find the instance name. This value is required if `--revision` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--revision`, `--rev`, `-r`, `--name`, `-n`
:   Display the events of all the instances of the specified application revision. This value is required if `--instance` is not specified. 

 
  
#### Example
{: #revision-events-example}

```txt
ibmcloud ce revision events -n myapp-00001
```
{: pre}

#### Example output
{: #revision-events-example-output}

{{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are not retained.
{: note}

```txt
Getting application revision 'newapp-mytest-00002'...
Getting events for all instances of application revision 'newapp-mytest-00002'...
OK

newapp-mytest-00002-deployment-7c87cfbf66-xnwkp:
Type     Reason     Age                Source                Messages
Normal   Scheduled  65s                default-scheduler     Successfully assigned bz8i2yh012p/newapp-mytest-00002-deployment-7c87cfbf66-xnwkp to 10.243.0.60
Normal   Pulling    63s                kubelet, 10.243.0.60  Pulling image "icr.io/codeengine/codeengine@sha256:b3150372958ab68eea5356a8cab31069ca5293c45959d64f6aaabbccddeeff123"
Normal   Created    60s                kubelet, 10.243.0.60  Created container queue-proxy
Normal   Created    60s                kubelet, 10.243.0.60  Created container user-container
Normal   Started    60s                kubelet, 10.243.0.60  Started container user-container
Normal   Pulled     60s                kubelet, 10.243.0.60  Container image "icr.io/obs/codeengine/knative-serving/knative.dev/serving/cmd/queue:v0.20.0-rc11@sha256:3fedfa9d9cdd74e85d11d4167043f13902074946caf415d16ff537620f04931a" already present on machine
Normal   Pulled     60s                kubelet, 10.243.0.60  Successfully pulled image "icr.io/codeengine/codeengine@sha256:b3150372958ab68eea5356a8cab31069ca5293c45959d64f6aaabbccddeeff123" in 2.67237432s
Normal   Started    60s                kubelet, 10.243.0.60  Started container queue-proxy
Normal   Pulling    60s                kubelet, 10.243.0.60  Pulling image "icr.io/obs/codeengine/istio/proxyv2:1.9.1-rc7"
Normal   Pulled     59s                kubelet, 10.243.0.60  Successfully pulled image "icr.io/obs/codeengine/istio/proxyv2:1.9.1-rc7" in 666.211288ms
Normal   Created    59s                kubelet, 10.243.0.60  Created container istio-proxy
Normal   Started    59s                kubelet, 10.243.0.60  Started container istio-proxy
```
{: screen}  
  
### `ibmcloud ce revision get`  
{: #cli-revision-get}  

Display the details of an application revision.  
  
```txt
ibmcloud ce revision get --name REVISION_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-revision-get} 

`--name`, `-n`
:   The name of the application revision. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #revision-get-example}

```txt
ibmcloud ce revision get --name newapp-mytest-00002
```
{: pre}

#### Example output
{: #revision-get-example-output}

```txt
Getting application revision 'newapp-mytest-00002'...
Getting application 'newapp-mytest'...
OK

Name:            newapp-mytest-00002
ID:              abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:    myproject
Project ID:      01234567-abcd-abcd-abcd-abcdabcd1111
Age:             27d
Created:         2021-05-05T11:50:00-04:00
Status Summary:  Revision is ready

Environment Variables:
    Type                      Name               Value
    ConfigMap full reference  mycolorconfigmap 
    Literal                   TARGET             Sunshine
Image:                  icr.io/codeengine/codeengine
Resource Allocation:
    CPU:                1
    Ephemeral Storage:  400M
    Memory:             4G
Port:                   8080

Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  0
    Timeout:        300

Conditions:
    Type                OK     Age    Reason
    Active              false  5d22h  NoTraffic : The target is not receiving traffic.
    ContainerHealthy    true   5d22h
    Ready               true   5d22h
    ResourcesAvailable  true   5d22h
```
{: screen}  
  
### `ibmcloud ce revision list`  
{: #cli-revision-list}  

List all application revisions in a project.  
  
```txt
ibmcloud ce revision list [--application APPLICATION] [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-revision-list} 

`--application`, `--app`, `-a`
:   Use this option to only display revisions from the specified application. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #revision-list-example}

```txt
ibmcloud ce revision list 
```
{: pre}

#### Example output
{: #revision-list-example-output}

{{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are not retained.
{: note}

```txt
Listing all application revisions...
OK

Name                   Application      Status  URL  Latest  Tag  Traffic  Age    Conditions  Reason
myapp-hc3u8-2           myapp            Ready                              16d    3 OK / 4
myapp-hc3u8-3           myapp            Ready        true         100%    2d8h    3 OK / 4  
newapp-mytest-00004     newapp-mytest    Ready                              4d20h  3 OK / 4
newapp-mytest-00005     newapp-mytest    Ready        true         100%     2d20h  3 OK / 4
```
{: screen}  
  
### `ibmcloud ce revision logs`  
{: #cli-revision-logs}  

Display the logs of application revision instances.  
  
```txt
ibmcloud ce revision logs (--instance REVISION_INSTANCE | --revision REVISION_NAME) [--all-containers] [--follow] [--output OUTPUT] [--quiet] [--tail TAIL] [--timestamps]
```
{: pre}

#### Command Options  
 {: #cmd-options-revision-logs} 

`--all-containers`, `--all`
:   Display the logs of all containers of the specified application revision instances. This value is *optional*. The default value is `false`.

`--follow`, `-f`
:   Follow the logs of application revision instances. Use this option to stream logs of application revision instances. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is *optional*. The default value is `false`.

`--instance`, `-i`
:   The name of a specific application revision instance. Use the `revision get` command to find the instance name. This value is required if `--revision` is not specified. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--revision`, `--rev`, `-r`, `--name`, `-n`
:   Display the logs of all the instances of the specified application revision. This value is required if `--instance` is not specified. 

`--tail`, `-t`
:   Limit the display of logs of containers of the specified application revision instances to a maximum number of recent lines per container. For example, to display the last `3` lines of the logs of the containers of the specified application revision instances, specify `--tail 3`. If this option is not specified, all lines of the logs of the containers of the specified application revision instances are displayed. This value is *optional*. The default value is `-1`.

`--timestamps`, `--ts`
:   Include timestamps on each line in the log output. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #revision-logs-example}

```txt
ibmcloud ce revision logs -n myapp-00001 
```
{: pre}

#### Example output
{: #revision-logs-example-output}

{{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are not retained.
{: note}

```txt
Getting logs for all instances of application revision 'newapp-mytest-00002'...
Getting application revision 'newapp-mytest-00002'...
OK

newapp-mytest-00002-deployment-7c87cfbf66-xnwkp/user-container:
2021-07-15 20:40:56 Listening on port 8080
```
{: screen}  
  
## Secret commands  
{: #cli-secret}  

A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `secret` commands.

For more information about working with secrets, see [Setting up and using secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret).

To see CLI help for the `secret` commands, run `ibmcloud ce secret -h`.
{: tip}  
  
### `ibmcloud ce secret create`  
{: #cli-secret-create}  

Create a generic secret.  
  
```txt
ibmcloud ce secret create --name SECRET_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-secret-create} 

`-n`, `--name`
:   The name of the generic secret. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--from-env-file`, `-e`
:   Create a generic secret from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. This value is required if `--from-literal` or `--from-file` is not specified. 

`--from-file`, `-f`
:   Create a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 

`--from-literal`, `-l`
:   Create a generic secret from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. This option can be specified multiple times. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #secret-create-example}

The following example creates a secret that is named `mysecret-fromliteral` with a username and password value pair.

```txt
ibmcloud ce secret create --name mysecret-fromliteral --from-literal username=devuser --from-literal password='S!B\*d$zDsb'
```
{: pre}

#### Example output
{: #secret-create-example-output}

```txt
Creating secret mysecret-fromliteral...
OK
```
{: screen}

#### Example of a secret with values from a file
{: #secret-create-example2}

The following example creates a secret that is named `mysecret-fromfile` with values from a file.

```txt
ibmcloud ce secret create --name mysecret-fromfile  --from-file ./username.txt --from-file ./password.txt
```
{: pre}

##### Example output of a secret with values from a file
{: #secret-create-example2-output}

```txt
Creating secret mysecret-fromfile...
OK
```
{: screen}
  
  
### `ibmcloud ce secret delete`  
{: #cli-secret-delete}  

Delete a generic secret.  
  
```txt
ibmcloud ce secret delete --name SECRET_NAME [--force] [--ignore-not-found] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-secret-delete} 

`--name`, `-n`
:   The name of the generic secret. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #secret-delete-example}

```txt
ibmcloud ce secret delete --name mysecret-fromfile -f
```
{: pre}

#### Example output
{: #secret-delete-example-output}

```txt
Deleting secret mysecret-fromfile...
OK
```
{: screen}  
  
### `ibmcloud ce secret get`  
{: #cli-secret-get}  

Display the details of a generic secret.  
  
```txt
ibmcloud ce secret get --name SECRET_NAME [--decode] [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-secret-get} 

`--name`, `-n`
:   The name of the generic secret. This value is *required*. 

`--decode`, `-d`
:   Show the `Data` output as decoded in the details. If this option is not specified, the `Data` details are base64-encoded. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #secret-get-example}

```txt
ibmcloud ce secret get --name mysecret-fromliteral
```
{: pre}

#### Example output
{: #secret-get-example-output}

```txt
Getting generic secret 'mysecret-fromliteral'...
OK

Name:          mysecret-fromliteral
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           66s
Created:       2021-03-10T18:44:18-05:00

Data:
---
password: UyFCXCpkJHpEc2I=
username: ZGV2dXNlcg==
```
{: screen}  
  
### `ibmcloud ce secret list`  
{: #cli-secret-list}  

List all generic secrets in a project.  
  
```txt
ibmcloud ce secret list [--all] [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-secret-list} 

`--all`, `-a`
:   Display all secrets of all types, including `generic`, `image registry access`, `Git repo`, and other types that are not managed by {{site.data.keyword.codeengineshort}}. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #secret-list-example}

```txt
ibmcloud ce secret list
```
{: pre}

#### Example output
{: #secret-list-example-output}

```txt
Listing secrets...
OK

Name                  Data  Age
mysecret-fromfile     2     20m38s
mysecret-fromliteral  2     30m38s
```
{: screen}  
  
### `ibmcloud ce secret update`  
{: #cli-secret-update}  

Update a generic secret.  
  
```txt
ibmcloud ce secret update --name SECRET_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE | --rm KEY) [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-secret-update} 

`--name`, `-n`
:   The name of the generic secret. This value is *required*. 

`--from-env-file`, `-e`
:   Update a generic secret from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. This value is required if `--from-literal` or `--from-file` is not specified. 

`--from-file`, `-f`
:   Update a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 

`--from-literal`, `-l`
:   Update a generic secret from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. This option can be specified multiple times. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--rm`
:   Remove an individual key-value pair in a generic secret by specifying the name of the key. This option can be specified multiple times. This value is *optional*. 

 
  
#### Example
{: #secret-update-example}

```txt
ibmcloud ce secret update --name mysecret-fromliteral --from-literal username=newuser --from-literal password='A!E\*$aBcD'
```
{: pre}


#### Example output
{: #secret-update-example-output}

```txt
Updating secret mysecret-fromliteral...
OK
```
{: screen}  
  
## Subscription cos commands  
{: #cli-subscription-cos}  

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


The {{site.data.keyword.cos_short}} event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform an action based on that change, perhaps consuming that new object.

You must be within the context of a [project](#cli-project) before you use `subscription cos` commands.

For more information about working with the {{site.data.keyword.cos_full_notm}} subscriptions, see [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer). See [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events) for more information about working with subscriptions in {{site.data.keyword.codeengineshort}}.

You can use either `subscription` or `sub` in your `subscription cos` commands. To see CLI help for the `subscription cos` command, run `ibmcloud ce sub cos -h`. 
{: tip}  
  
### `ibmcloud ce subscription cos create`  
{: #cli-subscription-cos-create}  

Create an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```txt
ibmcloud ce subscription cos create --name COS_SOURCE_NAME --destination DESTINATION_REF --bucket BUCKET_NAME [--destination-type DESTINATION_TYPE] [--event-type EVENT_TYPE] [--extension EXTENSION] [--force] [--no-wait] [--output OUTPUT] [--path PATH] [--prefix PREFIX] [--quiet] [--suffix SUFFIX] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cos-create} 

`--bucket`, `-b`
:   The bucket for events. The destination and the bucket must be in the same region of the project. This value is *required*. 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *required*. 

`-n`, `--name`
:   The name of the {{site.data.keyword.cos_full_notm}} event subscription. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. The default value is `app`.

`--event-type`, `-e`
:   The event types to watch. Valid values are `delete`, `write`, and `all`. This value is *optional*. The default value is `all`.

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--force`, `-f`
:   Force to create an {{site.data.keyword.cos_full_notm}} event subscription. This option skips the validation of the specified destination. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Create the {{site.data.keyword.cos_full_notm}} event subscription and do not wait for the subscription to be ready. If you specify the `--no-wait` option, the subscription create begins and does not wait. Use the `subscription cos get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--prefix`, `-p`
:   Prefix of the {{site.data.keyword.cos_full_notm}} object. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--suffix`, `-s`
:   Suffix of the {{site.data.keyword.cos_full_notm}} object. Consider the file type of your file when specifying the suffix. This value is *optional*. 

`--wait`, `-w`
:   Create the {{site.data.keyword.cos_full_notm}} event subscription and wait for the subscription to be ready. If you specify the `--wait` option, the subscription create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to become ready. If the subscription is not ready within the specified `--wait-timeout` period, the {{site.data.keyword.cos_full_notm}} event subscription create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the {{site.data.keyword.cos_full_notm}} event subscription to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `15`.

 
  
#### Example
{: #subscription-cos-create-example}

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. The following example creates a COS subscription called `mycosevent` for a bucket called `mybucket` that is attached to an app called `myapp`. The `--destination-type` option specifies the type of the `destination` which is `app` or `job`.  For this example, the `--destination-type` is `app`, which is the default for this option. The event is sent to the `/events` path by using the `--path` option so that the event is sent to `https://<base application URL>/events`.

```txt
ibmcloud ce subscription cos create --name mycosevent --destination myapp --bucket mybucket --destination-type app --path /events
```
{: pre}

#### Example output
{: #subscription-cos-create-example-output}

```txt
Creating COS source 'mycosevent'...
Run 'ibmcloud ce subscription cos get -n mycosevent' to check the COS source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription cos delete`  
{: #cli-subscription-cos-delete}  

Delete an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```txt
ibmcloud ce subscription cos delete --name COS_SOURCE_NAME [--force] [--ignore-not-found] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cos-delete} 

`--name`, `-n`
:   The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Delete the {{site.data.keyword.cos_full_notm}} event subscription and do not wait for the subscription to be deleted. If you specify the `--no-wait` option, the subscription delete begins and does not wait. Use the `subscription cos get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the {{site.data.keyword.cos_full_notm}} event subscription and wait for the subscription to be deleted. If you specify the `--wait` option, the subscription delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to be deleted. This command exits when the subscription is deleted or whenever `--wait-timeout` is reached, whichever comes first. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the {{site.data.keyword.cos_full_notm}} event subscription to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `15`.

 
  
#### Example
{: #subscription-cos-delete-example}

```txt
ibmcloud ce subscription cos delete --name mycosevent -f
```
{: pre}

#### Example output
{: #subscription-cos-delete-example-output}

```txt
Deleting COS source 'mycosevent'...
OK
```
{: screen}  
  
### `ibmcloud ce subscription cos get`  
{: #cli-subscription-cos-get}  

Display the details of an {{site.data.keyword.cos_full_notm}} event subscription. Displayed attributes include `Name`, `Destination`, `Bucket`, `Event Type`, `Prefix`, `Suffix`, `Ready`, and `Age`. To see specific details, attach `| grep <attribute>`.  
  
```txt
ibmcloud ce subscription cos get --name COS_SOURCE_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cos-get} 

`--name`, `-n`
:   The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #subscription-cos-get-example}

```txt
ibmcloud ce subscription cos get --name mycosevent
```
{: pre}

#### Example output
{: #subscription-cos-get-example-output}

```txt
Getting COS source 'mycosevent'...
OK

Name:          mycosevent
ID:            abcdefgh-abcd-abcd-abcd-fb6be2347a14  
Project Name:  myproject 
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           12s  
Created:       2021-03-14T13:28:45-05:00  

Destination:  App:myapp
Bucket:       mybucket
EventType:    all 
Ready:        true  

Conditions:    
    Type            OK    Age  Reason  
    CosConfigured   true  10s    
    Ready           true  10s    
    ReadyForEvents  true  10s    
    SinkProvided    true  10s    

Events:        
    Type    Reason          Age  Source                Messages  
    Normal  CosSourceReady  11s  cossource-controller  CosSource is ready  
```
{: screen}

When `Ready` is `true`, then the COS subscription is ready to trigger events per changes to the COS bucket. 
  
  
### `ibmcloud ce subscription cos list`  
{: #cli-subscription-cos-list}  

List all {{site.data.keyword.cos_full_notm}} event subscriptions in a project.  
  
```txt
ibmcloud ce subscription cos list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cos-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #subscription-cos-list-example}

```txt
ibmcloud ce subscription cos list
```
{: pre}

#### Example output
{: #subscription-cos-list-example-output}

```txt
Listing COS sources...
OK

Name        Age  Ready  Bucket        EventType  Prefix  Suffix  Destination
mycosevent  20m  true   mycosbucket  all                         http://myapp.2706b22d-676b.svc.cluster.local
```
{: screen}  
  
### `ibmcloud ce subscription cos update`  
{: #cli-subscription-cos-update}  

Update an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```txt
ibmcloud ce subscription cos update --name COS_SOURCE_NAME [--destination DESTINATION] [--destination-type DESTINATION_TYPE] [--event-type EVENT_TYPE] [--extension EXTENSION] [--extension-rm EXTENSION_RM] [--output OUTPUT] [--path PATH] [--prefix PREFIX] [--quiet] [--suffix SUFFIX]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cos-update} 

`--name`, `-n`
:   The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is *required*. 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *optional*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. 

`--event-type`, `-e`
:   The event types to watch. Valid values are `delete`, `write`, and `all`. This value is *optional*. 

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--extension-rm`, `--ext-rm`
:   Remove CloudEvents extensions to send to the destination by specifying the name of the key. Specify one extension per `--ext-rm` option; for example, `--ext-rm extA --ext-rm extB`. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--prefix`, `-p`
:   Prefix of the IBM Cloud Object Storage object. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--suffix`, `-s`
:   Suffix of the IBM Cloud Object Storage object. Consider the file type (extension) of your file when specifying the suffix. This value is *optional*. 

 
  
#### Example
{: #subscription-cos-update-example}

The following example updates a COS subscription called `mycosevent` to listen for only write events. 

```txt
ibmcloud ce subscription cos update --name mycosevent --event-type write
```
{: pre}

#### Example output
{: #subscription-cos-update-example-output}

```txt
Updating COS source 'mycosevent'...
Run 'ibmcloud ce subscription cos get -n mycosevent' to check the COS source status.
OK
```
{: screen}  
  
## Subscription cron commands  
{: #cli-subscription-cron}  

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


The cron event producer is based on cron and generates an event at regular intervals. Use a cron event producer when an action needs to be taken at well-defined intervals or at specific times.

You must be within the context of a [project](#cli-project) before you use `subscription cron` commands.

For more information about working with the {{site.data.keyword.cos_full_notm}} subscriptions, see [Working with the Periodic timer (cron) event producer](/docs/codeengine?topic=codeengine-subscribe-cron). See [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events) for more information about working with subscriptions in {{site.data.keyword.codeengineshort}}.

You can use either `subscription` or `sub` in your `subscription cron` commands. To see CLI help for the `subscription cron` command, run `ibmcloud ce sub cron -h`. 
{: tip}  
  
### `ibmcloud ce subscription cron create`  
{: #cli-subscription-cron-create}  

Create a cron event subscription.  
  
```txt
ibmcloud ce subscription cron create --name CRON_SOURCE_NAME  --destination DESTINATION_REF [--content-type CONTENT_TYPE] [--data DATA] [--data-base64 DATA_BASE64] [--destination-type DESTINATION_TYPE] [--extension EXTENSION] [--force] [--no-wait] [--output OUTPUT] [--path PATH] [--quiet] [--schedule SCHEDULE] [--time-zone TIME_ZONE] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cron-create} 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *required*. 

`-n`, `--name`
:   The name of the cron event subscription. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--content-type`, `--ct`
:   The media type of the `--data` or `--data-base64` option. Examples include `application/json`, `application/x-www-form-urlencoded`, `text/html`, and `text/plain`. This value is *optional*. 

`--da`, `--data`
:   The data to send to the destination; for example, `'{ "message": "Hello world!" }'`. If you specify the `--data` option, do not use the `--data-base64` option.


   This value is *optional*. 

`--data-base64`, `--db`
:   The base64-encoded data to send to the destination; for example, `Q29kZSBFbmdpbmU=`. If you specify the `--data-base64` option, do not use the `--data` option. This value is *optional*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. The default value is `app`.

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--force`, `-f`
:   Force to create a cron event subscription. This option skips the validation of the specified destination. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Create the cron event subscription and do not wait for the subscription to be ready. If you specify the `--no-wait` option, the subscription create begins and does not wait. Use the `subscription cron get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--schedule`, `-s`
:   Schedule how often the event is triggered, in crontab format. For example, specify `'*/2 * * * *'` (in string format) for every two minutes. By default, the cron event is triggered every minute and is set to the `UTC` time zone. To modify the time zone, use the `--time-zone` option. This value is *optional*. 

`--time-zone`, `--tz`
:   Set the time zone for your cron event; for example, `Asia/Tokyo`. If you specify the `--schedule` option, use this option to specify the time zone. For valid time zone values, see the [time zones database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). This value is *optional*. The default value is `UTC`.

`--wait`, `-w`
:   Create the cron event subscription and wait for the subscription to be ready. If you specify the `--wait` option, the subscription create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to become ready. If the subscription is not ready within the specified `--wait-timeout` period, the cron event subscription create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the cron event subscription to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `15`.

 
  
#### Example
{: #subscription-cron-create-example}

The following example creates a cron subscription that is called `mycronevent` that forwards a cron event to a job that is called `myjob` every 2 minutes.

```txt
ibmcloud ce subscription cron create --name mycronevent --destination myjob --schedule '*/2 * * * *' --destination-type job
```
{: pre}

#### Example output
{: #subscription-cron-create-example-output}

```txt
Creating cron source 'mycronevent'...
Run 'ibmcloud ce subscription cron get -n mycronevent' to check the cron source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription cron delete`  
{: #cli-subscription-cron-delete}  

Delete a cron event subscription.  
  
```txt
ibmcloud ce subscription cron delete --name CRON_SOURCE_NAME [--force] [--ignore-not-found] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cron-delete} 

`--name`, `-n`
:   The name of the cron event subscription. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--ignore-not-found`, `--inf`
:   If not found, do not fail. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Delete the cron event subscription and do not wait for the subscription to be deleted. If you specify the `--no-wait` option, the subscription delete begins and does not wait. Use the `subscription cron get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the cron event subscription and wait for the subscription to be deleted. If you specify the `--wait` option, the subscription delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to be deleted. This command exits when the subscription is deleted or whenever `--wait-timeout` is reached, whichever comes first. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the cron event subscription to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `15`.

 
  
#### Example
{: #subscription-cron-delete-example}

```txt
ibmcloud ce subscription cron delete --name mycronevent -f
```
{: pre}

#### Example output
{: #subscription-cron-delete-example-output}

```txt
Deleting cron source 'mycronevent'...
OK
```
{: screen}  
  
### `ibmcloud ce subscription cron get`  
{: #cli-subscription-cron-get}  

Display details of a cron event subscription.  
  
```txt
ibmcloud ce subscription cron get --name CRON_SOURCE_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cron-get} 

`--name`, `-n`
:   The name of the cron event subscription. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #subscription-cron-get-example}

```txt
ibmcloud ce subscription cron get --name mycronevent
```
{: pre}

#### Example output
{: #subscription-cron-get-example-output}

```txt
Getting cron source 'mycronevent'...
OK

Name:          mycronevent  
ID:            abcdefgh-abcd-abcd-abcd-fb6be2347a14  
Project Name:  myproject  
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           18s  
Created:       2021-03-14T13:33:53-05:00  

Destination:  App:kapp  
Schedule:     */2 * * * *  
Time Zone:    UTC  
Ready:        true 

Events:    
    Type     Reason           Age                Source                 Messages  
    Normal   FinalizerUpdate  19s                pingsource-controller  Updated "mycronevent" finalizers  
```
{: screen}

When `Ready` is `true`, then the cron subscription is ready to trigger events per the specified schedule. 
  
  
### `ibmcloud ce subscription cron list`  
{: #cli-subscription-cron-list}  

List all cron event subscriptions in a project.  
  
```txt
ibmcloud ce subscription cron list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cron-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #subscription-cron-list-example}

```txt
ibmcloud ce subscription cron list
```
{: pre}

#### Example output
{: #subscription-cron-list-example-output}

```txt
Listing cron sources...
OK

Name         Age  Ready  Destination                                   Schedule     Data
mycronevent  96m  true   http://myapp.cd4200a7-5037.svc.cluster.local  */2 * * * *
```
{: screen}  
  
### `ibmcloud ce subscription cron update`  
{: #cli-subscription-cron-update}  

Update a cron event subscription.  
  
```txt
ibmcloud ce subscription cron update --name CRON_SOURCE_NAME [--content-type CONTENT_TYPE] [--data DATA] [--data-base64 DATA_BASE64] [--destination DESTINATION] [--destination-type DESTINATION_TYPE] [--extension EXTENSION] [--extension-rm EXTENSION_RM] [--output OUTPUT] [--path PATH] [--quiet] [--schedule SCHEDULE] [--time-zone TIME_ZONE]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-cron-update} 

`--name`, `-n`
:   The name of the cron event subscription. This value is *required*. 

`--content-type`, `--ct`
:   The media type of the `--data` or `--data-base64` option. Examples include `application/json`, `application/x-www-form-urlencoded`, `text/html`, and `text/plain`. This value is *optional*. 

`--da`, `--data`
:   The data to send to the destination; for example, `'{ "message": "Hello world!" }'`. If you specify the `--data` option, do not use the `--data-base64` option.


   This value is *optional*. 

`--data-base64`, `--db`
:   The base64-encoded data to send to the destination; for example, `Q29kZSBFbmdpbmU=`. If you specify the `--data-base64` option, do not use the `--data` option. This value is *optional*. 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *optional*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. 

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--extension-rm`, `--ext-rm`
:   Remove CloudEvents extensions to send to the destination by specifying the name of the key. Specify one extension per `--ext-rm` option; for example, `--ext-rm extA --ext-rm extB`. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--schedule`, `-s`
:   Schedule how often the event is triggered, in crontab format. For example, specify `'*/2 * * * *'` (in string format) for every two minutes. By default, the cron event is triggered every minute and is set to the `UTC` time zone. To modify the time zone, use the `--time-zone` option. This value is *optional*. 

`--time-zone`, `--tz`
:   Set the time zone for your cron event; for example, `Asia/Tokyo`. If you specify the `--schedule` option, use this option to specify the time zone. For valid time zone values, see the [time zones database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). This value is *optional*. 

 
  
#### Example
{: #subscription-cron-update-example}

The following example updates a cron source subscription that is called `mycronevent` that forwards a cron event to a job that is called `myjob` every hour. 

```txt
ibmcloud ce subscription cron update --name mycronevent --destination myjob --schedule '0 * * * *' --destination-type job
```
{: pre}

#### Example output
{: #subscription-cron-update-example-output}

```txt
Updating cron source 'mycronevent'...
Run 'ibmcloud ce subscription cron get -n mycronevent' to check the cron source status.
OK
```
{: screen}  
  
## Subscription kafka commands  
{: #cli-subscription-kafka}  

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


The Kafka event producer watches for new messages to appear in a Kafka instance. When you create a {{site.data.keyword.codeengineshort}} Kafka subscription for a set of topics, your app or job receives a separate event for each new message that appears in one of the topics.

You must be within the context of a [project](#cli-project) before you use `subscription kafka` commands.

For more information about working with Kafka event subscriptions, see [Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer). See [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events) for more information about working with subscriptions in {{site.data.keyword.codeengineshort}}.

You can use either `subscription` or `sub` in your `subscription kafka` commands. To see CLI help for the `subscription` commands, run `ibmcloud ce sub kafka -h`. 
{: tip}  
  
### `ibmcloud ce subscription kafka create`  
{: #cli-subscription-kafka-create}  

Create a Kafka event subscription.  
  
```txt
ibmcloud ce subscription kafka create --name KAFKA_SOURCE_NAME --destination DESTINATION_REF --topic TOPIC --broker BROKER [--consumer-group CONSUMER_GROUP] [--destination-type DESTINATION_TYPE] [--extension EXTENSION] [--force] [--no-wait] [--output OUTPUT] [--password PASSWORD] [--path PATH] [--quiet] [--secret SECRET] [--username USERNAME] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-kafka-create} 

`--broker`, `-b`
:   Set a broker in the Kafka source. A broker is a Kafka server to which the consumer connects. This option can be specified multiple times. This value is *required*. 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *required*. 

`-n`, `--name`
:   The name of the Kafka event subscription. Use a name that is unique within the project.

   - The name must begin and end with a lowercase alphanumeric character.
   - The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).

   This value is *required*. 

`--topic`, `-t`
:   Set a topic in the Kafka source. Topics are used to filter messages to consume. This option can be specified multiple times. This value is *required*. 

`--consumer-group`, `--cg`
:   The name of the consumer group for events. This value is *optional*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. The default value is `app`.

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--force`, `-f`
:   Force to create a Kafka event subscription. This option skips the validation of the specified destination and secret. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Create the Kafka event subscription and do not wait for the subscription to be ready. If you specify the `--no-wait` option, the subscription create begins and does not wait. Use the `subscription kafka get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--output`, `-o`
:   Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--password`, `-p`
:   The password that is used to authenticate to the Kafka instance. If you specify the `--password` option, you must not specify the `--secret` option. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--secret`, `-s`
:   The name of the secret that is used to authenticate to the Kafka instance and which includes both `username` and `password` keys. If you specify the `--secret` option, you must not specify the `--username` or `--password` options. This value is *optional*. 

`--username`, `-u`
:   The username that is used to authenticate to the Kafka instance. If you specify the `--username` option, you must specify the `--password` option and must not specify the `--secret` option. This value is *optional*. The default value is `token`.

`--wait`, `-w`
:   Create the Kafka event subscription and wait for the subscription to be ready. If you specify the `--wait` option, the subscription create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to become ready. If the subscription is not ready within the specified `--wait-timeout` period, the Kafka event subscription create fails. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the Kafka event subscription to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `120`.

 
  
#### Example
{: #subscription-kafka-create-example}

The following example creates a Kafka event subscription that is called `mykafkaevent` that forwards a Kafka event to a receiving app that is called `kafka-receiver-app`. Specify a `--broker` option for each broker for your topic. The `--destination` option specifies the {{site.data.keyword.codeengineshort}} resource that receives the events. The `kafka-subscription-secret` provides credentials to access the message broker. 

```txt
ibmcloud ce subscription kafka create --name mykafkasubscription --destination kafka-receiver-app --secret kafka-subscription-secret --topic kafka-topic1 --broker broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker  broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
```
{: pre}

#### Example output
{: #subscription-kafka-create-example-output}

```txt
Creating Kafka event subscription 'mykafkasubscription'...
Run 'ibmcloud ce subscription kafka get -n mykafkasubscription' to check the Kafka event subscription status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription kafka delete`  
{: #cli-subscription-kafka-delete}  

Delete a Kafka event subscription.  
  
```txt
ibmcloud ce subscription kafka delete --name KAFKA_SOURCE_NAME [--force] [--no-wait] [--quiet] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-kafka-delete} 

`--name`, `-n`
:   The name of the Kafka event subscription. This value is *required*. 

`--force`, `-f`
:   Force deletion without confirmation. This value is *optional*. The default value is `false`.

`--no-wait`, `--nw`
:   Delete the Kafka event subscription and do not wait for the subscription to be deleted. If you specify the `--no-wait` option, the subscription delete begins and does not wait. Use the `subscription kafka get` command to check the subscription status. This value is *optional*. The default value is `false`.

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--wait`, `-w`
:   Delete the Kafka event subscription and wait for the subscription to be deleted. If you specify the `--wait` option, the subscription delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to be deleted. This command exits when the subscription is deleted or whenever `--wait-timeout` is reached, whichever comes first. This value is *optional*. The default value is `true`.

`--wait-timeout`, `--wto`
:   The length of time in seconds to wait for the Kafka event subscription to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is `15`.

 
  
#### Example
{: #subscription-kafka-delete-example}

```txt
ibmcloud ce subscription kafka delete --name mykafkasubscription -f
```
{: pre}

#### Example output
{: #subscription-kafka-delete-example-output}

```txt
Deleting Kafka event subscription 'mykafkasubscription'...
OK
```
{: screen}  
  
### `ibmcloud ce subscription kafka get`  
{: #cli-subscription-kafka-get}  

Display details of a Kafka event subscription.  
  
```txt
ibmcloud ce subscription kafka get --name KAFKA_SOURCE_NAME [--output OUTPUT] [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-kafka-get} 

`--name`, `-n`
:   The name of the Kafka event subscription. This value is *required*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

 
  
#### Example
{: #subscription-kafka-get-example}

```txt
ibmcloud ce subscription kafka get --name mykafkasubscription
```
{: pre}

#### Example output
{: #subscription-kafka-get-example-output}

```txt
Getting Kafka event subscription 'mykafkasubscription'...
OK

Name:          mykafkasubscription  
[...]
Destination Type:                 app
Destination:                      kafka-receiver-app2
Brokers:
broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
Consumer Group:                   knative-kafka-source-a4072fe1-1dfa-4470-9d07-bf7a0ff8e340
Topics:
kafka-topic1
Secret key reference (user):      kafka-subscription-secret.username
Secret key reference (password):  kafka-subscription-secret.password
Ready:                            true

Conditions:
Type                     OK    Age  Reason
ConnectionEstablished    true  24s
InitialOffsetsCommitted  true  24s
Ready                    true  24s
Scheduled                true  24s
SinkProvided             true  24s

Events:
Type     Reason           Age  Source                  Messages
Normal   FinalizerUpdate  26s  kafkasource-controller  Updated "mykafkasubscription" finalizers 
```
{: screen}

When `Ready` is `true`, then the Kafka subscription is ready to trigger events per the specified schedule. 
  
  
### `ibmcloud ce subscription kafka list`  
{: #cli-subscription-kafka-list}  

List all Kafka event subscriptions in a project.  
  
```txt
ibmcloud ce subscription kafka list [--output OUTPUT] [--quiet] [--sort-by SORT_BY]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-kafka-list} 

`--output`, `-o`
:   Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--sort-by`, `-s`
:   Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is *optional*. The default value is `name`.

 
  
#### Example
{: #subscription-kafka-list-example}

```txt
ibmcloud ce subscription kafka list
```
{: pre}

#### Example output
{: #subscription-kafka-list-example-output}

```txt
Listing Kafka event subscriptions...
OK

Name                 Age  Ready  Destination Type  Destination          Path  Consumer Group                                             Reason  
mykafkasubscription  94s  true   app               kafka-receiver-app        knative-kafka-source-dc367965-15e4-44f3-bedf-25d453524a68 
```
{: screen}  
  
### `ibmcloud ce subscription kafka update`  
{: #cli-subscription-kafka-update}  

Update a Kafka event subscription.  
  
```txt
ibmcloud ce subscription kafka update --name KAFKA_SOURCE_NAME [--broker BROKER] [--destination DESTINATION] [--destination-type DESTINATION_TYPE] [--extension EXTENSION] [--extension-rm EXTENSION_RM] [--output OUTPUT] [--password PASSWORD] [--path PATH] [--quiet] [--secret SECRET] [--topic TOPIC] [--username USERNAME]
```
{: pre}

#### Command Options  
 {: #cmd-options-subscription-kafka-update} 

`--name`, `-n`
:   The name of the Kafka event subscription. This value is *required*. 

`--broker`, `-b`
:   Set a broker in the Kafka source. A broker is a Kafka server to which the consumer connects. This option can be specified multiple times. This value is *optional*. 

`--destination`, `-d`
:   The name of the application or job resource that you want to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify an app destination. This value is *optional*. 

`--destination-type`, `--dt`
:   The type of the `destination`. Valid values are `app` and `job`. This value is *optional*. 

`--extension`, `--ext`
:   Set CloudEvents extensions to send to the destination. Must be in `NAME=VALUE` format. This action adds a new CloudEvents extension or overrides an existing CloudEvent attribute. Specify one extension per `--extension` option; for example, `--ext extA=A --ext extB=B`. This value is *optional*. 

`--extension-rm`, `--ext-rm`
:   Remove CloudEvents extensions to send to the destination by specifying the name of the key. Specify one extension per `--ext-rm` option; for example, `--ext-rm extA --ext-rm extB`. This value is *optional*. 

`--output`, `-o`
:   Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is *optional*. 

`--password`, `-p`
:   The password that is used to authenticate to the Kafka instance. If you specify the `--password` option, you must not specify the `--secret` option. This value is *optional*. 

`--path`
:   The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This option can only be specified if `destination-type` is `app`. This value is *optional*. 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

`--secret`, `-s`
:   The name of the secret that is used to authenticate to the Kafka instance and which includes both `username` and `password` keys. If you specify the `--secret` option, you must not specify the `--username` or `--password` options. This value is *optional*. 

`--topic`, `-t`
:   Set a topic in the Kafka source. Topics are used to filter messages to consume. This option can be specified multiple times. This value is *optional*. 

`--username`, `-u`
:   The username that is used to authenticate to the Kafka instance. If you specify the `--username` option, you must specify the `--password` option and must not specify the `--secret` option. This value is *optional*. The default value is `token`.

 
  
#### Example
{: #subscription-kafka-update-example}

The following example updates a Kafka event subscription to use `kafka-topic2` instead of `kafka-topic1`. 

```txt
ibmcloud ce subscription kafka update --name mykafkasubscription --topic kafka-topic2
```
{: pre}

#### Example output
{: #subscription-kafka-update-example-output}

```txt
Updating Kafka event subscription 'mykafkasubscription'...
Run 'ibmcloud ce subscription kafka get -n mykafkasubscription' to check the Kafka event subscription status.
OK
```
{: screen}  
  
## Version command  
{: #cli-version}  

Display the version of the `code-engine` command-line interface.  
  
### `ibmcloud ce version`  
{: #cli-versioncmd}  

Display the version of the `code-engine` command-line interface.  
  
```txt
ibmcloud ce version [--quiet]
```
{: pre}

#### Command Options  
 {: #cmd-options-version} 

`--quiet`, `-q`
:   Specify this option to reduce the output of the command. This value is *optional*. The default value is `false`.

  
  
#### Example
{: #version-example}

```txt
ibmcloud ce version
```
{: pre}

#### Example output
{: #version-example-output}

```txt
version:  v1.17.0
commit:   3ab130b746f4784c9ff8d3da7bb05b6e7acda6d5
```
{: screen}  
  
  

