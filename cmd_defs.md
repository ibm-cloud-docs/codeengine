---

copyright:
  years: 2020
lastupdated: "2020-09-29"

keywords: code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# {{site.data.keyword.codeenginefull_notm}} CLI
{: #kn-cli}

Run these commands to manage the entities that make up {{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}").
{: shortdesc}

To run {{site.data.keyword.codeenginefull_notm}} commands, use `ibmcloud code-engine` or `ibmcloud ce`.
{: tip}
  
  
## Project commands  
{: #cli-project}  

A project is a grouping of {{site.data.keyword.codeengineshort}} entities such as applications, jobs and builds. Projects are used to manage resources and provide access to its entities.
{: shortdesc}

You can use either `project` or `proj` in your project commands. To see CLI help for the project command, run `ibmcloud ce proj -h`.
{: tip}
  
  
### `ibmcloud ce project create`  
{: #cli-project-create}  

Create a project.  
  
```
 ibmcloud ce project create --name PROJECT_NAME [--select] [--tag TAG]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. Use a name that is unique to your region. The name must be 128 characters or fewer and can contain:
<ul>
	<li>Any Unicode character</li>
	<li>Only these special characters: spaces ( ), periods (.), colons (:), underscores (\_), and hyphens (-)</li>
</ul>
This value is required. </dd>
<dt>`-target`, `--select`</dt>
<dd>Select the project for context after this project is created. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource. The label must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. Specify one label per `--tag` flag; for example, `--tag tagA --tag tagB`. This value is optional. 
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
 ibmcloud ce project delete --name PROJECT_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
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
 ibmcloud ce project list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Name       ID                                    Status  Tags  Location  Resource Group  
myproject  fdd1fe68-abcd-abcd-abcd-f1de4aab5d5d  active        us-south  default        
```
{: screen}
  
  
### `ibmcloud ce project get`  
{: #cli-project-get}  

Display the details of a single project.  
  
```
 ibmcloud ce project get --name PROJECT_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Name:             myproject
ID:               fdd1fe68-abcd-abcd-abcd-f1de4aab5d5d
Status:           active
Tags:
Location:         us-south
Resource Group:   default
Created:          Wed, 09 Aug 2020 19:41:49 -0400
Updated:          Wed, 09 Aug 2020 19:43:06 -0400
```
{: screen}
  
  
### `ibmcloud ce project select`  
{: #cli-project-select}  

Select a project for context.  
  
```
 ibmcloud ce project select --name PROJECT_NAME [--kubecfg]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. 
</dd>
<dt>`-k`, `--kubecfg`</dt>
<dd>Append the project to the default Kubernetes configuration file. This value is optional. The default value is <code>false</code>.
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
Project Name:   myproject
Region:         us-south

To use kubectl with your project, run the following command:
export KUBECONFIG=/user/myusername/.bluemix/plugins/code-engine/myproject-70427b7b-abcd-abcd-ad28-9efee81a6673.yaml
```
{: screen}
  
  
## Application commands  
{: #cli-application}  

Before you use application commands, you must be targeting a [project](#cli-project).  An application runs your code to serve HTTP requests. The application has a URL for incoming requests. Use application commands to create, display details, update, and delete applications.
{: shortdesc}

You can use either `application` or `app` in your application commands. To see CLI help for the application command, run `ibmcloud ce app -h`.
{: tip}
  
  
### `ibmcloud ce application create`  
{: #cli-application-create}  

Create an application.  
  
```
 ibmcloud ce application create --name APP_NAME --image IMAGE_REF [--argument ARGUMENT] [--cluster-local] [--command COMMAND] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--no-wait] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--timeout TIMEOUT] [--user USER] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The name of the image that is used for this application. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter</li>
	<li>The name must end with a lowercase alphanumeric character</li>
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-)</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified within the container image. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified within the container image. This value is optional. 
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The target number of requests to be processed concurrently per instance. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0.1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-max`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. The default value is <code>1024Mi</code>.
</dd>
<dt>`-min`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This option is useful to ensure that no instances are running when not needed. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This option is useful to ensure that no instances are running when not needed. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-nw`, `--no-wait`</dt>
<dd>Create the application asynchronously. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-p`, `--port`</dt>
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid options are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time in seconds that can pass before the application must succeed or fail. This value is optional. The default value is <code>300</code>.
</dd>
<dt>`-u`, `--user`</dt>
<dd>The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be ready. This value is ignored when `no-wait` is specified. This value is optional. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application create --name myapp --image ibmcom/hello
```
{: pre}

**Example output**

```
Creating Application 'myapp'...
Successfully created application 'myapp' created. 
Run `ibmcloud ce application get -n 'myapp'` to check the application status.
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application get --name myapp
```
{: pre}

**Example output**

```
Name:       myapp
Namespace:  b49ca89f-g99q
Age:        19h
URL:        http://myapp.b49ca89f-g99q.us-south.codeengine.appdomain.cloud

Revisions:
  100%  @latest (myapp-zxxlr-1) [1] (19h)
        Image:  ibmcom/hello (pinned to be18cb)

Conditions:
  OK TYPE                   AGE REASON
  ++ Ready                  19h
  ++ ConfigurationsReady    19h
  ++ RoutesReady            19h

Command 'application get' performed successfully
```
{: screen}
  
  
### `ibmcloud ce application update`  
{: #cli-application-update}  

Update an application. Updating your application creates a revision. When calls are made to the application, traffic is routed to the revision.  
  
```
 ibmcloud ce application update --name APP_NAME [--argument ARGUMENT] [--cluster-local] [--command COMMAND] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--image IMAGE] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--timeout TIMEOUT] [--user USER] [--wait] [--wait-timeout WAIT_TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the application. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The target number of requests to be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the application. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables in the application from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables after the application is updated. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
<dt>`-max`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-min`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-p`, `--port`</dt>
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid options are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-u`, `--user`</dt>
<dd>The user ID (UID) that is used to run the application. This value overrides any user ID that is set in the application Dockerfile. The ID must conform to the operating system requirements of the container. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-w`, `--wait`</dt>
<dd>Perform the update of the application synchronously. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be ready. This value is optional. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application update --name myapp --image ibmcom/hello
```
{: pre}

**Example output**

```
Updating Application 'myapp' in namespace 'f0173a8d-abc3':
Application 'myapp' updated to latest revision 'myapp-oobym-3' and is available at URL:
http://myapp.f0173a8d-abc3.us-south.codeengine.appdomain.cloud
```
{: screen}
  
  
### `ibmcloud ce application delete`  
{: #cli-application-delete}  

Delete an application.  
  
```
 ibmcloud ce application delete --name APPLICATION_NAME [--force] [--wait] [--wait-timeout WAIT_TIMEOUT]
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
<dt>`-w`, `--wait`</dt>
<dd>Perform the deletion of the application synchronously. The command exits when the application is deleted or whenever `wait-timeout` is reached, whichever comes first. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be deleted. This value is ignored when `wait` is `false`. This value is optional. The default value is <code>300</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application delete --name myapp
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
 ibmcloud ce application list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example output**

```
NAME        URL                                                                    LATEST              AGE   CONDITIONS   READY   REASON
myapp       http://myapp.b49ca89f-g99q.us-south.codeengine.appdomain.cloud       myapp-zxxlr-1       19h   3 OK / 3     True
mytestapp   http://mytestapp.42734592-8355.us-south.codeengine.appdomain.cloud   mytestapp-qhmzn-1   20h   3 OK / 3     True
```
{: screen}
  
  
### `ibmcloud ce application bind`  
{: #cli-application-bind}  

Bind an {{site.data.keyword.cloud_notm}} service to an application.  
  
```
 ibmcloud ce application bind --name APP_NAME --service-instance SI_NAME [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL] [--wait-timeout WAIT_TIMEOUT]
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
<dt>`-p`, `--prefix`</dt>
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-sc`, `--service-credential`</dt>
<dd>The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is optional. 
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the service binding to be ready. If this option is not specified, the binding is performed asynchronously. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

In this example, bind your language-translator service instance called `langtranslator` to your application called `myapp`.

```
ibmcloud ce application bind --name myapp --service-instance langtranslator
```
{: pre}

**Example output**

```
Configuring your project for service bindings...
Project successfully configured for service bindings
Binding service...
Successfully created service binding for 'langtranslator'
```
{: screen}
  
  
### `ibmcloud ce application unbind`  
{: #cli-application-unbind}  

Unbind {{site.data.keyword.cloud_notm}} services from an application.  
  
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
<dd>Unbinds all service instances for this application. This value is required if `--service-instance` is not specified. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of the service instance to unbind for this application. This value is required if `--all` is not specified. This value is optional. 
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
Successfully removed service bindings
OK
```
{: screen}
  
  
### `ibmcloud ce application logs`  
{: #cli-application-logs}  

Display the logs of an application instance. Use the `app get` command to find the instance name.  
  
```
 ibmcloud ce application logs --instance APP_INSTANCE
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--instance`</dt>
<dd>The name of the application instance. This value is required. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce application logs --instance myapp-l3kk6-1-deployment-656d46f7d6-qr5b2
```
{: pre}

**Example output**

```
Logging application instance 'myapp-l3kk6-1-deployment-656d46f7d6-qr5b2'...
OK
Command 'application logs' performed successfully
Server running at http://0.0.0.0:8080/
```
{: screen}
  
  
## Configmap commands  
{: #cli-configmap}  

Use configmap commands to create, display details, update, and delete configmaps.
{: shortdesc}

You can use either `configmap` or `cm` in your configmap commands. To see CLI help for the configmap commands, run `ibmcloud ce configmap -h`.
{: tip}
  
  
### `ibmcloud ce configmap create`  
{: #cli-configmap-create}  

Create a configmap.  
  
```
 ibmcloud ce configmap create --name CONFIGMAP_NAME ([--from-file FILE | --from-file KEY=FILE] | [--from-literal KEY=VALUE])
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-f`, `--from-file`</dt>
<dd>Create the configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create the configmap from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
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

  Successfully created configmap 'configmap-fromliteral'. Run `ibmcloud ce configmap get -n 'configmap-fromliteral'` to see more details.
  ```
  {: screen}
  
- The following example creates a configmap that is named `configmap-fromfile` with values from multiple files.

  ```
  ibmcloud ce configmap create --name configmap-fromfile  --from-file ./color.txt --from-file ./size.txt
  ```
  {: pre}

  **Example output**

  ```
  Creating Configmap 'configmap-fromfile'...

  Successfully created configmap 'configmap-fromfile'. Run `ibmcloud ce configmap get -n 'configmap-fromfile'` to see more details.
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce configmap get --name configmap-fromliteral 
```
{: pre}

**Example output**

```
Getting Configmap 'configmap-fromliteral'...

Name:        configmap-fromliteral
Namespace:   401de621-cc61
Labels:      <none>
Annotations: <none>

Data
====
username:
password:
----
S!B99d$Y2Ksb
devuser
Events:  <none>

Successfully performed 'configmap get configmap-fromliteral' command
```
{: screen}
  
  
### `ibmcloud ce configmap update`  
{: #cli-configmap-update}  

Update a configmap.  
  
```
 ibmcloud ce configmap update --name CONFIGMAP_NAME ((--from-file FILE | --from-file KEY=FILE) | --from-literal KEY=VALUE | --rm KEY)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-f`, `--from-file`</dt>
<dd>Update a configmap from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Update the configmap from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
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
  Updating Configmap configmap-fromliteral...
  OK
  Successfully updated configmap 'configmap-fromliteral'. Run `ibmcloud ce configmap get -n configmap-fromliteral` to see more details.
  ```
  {: screen}
  
- The following example updates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud ce configmap update --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Example output**

  ```
  Updating Configmap configmap-fromfile...
  OK
  Successfully updated configmap 'configmap-fromfile'. Run `ibmcloud ce configmap get -n configmap-fromfile` to see more details.

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
ibmcloud ce configmap delete --name configmap-fromliteral
```
{: pre}

**Example output**

```
Deleting Configmap 'configmap-fromliteral'...

Successfully deleted configmap 'configmap-fromliteral'
```
{: screen}
  
  
### `ibmcloud ce configmap list`  
{: #cli-configmap-list}  

List all configmaps in a project.  
  
```
 ibmcloud ce configmap list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example output**

```
Listing Configmaps...
Name                    Data   Age
configmap-fromfile      2      19m13s
configmap-fromliteral   2      16m12s

Command 'configmap list' performed successfully
```
{: screen}
  
  
## Job commands  
{: #cli-job}  

A job runs your code to complete a task. Jobs are meant to be used for running container images that contain an executable that is designed to run one time and then exit. When you create a job, you can specify workload configuration information that is used each time the job is run. Before you use job commands, you must be targeting a [project](#cli-project).
{: shortdesc}

To see CLI help for the job commands, run `ibmcloud ce job -h`.
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
<dd>The name of the image used for this job. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for runs of the job. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for runs of the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for runs of the job. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for runs of the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. The default value is <code>128Mi</code>.
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
ibmcloud ce job create --image ibmcom/testjob --name hello --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Creating job 'hello'
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
<dd>The name of the job. Use a name that is unique within the project. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce job get --name hello
```
{: pre}

**Example output**

```
Getting job 'hello'...
OK

Name:              hello  
Project:           myproj  
Project ID:        378df04d-37e3-421d-b954-983fe9a1631fgh
Metadata:          
  Creation Timestamp:  2020-09-11 12:51:43 -0500 CDT  
  Generation:          1  
  Resource Version:    351348370  
  Self Link:           /apis/codeengine.cloud.ibm.com/v1beta1/namespaces/378df04d-37e3/jobdefinitions/hello  
  UID:                 37555d75-a93c-40cd-bc80-aa59081fd6f4  
Spec:              
  Array Indices:       0  
  Max Execution Time:  7200  
  Retry Limit:         3  
  Template:            
    Containers:  
      Arguments:              
      Commands:               
      Environment Variables:    
      Image:                  testjob  
      Name:                   hello  
      Resource Requests:      
        Cpu:                1  
        Ephemeral Storage:  500Mi  
        Memory:             128Mi  
Service Bindings:  
```
{: screen}
  
  
### `ibmcloud ce job update`  
{: #cli-job-update}  

Update a job.  
  
```
 ibmcloud ce job update --name JOB_NAME [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for runs of the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices that are used for runs of the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. 
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for runs of the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for runs of the job. This value updates any `--cpu` value that is assigned in the job. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for runs of the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for runs of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for runs of the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for runs of the job. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for runs of the job. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for runs of the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of the job before the job is marked as failed. An array index of a job is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce job update --name hello --cpu 2
```
{: pre}

**Example output**

```
Updating job 'hello'...
OK
```
{: screen}
  
  
### `ibmcloud ce job delete`  
{: #cli-job-delete}  

Delete a job and its associated jobruns.  
  
```
 ibmcloud ce job delete --name JOB_NAME [--force] [--orphan-job-runs]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. Use a name that is unique within the project. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-o`, `--orphan-job-runs`</dt>
<dd>Specify to keep any jobruns that are associated with this job configuration. These orphaned jobruns must then be deleted separately. This value is optional. The default value is <code>false</code>.
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

When you run `ibmcloud ce job delete` to delete a job, all the submitted jobruns that reference this job are also deleted.  
{: important}
  
  
### `ibmcloud ce job list`  
{: #cli-job-list}  

List all jobs in a project.  
  
```
 ibmcloud ce job list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example output**

```
NAME        AGE
hello       5d14h
hello2      5d14h
myjob    5d15h
```
{: screen}
  
  
### `ibmcloud ce job bind`  
{: #cli-job-bind}  

Bind an {{site.data.keyword.cloud_notm}} service to a job.  
  
```
 ibmcloud ce job bind --name JOB_NAME --service-instance SI_NAME [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL] [--wait-timeout WAIT_TIMEOUT]
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
<dt>`-p`, `--prefix`</dt>
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (\_), and cannot start with a number. This value is optional. 
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-sc`, `--service-credential`</dt>
<dd>The name of an existing service credential to use for this service binding. If you do not specify a service instance credential, new credentials are generated during the bind action. This value is optional. 
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the service binding to be ready. If this option is not specified, the binding is performed asynchronously. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

In this example, bind your service instance called `my-object-storage` to your job called `hello`.

```
ibmcloud ce job bind --name hello --service-instance my-object-storage
```
{: pre}

**Example output**

```
Binding service...
Configuring your project for service bindings...
OK
```
{: screen}
  
  
### `ibmcloud ce job unbind`  
{: #cli-job-unbind}  

Unbind {{site.data.keyword.cloud_notm}} services from a job to remove existing service bindings.  
  
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
<dd>Unbinds all service instances for this job. This value is required if `--service-instance` is not specified. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of the service instance to unbind from the job. This value is required if `--all` is not specified. This value is optional. 
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

Use jobrun commands to run instances of your job.
{: shortdesc}

To see CLI help for the job commands, run `ibmcloud ce jobrun -h`.
{: tip}
  
  
### `ibmcloud ce jobrun submit`  
{: #cli-jobrun-submit}  

Submit a jobrun based on a job.  
  
```
 ibmcloud ce jobrun submit (--name JOBRUN_NAME | --job JOB_NAME) [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for this jobrun. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for this jobrun. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for this jobrun. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for this jobrun. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for this jobrun. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for each array index for this jobrun. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for this jobrun. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for this jobrun from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for this jobrun from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage for this jobrun. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this jobrun. The `--name` and the `--image` values are required, if you do not specify the `--job` value. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition. This value is optional. 
</dd>
<dt>`-j`, `--job`</dt>
<dd>The name of the job configuration. View job configurations with the `job list` command. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for this jobrun. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to this jobrun. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. The default value is <code>128Mi</code>.
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name this jobrun. The `--name` and the `--image` values are required, if you do not specify the `--job` value. Use a name that is unique within the project.
<ul>
	<li>  The name must begin with a lowercase letter.</li>
	<li>  The name must end with a lowercase alphanumeric character.</li>
	<li>  The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of this jobrun before the jobrun is marked as failed. An array index of a jobrun is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun submit --name myjobrun --image ibmcom/testjob --array-indices 1-10
```
{: pre}

**Example output**

```
Creating job run 'myjobrun'...
OK
```
{: screen}
  
  
### `ibmcloud ce jobrun get`  
{: #cli-jobrun-get}  

Display the details of a jobrun.  
  
```
 ibmcloud ce jobrun get --name JOBRUN_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the jobrun. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobrun get --name myjobrun  
```
{: pre}

**Example output**

```
Getting job run 'myjobrun'...
OK

Name:               myjobrun
Project:            myproject
Project ID:         b2466a82-6ce6-4012-9d6f-da2352060394
Running Instances:
  Name           Ready  Status     Restarts  Age
  myjobrun-1-0   0/1    Succeeded  0         44s
  myjobrun-10-0  0/1    Succeeded  0         44s
  myjobrun-2-0   0/1    Succeeded  0         44s
  myjobrun-3-0   0/1    Succeeded  0         44s
  myjobrun-4-0   0/1    Succeeded  0         44s
  myjobrun-5-0   0/1    Succeeded  0         44s
  myjobrun-6-0   0/1    Succeeded  0         44s
  myjobrun-7-0   0/1    Succeeded  0         44s
  myjobrun-8-0   0/1    Succeeded  0         44s
  myjobrun-9-0   0/1    Succeeded  0         44s
Metadata:
  Creation Timestamp:  2020-09-09 20:34:35 -0400 EDT
  Generation:          1
  Resource Version:    345829786
  Self Link:           /apis/codeengine.cloud.ibm.com/namespaces/abcdabcd-abcd/jobruns/myjobrun
  UID:                 abcdabcd-abcd-abcd-aaaa-abcdabcdabcd
Spec:
  Job Definition Ref:
  Job Definition Spec:
    Array Indices:       1-10
    Max Execution Time:  7200
    Retry Limit:         3
    Template:
      Containers:
        Arguments:
        Commands:
        Environment Variables:
        Image:                  ibmcom/testjob
        Name:                   myjobrun
        Resource Requests:
          Cpu:                1
          Ephemeral Storage:  500Mi
          Memory:             128Mi
Status:
  Start Time:       2020-09-09 20:34:35 -0400 EDT
  Completion Time:  2020-09-09 20:34:40 -0400 EDT
  Conditions:
    Last Probe Time:       2020-09-09 20:34:35 -0400 EDT
    Last Transition Time:  2020-09-09 20:34:35 -0400 EDT
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-09-09 20:34:38 -0400 EDT
    Last Transition Time:  2020-09-09 20:34:38 -0400 EDT
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-09-09 20:34:40 -0400 EDT
    Last Transition Time:  2020-09-09 20:34:40 -0400 EDT
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Array Indices:       1-10
    Max Execution Time:  7200
    Retry Limit:         3
    Template:
      Containers:
        Arguments:
        Commands:
        Environment Variables:
        Image:                  ibmcom/testjob
        Name:                   myjobrun
        Resource Requests:
          Cpu:                1
          Ephemeral Storage:  500Mi
          Memory:             128Mi
  Instances:
    Failed:     0
    Pending:    0
    Running:    0
    Succeeded:  10
    Unknown:    0
```
{: screen}
  
  
### `ibmcloud ce jobrun resubmit`  
{: #cli-jobrun-resubmit}  

Resubmit a jobrun based on the configuration of a previous jobrun.  
  
```
 ibmcloud ce jobrun resubmit --jobrun REFERENCED_JOBRUN_NAME [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--name NAME] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-j`, `--jobrun`</dt>
<dd>The name of the previous jobrun that this jobrun is based on. This value is required. 
</dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for this jobrun. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for this jobrun. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the array indices that are used for this jobrun. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7-8,10`. The maximum is `999999`. This value is optional. 
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for this jobrun. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for this jobrun. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for each array index for this jobrun. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for this jobrun. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for this jobrun from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for this jobrun from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage for this jobrun. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for this jobrun. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to this jobrun. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of this jobrun. Required if the referenced job does not have a related job configuration. Use a name that is unique within the project.
<ul>
	<li>  The name must begin with a lowercase letter.</li>
	<li>  The name must end with a lowercase alphanumeric character.</li>
	<li>  The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to rerun an instance of this jobrun before the jobrun is marked as failed. An array index of a jobrun is rerun when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

The following example reruns the `myjobrun` job for instances `9-10`. The name of the resubmitted job is `myjobresubmit`. 

```
ibmcloud ce jobrun resubmit --name myjobresubmit --jobrun myjobrun --array-indices 9-10
```
{: pre}

**Example output**

```
Getting job run 'myjobrun'...
Rerunning job run 'myjobresubmit'...
OK
```
{: screen}
  
  
### `ibmcloud ce jobrun delete`  
{: #cli-jobrun-delete}  

Delete a jobrun.  
  
```
 ibmcloud ce jobrun delete --name JOBRUN_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the jobrun to delete. This value is required. 
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

List all jobruns in a project.  
  
```
 ibmcloud ce jobrun list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Name           Age
myjob          19m2s
myjobresubmit  4m1s
myjobrun       16m2s
```
{: screen}

The name of the job listed indicates the name of the job and the current revision of the job.  
{: tip}
  
  
### `ibmcloud ce jobrun logs`  
{: #cli-jobrun-logs}  

Display the logs of a jobrun instance. Use the `jobrun get` command to find the instance name.  
  
```
 ibmcloud ce jobrun logs --instance JOBRUN_INSTANCE
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--instance`</dt>
<dd>The name of the jobrun instance. This value is required. 
</dd>
</dl>  
  
**Example**

Use the `jobrun get` command to obtain the name of the jobrun instances. 
{: tip}

```
ibmcloud ce jobrun logs --instance myjobrun-10-0
```
{: pre}

**Example output**

```
Logging job run instance 'myjobrun-10-0'...
OK

Hello World!
```
{: screen}
  
  
## Secret commands  
{: #cli-secret}  

Work with generic secrets.
{: shortdesc}

To see CLI help for the secret commands, run `ibmcloud ce secret -h`.
{: tip}
  
  
### `ibmcloud ce secret create`  
{: #cli-secret-create}  

Create a generic secret.  
  
```
 ibmcloud ce secret create --name SECRET_NAME (--from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE)
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
<dt>`-f`, `--from-file`</dt>
<dd>Create a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create a generic secret from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce secret get --name mysecret-fromliteral
```
{: pre}

**Example output**

```
Getting secret mysecret-fromliteral...
OK

Name:        mysecret-fromliteral
Project:     myproject
Project ID:  b2466a82-abcd-abcd-abcd-da2352060394
Created:     Wed, 09 Aug 2020 20:09:24 -0400
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
 ibmcloud ce secret update --name SECRET_NAME (--from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE | --rm KEY)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. 
</dd>
<dt>`-f`, `--from-file`</dt>
<dd>Update a generic secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Update a generic secret from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
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
 ibmcloud ce secret list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Work with Git repository access secrets.
{: shortdesc}

To see CLI help for the `repo` command, run `ibmcloud ce repo -h`.
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
<dd>The path to your SSH private key file. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the Git repository access secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-khp`, `--known-hosts-path`</dt>
<dd>The path to your known hosts file. This value is a security feature to ensure that the private key is only used to authenticate at hosts that you previously accessed, specifically, the GitHub or GitLab hosts. You find the value by running `cat ~/.ssh/known_hosts | base64` (OSX) or `cat ~/.ssh/known_hosts | base64 -w 0` (UNIX). This value is optional. 
</dd>
</dl>  
  
**Example**

The following command creates a Git access secret called `github` for host `github.com` and authenticates with an ssh key located at `/<filepath>/.ssh/id_rsa`, where `<filepath>` is the path on your system.

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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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
Project ID:  858ef04d-36e3-421c-a094-985ce9a1532c  
Created:     Fri, 11 Sep 2020 15:11:54 -0500  
Host:        github.com  
Data:          
---
ssh-privatekey: LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQ21GbGN6STFOaTFqZEhJQUFBQUdZbU55ZVhCME
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
 ibmcloud ce repo list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Work with image registry access secrets.
{: shortdesc}

To see CLI help for the application command, run `ibmcloud ce registry -h`.
{: tip}
  
  
### `ibmcloud ce registry create`  
{: #cli-registry-create}  

Create an image registry access secret.  
  
```
 ibmcloud ce registry create --name NAME --server SERVER --username USERNAME (--password PASSWORD | --password-from-file PASSWORD_FILE) [--email EMAIL]
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
<dt>`-s`, `--server`</dt>
<dd>The URL of the registry server. This value is required. 
</dd>
<dt>`-u`, `--username`</dt>
<dd>The username to access the registry server. This value is required. 
</dd>
<dt>`-e`, `--email`</dt>
<dd>The email address to access the registry server. This value is optional. 
</dd>
<dt>`-p`, `--password`</dt>
<dd>The password to access the registry server. This value is optional. 
</dd>
<dt>`-pf`, `--password-from-file`</dt>
<dd>The path to a file containing the password to access the registry server. This value is optional. 
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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
 ibmcloud ce registry list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

The `buildrun` commands submit build runs based on a configuration file. Before you use build commands, you must be targeting a [project](#cli-project). You can use a build definition as a template for your build, or you can set build parameters with the build run command. Use build commands to run, display details, and delete builds. 
{: shortdesc}

You can use either `buildrun` or `br` in your build commands. To see CLI help for the build command, run `ibmcloud ce br`.
{: tip}
  
  
### `ibmcloud ce build create`  
{: #cli-build-create}  

Create a build.  
  
```
 ibmcloud ce build create --name BUILD_NAME --image IMAGE_REF --source SOURCE --registry-secret REGISTRY_REF [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--repo REPO] [--revision REVISION] [--size SIZE] [--strategy STRATEGY] [--timeout TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The location where the image can be pushed. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. This value is required. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The image registry access secret that is used to access the registry. You can add the image registry access secret by running the `registry create` command. This value is required. 
</dd>
<dt>`-src`, `--source`</dt>
<dd>The Git repository hostname that contains your source code; for example `github.com`. This value is required. 
</dd>
<dt>`-cdr`, `--context-dir`</dt>
<dd>The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. 
</dd>
<dt>`-df`, `--dockerfile`</dt>
<dd>The name of the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is optional. The default value is <code>Dockerfile</code>.
</dd>
<dt>`-r`, `--repo`</dt>
<dd>The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. This value is optional. 
</dd>
<dt>`-rv`, `--revision`</dt>
<dd>Specify which branch or commit in the source repository to pull from. This value is optional. 
</dd>
<dt>`-sz`, `--size`</dt>
<dd>The size for the build, which determines the amount of resources used. Valid options are `small`, `medium`, `large`, `xlarge`. This value is optional. The default value is <code>medium</code>.
</dd>
<dt>`-str`, `--strategy`</dt>
<dd>The strategy to use for building the image. Valid options are `kaniko` and `buildpacks`. This value is optional. The default value is <code>kaniko</code>.
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build must succeed or fail. This value is optional. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

The following example creates a build configuration file called `helloworld-build` from a source Dockerfile (`kaniko`), `medium` size, and located in `https://github.com/IBM/CodeEngine` inside the `hello` directory in the `master` branch.  When this build is submitted, the built image container will be stored in a {{site.data.keyword.registryshort}} instance at `us.icr.io/mynamespace/codeengine-helloworld` that is accessed by using a image registry secret called `myregistry`.

```
ibmcloud ce build create --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --revision master --strategy kaniko --size medium --image us.icr.io/mynamespace/codeengine-helloworld --registry-secret myregistry
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Name:    helloworld-build  
Status:  Succeeded  
Spec:    
  Image:              us.icr.io/mynamespace/codeengine/helloworld 
  Registry Secret:    myregistry  
  Build Strategy:     kaniko-medium  
  Timeout:            10m0s  
  Source:             https://github.com/IBM/CodeEngine  
  Revision:           master  
  Context Directory:  /hello  
  Dockerfile:         Dockerfile  
Buildruns:  
  Name        Status     Age  
  mybuildrun  Succeeded  3m27s  
```
{: screen}
  
  
### `ibmcloud ce build update`  
{: #cli-build-update}  

Update a build.  
  
```
 ibmcloud ce build update --name BUILD_NAME [--context-dir CONTEXT_DIR] [--dockerfile DOCKERFILE] [--image IMAGE] [--registry-secret REGISTRY_SECRET] [--repo REPO] [--revision REVISION] [--source SOURCE] [--timeout TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the build. This value is required. 
</dd>
<dt>`-cdr`, `--context-dir`</dt>
<dd>The directory in the repository that contains the buildpacks file or the Dockerfile. This value is optional. 
</dd>
<dt>`-df`, `--dockerfile`</dt>
<dd>The name of the Dockerfile. Specify this option only if the name is other than `Dockerfile`. This value is optional. The default value is <code>Dockerfile</code>.
</dd>
<dt>`-i`, `--image`</dt>
<dd>The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--repo`</dt>
<dd>The name of the Git repository access secret to access the private repository. This repository contains the source code to build your container image. To create this access secret, use the `repo create` command. This value is optional. 
</dd>
<dt>`-rv`, `--revision`</dt>
<dd>Specify which branch or commit in the source repository to pull from. This value is optional. 
</dd>
<dt>`-src`, `--source`</dt>
<dd>The Git repository hostname that contains your source code; for example `github.com`. This value is optional. 
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build must succeed or fail. This value is optional. The default value is <code>600</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce build update --name helloworld-build --source https://github.com/IBM/CodeEngine  --context-dir /hello --revision master --timeout 900
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
 ibmcloud ce build list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

{[cli-buildrun-commands-docdesc.md]}  
  
### `ibmcloud ce buildrun submit`  
{: #cli-buildrun-submit}  

Submit a build run.  
  
```
 ibmcloud ce buildrun submit --name BUILDRUN_NAME --build BUILD_NAME [--image IMAGE] [--timeout TIMEOUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-bd`, `--build`</dt>
<dd>The name of the build configuration to use. This value is required. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The location of the image registry. The format of the location must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the build run. Use a name that is unique within the project. This value is optional. 
</dd>
<dt>`-to`, `--timeout`</dt>
<dd>The amount of time, in seconds, that can pass before the build run must succeed or fail. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

The following command submits a build run called `mybuildrun` and uses the build configuration file called `hellworld-build`.

```
ibmcloud ce buildrun submit --name mybuildrun --build helloworld-build
```
{: pre}

**Example output**

```
Submitting build run 'mybuildrun'...
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
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
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

Metadata:  
  Creation Timestamp:  2020-09-11 16:11:05 -0500 CDT  
  Generation:          1  
  Resource Version:    351833286  
  Self Link:           /apis/build.dev/v1alpha1/namespaces/358ee96d-37f3/buildruns/mybuildrun  
  UID:                 2e393ea2-b6b8-4d90-b225-a1ad3d566562  
Status:  
  Reason:      Succeeded  
  Registered:  True  
Instances:  
  Name                        Ready  Status  Restarts  Age  
  mybuildrun-rvdjv-pod-dbh2f  0/0            0         6m36s   
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
 ibmcloud ce buildrun list [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example output**

```
Listing builds...
OK

Name                                     Succeeded  BuildDef Name                  Age  
codeengine-app-72-build-tmnz2-run-xdd98  True       codeengine-app-72-build-tmnz2  6h59m  
mybuildrun                               True       helloworld-build               9m28s  
```
{: screen}
  
  
### `ibmcloud ce buildrun logs`  
{: #cli-buildrun-logs}  

Display the logs of a build run instance. Use the `buildrun get` command to find the instance name.  
  
```
 ibmcloud ce buildrun logs --instance BUILDRUN_INSTANCE
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--instance`</dt>
<dd>The name of the build run instance. This value is required. 
</dd>
</dl>  
  
**Example**

You can find the buildrun instance name by running `ibmcloud ce buildrun get` command.

```
ibmcloud ce buildrun logs --instance mybuildrun-rvdjv-pod-dbh2f
```
{: pre}

**Example output**

```
Logging build run instance 'mybuildrun-rvdjv-pod-dbh2f'...
OK

{"level":"info","ts":1599858676.9746084,"caller":"git/git.go:139","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 9540bad5ba01b94b820339640987f3059e93ae9b (grafted, HEAD, origin/master) in path /workspace/source"}
{"level":"info","ts":1599858677.7159889,"caller":"git/git.go:180","msg":"Successfully initialized and updated submodules in path /workspace/source"}
INFO[0003] Retrieving image manifest node:12-alpine     
INFO[0004] Retrieving image manifest node:12-alpine     
INFO[0005] Built cross stage deps: map[]                
INFO[0005] Retrieving image manifest node:12-alpine     
INFO[0005] Retrieving image manifest node:12-alpine     
INFO[0006] Executing 0 build triggers                   
INFO[0006] Unpacking rootfs as cmd RUN npm install requires it. 
INFO[0011] RUN npm install                              
INFO[0011] Taking snapshot of full filesystem...        
INFO[0012] cmd: /bin/sh                                 
INFO[0012] args: [-c npm install]                       
INFO[0012] Running: [/bin/sh -c npm install]            
npm WARN saveError ENOENT: no such file or directory, open '/package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open '/package.json'
npm WARN !invalid#2 No description
npm WARN !invalid#2 No repository field.
npm WARN !invalid#2 No README data
npm WARN !invalid#2 No license field.

up to date in 0.506s
found 0 vulnerabilities

INFO[0013] Taking snapshot of full filesystem...        
INFO[0013] COPY hello.js .                              
INFO[0013] Taking snapshot of files...                  
INFO[0013] EXPOSE 8080                                  
INFO[0013] cmd: EXPOSE                                  
INFO[0013] Adding exposed port: 8080/tcp                
INFO[0013] CMD [ "node", "hello.js" ]                   
{"level":"info","ts":1599858699.613167,"logger":"fallback-logger","caller":"imagedigestexporter/main.go:59","msg":"No index.json found for: image","commit":"3e43a06"}
```
{: screen}
  
  
