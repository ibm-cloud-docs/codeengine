---

copyright:
  years: 2021
lastupdated: "2021-03-09"

keywords: cli for code engine, command-line interface for code engine, cli commands for code engine, reference for code engine cli, ibmcloud ce, ibmcloud codeengine

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
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
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
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
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
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
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



# {{site.data.keyword.codeenginefull_notm}} CLI
{: #cli}

Run these commands to manage the entities that make up {{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}").
{: shortdesc}

To run {{site.data.keyword.codeenginefull_notm}} commands, use `ibmcloud code-engine` or `ibmcloud ce`.
{: tip}

## Prerequisites
{: #codeengine-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the {{site.data.keyword.codeengineshort}} CLI by running the following command:

   ```sh
   ibmcloud plugin install code-engine
   ```
   {: pre}  
  
## Project commands  
{: #cli-project}  

Use `project` commands to create, list, delete, and select a project as the current context.
{: shortdesc}

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs, and builds. A project is based on a Kubernetes namespace. The name of your project must be unique within your {{site.data.keyword.cloud}} resource group, user account, and region. Projects are used to manage resources and provide access to its entities. A project provides the following items:<ul><li>Provides a unique namespace for entity names.</li><li> Manages access to project resources (inbound access).</li><li> Manages access to backing services, registries, and repositories (outbound access).</li><li> Has an automatically generated certificate for Transport Layer Service (TLS).</li></ul>

You can use either `project` or `proj` in your `project` commands. To see CLI help for the `project` commands, run `ibmcloud ce proj -h`.
{: tip}  
  
### `ibmcloud ce project create`  
{: #cli-project-create}  

Create a project.  
  
```
 ibmcloud ce project create --name PROJECT_NAME [--no-select] [--tag TAG]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. Use a name that is unique to your region. The name must be 128 characters or fewer and can contain:
<ul>
	<li>Any Unicode or alphanumeric character.</li>
	<li>Only these special characters: spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-ns`, `--no-select`</dt>
<dd>Do not select the project as the current context after this project is created. If you do not select this option, the project is automatically selected. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource. The label must be 128 characters or fewer and can contain letters, numbers, spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-). Specify one label per `--tag` option; for example, `--tag tagA --tag tagB`. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce project create --name myproject  
```
{: pre}

**Example output**

```
Creating project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project delete`  
{: #cli-project-delete}  

Delete a project.  
  
```
 ibmcloud ce project delete (--name PROJECT_NAME | --id PROJECT_ID) [--force] [--hard]
```
{: pre}

**Command Options**  
<dl>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`--hard`</dt>
<dd>Immediately delete the project. If you do not specify the `--hard` option, the project can be restored within 7 days by using {{site.data.keyword.cloud_notm}} resource reclamation. This value is optional. The default value is <code>false</code>.</dd>
<dt>`-guid`, `--id`</dt>
<dd>The ID of the project. This value is required if `--name` is not specified. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required if `--id` is not specified. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce project delete --name myproject -f
```
{: pre}

**Example output**

```
Deleting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project list`  
{: #cli-project-list}  

List all projects.  
  
```
 ibmcloud ce project list [--output OUTPUT] [--regions REGIONS] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-r`, `--regions`</dt>
<dd>Limit the display of projects to specified regions. Provide the name of one or more regions; for example, `us-south,eu-de`. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce project list
```
{: pre}

**Example output**

```
Getting projects...
OK

Name             ID                                    Status  Selected  Tags  Region    Resource Group  Age
myproj-eude      09768af4-abcd-abcd-abcd-24674ba90db0  active  false           eu-de     default         27d
myproject        cd09cfe1-abcd-abcd-abcd-0f8a8a1d0ddf  active  true            us-south  default         52d
```
{: screen}  
  
### `ibmcloud ce project get`  
{: #cli-project-get}  

Display the details of a single project.  
  
```
 ibmcloud ce project get (--name PROJECT_NAME | --id PROJECT_ID) [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-guid`, `--id`</dt>
<dd>The ID of the project. This value is required if `--name` is not specified. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required if `--id` is not specified. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce project get --name myproject
```
{: pre}

**Example output**

```
Getting project 'myproject'...
OK

Name:            myproject
ID:              abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
Status:          active
Selected:        true
Region:          us-south
Resource Group:  default
Age:             52d
Created:         Fri, 15 Jan 2021 13:32:30 -0500
Updated:         Fri, 15 Jan 2021 13:32:45 -0500
```
{: screen}  
  
### `ibmcloud ce project select`  
{: #cli-project-select}  

Select a project as the current context.  
  
```
 ibmcloud ce project select (--name PROJECT_NAME | --id PROJECT_ID) [--kubecfg]
```
{: pre}

**Command Options**  
<dl>
<dt>`-guid`, `--id`</dt>
<dd>The ID of the project. This value is required if `--name` is not specified. 
</dd>
<dt>`-k`, `--kubecfg`</dt>
<dd>Append the project to the default Kubernetes configuration file. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required if `--id` is not specified. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce project select --name myproject
```
{: pre}

**Example output**

```
Selecting project 'myproject'...
OK
```
{: screen}  
  
### `ibmcloud ce project current`  
{: #cli-project-current}  

Display the details of the project that is currently targeted.  
  
```
 ibmcloud ce project current
```
{: pre}

**Example output**

```
Getting the current project context...
OK

Project Name:     myproject
Project ID:       cd09cfe1-abcd-abcd-abcd-abcdabcdabcd
Region:           us-south
Kubectl Context:  4svg40kna19

To use kubectl with your project, run the following command:
export KUBECONFIG=/user/myusername/.bluemix/plugins/code-engine/myproject-cd09cfe1-abcd-abcd-abcd-abcdabcdabcd.yaml
```
{: screen}  
  
## Application commands  
{: #cli-application}  

An application, or app, runs your code to serve HTTP requests. In addition to traditional HTTP requests, {{site.data.keyword.codeengineshort}} also supports applications that use WebSockets as their communications protocol. The number of running instances of an app are automatically scaled up or down (to zero) based on incoming workloads and your configuration settings. An app contains one or more revisions. A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app. 
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `application` commands.

You can use either `application` or `app` in your `application` commands. To see CLI help for the `application` commands, run `ibmcloud ce app -h`.
{: tip}  
  
### `ibmcloud ce application create`  
{: #cli-application-create}  

Create an application.  
  
```
 ibmcloud ce application create --name APP_NAME --image IMAGE_REF [--argument ARGUMENT] [--cluster-local] [--command COMMAND] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-secret MOUNT_SECRET] [--no-cluster-local] [--no-wait] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--request-timeout REQUEST_TIMEOUT] [--user USER] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for this application. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 55 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value overrides the default values that are specified within the container image. This value is optional. 
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>100</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The threshold of concurrent requests per instance at which one or more additional instances are created. Use this value to scale up instances based on concurrent number of requests. This option defaults to the value of the `--concurrency` option, if not specified. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0.1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for the instance of the application. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-max`, `-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. The default value is <code>1024Mi</code>.
</dd>
<dt>`-min`, `-minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This option is useful to ensure that no instances are running when not needed. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-mount-cm`, `--mount-configmap`</dt>
<dd>Add the contents of a configmap to the file system of your application container by providing a mount directory and the name of a configmap, with the format MOUNT_DIRECTORY=CONFIGMAP_NAME. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is optional. 
</dd>
<dt>`-mount-sec`, `--mount-secret`</dt>
<dd>Add the contents of a secret to the file system of your application container by providing a mount directory and the name of a secret, with the format MOUNT_DIRECTORY=SECRET_NAME. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is optional. 
</dd>
<dt>`-ncl`, `--no-cluster-local`</dt>
<dd>Deploy the application with a public endpoint. The application has exposure to external traffic. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Create the application and do not wait for the application to be ready. If you specify the `--no-wait` option, the application create begins and does not wait.  Use the `app get` command to check the application status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-p`, `--port`</dt>
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your application needs to listen on a port other than port `8080`, use `--port` to specify the port. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-rt`, `-timeout`, `-t`, `--request-timeout`</dt>
<dd>The amount of time in seconds that can pass before requests made to the application must succeed or fail. This value is optional. The default value is <code>300</code>.
</dd>
<dt>`-u`, `--user`</dt>
<dd>The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Create the application and wait for the application to be ready. If you specify the `--wait` option, the application create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become ready. If the application is not ready within the specified `wait-timeout` period, the application create fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application create --name myapp --image ibmcom/hello
```
{: pre}

**Example output**

```
Creating application 'myapp'...
[...]
Run `ibmcloud ce application get -n 'myapp'` to check the application status.
OK

https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}

When you run `ibmcloud ce application get -n 'myapp'` to check the application status, the URL for your application is displayed.  
{: tip}  
  
### `ibmcloud ce application get`  
{: #cli-application-get}  

Display the details of an application.  
  
```
 ibmcloud ce application get --name APPLICATION_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, `jsonpath-as-json=JSONPATH_EXPRESSION`, and `url`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application get --name myapp
```
{: pre}

**Example output**

```
OK

Name:          myapp
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           35s
Created:       2021-03-01T13:13:12-05:00
URL:           https://myapp.01234567-abcd.us-south.codeengine.appdomain.cloud
Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

Status Summary:  Application deployed successfully

Image:                ibmcom/hello
Resource Allocation:
  CPU:                0.1
  Ephemeral Storage:  500Mi
  Memory:             1Gi

Revisions:
  myapp-atfte-1:
    Age:                3d6h
    Traffic:            100%
    Image:              ibmcom/hello (pinned to f0dc03)
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
  myapp-atfte-1-deployment-5dc989d584-nvmml  myapp-atfte-1  2/2      Running  0         48s
```
{: screen}  
  
### `ibmcloud ce application update`  
{: #cli-application-update}  

Update an application. Updating your application creates a revision. When calls are made to the application, traffic is routed to the revision.  
  
```
 ibmcloud ce application update --name APP_NAME [--argument ARGUMENT] [--arguments-clear] [--cluster-local] [--command COMMAND] [--commands-clear] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--mount-configmap MOUNT_CONFIGMAP] [--mount-rm MOUNT_RM] [--mount-secret MOUNT_SECRET] [--no-cluster-local] [--no-wait] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--registry-secret-clear] [--request-timeout REQUEST_TIMEOUT] [--user USER] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ac`, `--arguments-clear`</dt>
<dd>Clear application arguments. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cc`, `--commands-clear`</dt>
<dd>Clear application commands. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The threshold of concurrent requests per instance at which one or more additional instances are created. Use this value to scale up instances based on concurrent number of requests. This option defaults to the value of the `--concurrency` option, if not specified. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for the instance of the application. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for this application. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is optional. 
</dd>
<dt>`-max`, `-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-min`, `-minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-mount-cm`, `--mount-configmap`</dt>
<dd>Add the contents of a configmap to the file system of your application container by providing a mount directory and the name of a configmap, with the format MOUNT_DIRECTORY=CONFIGMAP_NAME. Each mounted configmap must use a unique mount directory. For each key-value pair in the configmap, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-configmap` option; for example, `--mount-configmap /etc/config-a=config-a --mount-configmap /etc/config-b=config-b`. This value is optional. 
</dd>
<dt>`--mount-rm`</dt>
<dd>Remove the contents of a configmap or secret from the file system of your application container by specifying the directory where the configmap or secret is mounted. Specify one mount directory per `--mount-rm` option; for example, `--mount-rm /etc/configmap-a --mount-rm /etc/secret-b`. This value is optional. </dd>
<dt>`-mount-sec`, `--mount-secret`</dt>
<dd>Add the contents of a secret to the file system of your application container by providing a mount directory and the name of a secret, with the format MOUNT_DIRECTORY=SECRET_NAME. Each mounted secret must use a unique mount directory. For each key-value pair in the secret, a file is added to the specified mount directory where the filename is the key and the contents of the file is the value of the key-value pair. Specify one mount configuration per `--mount-secret` option; for example, `--mount-secret /etc/secret-a=secret--a --mount-secret /etc/secret-b=secret-b`. This value is optional. 
</dd>
<dt>`-ncl`, `--no-cluster-local`</dt>
<dd>Deploy the application with a public endpoint. The application has exposure to external traffic. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Update the application and do not wait for the application to be ready. If you specify the `no-wait` option, the application update begins and does not wait. Use the `app get` command to check the application status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-p`, `--port`</dt>
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. By default, {{site.data.keyword.codeengineshort}} assumes apps listen for incoming connections on port `8080`. If your application needs to listen on a port other than port `8080`, use `--port` to specify the port. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-rsc`, `--registry-secret-clear`</dt>
<dd>Clear the image registry access secret. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rt`, `-timeout`, `-t`, `--request-timeout`</dt>
<dd>The amount of time in seconds that can pass before requests made to the application must succeed or fail. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-u`, `--user`</dt>
<dd>The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Update the application and wait for the application to be ready. If you specify the `--wait` option, the application update waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become ready. If the application is not ready within the specified `--wait-timeout` period, the application create fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be updated. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application update --name myapp --image ibmcom/hello
```
{: pre}

**Example output**

```
Updating application 'myapp' to latest revision.
[...]
Run 'ibmcloud ce application get -n myapp' to check the application status.
OK

https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
```
{: screen}  
  
### `ibmcloud ce application delete`  
{: #cli-application-delete}  

Delete an application.  
  
```
 ibmcloud ce application delete --name APPLICATION_NAME [--force] [--no-wait] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Delete the application and do not wait for the application to be deleted. If you specify the `no-wait` option, the application delete begins and does not wait.  Use the `app get` command to check the application status. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Delete the application and wait for the application to be deleted. If you specify the `--wait` option, the application delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the application to become deleted. If the application is not deleted within the specified `--wait-timeout` period, the application delete fails. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application delete --name myapp -f
```
{: pre}

**Example output**

```
Deleted application 'myapp'
```
{: screen}  
  
### `ibmcloud ce application list`  
{: #cli-application-list}  

List all applications in a project.  
  
```
 ibmcloud ce application list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce app list --sort-by age
```
{: pre}

**Example output**

```
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
  
### `ibmcloud ce application bind`  
{: #cli-application-bind}  

Bind an {{site.data.keyword.cloud_notm}} service instance to an application.  
  
```
 ibmcloud ce application bind --name APP_NAME --service-instance SI_NAME [--no-wait] [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application to bind. This value is required. 
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the application. This value is required. 
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Bind the service instance and do not wait for the service binding to be ready. If you specify the `no-wait` option, the service binding creation is started and the command exits without waiting for it to complete. Use the `app get` command to check the app bind status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-p`, `--prefix`</dt>
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-sc`, `--service-credential`</dt>
<dd>The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is optional. 
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Bind the service instance and wait for the service binding to be ready. If you specify the `--wait` option, the app bind waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the app bind to complete successfully. If the app bind is not completed successfully or fails within the specified `--wait-timeout` period, the command fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the service binding to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

In this example, bind your {{site.data.keyword.languagetranslationshort}} service instance called `langtranslator` to your application called `myapp`.

```
ibmcloud ce application bind --name myapp --service-instance langtranslator
```
{: pre}

**Example output**

```
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
  
### `ibmcloud ce application unbind`  
{: #cli-application-unbind}  

Unbind {{site.data.keyword.cloud_notm}} service instances from an application.  
  
```
 ibmcloud ce application unbind --name APP_NAME (--service-instance SERVICE_INSTANCE_NAME | --all) [--quiet]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application to unbind. This value is required. 
</dd>
<dt>`-A`, `--all`</dt>
<dd>Unbinds all service instances for this application. This value is required if `--service-instance` is not specified. The default value is <code>false</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of the service instance to unbind for this application. This value is required if `--all` is not specified. 
</dd>
</dl>  
  
**Example**

In this example, remove all bindings from your application called `myapp`.

```
ibmcloud ce application unbind --name myapp --all
```
{: pre}

**Example output**

```
Removing service bindings...
OK
```
{: screen}  
  
### `ibmcloud ce application logs`  
{: #cli-application-logs}  

Display the logs of application instances.  
  
```
 ibmcloud ce application logs (--instance APP_INSTANCE | --application APP_NAME) [--all-containers] [--follow] [--output OUTPUT] [--tail TAIL] [--timestamps]
```
{: pre}

**Command Options**  
<dl>
<dt>`-all`, `--all-containers`</dt>
<dd>Display the logs of all containers of the specified application instances. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-app`, `-a`, `-name`, `-n`, `--application`</dt>
<dd>Display the logs of all the instances of the specified application. This value is required if `--instance` is not specified. 
</dd>
<dt>`-f`, `--follow`</dt>
<dd>Follow the logs of application instances. Use this option to stream logs of application instances. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-i`, `--instance`</dt>
<dd>The name of a specific application instance. Use the `app get` command to find the instance name. This value is required if `--application` is not specified. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-t`, `--tail`</dt>
<dd>Limit the display of logs of containers of the specified application instances to a maximum number of recent lines per container. For example, to display the last `3` lines of the logs of the containers of the specified application instances, specify `--tail 3`. If this option is not specified, all lines of the logs of the containers of the specified application instances are displayed. This value is optional. The default value is <code>-1</code>.
</dd>
<dt>`-ts`, `--timestamps`</dt>
<dd>Include timestamps on each line in the log output. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

This example displays the logs of a specific instance of an app. Use the `app get` command to obtain the name of the app instances. 

```
ibmcloud ce application logs --instance myapp-zhk9x-1-deployment-6f955f5cc5-abcde
```
{: pre}

**Example output**

```
Getting logs for application instance 'myapp-zhk9x-1-deployment-6f955f5cc5-abcde'...
OK

myapp-zhk9x-1-deployment-6f955f5cc5-abcde:
Server running at http://0.0.0.0:8080/
```
{: screen}

**Example**

This example displays the logs of all of the instances of an app.   

```
ibmcloud ce application logs --app myapp
```
{: pre}

**Example output**

```
Getting application 'myapp'...
Getting revisions for application 'myapp'...
Getting instances for application 'myapp'...
Getting logs for all instances of application 'myapp'...
OK

myapp-zhk9x-1-deployment-6f955f5cc5-abcde:
Server running at http://0.0.0.0:8080/
```
{: screen}

  
  
### `ibmcloud ce application events`  
{: #cli-application-events}  

Display the events of application instances.  
  
```
 ibmcloud ce application events (--instance APP_INSTANCE | --application APP_NAME) [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-app`, `-a`, `-name`, `-n`, `--application`</dt>
<dd>Display the events of all the instances of the specified application.  This value is required if `--instance` is not specified. 
</dd>
<dt>`-i`, `--instance`</dt>
<dd>The name of a specific application instance. Use the `app get` command to find the instance name. This value is required if `--application` is not specified. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

This example displays the system event information for all the instances of a specified application.   

```
ibmcloud ce application events --application myapp 
```
{: pre}

**Example output**

```
Getting events for all instances of application 'myapp'...
OK

myapp-atfte-1-deployment-6b49c5fb85-kf4m2:
  Type    Reason     Age  Source                Messages
  Normal  Scheduled  31s  default-scheduler     Successfully assigned 4svg40kna19/myapp-atfte-1-deployment-6b49c5fb85-kf4m2 to 10.240.0.15
  Normal  Pulling    29s  kubelet, 10.240.0.15  Pulling image "index.docker.io/ibmcom/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
  Normal  Pulled     24s  kubelet, 10.240.0.15  Successfully pulled image "index.docker.io/ibmcom/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6" in 4.907426108s
  Normal  Created    24s  kubelet, 10.240.0.15  Created container user-container
  Normal  Started    24s  kubelet, 10.240.0.15  Started container user-container
  Normal  Pulled     24s  kubelet, 10.240.0.15  Container image "icr.io/obs/codeengine/knative-serving/queue-39be6f1d08a095bd076a71d288d295b6:v0.20.0-rc1@sha256:8988bea781130827b3e1006e6e5e7f49094343a5505c1927bb832be3470455f6" already present on machine
  Normal  Created    23s  kubelet, 10.240.0.15  Created container queue-proxy
  Normal  Started    23s  kubelet, 10.240.0.15  Started container queue-proxy
```
{: screen}

**Example**

This example displays the system event information for a specified instance of an app. Use the `app get` command to displays details about your app, including the running instances of the app.

```
ibmcloud ce application events --instance myapp-li17x-1-deployment-69fd57bcb6-sr9tl
```
{: pre}

**Example output**

```
Getting events for application instance 'myapp-li17x-1-deployment-69fd57bcb6-sr9tl'...
OK

myapp-li17x-1-deployment-69fd57bcb6-sr9tl:
  Type     Reason     Age                    Source                Messages
  Normal   Scheduled  6m40s                  default-scheduler     Successfully assigned 4svg40kna19/myapp-li17x-1-deployment-69fd57bcb6-sr9tl to 10.240.64.6
  Normal   Pulling    6m39s                  kubelet, 10.240.64.6  Pulling image "index.docker.io/ibmcom/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
  Normal   Pulled     6m36s                  kubelet, 10.240.64.6  Successfully pulled image "index.docker.io/ibmcom/hello@sha256:f0dc03250736a7b40a66ee70fee94fc470e08c864197aa2140054fee6ca9f9d6"
  Normal   Created    6m34s                  kubelet, 10.240.64.6  Created container user-container
  Normal   Started    6m33s                  kubelet, 10.240.64.6  Started container user-container
  Normal   Pulled     6m33s                  kubelet, 10.240.64.6  Container image "icr.io/obs/codeengine/knative-serving/queue-39be6f1d08a095bd076a71d288d295b6:v0.19.0-rc3@sha256:9cb525af53896afa6b5210b5ac56a893cf85b6cd013a61cb6503a005e40c5c6f" already present on machine
  Normal   Created    6m33s                  kubelet, 10.240.64.6  Created container queue-proxy
  Normal   Started    6m32s                  kubelet, 10.240.64.6  Started container queue-proxy
  [...]
```
{: screen}  
  
## Configmap commands  
{: #cli-configmap}  

A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app or job portable. A configmap contains information in key-value pairs. Use `configmap` commands to create, display details, update, and delete configmaps.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `configmap` commands.

You can use either `configmap` or `cm` in your `configmap` commands. To see CLI help for the `configmap` commands, run `ibmcloud ce configmap -h`.
{: tip}  
  
### `ibmcloud ce configmap create`  
{: #cli-configmap-create}  

Create a configmap.  
  
```
 ibmcloud ce configmap create --name CONFIGMAP_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-e`, `--from-env-file`</dt>
<dd>Create a configmap from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. This value is required if `--from-literal` or `--from-file` is not specified. 
</dd>
<dt>`-f`, `--from-file`</dt>
<dd>Create a configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create a configmap from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. 
</dd>
</dl>  
  
**Examples**

- The following example creates a configmap that is named `configmap-fromliteral` with two key pair values: `color=blue` and `size=large`.

  ```
  ibmcloud ce configmap create --name configmap-fromliteral --from-literal color=blue --from-literal size=large
  ```
  {: pre}

  **Example output**

  ```
  Creating Configmap 'configmap-fromliteral'...
  OK
  Run 'ibmcloud ce configmap get -n configmap-fromliteral' to see more details.
  ```
  {: screen}
  
- The following example creates a configmap that is named `configmap-fromfile` with values from multiple files.

  ```
  ibmcloud ce configmap create --name configmap-fromfile  --from-file ./color.txt --from-file ./size.txt
  ```
  {: pre}

  **Example output**

  ```
  Creating configmap 'configmap-fromfile'...
  OK
  Run 'ibmcloud ce configmap get -n configmap-fromfile' to see more details.
  ```
  {: screen}  
  
### `ibmcloud ce configmap get`  
{: #cli-configmap-get}  

Display the details of a configmap.  
  
```
 ibmcloud ce configmap get --name CONFIGMAP_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce configmap get --name configmap-fromliteral 
```
{: pre}

**Example output**

```
Getting configmap 'configmap-fromliteral'...
OK

Name:          configmap-fromliteral
ID:            abcdabcd-abcd-abcd-abcd-ff26f297c4f7
Project Name:  myproj
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           21s
Created:       2021-03-01T13:50:56-05:00

Data:
---
color: blue
size: large
```
{: screen}  
  
### `ibmcloud ce configmap update`  
{: #cli-configmap-update}  

Update a configmap.  
  
```
 ibmcloud ce configmap update --name CONFIGMAP_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE | --rm KEY)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. 
</dd>
<dt>`-e`, `--from-env-file`</dt>
<dd>Update a configmap from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. This value is required if `--from-literal` or `--from-file` is not specified. 
</dd>
<dt>`-f`, `--from-file`</dt>
<dd>Update a configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Update a configmap from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or  or `--from-env-file`is not specified. 
</dd>
<dt>`--rm`</dt>
<dd>Remove an individual key-value pair in a configmap by specifying the name of the key. This value is optional. </dd>
</dl>  
  
**Examples**

- The following example updates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud ce configmap update --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Example output**

  ```
  Updating configmap 'configmap-fromliteral'...
  OK
  Run 'ibmcloud ce configmap get -n configmap-fromliteral' to see more details.
  ```
  {: screen}
  
- The following example updates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud ce configmap update --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Example output**

  ```
  Updating configmap 'configmap-fromfile'...
  OK
  Run 'ibmcloud ce configmap get -n configmap-fromfile' to see more details.

  ```
  {: screen}  
  
### `ibmcloud ce configmap delete`  
{: #cli-configmap-delete}  

Delete a configmap.  
  
```
 ibmcloud ce configmap delete --name CONFIGMAP_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce configmap delete --name configmap-fromliteral -f
```
{: pre}

**Example output**

```
Deleting Configmap 'configmap-fromliteral'...
OK
```
{: screen}  
  
### `ibmcloud ce configmap list`  
{: #cli-configmap-list}  

List all configmaps in a project.  
  
```
 ibmcloud ce configmap list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example output**

```
Listing Configmaps...
Name                    Data   Age
configmap-fromfile      2      19m13s
configmap-fromliteral   2      16m12s
```
{: screen}  
  
## Job commands  
{: #cli-job}  

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. Use `job` commands to create a configuration for your job.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `job` commands.

To see CLI help for the `job` commands, run `ibmcloud ce job -h`.
{: tip}  
  
### `ibmcloud ce job create`  
{: #cli-job-create}  

Create a job.  
  
```
 ibmcloud ce job create --name JOB_NAME --image IMAGE_REF [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for runs of the job. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 63 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for runs of the job. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for runs of the job. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for runs of the job. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for runs of the job. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. The default value is <code>128Mi</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of the job before the job is marked as failed. An array index of a job is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
</dd>
</dl>  
  
**Example**

The following example uses the container image `ibmcom/testjob` and assigns 128 MB as memory and 1 CPU to the container.

```
ibmcloud ce job create --image ibmcom/firstjob --name hellojob --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Creating job 'hellojob'...
OK
```
{: screen}  
  
### `ibmcloud ce job get`  
{: #cli-job-get}  

Display the details of a job.  
  
```
 ibmcloud ce job get --name JOB_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce job get --name hellojob
```
{: pre}

**Example output**

```
Getting job 'hellojob'...
OK

Name:          hellojob
ID:            abcdabcd-abcd-abcd-abcd-abcdabcd1111
Project Name:  myproj
Project ID:    01234567-abcd-abcd-abcd-abcdabcd2222
Age:           59s
Created:       2021-03-01T15:33:30-05:00

Image:                ibmcom/firstjob
Resource Allocation:
  CPU:     1
  Memory:  128Mi

Runtime:
  Array Indices:       0
  Max Execution Time:  7200
  Retry Limit:         3
```
{: screen}  
  
### `ibmcloud ce job update`  
{: #cli-job-update}  

Update a job.  
  
```
 ibmcloud ce job update --name JOB_NAME [--argument ARGUMENT] [--arguments-clear] [--array-indices ARRAY_INDICES] [--command COMMAND] [--commands-clear] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--registry-secret-clear] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ac`, `--arguments-clear`</dt>
<dd>Clear job arguments. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. 
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cc`, `--commands-clear`</dt>
<dd>Clear job commands. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for runs of the job. This value updates any `--cpu` value that is assigned in the job. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for runs of the job. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for runs of the job. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for runs of the job. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for runs of the job. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-rsc`, `--registry-secret-clear`</dt>
<dd>Clear the image registry access secret. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of the job before the job is marked as failed. An array index of a job is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce job update --name hellojob --cpu 2
```
{: pre}

**Example output**

```
Updating job 'hellojob'...
OK
```
{: screen}  
  
### `ibmcloud ce job delete`  
{: #cli-job-delete}  

Delete a job and its associated job runs.  
  
```
 ibmcloud ce job delete --name JOB_NAME [--force] [--orphan-job-runs]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-o`, `--orphan-job-runs`</dt>
<dd>Specify to keep any job runs that are associated with this job configuration. These orphaned job runs must then be deleted separately. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce job delete --name hello
```
{: pre}

**Example output**

```
Are you sure you want to delete job hello? [y/N]> y
Deleting job 'hello'...
OK
```
{: screen}

When you run the `ibmcloud ce job delete` command to delete a job, all the submitted job runs that reference this job are also deleted.  
{: important}  
  
### `ibmcloud ce job list`  
{: #cli-job-list}  

List all jobs in a project.  
  
```
 ibmcloud ce job list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example output**

```
Name            Age
firstjob        12d
hellojob        2m21s
myjob           11d
```
{: screen}  
  
### `ibmcloud ce job bind`  
{: #cli-job-bind}  

Bind an {{site.data.keyword.cloud_notm}} service instance to a job.  
  
```
 ibmcloud ce job bind --name JOB_NAME --service-instance SI_NAME [--no-wait] [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to bind. This value is required. 
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the job. This value is required. 
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Bind the service instance and do not wait for the service binding to be ready. If you specify the `--no-wait` option, the service binding creation is started and the command exits without waiting for it to complete. Use the `job get` command to check the job bind status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-p`, `--prefix`</dt>
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-sc`, `--service-credential`</dt>
<dd>The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is optional. 
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Bind the service instance and wait for the service binding to be ready. If you specify the `--wait` option, the job bind waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job bind to complete successfully. If the job bind is not completed successfully or fails within the specified `--wait-timeout` period, the command fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the service binding to be ready. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

In this example, bind your service instance called `my-object-storage` to your job that is called `hello`.

```
ibmcloud ce job bind --name hello --service-instance my-object-storage
```
{: pre}

**Example output**

```
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
  
### `ibmcloud ce job unbind`  
{: #cli-job-unbind}  

Unbind {{site.data.keyword.cloud_notm}} service instances from a job to remove existing service bindings.  
  
```
 ibmcloud ce job unbind --name JOB_NAME (--service-instance SERVICE_INSTANCE_NAME | --all) [--quiet]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to unbind. This value is required. 
</dd>
<dt>`-A`, `--all`</dt>
<dd>Unbinds all service instances for this job. This value is required if `--service-instance` is not specified. The default value is <code>false</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of the service instance to unbind from the job. This value is required if `--all` is not specified. 
</dd>
</dl>  
  
**Example**

In this example, remove all bindings from your job called `hello`.

```
ibmcloud ce job unbind --name hello --all
```
{: pre}

**Example output**

```
Removing service bindings...
OK
```
{: screen}  
  
## Jobrun commands  
{: #cli-jobrun}  

A job runs one or more instances of your executable code. Unlike applications, which handle HTTP requests, jobs are designed to run one time and exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. Use `jobrun` commands to run instances of your job.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `jobrun` commands.

To see CLI help for the `jobrun` commands, run `ibmcloud ce jobrun -h`.
{: tip}  
  
### `ibmcloud ce jobrun submit`  
{: #cli-jobrun-submit}  

Submit a job run based on a job.  
  
```
 ibmcloud ce jobrun submit ((--name JOBRUN_NAME --image IMAGE) | (--job JOB_NAME [--name JOBRUN_NAME])) [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--no-wait] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for this job run. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for this job run. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for this job run. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for each array index for this job run. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for this job run. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for this job run from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for this job run from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage for this job run. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for this job run. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. The `--name` and the `--image` values are required, if you do not specify the `--job` value. This value is optional. 
</dd>
<dt>`-j`, `--job`</dt>
<dd>The name of the job configuration. View job configurations with the `job list` command. If you specify the `--job` value, you can optionally specify the `--name` value. If you don't specify the `--job` value, you must specify the `--name` and `--image` values. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for this job run. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to this job run. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. The default value is <code>128Mi</code>.
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of this job run. The `--name` and the `--image` values are required, if you do not specify the `--job` value. Use a name that is unique within the project.
<ul>
	<li>  The name must begin and end with a lowercase alphanumeric character.</li>
	<li>  The name must be 53 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Submit the job run and do not wait for the instances of this job run to complete. If you specify the `--no-wait` option, the job run submit begins and does not wait. Use the `jobrun get` command to check the job run status. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of this job run before the job run is marked as failed. An array index of a job run is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Submit the job run and wait for the instances of this job run to complete. If you specify the `--wait` option, the job run submit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job run to complete. If the job run is not completed within the specified `--wait-timeout` period, the job run submit fails. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the instances of this job run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun submit --name myjobrun --image ibmcom/firstjob --array-indices 1-5
```
{: pre}

**Example output**

```
Submitting job run 'myjobrun'...
Run 'ibmcloud ce jobrun get -n myjobrun' to check the job run status.
OK
```
{: screen}  
  
### `ibmcloud ce jobrun get`  
{: #cli-jobrun-get}  

Display the details of a job run.  
  
```
 ibmcloud ce jobrun get --name JOBRUN_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job run. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun get --name myjobrun  
```
{: pre}

**Example output**

```
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
Getting events of jobrun 'myjobrun'...
OK

Name:          myjobrun
[...]
Created:       2021-03-02T10:31:13-05:00

Image:                ibmcom/firstjob
Resource Allocation:
  CPU:                1
  Ephemeral Storage:  400M
  Memory:             128Mi

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
  
### `ibmcloud ce jobrun resubmit`  
{: #cli-jobrun-resubmit}  

Resubmit a job run based on the configuration of a previous job run.  
  
```
 ibmcloud ce jobrun resubmit --jobrun REFERENCED_JOBRUN_NAME [--argument ARGUMENT] [--arguments-clear] [--array-indices ARRAY_INDICES] [--command COMMAND] [--commands-clear] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--name NAME] [--no-wait] [--retrylimit RETRYLIMIT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-j`, `--jobrun`</dt>
<dd>The name of the previous job run that this job run is based on. This value is required. 
</dd>
<dt>`-arg`, `-a`, `--argument`</dt>
<dd>Set arguments for this job run. Specify one argument per `--argument` option; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ac`, `--arguments-clear`</dt>
<dd>Clear job run arguments. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for this job run. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. 
</dd>
<dt>`-cmd`, `-c`, `--command`</dt>
<dd>Set commands for this job run. Specify one command per `--command` option; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cc`, `--commands-clear`</dt>
<dd>Clear job run commands. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for each array index for this job run. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for this job run. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` option; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for this job run from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps by using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for this job run from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets by using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage for this job run. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for this job run. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to this job run. Use `Mi` for `mebibytes` or `Gi` for `gibibytes`. This value is optional. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of this job run. Required if the referenced job does not have a related job configuration. Use a name that is unique within the project.
<ul>
	<li>  The name must begin and end with a lowercase alphanumeric character.</li>
	<li>  The name must be 53 characters or fewer and can contain lowercase letters, numbers, and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Resubmit the job run and do not wait for the instances of this job run to complete. If you specify the `--no-wait` option, the job run resubmit begins and does not wait. Use the `jobrun get` command to check the job run status. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of this job run before the job run is marked as failed. An array index of a job run is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Resubmit the job run and wait for the instances of this job run to complete. If you specify the `--wait` option, the job run resubmit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the job run to complete. If the job run is not completed within the specified `--wait-timeout` period, the job run resubmit fails. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the instances of this job run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

The following example reruns the `myjobrun` job run for instances `4-5`. The name of the resubmitted job run is `myjobresubmit`. 

```
ibmcloud ce jobrun resubmit --name myjobresubmit --jobrun myjobrun --array-indices 4-5
```
{: pre}

**Example output**

```
Getting job run 'myjobrun'...
Rerunning job run 'myjobresubmit'...
Run 'ibmcloud ce jobrun get -n myjobresubmit' to check the job run status.
OK
```
{: screen}  
  
### `ibmcloud ce jobrun delete`  
{: #cli-jobrun-delete}  

Delete a job run.  
  
```
 ibmcloud ce jobrun delete --name JOBRUN_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job run to delete. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun delete --name myjobrun -f
```
{: pre}

**Example output**

```
Deleting job run 'myjobrun'...
OK
```
{: screen}  
  
### `ibmcloud ce jobrun list`  
{: #cli-jobrun-list}  

List all job runs in a project.  
  
```
 ibmcloud ce jobrun list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun list
```
{: pre}

**Example output**

```
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
  
```
 ibmcloud ce jobrun logs (--instance JOBRUN_INSTANCE | --jobrun JOBRUN_NAME) [--follow] [--output OUTPUT] [--tail TAIL] [--timestamps]
```
{: pre}

**Command Options**  
<dl>
<dt>`-f`, `--follow`</dt>
<dd>Follow the logs of job run instances. Use this option to stream logs of job run instances. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-i`, `--instance`</dt>
<dd>The name of a specific job run instance. Use the `jobrun get` command to find the instance name. This value is required if `--jobrun` is not specified. 
</dd>
<dt>`-j`, `-name`, `-n`, `--jobrun`</dt>
<dd>Display the logs of all the instances of the specified job run. This value is required if `--instance` is not specified. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-t`, `--tail`</dt>
<dd>Limit the display of logs of the specified job run instances to a maximum number of recent lines. For example, to display the last `3` lines of the logs of the specified job run instances, specify `--tail 3`. If this option is not specified, all lines of the logs of the specified job run instances are displayed. This value is optional. The default value is <code>-1</code>.
</dd>
<dt>`-ts`, `--timestamps`</dt>
<dd>Include timestamps on each line in the log output. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

This example displays the logs of a specific instance of a job run. Use the `jobrun get` command to obtain the name of the job run instances. 

```
ibmcloud ce jobrun logs --instance myjobrun-3-0
```
{: pre}

**Example output**

```
Getting logs for job run instance 'myjobrun-3-0'...
OK

myjobrun-3-0/myjobrun:
Hi from a batch job! My index is: 3
```
{: screen}

**Example**

This example displays the logs of all of the instances of a job run. 

```
ibmcloud ce jobrun logs --jobrun myjobrun
```
{: pre}

**Example output**

```
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
  
### `ibmcloud ce jobrun events`  
{: #cli-jobrun-events}  

Display the events of job run instances.  
  
```
 ibmcloud ce jobrun events (--instance JOBRUN_INSTANCE | --jobrun JOBRUN_NAME) [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--instance`</dt>
<dd>The name of a specific job run instance. Use the `jobrun get` command to find the instance name. This value is required if `--jobrun` is not specified. 
</dd>
<dt>`-j`, `-name`, `-n`, `--jobrun`</dt>
<dd>Display the events of all the instances of the specified job run. This value is required if `--instance` is not specified. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

This example displays the system event information for all the instances of a specified job run.   

```
ibmcloud ce jobrun events --jobrun myjobrun
```
{: pre}

**Example output**

```
Getting jobrun 'myjobrun'...
Getting instances of jobrun 'myjobrun'...
Getting events for all instances of job run 'myjobrun'...
OK

myjobrun-1-0:
  Type     Reason                  Age  Source                  Messages
  Normal   Scheduled               49s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-1-0 to 10.240.64.136
  [...]
  Normal   Pulling                 34s  kubelet, 10.240.64.136  Pulling image "ibmcom/testjob"

myjobrun-2-0:
  Type    Reason     Age  Source                  Messages
  Normal  Scheduled  50s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-2-0 to 10.240.64.131
  Normal  Pulling    48s  kubelet, 10.240.64.131  Pulling image "ibmcom/testjob"

```
{: screen}

**Example**

You can also display system event information for a specified instance of a job run by using the `--instance` option with the [`ibmcloud ce jobrun events`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events) command. Use the `jobrun get` command to display details about your job run, including the running instances of the job run. 

```
ibmcloud ce jobrun events --instance myjobrun-2-0
```
{: pre}

**Example output**

```
Getting events for job run instance 'myjobrun-2-0'...
OK

myjobrun-2-0:
  Type    Reason     Age    Source                  Messages
  Normal  Scheduled  3m39s  default-scheduler       Successfully assigned 4svg40kna19/myjobrun-2-0 to 10.240.64.131
  Normal  Pulling    3m37s  kubelet, 10.240.64.131  Pulling image "ibmcom/testjob"
  Normal  Pulled     2m42s  kubelet, 10.240.64.131  Successfully pulled image "ibmcom/testjob"
  Normal  Created    2m42s  kubelet, 10.240.64.131  Created container myjobrun
  Normal  Started    2m41s  kubelet, 10.240.64.131  Started container myjobrun
```
{: screen}
  
  
## Secret commands  
{: #cli-secret}  

A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `secret` commands.

To see CLI help for the `secret` commands, run `ibmcloud ce secret -h`.
{: tip}  
  
### `ibmcloud ce secret create`  
{: #cli-secret-create}  

Create a generic secret.  
  
```
 ibmcloud ce secret create --name SECRET_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the generic secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-e`, `--from-env-file`</dt>
<dd>Create a generic secret from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. This value is required if `--from-literal` or `--from-file` is not specified. 
</dd>
<dt>`-f`, `--from-file`</dt>
<dd>Create a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create a generic secret from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. 
</dd>
</dl>  
  
**Examples**

- The following example creates a secret that is named `mysecret-fromliteral` with a username and password value pair.

  ```
  ibmcloud ce secret create --name mysecret-fromliteral --from-literal username=devuser --from-literal password='S!B\*d$zDsb'
  ```
  {: pre}

  **Example output**

  ```
  Creating secret mysecret-fromliteral...
  OK
  ```
  {: screen}

- The following example creates a secret that is named `mysecret-fromfile` with values from a file.

  ```
  ibmcloud ce secret create --name mysecret-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Example output**

  ```
  Creating secret mysecret-fromfile...
  OK
  ```
  {: screen}
    
  
### `ibmcloud ce secret get`  
{: #cli-secret-get}  

Display the details of a generic secret.  
  
```
 ibmcloud ce secret get --name SECRET_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the generic secret. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce secret get --name mysecret-fromliteral
```
{: pre}

**Example output**

```
Getting generic secret 'mysecret-fromliteral'...
OK

Name:          mysecret-fromliteral
ID:            abcdabcd-abcd-abcd-abcd-abcdabcd1111
Project Name:  myproj
Project ID:    01234567-abcd-bcde-cdef-abcdabcd2222
Age:           66s
Created:       2020-10-13 15:46:03 -0400 EDT

Data:
---
password: UyFCXCpkJHpEc2I=
username: ZGV2dXNlcg==
```
{: screen}  
  
### `ibmcloud ce secret update`  
{: #cli-secret-update}  

Update a generic secret.  
  
```
 ibmcloud ce secret update --name SECRET_NAME (--from-env-file FILE | --from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE | --rm KEY)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the generic secret. This value is required. 
</dd>
<dt>`-e`, `--from-env-file`</dt>
<dd>Update a generic secret from a file which contains one or more lines that match the format `KEY=VALUE`. You must provide the path to the file as a value. Each line from the specified file is added as a key-value pair. This value is required if `--from-literal` or `--from-file` is not specified. 
</dd>
<dt>`-f`, `--from-file`</dt>
<dd>Update a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` or `--from-env-file` is not specified. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Update a generic secret from a key-value pair. Must be in `KEY=VALUE` format. This value is required if `--from-file` or `--from-env-file` is not specified. 
</dd>
<dt>`--rm`</dt>
<dd>Remove an individual key-value pair in a generic secret by specifying the name of the key. This value is optional. </dd>
</dl>  
  
**Example**

```
ibmcloud ce secret update --name mysecret-fromliteral --from-literal username=newuser --from-literal password='A!E\*$aBcD'
```
{: pre}


**Example output**

```
Updating secret mysecret-fromliteral...
OK
```
{: screen}  
  
### `ibmcloud ce secret delete`  
{: #cli-secret-delete}  

Delete a generic secret.  
  
```
 ibmcloud ce secret delete --name SECRET_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the generic secret. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce secret delete --name mysecret-fromfile -f
```
{: pre}

**Example output**

```
Deleting secret mysecret-fromfile...
OK
```
{: screen}  
  
### `ibmcloud ce secret list`  
{: #cli-secret-list}  

List all generic secrets in a project.  
  
```
 ibmcloud ce secret list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce secret list
```
{: pre}

**Example output**

```
Listing secrets...
OK

Name                  Data  Age
mysecret-fromfile     2     20m38s
mysecret-fromliteral  2     30m38s
```
{: screen}  
  
## Repo commands  
{: #cli-repo}  

A code repository, such as GitHub or GitLab, stores source code. With {{site.data.keyword.codeengineshort}}, you can add access to a private code repository and then reference that repository from your build.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `repo` commands.

To see CLI help for the `repo` commands, run `ibmcloud ce repo -h`.
{: tip}  
  
### `ibmcloud ce repo create`  
{: #cli-repo-create}  

Create a Git repository access secret.  
  
```
 ibmcloud ce repo create --name SECRET_NAME --key-path SSH_KEY_PATH --host HOST_ADDRESS [--known-hosts-path KNOWN_HOSTS_PATH]
```
{: pre}

**Command Options**  
<dl>
<dt>`-ho`, `--host`</dt>
<dd>The address of the host; for example `github.com`. This value is required. 
</dd>
<dt>`-kp`, `--key-path`</dt>
<dd>The path to your unencrypted SSH private key file. If you use your personal private SSH key, then this file is usually located at `$HOME/.ssh/id_rsa` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\id_rsa` (Windows). This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the Git repository access secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-khp`, `--known-hosts-path`</dt>
<dd>The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. This file is usually located at `$HOME/.ssh/known_hosts` (Mac OS or Linux) or at `%HOMEPATH%\.ssh\known_hosts` (Windows). This value is optional. 
</dd>
</dl>  
  
**Example**

The following command creates a Git access secret called `github` for host `github.com` and authenticates with an SSH key located at `/<filepath>/.ssh/id_rsa`, where `<filepath>` is the path on your system.

```
ibmcloud ce repo create -n github --key-path /<filepath>/.ssh/id_rsa --host github.com  
```
{: pre}

**Example output**

```
Creating Git access secret github...
OK
```
{: screen}  
  
### `ibmcloud ce repo get`  
{: #cli-repo-get}  

Display the details of a Git repository access secret.  
  
```
 ibmcloud ce repo get --name NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the Git repository access secret. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce repo get -n github
```
{: pre}

**Example output**

```
Getting Git access secret github...
OK

Name:        github  
Project:     myproj  
Project ID:  858ef04d-abcd-abcd-abcd-abcdabcd1111  
Created:     Fri, 11 Sep 2020 15:11:54 -0500  
Host:        github.com  
Data:          
---
ssh-privatekey: 
ABCDABCDABCDABCDABCDU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjABCDABCDABCDABCDhrdGRqRUFBQUFBQ21GbGN6STFOaABCDABCDABCDABCDABCDABCDE
...
```
{: screen}  
  
### `ibmcloud ce repo delete`  
{: #cli-repo-delete}  

Delete a Git repository access secret.  
  
```
 ibmcloud ce repo delete --name NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the Git repository access secret. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce repo delete --name github
```
{: pre}

**Example output**

```
Are you sure you want to delete the Git access secret github? [y/N]> y
Deleting Git access secret github...
OK

```
{: screen}  
  
### `ibmcloud ce repo list`  
{: #cli-repo-list}  

List all Git repository access secrets in a project.  
  
```
 ibmcloud ce repo list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example output**

```
Listing Git access secrets...
OK

Name    Age  
github  13m0s  
```
{: screen}  
  
## Registry commands  
{: #cli-registry}  

A container image registry, or registry, is a repository for your container images. For example, Docker Hub and {{site.data.keyword.registryfull_notm}} are container image registries. A container image registry can be public or private. With {{site.data.keyword.codeengineshort}}, you can add access to your private container image registries.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `registry` commands.

To see CLI help for the `registry` commands, run `ibmcloud ce registry -h`.
{: tip}  
  
### `ibmcloud ce registry create`  
{: #cli-registry-create}  

Create an image registry access secret.  
  
```
 ibmcloud ce registry create --name NAME (--password PASSWORD | --password-from-file PASSWORD_FILE) [--email EMAIL] [--server SERVER] [--username USERNAME]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the image registry access secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-e`, `--email`</dt>
<dd>The email address to access the registry server. This value is optional. 
</dd>
<dt>`-p`, `--password`</dt>
<dd>The password to access the registry server. If neither the `--password` nor the `--password-from-file` option is specified, you are prompted for the password. This value is optional. 
</dd>
<dt>`-pf`, `--password-from-file`</dt>
<dd>The path to a file containing the password to access the registry server. The first line of the file is used for the password. If neither the `--password` nor the `--password-from-file` option is specified, you are prompted for the password. This value is optional. 
</dd>
<dt>`-s`, `--server`</dt>
<dd>The URL of the registry server. This value is optional. The default value is <code>us.icr.io</code>.
</dd>
<dt>`-u`, `--username`</dt>
<dd>The username to access the registry server. This value is optional. The default value is <code>iamapikey</code>.
</dd>
</dl>  
  
**Example**

The following example creates image registry access that is called `myregistry` to a {{site.data.keyword.registryshort}} instance that is located at `us.icr.io` and uses a username of `iamapikey` and the IAM API key as a password.
```
ibmcloud ce registry create --name myregistry --server us.icr.io --username iamapikey --password API_KEY   
```
{: pre}

**Example output**

```
Creating image registry access secret myregistry...

OK
```
{: screen}  
  
### `ibmcloud ce registry get`  
{: #cli-registry-get}  

Display the details of an image registry access secret.  
  
```
 ibmcloud ce registry get --name NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the image registry access secret. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce registry get --name myregistry   
```
{: pre}

**Example output**

```
Getting image registry access secret myregistry...
OK

Name:        myregistry
Project:     myproject
Project ID:  b246abcd-abcd-abcd-abcd-abcd52060394
Created:     Thu, 10 Sep 2020 18:59:13 -0400
Data:
---
.dockerconfigjson: abcdabcdabcdabcdabcdnVzZXJuYW1lIjoiaWFtYXBpa2V5IiwicGFzc3dvcmQiOiJoQllTSTc5Uk8yQUIxSDV3RUs2UzhScV9uNzE4NkQ1eWt1M1FOUk85aFpfaCIsImVtYWlsIjoiYUBiLmMiLCabcdabcdabcdabcdabcdT21oQ1dWTkpOemxTVHpKQlFqRklOWGRGU3paVE9GSnhYMjQzTVRnMlJEVjabcdabcdabcdabcdabcdbG9XbDlvIn19fQ==
```
{: screen}  
  
### `ibmcloud ce registry delete`  
{: #cli-registry-delete}  

Delete an image registry access secret.  
  
```
 ibmcloud ce registry delete --name NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the image registry access secret. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce registry delete --name myregistry -f   
```
{: pre}

**Example output**

```
Deleting image registry access secret myregistry...

OK
```
{: screen}  
  
### `ibmcloud ce registry list`  
{: #cli-registry-list}  

List all image registry access secrets in a project.  
  
```
 ibmcloud ce registry list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce registry list   
```
{: pre}

**Example output**

```
Listing image registry access secrets...

OK

Name        Age
myregistry  19m22s
```
{: screen}  
  
## Version command  
{: #cli-version}  

Display the version of the `code-engine` command-line interface.  
  
### `ibmcloud ce version`  
{: #cli-versioncmd}  

Display the version of the `code-engine` command-line interface.  
  
```
 ibmcloud ce version
```
{: pre}

**Example output**

```
v0.3.1363
commit: 166d5062462579e4216c4dbb1c3b2768037a00f9
```
{: screen}  
  
  

## Build commands  
{: #cli-build}  

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpacks. Use `build` commands to create, display details, update, and delete build configurations. After you create a build configuration, one or more [`buildrun` commands](#cli-buildrun) can be submitted based on the build configuration.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `build` commands.

You can use either `build` or `bd` in your `build` commands. To see CLI help for the `build` commands, run `ibmcloud ce build -h`.
{: tip}  
  
### `ibmcloud ce build create`  
{: #cli-build-create}  

Create a build.  
  
```
 ibmcloud ce build create --name BUILD_NAME --image IMAGE_REF --source SOURCE --registry-secret REGISTRY_REF [--commit COMMIT] [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--git-repo-secret GIT_REPO_SECRET] [--size SIZE] [--strategy STRATEGY] [--timeout TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The image registry access secret that is used to access the registry. You can add the image registry access secret by running the `registry create` command. This value is required. 
</dd>
<dt>`-src`, `--source`</dt>
<dd>The URL of the Git repository that contains your source code; for example `https://github.com/IBM/CodeEngine`. This value is required. 
</dd>
<dt>`-cm`, `-revision`, `--commit`</dt>
<dd>The commit, tag, or branch in the source repository to pull. This value is optional. The default value is <code>main</code>.
</dd>
<dt>`-cdr`, `--context-dir`</dt>
<dd>The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. 
</dd>
<dt>`-df`, `--dockerfile`</dt>
<dd>The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is optional. The default value is <code>Dockerfile</code>.
</dd>
<dt>`-grs`, `-repo`, `-r`, `--git-repo-secret`</dt>
<dd>The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. This value is optional. 
</dd>
<dt>`-sz`, `--size`</dt>
<dd>The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. This value is optional. The default value is <code>medium</code>.
</dd>
<dt>`-str`, `--strategy`</dt>
<dd>The strategy to use for building the image. Valid values are `kaniko` and `buildpacks`. This value is optional. The default value is <code>kaniko</code>.
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build must succeed or fail. This value is optional. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

The following example creates a build configuration file called `helloworld-build` from a source Dockerfile (`kaniko`), `medium` size, and located in `https://github.com/IBM/CodeEngine` inside the `hello` directory in the `main` branch.  When this build is submitted, the container image that is built is stored in a {{site.data.keyword.registryshort}} instance at `us.icr.io/mynamespace/codeengine-helloworld` that is accessed by using a image registry secret called `myregistry`.

```
ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --commit main --strategy kaniko --size medium --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry
```
{: pre}

**Example output**

```
Creating build helloworld-build...
OK
```
{: screen}  
  
### `ibmcloud ce build get`  
{: #cli-build-get}  

Display the details of a build.  
  
```
 ibmcloud ce build get --name BUILD_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce build get --name helloworld-build
```
{: pre}

**Example output**

```
Getting build 'helloworld-build'
OK

Name:          helloworld-build
ID:            abcdabcd-abcd-abcd-abcd-abcdabcd1111
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
Age:           15s
Created:       2021-03-01T13:33:58-05:00
Status:        Succeeded

Image:              us.icr.io/mynamespace/codeengine-helloworld
Registry Secret:    myregistry
Build Strategy:     kaniko-medium
Timeout:            10m0s
Source:             https://github.com/IBM/CodeEngine
Commit:             main
Context Directory:  /hello
Dockerfile:         Dockerfile 

Build Runs:
  Name                                  Status     Age
  helloworld-build-run                  Succeeded  6d19h
  mybuildrun                            Succeeded  21h
  mybuildrun2                           Succeeded  20h
```
{: screen}  
  
### `ibmcloud ce build update`  
{: #cli-build-update}  

Update a build.  
  
```
 ibmcloud ce build update --name BUILD_NAME [--commit COMMIT] [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--git-repo-secret GIT_REPO_SECRET] [--image IMAGE] [--registry-secret REGISTRY_SECRET] [--size SIZE] [--source SOURCE] [--strategy STRATEGY] [--timeout TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. This value is required. 
</dd>
<dt>`-cm`, `-revision`, `--commit`</dt>
<dd>The commit, tag, or branch in the source repository to pull. This value is optional. 
</dd>
<dt>`-cdr`, `--context-dir`</dt>
<dd>The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. 
</dd>
<dt>`-df`, `--dockerfile`</dt>
<dd>The path to the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is optional. The default value is <code>Dockerfile</code>.
</dd>
<dt>`-grs`, `-repo`, `-r`, `--git-repo-secret`</dt>
<dd>The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is optional. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-sz`, `--size`</dt>
<dd>The size for the build, which determines the amount of resources used. Valid values are `small`, `medium`, `large`, `xlarge`. This value is optional. 
</dd>
<dt>`-src`, `--source`</dt>
<dd>The URL of the Git repository that contains your source code; for example `https://github.com/IBM/CodeEngine`. This value is optional. 
</dd>
<dt>`-str`, `--strategy`</dt>
<dd>The strategy to use for building the image. Valid values are `kaniko` and `buildpacks`. This value is optional. 
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build must succeed or fail. This value is optional. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce build update --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --commit main --timeout 900
```
{: pre}

**Example output**

```
Updating build helloworld-build...
OK
```
{: screen}  
  
### `ibmcloud ce build delete`  
{: #cli-build-delete}  

Delete a build.  
  
```
 ibmcloud ce build delete --name BUILD_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce build delete --name helloworld-build
```
{: pre}

**Example output**

```
Are you sure you want to delete build helloworld-build? [y/N]> y
Deleting build 'helloworld-build'...
OK
```
{: screen}  
  
### `ibmcloud ce build list`  
{: #cli-build-list}  

List all builds in a project.  
  
```
 ibmcloud ce build list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example output**

```
Listing builds...
OK

Name                           Registered  Reason     Build Strategy  Age  
codeengine-app-72-build-tmnz2  True        Succeeded  kaniko-medium   6h23m  
helloworld-build               True        Succeeded  kaniko-medium   39s 
```
{: screen}  
  
## Buildrun commands  
{: #cli-buildrun}  

A build, or image build, is a mechanism that you can use to create a container image from your source code. {{site.data.keyword.codeengineshort}} supports building from a Dockerfile and buildpacks. Use `buildrun` commands to submit, display details, and delete build runs.
{: shortdesc}

You must be within the context of a [project](#cli-project) before you use `buildrun` commands.

You can use either `buildrun` or `br` in your `buildrun` commands. To see CLI help for the `buildrun` commands, run `ibmcloud ce br -h`.
{: tip}  
  
### `ibmcloud ce buildrun submit`  
{: #cli-buildrun-submit}  

Submit a build run.  
  
```
 ibmcloud ce buildrun submit --build BUILD_NAME [--image IMAGE] [--name NAME] [--no-wait] [--timeout TIMEOUT] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-bd`, `--build`</dt>
<dd>The name of the build configuration to use. This value is required. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The location of the image registry. The format is `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `TAG` is optional. If `TAG` is not specified, the default is `latest`. This value is optional. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the build run. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 63 characters or fewer and can contain lowercase alphanumeric characters and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Submit the build run and do not wait for this build run to complete. If you specify the `--no-wait` option, the build run submit begins and does not wait. Use the `buildrun get` command to check the build run status. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build run must succeed or fail. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Submit the build run and wait for this build run to complete. If you specify the `--wait` option, the build run submit waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the build run to complete. If the build run is not completed within the specified `--wait-timeout` period, the build run submit fails. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for this build run to complete. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

The following command submits a build run called `mybuildrun` and uses the build configuration file called `helloworld-build`.

```
ibmcloud ce buildrun submit --name mybuildrun --build helloworld-build
```
{: pre}

**Example output**

```
Submitting build run 'mybuildrun'...
Run 'ibmcloud ce buildrun get -n mybuildrun' to check the build run status.
OK 
```
{: screen}  
  
### `ibmcloud ce buildrun get`  
{: #cli-buildrun-get}  

Display the details of a build run.  
  
```
 ibmcloud ce buildrun get --name BUILDRUN_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build run. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce buildrun get --name mybuildrun
```
{: pre}

**Example output**

```
Getting build run 'mybuildrun'...
OK

Name:          mybuildrun
ID:            abcdabcd-abcd-abcd-abcd-abcdabcd1122
Project Name:  myproject
Project ID:    01c71469-abcd-abcd-abcd-abcdabcd1123
Age:           23s
Created:       2021-03-01T13:38:26-05:00

Summary:  Succeeded
Status:   Succeeded
Reason:   Succeeded
```
{: screen}  
  
### `ibmcloud ce buildrun delete`  
{: #cli-buildrun-delete}  

Delete a build run.  
  
```
 ibmcloud ce buildrun delete --name BUILDRUN_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build run. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example** 

```
ibmcloud ce buildrun delete --name mybuildrun
```
{: pre}

**Example output**

```
Are you sure you want to delete build run mybuildrun? [y/N]> y
Deleting build run 'mybuildrun'...
OK
```
{: screen}  
  
### `ibmcloud ce buildrun list`  
{: #cli-buildrun-list}  

List all build runs in a project.  
  
```
 ibmcloud ce buildrun list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example output**

```
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
  
```
 ibmcloud ce buildrun logs --buildrun BUILDRUN_NAME [--follow] [--output OUTPUT] [--tail TAIL] [--timestamps]
```
{: pre}

**Command Options**  
<dl>
<dt>`-b`, `-name`, `-n`, `--buildrun`</dt>
<dd>The name of the build run. This value is required. 
</dd>
<dt>`-f`, `--follow`</dt>
<dd>Follow the logs of the build run. Use this option to stream logs of the build run. If you specify the `--follow` option, you must enter `Ctrl+C` to terminate this log command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-t`, `--tail`</dt>
<dd>Limit the display of logs of containers of the specified build run to a maximum number of recent lines per container. For example, to display the last `3` lines of the logs of the containers of the specified build run, specify `--tail 3`. If this option is not specified, all lines of the logs of the containers of the specified build run are displayed. This value is optional. The default value is <code>-1</code>.
</dd>
<dt>`-ts`, `--timestamps`</dt>
<dd>Include timestamps on each line in the log output. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

**Example output**

```
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
  
### `ibmcloud ce buildrun events`  
{: #cli-buildrun-events}  

Display the events of a build run.  
  
```
 ibmcloud ce buildrun events --buildrun BUILDRUN_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-b`, `-name`, `-n`, `--buildrun`</dt>
<dd>The name of the build run. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

This example displays the system event information for a build run. 

```
ibmcloud ce buildrun events --buildrun mybuildrun
```
{: pre}

**Example output**

```
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
  
## Subscription commands  
{: #cli-subscription}  

In distributed environments, oftentimes, you want your applications to react to messages (events) that are generated from other components, usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications can subscribe to event producers so that events that are of interest can be delivered as HTTP requests to those applications.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports two types of event producers. First, is a ping (cron) event producer that generates an event at regular intervals. This type of event producer is often used when an action needs to be taken at well-defined intervals or specific times. Secondly, is an {{site.data.keyword.cos_full_notm}} event producer. This type of event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform some action based on that change, perhaps consuming that new object.

You must be within the context of a [project](#cli-project) before you use `subscription` commands.

You can use either `subscription` or `sub` in your `subscription` commands. To see CLI help for the `subscription` commands, run `ibmcloud ce sub -h`. 
{: tip}  
  
### `ibmcloud ce subscription cos`  
{: #cli-subscription-cos}  

Manage {{site.data.keyword.cos_full_notm}} event subscriptions.  
  
```
 ibmcloud ce subscription cos COMMAND
```
{: pre}

### `ibmcloud ce subscription cos create`  
{: #cli-subscription-cos-create}  

Create an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```
 ibmcloud ce subscription cos create --name COS_SOURCE_NAME --destination DESTINATION_REF --bucket BUCKET_NAME [--event-type EVENT_TYPE] [--force] [--no-wait] [--path PATH] [--prefix PREFIX] [--suffix SUFFIX] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-b`, `--bucket`</dt>
<dd>The bucket for events. The destination and the bucket must be in the same region of the project. This value is required. 
</dd>
<dt>`-d`, `--destination`</dt>
<dd>The name of the application to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify the destination. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the {{site.data.keyword.cos_full_notm}} event subscription. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-e`, `--event-type`</dt>
<dd>The event types to watch. Valid values are `delete`, `write`, and `all`. This value is optional. The default value is <code>all</code>.
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force to create an {{site.data.keyword.cos_full_notm}} event subscription. This option skips the validation of users' specified destination. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Create the {{site.data.keyword.cos_full_notm}} event subscription and do not wait for the subscription to be ready. If you specify the `--no-wait` option, the subscription create begins and does not wait. Use the `subscription cos get` command to check the subscription status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`--path`</dt>
<dd>The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This value is optional. The default value is <code>/</code>.</dd>
<dt>`-p`, `--prefix`</dt>
<dd>Prefix of the {{site.data.keyword.cos_full_notm}} object. This value is optional. 
</dd>
<dt>`-s`, `--suffix`</dt>
<dd>Suffix of the {{site.data.keyword.cos_full_notm}}. Consider the file type of your file when specifying the suffix. This value is optional. 
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Create the {{site.data.keyword.cos_full_notm}} event subscription and wait for the subscription to be ready. If you specify the `--wait` option, the subscription create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to become ready. If the subscription is not ready within the specified `--wait-timeout` period, the {{site.data.keyword.cos_full_notm}} event subscription create fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the {{site.data.keyword.cos_full_notm}} event subscription to be ready to start. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>15</code>.
</dd>
</dl>  
  
**Example**

The {{site.data.keyword.cos_full_notm}} subscription listens for changes to an {{site.data.keyword.cos_short}} bucket. The following example creates a COS subscription called `mycosevent` for a bucket called `mybucket` that is attached to an app called `myapp`. 

```
ibmcloud ce subscription cos create --name mycosevent --destination myapp --bucket mybucket
```
{: pre}

**Example output**

```
Creating COS source 'mycosevent'...
Run 'ibmcloud ce subscription cos get -n mycosevent' to check the COS source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription cos delete`  
{: #cli-subscription-cos-delete}  

Delete an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```
 ibmcloud ce subscription cos delete --name COS_SOURCE_NAME [--force] [--no-wait] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Delete the {{site.data.keyword.cos_full_notm}} event subscription and do not wait for the subscription to be deleted. If you specify the `--no-wait` option, the subscription delete begins and does not wait. Use the `subscription cos get` command to check the subscription status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Delete the {{site.data.keyword.cos_full_notm}} event subscription and wait for the subscription to be deleted. If you specify the `--wait` option, the subscription delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to be deleted. This command exits when the subscription is deleted or whenever `--wait-timeout` is reached, whichever comes first. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the {{site.data.keyword.cos_full_notm}} event subscription to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>15</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription cos delete --name mycosevent -f
```
{: pre}

**Example output**

```
Deleting COS source 'mycosevent'...
OK
```
{: screen}  
  
### `ibmcloud ce subscription cos list`  
{: #cli-subscription-cos-list}  

List all {{site.data.keyword.cos_full_notm}} event subscriptions in a project.  
  
```
 ibmcloud ce subscription cos list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription cos list
```
{: pre}

**Example output**

```
Listing COS sources...
OK

Name        Age  Ready  Bucket        EventType  Prefix  Suffix  Destination
mycosevent  20m  true   mycosbucket  all                         http://myapp.2706b22d-676b.svc.cluster.local
```
{: screen}  
  
### `ibmcloud ce subscription cos get`  
{: #cli-subscription-cos-get}  

Display the details of an {{site.data.keyword.cos_full_notm}} event subscription. Displayed attributes include `Name`, `Destination`, `Bucket`, `Event Type`, `Prefix`, `Suffix`, `Ready`, and `Age`. To see specific details, attach `| grep <attribute>`.  
  
```
 ibmcloud ce subscription cos get --name COS_SOURCE_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription cos get --name mycosevent
```
{: pre}

**Example output**

```
Getting COS source 'mycosevent'...
OK

Name:          mycosevent
[...]
Destination:  http://myapp.2706b22d-676b.svc.cluster.local
Bucket:       mycosbucket
EventType:    all
Ready:        true

Events:
  Type     Reason           Age                From                  Messages
  Normal   FinalizerUpdate  24s                cossource-controller  Updated "mycosevent" finalizers
  Normal   CosSourceReady   22s (x3 over 22s)  cossource-controller  CosSource is ready
```
{: screen}

When `Ready` is `true`, then the COS subscription is ready to trigger events per changes to the COS bucket. 
  
  
### `ibmcloud ce subscription cos update`  
{: #cli-subscription-cos-update}  

Update an {{site.data.keyword.cos_full_notm}} event subscription.  
  
```
 ibmcloud ce subscription cos update --name COS_SOURCE_NAME [--destination DESTINATION] [--event-type EVENT_TYPE] [--path PATH] [--prefix PREFIX] [--suffix SUFFIX]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the {{site.data.keyword.cos_full_notm}} event subscription. This value is required. 
</dd>
<dt>`-d`, `--destination`</dt>
<dd>The name of the application to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify the destination. This value is optional. 
</dd>
<dt>`-e`, `--event-type`</dt>
<dd>The event types to watch. Valid values are `delete`, `write`, and `all`. This value is optional. 
</dd>
<dt>`--path`</dt>
<dd>The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This value is optional. </dd>
<dt>`-p`, `--prefix`</dt>
<dd>Prefix of the IBM Cloud Object Storage object. This value is optional. 
</dd>
<dt>`-s`, `--suffix`</dt>
<dd>Suffix of the IBM Cloud Object Storage object. Consider the file type (extension) of your file when specifying the suffix. This value is optional. 
</dd>
</dl>  
  
**Example**

The following example updates a COS subscription called `mycosevent` to listen for only write events. 

```
ibmcloud ce subscription cos update --name mycosevent --event-type write
```
{: pre}

**Example output**

```
Updating COS source 'mycosevent'...
Run 'ibmcloud ce subscription cos get -n mycosevent' to check the COS source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription ping`  
{: #cli-subscription-ping}  

Manage ping event subscriptions.  
  
```
 ibmcloud ce subscription ping COMMAND
```
{: pre}

### `ibmcloud ce subscription ping create`  
{: #cli-subscription-ping-create}  

Create a ping event subscription.  
  
```
 ibmcloud ce subscription ping create --name PING_SOURCE_NAME  --destination DESTINATION_REF [--data DATA] [--force] [--no-wait] [--path PATH] [--schedule SCHEDULE] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-d`, `--destination`</dt>
<dd>The name of the application to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify the destination. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the ping event subscription. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-da`, `--data`</dt>
<dd>The JSON data to send to the destination. This value is optional. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force to create a ping event subscription. This option skips the validation of the user specified destination. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Create the ping event subscription and do not wait for the subscription to be ready. If you specify the `--no-wait` option, the subscription create begins and does not wait.  Use the `subscription ping get` command to check the subscription status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`--path`</dt>
<dd>The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This value is optional. The default value is <code>/</code>.</dd>
<dt>`-s`, `--schedule`</dt>
<dd>Schedule how often the event is triggered, in crontab format. For example, specify `'*/2 * * * *'` (in string format) for every two minutes. By default, the ping event is triggered every minute. This value is optional. 
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Create the ping event subscription and wait for the subscription to be ready. If you specify the `--wait` option, the subscription create waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to become ready. If the subscription is not ready within the specified `--wait-timeout` period, the ping event subscription create fails. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the ping event subscription to be ready to start. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>15</code>.
</dd>
</dl>  
  
**Example**

The following example creates a ping subscription called `mypingevent` that attaches to an existing app called `myapp` that is triggered every 2 minutes. 

```
ibmcloud ce subscription ping create --name mypingevent --destination myapp --schedule '*/2 * * * *'
```
{: pre}

**Example output**

```
Creating Ping source 'mypingevent'...
Run 'ibmcloud ce subscription ping get -n mypingevent' to check the Ping source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription ping delete`  
{: #cli-subscription-ping-delete}  

Delete a ping event subscription.  
  
```
 ibmcloud ce subscription ping delete --name PING_SOURCE_NAME [--force] [--no-wait] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the ping event subscription. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Delete the ping event subscription and do not wait for the subscription to be deleted. If you specify the `--no-wait` option, the subscription delete begins and does not wait.  Use the `subscription ping get` command to check the subscription status. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Delete the ping event subscription and wait for the subscription to be deleted. If you specify the `--wait` option, the subscription delete waits for a maximum time in seconds, as set by the `--wait-timeout` option, for the subscription to be deleted. This command exits when the subscription is deleted or whenever `--wait-timeout` is reached, whichever comes first. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the ping event subscription to be deleted. This value is required if the `--wait` option is specified. This value is ignored if the `--no-wait` option is specified. The default value is <code>15</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription ping delete --name mypingevent -f
```
{: pre}

**Example output**

```
Deleting Ping source 'mypingevent'...
OK
```
{: screen}  
  
### `ibmcloud ce subscription ping list`  
{: #cli-subscription-ping-list}  

List all ping event subscriptions in a project.  
  
```
 ibmcloud ce subscription ping list [--output OUTPUT] [--sort-by SORT_BY]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
<dt>`-s`, `--sort-by`</dt>
<dd>Specifies the column by which to sort the list. Valid values are `name` and `age`. This value is optional. The default value is <code>name</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription ping list
```
{: pre}

**Example output**

```
Listing Ping sources...
OK

Name         Age  Ready  Destination                                   Schedule     Data
mypingevent  96m  true   http://myapp.cd4200a7-5037.svc.cluster.local  */2 * * * *
```
{: screen}  
  
### `ibmcloud ce subscription ping update`  
{: #cli-subscription-ping-update}  

Update a ping event subscription.  
  
```
 ibmcloud ce subscription ping update --name PING_SOURCE_NAME [--data DATA] [--destination DESTINATION] [--path PATH] [--schedule SCHEDULE]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the ping event subscription. This value is required. 
</dd>
<dt>`-da`, `--data`</dt>
<dd>The JSON data to send to the destination. This value is optional. 
</dd>
<dt>`-d`, `--destination`</dt>
<dd>The name of the application to receive events; for example, `myapp`. If needed, use the `--path` option to further qualify the destination. This value is optional. 
</dd>
<dt>`--path`</dt>
<dd>The path within the `destination` application where events are forwarded; for example, `/events`. The default path is the root URL of the `destination` application. This value is optional. </dd>
<dt>`-s`, `--schedule`</dt>
<dd>Schedule how often the event is triggered, in crontab format. For example, specify `'*/2 * * * *'` (in string format) for every two minutes. By default, the Ping event is triggered every minute. This value is optional. 
</dd>
</dl>  
  
**Example**

The following example updates a ping subscription called `mypingevent` that attaches to an existing app called `myapp` that is triggered every hour.  

```
ibmcloud ce subscription ping update --name mypingevent --destination myapp --schedule '0 * * * *'
```
{: pre}

**Example output**

```
Updating Ping source 'mypingevent'...
Run 'ibmcloud ce subscription ping get -n mypingevent' to check the Ping source status.
OK
```
{: screen}  
  
### `ibmcloud ce subscription ping get`  
{: #cli-subscription-ping-get}  

Display details of a ping event subscription.  
  
```
 ibmcloud ce subscription ping get --name PING_SOURCE_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the ping event subscription. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid values are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce subscription ping get --name mypingevent
```
{: pre}

**Example output**

```
Getting Ping source 'mypingevent'...
OK

Name:          mypingevent
[...]
Destination:  http://myapp.40c93bf3-8bd6.svc.cluster.local
Schedule:     */2 * * * *
Ready:        true

Events:
  Type    Reason           Age  From                   Messages
  Normal  FinalizerUpdate  27s  pingsource-controller  Updated "mypingevent" finalizers
```
{: screen}

When `Ready` is `true`, then the ping subscription is ready to trigger events per the specified schedule. 
  
  
