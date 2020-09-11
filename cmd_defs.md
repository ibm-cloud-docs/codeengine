---

copyright:
  years: 2020
lastupdated: "2020-09-11"

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
 ibmcloud ce project create --name PROJECT_NAME [--tag TAG] [--target]
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
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource. The label must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. Specify one label per `--tag` flag; for example, `--tag tagA --tag tagB`. This value is optional. 
</dd>
<dt>`-tg`, `--target`</dt>
<dd>Target the project after this project is created. This value is optional. The default value is <code>false</code>.
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
  
  
### `ibmcloud ce project target`  
{: #cli-project-target}  

Target a project for context.  
  
```
 ibmcloud ce project target --name PROJECT_NAME [--kubecfg]
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
ibmcloud ce project target --name myproject
```
{: pre}

**Example output**

```
Targeting project 'myproject'...
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

**Example**

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
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The target number of requests to be processed concurrently per instance. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0.1</code>.
</dd>
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
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. This value is optional. 
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
<dd>The length of time in seconds to wait for the application to start. This value is ignored when `no-wait` is specified. This value is optional. The default value is <code>300</code>.
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
 ibmcloud ce application get --name APPLICATION_NAME [--more-details] [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-md`, `--more-details`</dt>
<dd>Use this option to see more details about the application and associated parameters. This value is optional. The default value is <code>false</code>.
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
 ibmcloud ce application update --name APP_NAME [--argument ARGUMENT] [--cluster-local] [--command COMMAND] [--concurrency CONCURRENCY] [--concurrency-target CONCURRENCY_TARGET] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--image IMAGE] [--max-scale MAX_SCALE] [--memory MEMORY] [--min-scale MIN_SCALE] [--port PORT] [--quiet] [--registry-secret REGISTRY_SECRET] [--timeout TIMEOUT] [--user USER]
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
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the application. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The maximum number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-ct`, `--concurrency-target`</dt>
<dd>The target number of requests to be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0</code>.
</dd>
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
<dd>The port where the application listens. The format is `[NAME:]PORT`, where `[NAME:]` is optional. If `[NAME:]` is specified, valid values are `h2c`, or `http1`. When `[NAME:]` is not specified or is `http1`, the port uses HTTP/1.1. When `[NAME:]` is `h2c`, the port uses unencrypted HTTP/2. This value is optional. 
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
 ibmcloud ce application bind --name APP_NAME --service-instance SI_NAME [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL]
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

Display the logs of an application instance.  
  
```
 ibmcloud ce application logs --instance APP_INSTANCE
```
{: pre}

**Command Options**  
<dl>
<dt>`--instance`</dt>
<dd>The name of the application instance. This value is required. </dd>
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
  
  
## Jobdef commands  
{: #cli-jobdef}  

Before you use job definition commands, you must be targeting a [project](#cli-project). A job definition is a template that contains workload configuration information that is used to run [jobs](#cli-job-run). After you create a job definition, one or more jobs can be submitted based on the job definition, optionally overwriting values of the job definition. Use job definition commands to create, display details, update, and delete jobs.
{: shortdesc}

You can use either `jobdef` or `jd` in your job definition commands. To see CLI help for the job definition command, run `ibmcloud ce jd`.
{: tip}
  
  
### `ibmcloud ce jobdef create`  
{: #cli-jobdef-create}  

Create a job definition.  
  
```
 ibmcloud ce jobdef create --name JOBDEF_NAME --image IMAGE_REF [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job definition. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for instances of the job definition. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for instances of the job definition. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9`, `1-5,7-8,10`, or `"1 - 10"`. The maximum is `9999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for instances of the job definition. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for instances of the job definition. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for the instance of the job definition. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for instances of the job definition. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for instances of the job definition from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run that uses this job definition. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for instances of the job definition from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run that uses this job definition. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for instances of the job definition. Use 'Mi' for mebibytes or 'Gi' for gibibytes. This value is optional. The default value is <code>500Mi</code>.
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for the job. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the job definition. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional. The default value is <code>128Mi</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
</dd>
</dl>  
  
**Example**

The following example uses the container image `busybox` and uses the arguments `/bin/sh -c echo Hello $JOB_INDEX ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3`, assigning 128 MB as memory and 1 CPU to the container.

```
ibmcloud ce jobdef create --image busybox --name hello --argument /bin/sh --argument "-c" --argument "echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3" -e "ENV1=env1 from jobdef" -e "ENV2=env2 from jobdef" -e "ENV3=env3 from jobdef" --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Created successfully Job Definition 'hello'
```
{: screen}
  
  
### `ibmcloud ce jobdef get`  
{: #cli-jobdef-get}  

Display the details of a job definition.  
  
```
 ibmcloud ce jobdef get --name JOBDEF_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project. This value is required. 
</dd>
<dt>`-o`, `--output`</dt>
<dd>Specifies the format of the command output. Valid options are `json`, `yaml`, `jsonpath=JSONPATH_EXPRESSION`, and `jsonpath-as-json=JSONPATH_EXPRESSION`. Use `jsonpath` to specify the path to an element of the JSON output. This value is optional. 
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobdef get --name myjobdef
```
{: pre}

**Example output**

```
Getting job definition 'myjobdef'...
Name:         myjobdef
Namespace:    70427b7b-fa35
Metadata:
  Creation Timestamp  2020-07-21 12:31:43 -0400 EDT
  Generation:         1
  Resource Version:   232453744
  Self Link:          /apis/codeengine.cloud.ibm.com/v1alpha1/namespaces/70427b7b-fa35/jobdefinitions/myjobdef
  UID:                252ec46e-20d1-4946-ae4a-276e0957c6cb
Spec:
  Containers:
    Image:   ibmcom/testjob
    Name:    myjobdef
    Command:
    Argument:
    Resources:
      Requests:
        Cpu:     1
        Memory:  128Mi
OK
Command 'jobdef get' performed successfully
```
{: screen}
  
  
### `ibmcloud ce jobdef update`  
{: #cli-jobdef-update}  

Update a job definition.  
  
```
 ibmcloud ce jobdef update --name JOBDEF_NAME [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-configmap-rm ENV_FROM_CONFIGMAP_RM] [--env-from-secret ENV_FROM_SECRET] [--env-from-secret-rm ENV_FROM_SECRET_RM] [--env-rm ENV_RM] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for instances of the job definition. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for instances of the job definition. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9`, `1-5,7-8,10`, or `"1 - 10"`. The maximum is `9999`. This value is optional. 
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for instances of the job definition. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for instances of the job definition. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for the instance of the job definition. This value updates any `--cpu` value that is assigned in the job definition. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables for instances of the job definition. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for instances of the job definition from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run that uses this job definition. This value is optional. 
</dd>
<dt>`-env-cm-rm`, `--env-from-configmap-rm`</dt>
<dd>Remove environment variable references to full configmaps using the configmap name. To remove individual key references to configmaps, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for instances of the job definition from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run that uses this job definition. This value is optional. 
</dd>
<dt>`-env-sec-rm`, `--env-from-secret-rm`</dt>
<dd>Remove environment variable references to full secrets using the secret name. To remove individual key references to secrets, use the `--env-rm` option. This value is optional. 
</dd>
<dt>`--env-rm`</dt>
<dd>Remove environment variable references to the key of a key-value pair in a configmap or secret. To remove individual key references and literal values, specify the name of the key. This value is optional. </dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>The amount of ephemeral storage to set for instances of the job definition. Use 'Mi' for mebibytes or 'Gi' for gibibytes. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job definition. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for the job. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for the job definition. Use `Mi` for mebibytes or `Gi` for gibibytes. This value updates any `--memory` value that is assigned in the job definition. This value is optional. 
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image registry access secret. The image registry access secret is used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobdef update --name myjobdef --cpu 2
```
{: pre}

**Example output**

```
Successfully updated job definition 'myjobdef'
```
{: screen}
  
  
### `ibmcloud ce jobdef delete`  
{: #cli-jobdef-delete}  

Delete a job definition.  
  
```
 ibmcloud ce jobdef delete --name JOBDEF_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>false</code>.
</dd>
</dl>  
  
**Example**

```
ibmcloud ce jobdef delete --name myjobdef
```
{: pre}

**Example output**

```
Deleted JobDefinition 'myjobdef'
```
{: screen}
  
  
### `ibmcloud ce jobdef list`  
{: #cli-jobdef-list}  

List all job definitions in a project.  
  
```
 ibmcloud ce jobdef list [--output OUTPUT]
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
myjobdef    5d15h
```
{: screen}
  
  
### `ibmcloud ce jobdef bind`  
{: #cli-jobdef-bind}  

Bind an {{site.data.keyword.cloud_notm}} service to a job definition.  
  
```
 ibmcloud ce jobdef bind --name JOBDEF_NAME --service-instance SI_NAME [--prefix PREFIX] [--quiet] [--service-credential SERVICE_CREDENTIAL]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition to bind. This value is required. 
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of an existing {{site.data.keyword.cloud_notm}} service instance to bind to the job definition. This value is required. 
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
</dl>  
  
**Example**

In this example, bind your service instance called `my-object-storage` to your job definition called `myjobdef`.

```
ibmcloud ce jobdef bind --name myjobdef --service-instance my-object-storage
```
{: pre}

**Example output**

```
Binding service...
Successfully created service binding for 'my-object-storage'
```
{: screen}
  
  
### `ibmcloud ce jobdef unbind`  
{: #cli-jobdef-unbind}  

Unbind {{site.data.keyword.cloud_notm}} services from a job definition to remove existing service bindings from the job definition.  
  
```
 ibmcloud ce jobdef unbind --name JOBDEF_NAME (--service-instance SERVICE_INSTANCE_NAME | --all) [--quiet]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required. 
</dd>
<dt>`-A`, `--all`</dt>
<dd>Unbinds all service instances for this job definition. This value is required if `--service-instance` is not specified. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-si`, `--service-instance`</dt>
<dd>The name of the service instance to unbind from the job definition. This value is required if `--all` is not specified. This value is optional. 
</dd>
</dl>  
  
**Example**

In this example, remove all bindings from your job definition called `myjobdef`.

```
ibmcloud ce jobdef unbind --name myjobdef --all
```
{: pre}

**Example output**

```
Removing service bindings...
Successfully removed service bindings
OK
```
{: screen}
  
  
## Jobrun commands  
{: #cli-jobrun}  

A job runs your code to complete a task. Jobs are meant to be used for running container images that contain an executable that is designed to run one time and then exit. When you create a job, you can specify workload configuration information that is used each time the job is run. Before you use job commands, you must be targeting a [project](#cli-project).
{: shortdesc}

To see CLI help for the job commands, run `ibmcloud ce job -h`.
{: tip}
  
  
### `ibmcloud ce jobrun submit`  
{: #cli-jobrun-submit}  

Run a job based on a job definition. You can use either `job run` or `job create` to run this command.  
  
```
 ibmcloud ce jobrun submit (--name JOBRUN_NAME | --jobdef JOBDEF_NAME) [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--image IMAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--registry-secret REGISTRY_SECRET] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified in the job definition. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified in the job definition. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9`, `1-5,7-8,10`, or `"1 - 10"`. The maximum is `9999`. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the job that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for instances of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for instances of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>☞☞☞☞ MISSING DOC DESCRIPTION ☜☜☜☜ This value is optional. The default value is <code>500Mi</code>.
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. For images in Docker Hub, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition. This value is optional. 
</dd>
<dt>`-jd`, `--jobdef`</dt>
<dd>The name of the job definition that contains the description of the job to be run. This value is required if you do not specify the `--name` and `image` values. This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for the job. This value is optional. The default value is <code>7200</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value overrides any `--memory` value that is assigned in the job definition. This value is optional. The default value is <code>128Mi</code>.
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. Use a name that is unique within the project.
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
<dd>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
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

Display the details of a job.  
  
```
 ibmcloud ce jobrun get --name JOBRUN_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
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

Rerun a job based on the configuration of a previous job run.  
  
```
 ibmcloud ce jobrun resubmit --jobrun REFERENCED_JOBRUN_NAME [--argument ARGUMENT] [--array-indices ARRAY_INDICES] [--command COMMAND] [--cpu CPU] [--env ENV] [--env-from-configmap ENV_FROM_CONFIGMAP] [--env-from-secret ENV_FROM_SECRET] [--ephemeral-storage EPHEMERAL_STORAGE] [--maxexecutiontime MAXEXECUTIONTIME] [--memory MEMORY] [--name NAME] [--retrylimit RETRYLIMIT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-j`, `--jobrun`</dt>
<dd>☞☞☞☞ MISSING DOC DESCRIPTION ☜☜☜☜ This value is required. 
</dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified in the job definition. This value is optional. 
</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the job. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified in the job definition. This value is optional. 
</dd>
<dt>`-ai`, `--array-indices`</dt>
<dd>Specifies the indices of the instances that are used to run the job. Specify the list or range of indices that are separated by hyphens (-) or commas (,); for example, `1,3,6,9` or `1-5,7 - 8,10`. The maximum is `9999`. This value is optional. 
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the job. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the job that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. This value is optional. The default value is <code>0</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the job. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for instances of the job from the key-value pairs that are stored in this configmap. To reference the full configmap, specify the name of the configmap. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `key1` in a configmap that is named `configmapName`, use the value `configmapName:key1`. To add environment variables for all keys in a configmap that is named `configmapName`, use the value `configmapName`. Keys added to a configmap with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for instances of the job from the key-value pairs that are stored in this secret. To reference the full secret, specify the name of the secret. To reference individuals keys, use the format `NAME:KEY_A,KEY_B`. For example, to add an environment variable for a single key `password` in a secret that is named `secretName`, use the value `secretName:password`. To add environment variables for all keys in a secret that is named `secretName`, use the value `secretName`. Keys that are added to a secret with a full reference display as environment variables when a new job is run. This value is optional. 
</dd>
<dt>`-es`, `--ephemeral-storage`</dt>
<dd>☞☞☞☞ MISSING DOC DESCRIPTION ☜☜☜☜ This value is optional. 
</dd>
<dt>`-met`, `--maxexecutiontime`</dt>
<dd>The maximum execution time in seconds for the job. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory to assign to the job. Use `Mi` for mebibytes or `Gi` for gibibytes. This value overrides any `--memory` value that is assigned in the job definition. This value is optional. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. Required if referenced job does not have a related job definition. Use a name that is unique within the project.
<ul>
	<li>  The name must begin with a lowercase letter.</li>
	<li>  The name must end with a lowercase alphanumeric character.</li>
	<li>  The name must be 53 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is <code>0</code>.
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

Delete a job.  
  
```
 ibmcloud ce jobrun delete --name JOBRUN_NAME [--force]
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

List all running jobs in a project.  
  
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

Display the logs of a job instance.  
  
```
 ibmcloud ce jobrun logs --instance JOBRUN_INSTANCE
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--instance`</dt>
<dd>☞☞☞☞ MISSING DOC DESCRIPTION ☜☜☜☜ This value is required. 
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

Work with secrets.
{: shortdesc}

To see CLI help for the secret commands, run `ibmcloud ce secret -h`.
{: tip}
  
  
### `ibmcloud ce secret create`  
{: #cli-secret-create}  

Create a secret.  
  
```
 ibmcloud ce secret create --name SECRET_NAME (--from-file FILE | --from-file KEY=FILE | --from-literal KEY=VALUE)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-f`, `--from-file`</dt>
<dd>Create a secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create a secret from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
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

Display the details of a secret.  
  
```
 ibmcloud ce secret get --name SECRET_NAME [--output OUTPUT]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. 
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

Update a secret.  
  
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
<dd>Update a secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Update a secret from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
</dd>
<dt>`--rm`</dt>
<dd>Remove an individual key-value pair in a secret by specifying the name of the key. This value is optional. </dd>
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

Delete a secret.  
  
```
 ibmcloud ce secret delete --name SECRET_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. 
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

List all secrets in a project.  
  
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

Work with repositories.  
  
### `ibmcloud ce repo create`  
{: #cli-repo-create}  

Create a Git access secret.  
  
```
 ibmcloud ce repo create --name SECRET_NAME --key-path SSH_KEY_PATH --host HOST_ADDRESS [--known-hosts-path KNOWN_HOSTS_PATH]
```
{: pre}

**Command Options**  
<dl>
<dt>`-ho`, `--host`</dt>
<dd>The address of the host; for example `github.com`. This value is required. 
</dd>
<dt>`-fp`, `--key-path`</dt>
<dd>The path to your SSH key file. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin and end with a lowercase alphanumeric character.</li>
	<li>The name must be 253 characters or fewer and can contain lowercase letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-khp`, `--known-hosts-path`</dt>
<dd>The path to your known hosts file. This value is optional. 
</dd>
</dl>  
  
**FIX FIX FIX FIX MUST UPDATE**

**Example**

```
ibmcloud ce command usage   
```
{: pre}

**Example output**

```
Creating project 'myproject'...
Successfully created project 'myproject'
```
{: screen}
  
  
## Registry commands  
{: #cli-registry}  

Work with image registry access secrets.  
  
### `ibmcloud ce registry create`  
{: #cli-registry-create}  

Create an image registry access secret.  
  
```
 ibmcloud ce registry create --name NAME --server SERVER --username USERNAME --password PASSWORD [--email EMAIL]
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
<dt>`-p`, `--password`</dt>
<dd>The password to access the registry server. This value is required. 
</dd>
<dt>`-s`, `--server`</dt>
<dd>The URL of the registry server. This value is required. 
</dd>
<dt>`-u`, `--username`</dt>
<dd>The username to access the registry server. This value is required. 
</dd>
<dt>`-e`, `--email`</dt>
<dd>The email address to access the registry server. This value is optional. 
</dd>
</dl>  
  
**Example**

The following example creates registry access to a {{site.data.keyword.registryshort}} instance called `myregistry` that is located at `us.icr.io` and where password is your API key.:
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
  
  
  

