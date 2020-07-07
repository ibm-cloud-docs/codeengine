---

copyright:
  years: 2020
lastupdated: "2020-07-07"

keywords: knative

subcollection: code-engine

---

{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:pre: .pre}  
{:table: .aria-labeledby="caption"}  
{:external: target="_blank" .external}  
{:codeblock: .codeblock}  
{:tip: .tip}  
{:note: .note}  
{:important: .important}  
{:deprecated: .deprecated}  
{:download: .download}  
{:gif: data-image-type='gif'}  


# Project {{site.data.keyword.codeengineshort}} CLI TEST 6
{: #kn-cli-test}  

Run these commands to manage the entities that make up Project {{site.data.keyword.codeengineshort}} (or "{{site.data.keyword.codeengineshort}}").  
{: shortdesc}  
  
## Project commands  
{: #cli-project}  

A project is a container for components, such as applications and job definitions. By using projects, you can manage resources and provide access to components in the project. Use project commands to create, display details, and delete projects.
{: shortdesc}

You can use either `project` or `proj` in your project commands. To see CLI help for the project command, run `ibmcloud coligo proj`.  
{: tip}


### `ibmcloud coligo project create`  
{: #cli-project-create}  

Create a project.
{: shortdesc}

```
 ibmcloud coligo project create --name PROJECT_NAME [--tag TAG] [--target]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. Use a name that is unique to your region. The name must be 128 characters or fewer and can contain:
<ul>
	<li>Any Unicode character</li>
	<li>Only these special characters: spaces ( ), periods (.), colons (:), underscores (_), and hyphens (-)</li>
</ul>
This value is required. </dd>
<dt>`--json`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is optional. The default value is <code>false</code>.</dd>
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource. The label must start with a letter, can contain letters, numbers, and hyphen (`-`), and must be 35 characters or fewer. Use a name that is unique across regions. Specify one label per `--tag` flag; for example, `--tag tagA --tag tagB`. This value is optional. 
</dd>
<dt>`-tg`, `--target`</dt>
<dd>Target the project after this project is created. This value is optional. The default value is <code>false</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo project create --name myproject  
```
{: pre}

**Example output**

```
Successfully created project myproject
```
{: screen}
  


### `ibmcloud coligo project delete`  
{: #cli-project-delete}  

Delete a project.
{: shortdesc}

```
 ibmcloud coligo project delete --name PROJECT_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`--guid`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is optional.</dd>
</dl>

**Example**

```
ibmcloud coligo project delete --name myproject
```
{: pre}

**Example output**

```
Deleted project myproject
```
{: screen}
  


### `ibmcloud coligo project list`  
{: #cli-project-list}  

List all projects.
{: shortdesc}

```
 ibmcloud coligo project list
```
{: pre}

**Example output**

```
Name            ID                                    Status         Tags   Location   Resource Group
myproject       42642513-8805-4da8-8dbf-bc4f409g9089   active               us-south   Default
new_proj        d294c0a3-30d8-49bc-b070-1921692f41d4   active               us-south   Default

Command 'project list' performed successfully
```
{: screen}
  


### `ibmcloud coligo project get`  
{: #cli-project-get}  

Display the details of a single project.
{: shortdesc}

```
 ibmcloud coligo project get --name PROJECT_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. 
</dd>
</dl>

**Example**

```
ibmcloud coligo project get --name myproject
```
{: pre}

**Example output**

```
Getting project 'myproject'...

Name: myproject
ID: 42642513-8805-4da8-8dbf-bc4f409g9089
Status: active
Tags: []
Location: us-south
Resource Group: Default
Created: Tue, 28 Apr 2020 09:27:22 -0400
Updated: Tue, 28 Apr 2020 09:27:57 -0400

Command 'project get' performed successfully
```
{: screen}
  


### `ibmcloud coligo project current`  
{: #cli-project-current}  

Display the details of the project that is currently targeted.
{: shortdesc}

```
 ibmcloud coligo project current
```
{: pre}

**Example output**

```
Getting current project...
Region:         myproject
Region:         us-south
export KUBECONFIG=/user/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-ae4f409f8054.yaml
```
{: screen}
  


## Target command  
{: #cli-target}  

Target a project for context.
{: shortdesc}


### `ibmcloud coligo target`  
{: #cli-targetcmd}  

Target a project for context.
{: shortdesc}

```
 ibmcloud coligo target --name PROJECT_NAME [--project-api API_URL]
```
{: pre}

**Example**

```
ibmcloud coligo target --name myproject
```
{: pre}

**Example output**

```
Now targeting environment 'myproject' (42642513-8805-4da8-8dbf-bc4f409g9089). Set the KUBECONFIG environment variable to use kubectl with your project:
export KUBECONFIG=/user/myusername/.bluemix/plugins/coligo/myproject-42642513-8805-4da8-8dbf-bc4f409g9089.yaml
```
{: screen}
  


## Application commands  
{: #cli-application}  

Before you use application commands, you must be targeting a [project](#cli-project).  An application runs your code to serve HTTP requests. The application has a URL for incoming requests. Use application commands to create, display details, update, and delete applications.
{: shortdesc}

You can use either `application` or `app` in your application commands. To see CLI help for the application command, run `ibmcloud coligo app`.  
{: tip}


### `ibmcloud coligo application create`  
{: #cli-application-create}  

Create an application.
{: shortdesc}

```
 ibmcloud coligo application create --image IMAGE_REF --name APP_NAME [--registry-secret SECRET_NAME] [--cpu CPU] [--memory MEMORY] [--timeout TIME] [--concurrency CONCURRENCY] [--min-scale MIN_INSTANCES] [--max-scale MAX_INSTANCES] [--command COMMAND] [--argument ARGUMENT] [--env KEYS_VALUE] [--env-from-secret SECRET_KEY] [--env-from-configmap CONFIGMAP_KEY] [--wait-timeout TIME] [--quiet] [--no-wait] [--cluster-local]
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
<dd>Set arguments for the container. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified within the container image. This value is optional. 
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the container. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0.1</code>.
</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the container. Must be in `NAME=VALUE` format. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this configmap. For example, a configmap that contains `configmapName:value` results in an environment variable called `configmapName` that is set to `value`. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this secret. For example, a secret that contains `secretName:value` results in an environment variable called `secretName` that is set to `value`. This value is optional. 
</dd>
<dt>`-max`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>10</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `M` for mebibytes or `G` for gibibytes. This value is optional. The default value is <code>1024M</code>.
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
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image pull secret. Pull secrets are used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time in seconds that can pass before the application must succeed or fail. This value is optional. The default value is <code>300</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to start. This value is ignored when `no-wait` is specified. This value is optional. The default value is <code>300</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo application create --name myapp --image ibmcom/helloworld 
```
{: pre}

**Example output**

```
Creating Application 'myapp'...
Successfully created application 'myapp' created. 
Run `ibmcloud coligo application get -n 'myapp'` to check the application status.
```
{: screen}

When you run `ibmcloud coligo application get -n 'myapp'` to check the application status, the URL for your application is displayed.  
{: tip}
  


### `ibmcloud coligo application get`  
{: #cli-application-get}  

Display the details of an application.
{: shortdesc}

```
 ibmcloud coligo application get --name APPLICATION_NAME [--more-details]
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
</dl>

**Example**

```
ibmcloud coligo application get --name myapp
```
{: pre}

**Example output**

```
Name:       myapp
Namespace:  b49ca89f-g99q
Age:        19h
URL:        http://myapp.b49ca89f-g99q.us-south.knative.test.appdomain.cloud

Revisions:
  100%  @latest (myapp-zxxlr-1) [1] (19h)
        Image:  ibmcom/helloworld (pinned to be18cb)

Conditions:
  OK TYPE                   AGE REASON
  ++ Ready                  19h
  ++ ConfigurationsReady    19h
  ++ RoutesReady            19h

Command 'application get' performed successfully
```
{: screen}
  


### `ibmcloud coligo application update`  
{: #cli-application-update}  

Update an application. Updating your application creates a revision. When calls are made to the application, traffic is routed to the revision.
{: shortdesc}

```
 ibmcloud coligo application update --name APP_NAME [ --image IMAGE_REF] [--registry-secret SECRET_NAME] [--cpu CPU] [--memory MEMORY] [--timeout TIME] [--concurrency CONCURRENCY] [--min-scale MIN_INSTANCES] [--max-scale MAX_INSTANCES] [--command COMMAND] [--argument ARGUMENT] [--env KEY=VALUE] [--env-from-secret SECRET_KEY] [--env-from-configmap CONFIGMAP_KEY]  [--quiet] [--cluster-local]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-arg`, `--argument`</dt>
<dd>Set arguments for the container. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. The application has no exposure to external traffic. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-cmd`, `--command`</dt>
<dd>Set commands for the container. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`-cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently per instance. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the container. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this configmap. For example, a configmap that contains `configmapName:value` results in an environment variable called `configmapName` that is set to `value`. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this secret. For example, a secret that contains `secretName:value` results in an environment variable called `secretName` that is set to `value`. This value is optional. 
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value is optional. 
</dd>
</dl>
<dl>
<dt>`-max`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `M` for mebibytes or `G` for gibibytes. This value is optional. 
</dd>
<dt>`-min`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This value is optional. The default value is <code>0</code>.
</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. This value is optional. The default value is <code>false</code>.
</dd>
<dt>`-rs`, `--registry-secret`</dt>
<dd>The name of the image pull secret. Pull secrets are used to authenticate with a private registry when you download the container image. This value is optional. 
</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. This value is optional. The default value is <code>0</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo application update --name myapp --image ibmcom/helloworld 
```
{: pre}

**Example output**

```
Updating Application 'myapp' in namespace 'f0173a8d-abc3':
Application 'fmoapp' updated to latest revision 'myapp-oobym-3' and is available at URL:
http://myapp.f0173a8d-abc3.us-south.knative.appdomain.cloud
```
{: screen}
  


### `ibmcloud coligo application delete`  
{: #cli-application-delete}  

Delete an application.
{: shortdesc}

```
 ibmcloud coligo application delete --name APPLICATION_NAME [--wait-timeout TIME] [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
<dt>`-wto`, `--wait-timeout`</dt>
<dd>The length of time in seconds to wait for the application to be deleted. This value is optional. The default value is <code>300</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo application delete --name myapp
```
{: pre}

**Example output**

```
Deleted application 'myapp'
```
{: screen}
  


### `ibmcloud coligo application list`  
{: #cli-application-list}  

List all applications in a project.
{: shortdesc}

```
 ibmcloud coligo application 
```
{: pre}

**Example output**

```
NAME        URL                                                                    LATEST              AGE   CONDITIONS   READY   REASON
myapp       http://myapp.b49ca89f-g99q.us-south.knative.test.appdomain.cloud       myapp-zxxlr-1       19h   3 OK / 3     True
mytestapp   http://mytestapp.42734592-8355.us-south.knative.test.appdomain.cloud   mytestapp-qhmzn-1   20h   3 OK / 3     True
```
{: screen}
  


### `ibmcloud coligo application bind`  
{: #cli-application-bind}  

Bind an {{site.data.keyword.cloud_notm}} service to an application.
{: shortdesc}

```
 ibmcloud coligo application bind --name APP_NAME --service-instance SI_NAME [--service-credential SI_CREDENTIAL_NAME] [--prefix PREFIX] [--quiet]
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
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (_), and cannot start with a number. This value is optional. 
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
ibmcloud coligo application bind --name myapp --service-instance langtranslator
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
  


### `ibmcloud coligo application unbind`  
{: #cli-application-unbind}  

Unbind {{site.data.keyword.cloud_notm}} services from an application.
{: shortdesc}

```
 ibmcloud coligo application unbind --name APP_NAME (--service-instance SERVICE_INSTANCE_NAME | --all) [--quiet] 
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
ibmcloud coligo application unbind --name myapp --all
```
{: pre}

**Example output**

```
Removing service bindings...
Successfully removed service bindings
OK
```
{: screen}
 

## Configmap commands  
{: #cli-configmap}  

Use configmap commands to create, display details, update, and delete configmaps.
{: shortdesc}

You can use either `configmap` or `cm` in your configmap commands. To see CLI help for the configmap commands, run `ibmcloud coligo configmap`.  
{: tip}


### `ibmcloud coligo configmap create`  
{: #cli-configmap-create}  

Create a configmap.
{: shortdesc}

```
 ibmcloud coligo configmap create --name CONFIGMAP_NAME ([--from-file FILE] | [--from-literal KEY=VALUE])
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

- The following example creates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud coligo configmap create --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Example output**

  ```
  Creating Configmap 'configmap-fromliteral'...

  Successfully created configmap 'configmap-fromliteral'. Run `ibmcloud coligo configmap get -n 'configmap-fromliteral'` to see more details.
  ```
  {: screen}
  
- The following example creates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud coligo configmap create --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Example output**

  ```
  Creating Configmap 'configmap-fromfile'...

  Successfully created configmap 'configmap-fromfile'. Run `ibmcloud coligo configmap get -n 'configmap-fromfile'` to see more details.
  ```
  {: screen}
  


### `ibmcloud coligo configmap get`  
{: #cli-configmap-get}  

Display the details of a configmap.
{: shortdesc}

```
 ibmcloud coligo configmap get --name CONFIGMAP_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. 
</dd>
</dl>

**Example**

```
ibmcloud coligo configmap get --name configmap-fromliteral 
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
  


### `ibmcloud coligo configmap update`  
{: #cli-configmap-update}  

Update a configmap.
{: shortdesc}

```
 ibmcloud coligo configmap update --name CONFIGMAP_NAME ([--from-file FILE] | [--from-literal KEY=VALUE])
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
</dl>

**Examples**

- The following example updates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud coligo configmap update --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Example output**

  ```
  Updating Configmap configmap-fromliteral...
  OK
  Successfully updated configmap 'configmap-fromliteral'. Run `ibmcloud coligo configmap get -n configmap-fromliteral` to see more details.
  ```
  {: screen}
  
- The following example updates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud coligo configmap update --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
  ```
  {: pre}

  **Example output**

  ```
  Updating Configmap configmap-fromfile...
  OK
  Successfully updated configmap 'configmap-fromfile'. Run `ibmcloud coligo configmap get -n configmap-fromfile` to see more details.

  ```
  {: screen}
  


### `ibmcloud coligo configmap delete`  
{: #cli-configmap-delete}  

Delete a configmap.
{: shortdesc}

```
 ibmcloud coligo configmap delete --name CONFIGMAP_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo configmap delete --name configmap-fromliteral
```
{: pre}

**Example output**

```
Deleting Configmap 'configmap-fromliteral'...

Successfully deleted configmap 'configmap-fromliteral'
```
{: screen}
  


### `ibmcloud coligo configmap list`  
{: #cli-configmap-list}  

List all configmaps in a project.
{: shortdesc}

```
 ibmcloud coligo configmap list
```
{: pre}

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

Before you use job definition commands, you must be targeting a [project](#cli-project). A job definition is a template that contains workload configuration information that is used to run [jobs](#cli-job-runcmd). After you create a job definition, one or more jobs can be submitted based on the job definition, optionally overwriting values of the job definition. Use job definition commands to create, display details, update, and delete jobs.
{: shortdesc}

You can use either `jobdef` or `jd` in your job definition commands. To see CLI help for the job definition command, run `ibmcloud coligo jd`.  
{: tip}


### `ibmcloud coligo jobdef create`  
{: #cli-jobdef-create}  

Create a job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef create --name JOBDEF_NAME --image IMAGE_REF [--env KEY=VALUE] [--env-from-secret SECRET_KEY] [--env-from-configmap CONFIGMAP_KEY] [--argument ARGUMENT] [--command COMMAND] [--cpu CPU] [--memory MEMORY]
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
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the container. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the container. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for the instance of the job definition. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the container. Must be in `NAME=VALUE` format.  Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this configmap. For example, a configmap that contains `configmapName:value` results in an environment variable called `configmapName` that is set to `value`. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this secret. For example, a secret that contains `secretName:value` results in an environment variable called `secretName` that is set to `value`. This value is optional. 
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the job definition. Use `M` for mebibytes or `G` for gibibytes. This value is optional. The default value is <code>128M</code>.
</dd>
</dl>

**Example**

The following example uses the container image `busybox` and uses the arguments `/bin/sh -c echo Hello $JOB_INDEX ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3`, assigning 128 MB as memory and 1 CPU to the container.

```
ibmcloud coligo jobdef create --image busybox --name hello --argument /bin/sh --argument "-c" --argument "echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3" -e "ENV1=env1 from jobdef" -e "ENV2=env2 from jobdef" -e "ENV3=env3 from jobdef" --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Created successfully Job Definition 'hello'
```
{: screen}
  


### `ibmcloud coligo jobdef get`  
{: #cli-jobdef-get}  

Display the details of a job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef get --name JOBDEF_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project. This value is required. 
</dd>
</dl>

**Example**

```
ibmcloud coligo jobdef get --name myjobdef
```
{: pre}

**Example output**

```
Name:         myjobdef
Namespace:    b49ca89f-g99q
Labels:       <none>
Annotations:  <none>
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobDefinition
Metadata:
  Creation Timestamp:  2020-04-16T15:21:41Z
  Generation:          1
  Resource Version:    69009760
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/b49ca89f-g99q/jobdefinitions/myjobdef
  UID:                 6ac2e78c-0883-4564-9158-4c7e08762a41
Spec:
  Containers:
    Args:
      /bin/sh
      -c
      echo Hello $JOB_INDEX. ENV1 is $ENV1, ENV2 is $ENV2, ENV3 is $ENV3
    Env:
      Name:   ENV1
      Value:  env1 from jobdef
      Name:   ENV2
      Value:  env2 from jobdef
      Name:   ENV3
      Value:  env3 from jobdef
    Image:    busybox
    Name:     myjobdef
    Resources:
      Requests:
        Cpu:     1
        Memory:  128Mi
Events:          <none>

Command 'job definition get' performed successfully
```
{: screen}
  



### `ibmcloud coligo jobdef update`  
{: #cli-jobdef-update}  

Update a job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef update --name JOBDEF_NAME --image IMAGE_REF [--env KEY=VALUE] [--env-from-secret SECRET_KEY] [--env-from-configmap CONFIGMAP_KEY] [--argument ARGUMENT] [--command COMMAND] [--cpu CPU] [--memory MEMORY]
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
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the container. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value is optional. 
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the container. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU to set for the instance of the job definition. This value updates any `--cpu` value that is assigned in the job definition. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the container. Must be in `NAME=VALUE` format.  This action adds a new environment variable or overrides an existing environment variable. Specify one environment variable per `--env` flag; for example, `--env envA=A --env envB=B`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this configmap. For example, a configmap that contains `configmapName:value` results in an environment variable called `configmapName` that is set to `value`. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this secret. For example, a secret that contains `secretName:value` results in an environment variable called `secretName` that is set to `value`. This value is optional. 
</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory that is set for the job definition. Use `M` for mebibytes or `G` for gibibytes. This value updates any `--memory` value that is assigned in the job definition. This value is optional. The default value is <code>128M</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo jobdef update --name myjobdef --cpu 2
```
{: pre}

**Example output**

```
Successfully updated job definition 'myjobdef'
```
{: screen}
  


### `ibmcloud coligo jobdef delete`  
{: #cli-jobdef-delete}  

Delete a job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef delete --name JOBDEF_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. Use a name that is unique within the project. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo jobdef delete --name myjobdef
```
{: pre}

**Example output**

```
Deleted JobDefinition 'myjobdef'
```
{: screen}
  


### `ibmcloud coligo jobdef list`  
{: #cli-jobdef-list}  

List all job definitions in a project.
{: shortdesc}

```
 ibmcloud coligo jobdef 
```
{: pre}

**Example output**

```
NAME        AGE
hello       5d14h
hello2      5d14h
myjobdef    5d15h
```
{: screen}
  


### `ibmcloud coligo jobdef bind`  
{: #cli-jobdef-bind}  

Bind an {{site.data.keyword.cloud_notm}} service to a job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef bind --name JOBDEF_NAME --service-instance SI_NAME [--service-credential SI_CREDENTIAL_NAME] [--prefix PREFIX] [--quiet]
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
<dd>A prefix for environment variables that are created for this service binding. Must contain only uppercase letters, numbers, and underscores (_), and cannot start with a number. This value is optional. 
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
ibmcloud coligo jobdef bind --name myjobdef --service-instance my-object-storage
```
{: pre}

**Example output**

```
Binding service...
Successfully created service binding for 'my-object-storage'
```
{: screen}
  


### `ibmcloud coligo jobdef unbind`  
{: #cli-jobdef-unbind}  

Unbind {{site.data.keyword.cloud_notm}} services from a job definition to remove existing service bindings from the job definition.
{: shortdesc}

```
 ibmcloud coligo jobdef unbind --name JOBDEF_NAME (--service-instance SERVICE_INSTANCE_NAME | --all) [--quiet] 
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
ibmcloud coligo jobdef unbind --name myjobdef --all
```
{: pre}

**Example output**

```
Removing service bindings...
Successfully removed service bindings
OK
```
{: screen}
  


## Job commands  
{: #cli-job}  

A job runs your code to complete a task. Before you use job commands, you must be targeting a [project](#cli-project). You can use a job definition as a template for your job, or you can set job parameters with the job run command. Use job commands to run, display details, and delete jobs.
{: shortdesc}

To see CLI help for the job commands, run `ibmcloud coligo job`.  
{: tip}


### `ibmcloud coligo job run`  
{: #cli-job-run}  

Run a job based on a job definition.
{: shortdesc}

```
 ibmcloud coligo job run (--name JOB_NAME | --jobdef JOBDEF_NAME) [--image IMAGE_REF] [--env KEY=VALUE] [--env-from-secret SECRET_KEY] [--env-from-configmap CONFIGMAP_KEY] [--argument ARGUMENT] [--command COMMAND] [--cpu CPU] [--memory MEMORY] [--arraysize ARRAYSIZE] [--retrylimit RETRY_LIMIT] [--maxexecutiontime MAX_TIME]
```
{: pre}

**Command Options**  
<dl>
<dt>`-a`, `--argument`</dt>
<dd>Set arguments for the container. Specify one argument per `--argument` flag; for example, `-a argA -a argB`. This value overrides the default arguments that are specified in the job definition. This value is optional. 
</dd>
<dt>`-as`, `--arraysize`</dt>
<dd>The number of pods that are used to run the container. Specifies how many instances of the job definition to run. This value is optional. The default value is <code>1</code>.
</dd>
<dt>`-c`, `--command`</dt>
<dd>Set commands for the container. Specify one command per `--command` flag; for example, `--cmd cmdA --cmd cmdB`. This value overrides the default command that is specified within the container image. This value is optional. 
</dd>
<dt>`--cpu`</dt>
<dd>The amount of CPU set for the instance of the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. This value is optional. The default value is <code>1</code>.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set environment variables in the container. Must be in `NAME=VALUE` format. This action adds a new environment variable or overrides an existing environment variable.  Specify one environment variable per `--env` flag; for example, `-e envA -e envB`. This value is optional. 
</dd>
<dt>`-env-cm`, `--env-from-configmap`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this configmap. For example, a configmap that contains `configmapName:value` results in an environment variable called `configmapName` that is set to `value`. This value is optional. 
</dd>
<dt>`-env-sec`, `--env-from-secret`</dt>
<dd>Set environment variables for the key-value pairs that are stored in this secret. For example, a secret that contains `secretName:value` results in an environment variable called `secretName` that is set to `value`. This value is optional. 
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
<dd>The amount of memory to assign to the container that is running the image. Use `M` for mebibytes or `G` for gibibytes. This value overrides any `--memory` value that is assigned in the job definition. This value is optional. The default value is <code>128M</code>.
</dd>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is optional. </dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>The number of times to retry the job. A job is retried when it gives an exit code other than zero. This value is optional. The default value is <code>3</code>.
</dd>
</dl>

**Example**

The following example creates three new pods to run the container image specified in the `hello` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud coligo job run --name myjobrun --jobdef myjobdef --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Creating Job 'myjobrun'...
OK
Successfully created Job 'myjobrun'
```
{: screen}
  


### `ibmcloud coligo job get`  
{: #cli-job-get}  

Display the details of a job.
{: shortdesc}

```
 ibmcloud coligo job get --name JOBRUN_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
</dl>

**Example**

```
ibmcloud coligo job get --name hellojob
```
{: pre}

**Example output**

```
Getting Job 'myjobrun'...
Name:         myjobrun-gvq57
Namespace:    42642513-8805
Labels:       coligo.cloud.ibm.com/job-definition=myjobdef
              jobrun=myjobrun
Annotations:  coligo.cloud.ibm.com/pod-expectations: 5
API Version:  coligo.cloud.ibm.com/v1alpha1
Kind:         JobRun
Metadata:
  Creation Timestamp:  2020-05-04T17:41:37Z
  Generate Name:       myjobrun-
  Generation:          1
  Resource Version:    87729212
  Self Link:           /apis/coligo.cloud.ibm.com/v1alpha1/namespaces/42642513-8805/jobruns/myjobrun-gvq57
  UID:                 25de99f4-b4a3-4ad6-a226-06aa5cdf297c
Spec:
  Array Size:          5
  Job Definition Ref:  myjobdef
  Job Definition Spec:
    Containers:
      Image:  busybox
      Name:   myjobdef
      Resources:
        Requests:
          Cpu:         1
          Memory:      128Mi
  Max Execution Time:  7200
  Retry Limit:         2
Status:
  Completion Time:  2020-05-04T17:41:42Z
  Conditions:
    Last Probe Time:       2020-05-04T17:41:37Z
    Last Transition Time:  2020-05-04T17:41:37Z
    Status:                True
    Type:                  Pending
    Last Probe Time:       2020-05-04T17:41:40Z
    Last Transition Time:  2020-05-04T17:41:40Z
    Status:                True
    Type:                  Running
    Last Probe Time:       2020-05-04T17:41:42Z
    Last Transition Time:  2020-05-04T17:41:42Z
    Status:                True
    Type:                  Complete
  Effective Job Definition Spec:
    Containers:
      Args:
        /bin/sh
        -c
        echo Hello . ENV1 is , ENV2 is , ENV3 is
      Env:
        Name:   ENV1
        Value:  env1 from jobdef
        Name:   ENV2
        Value:  env2 from jobdef
        Name:   ENV3
        Value:  env3 from jobdef
      Image:    busybox
      Name:     myjobdef
      Resources:
        Requests:
          Cpu:     1
          Memory:  128Mi
  Start Time:      2020-05-04T17:41:37Z
  Succeeded:       5
Events:
  Type    Reason     Age                   From                  Message
  ----    ------     ----                  ----                  -------
  Normal  Updated    3m57s (x9 over 4m1s)  batch-job-controller  Updated JobRun "myjobrun-gvq57"
  Normal  Completed  3m57s                 batch-job-controller  JobRun completed successfully

Command 'job get' performed successfully
```
{: screen}
  


### `ibmcloud coligo job delete`  
{: #cli-job-delete}  

Delete a job.
{: shortdesc}

```
 ibmcloud coligo job delete --name JOBRUN_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo job delete --name myjobrun
```
{: pre}

**Example output**

```
Deleting Job 'myjobrun'...

Deleted Job 'myjobrun'
```
{: screen}
  


### `ibmcloud coligo job list`  
{: #cli-job-list}  

List all running jobs in a project.
{: shortdesc}

```
 ibmcloud coligo job 
```
{: pre}

**Example output**

```
NAME             AGE
hellojob-sjf2t   2d17h
myjobrun-gvq57   2m18s
```
{: screen}

The name of the job listed indicates the name of the job and the current revision of the job.  
{: tip}
  


### `ibmcloud coligo job logs`  
{: #cli-job-logs}  

Display the logs of one job.
{: shortdesc}

```
 ibmcloud coligo job logs --name JOBRUN_NAME [--pod POD_INDEX]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required. 
</dd>
<dt>`-p`, `--pod`</dt>
<dd>The job pod index. This value is optional. The default value is <code>0</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo job logs --name myjobrun
```
{: pre}

**Example output**

```
Logging Job 'myjobrun' on Pod 0...

Hello . ENV1 is , ENV2 is , ENV3 is

Command 'job logs' performed successfully
```
{: screen}
  


## Secret commands  
{: #cli-secret}  

Work with secrets.
{: shortdesc}

To see CLI help for the secret commands, run `ibmcloud coligo secret`.  
{: tip}


### `ibmcloud coligo secret create`  
{: #cli-secret-create}  

Create a secret.
{: shortdesc}

```
 ibmcloud coligo secret create --name SECRET_NAME (--from-file FILE | --from-literal KEY=VALUE | --from-registry REGISTRY --username USERNAME --password PASSWORD)
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. Use a name that is unique within the project.
<ul>
	<li>The name must begin with a lowercase letter.</li>
	<li>The name must end with a lowercase alphanumeric character.</li>
	<li>The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-).</li>
</ul>
This value is required. </dd>
<dt>`-f`, `--from-file`</dt>
<dd>Create a secret from a file. You must provide the path to the file as a value. This value is required if `--from-literal` is not specified. This value is optional. 
</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Create a secret from a key-value pair. Must be in `NAME=VALUE` format. This value is required if `--from-file` is not specified. This value is optional. 
</dd>
<dt>`-r`, `--from-registry`</dt>
<dd>The URL of an image registry that contains the secret. This value is optional. 
</dd>
<dt>`-p`, `--password`</dt>
<dd>Provide the password for the secret in the registry. This value is optional. 
</dd>
<dt>`-u`, `--username`</dt>
<dd>Provide the username for the secret in the registry. This value is optional. 
</dd>
</dl>

{[cli-secret-create-example.md]}  


### `ibmcloud coligo secret get`  
{: #cli-secret-get}  

Display the details of a secret.
{: shortdesc}

```
 ibmcloud coligo secret get --name SECRET_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. 
</dd>
</dl>

**Example**

```
ibmcloud coligo secret get mysecret
```
{: pre}

**Example output**

```
ok:
```
{: screen}
  

### `ibmcloud coligo secret update`  
{: #cli-secret-update}  

Update a secret.
{: shortdesc}

```
 ibmcloud coligo secret update --name SECRET_NAME (--from-file FILE | --from-literal KEY=VALUE | --from-registry REGISTRY --username USERNAME --password PASSWORD)
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
<dt>`-r`, `--from-registry`</dt>
<dd>The URL of an image registry that contains the secret. This value is optional. 
</dd>
<dt>`-p`, `--password`</dt>
<dd>Provide the password for the secret in the registry. This value is optional. 
</dd>
<dt>`-u`, `--username`</dt>
<dd>Provide the username for the secret in the registry. This value is optional. 
</dd>
</dl>

{[cli-secret-update-example.md]}  


### `ibmcloud coligo secret delete`  
{: #cli-secret-delete}  

Delete a secret.
{: shortdesc}

```
 ibmcloud coligo secret delete --name SECRET_NAME [--force]
```
{: pre}

**Command Options**  
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. 
</dd>
<dt>`-f`, `--force`</dt>
<dd>Force deletion without confirmation. This value is optional. The default value is <code>true</code>.
</dd>
</dl>

**Example**

```
ibmcloud coligo secret delete mysecret
```
{: pre}

**Example output**

```
Deleting Secret mysecret...

Successfully deleted secret 'mysecret'.
```
{: screen}
  


### `ibmcloud coligo secret list`  
{: #cli-secret-list}  

List all secrets in a project.
{: shortdesc}

```
 ibmcloud coligo secret list
```
{: pre}

{[cli-secret-list-example.md]}  

## Help command  
{: #cli-help}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}


### `ibmcloud coligo help`  
{: #cli-helpcmd}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}

```
 ibmcloud coligo ${COMMAND_NAME} coligo help [command]
```
{: pre}

{[cli-help-example.md]}  


## Version command  
{: #cli-version}  

Display the version of the {{site.data.keyword.codeengineshort}} command line interface.
{: shortdesc}


### `ibmcloud coligo version`  
{: #cli-versioncmd}  

Display the version of the {{site.data.keyword.codeengineshort}} command line interface.
{: shortdesc}

```
 ibmcloud coligo ${COMMAND_NAME} coligo version 
```
{: pre}

{[cli-version-example.md]}  

## Builddef commands  
{: #cli-builddef}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}


### `ibmcloud coligo builddef create`  
{: #cli-builddef-create}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}

```
 ibmcloud coligo builddef create --name BUILDDEF_NAME --image IMAGE_REF --source SOURCE --secret SECRET
```
{: pre}

**Command Options**  
<dl>
<dt>`-i`, `--image`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
<dt>`-sec`, `--secret`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
<dt>`-src`, `--source`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
</dl>

{[cli-builddef-create-example.md]}  


## Build commands  
{: #cli-build}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}


### `ibmcloud coligo build run`  
{: #cli-build-run}  

A detailed explanation. Print this to the docs rather than the CLIDescription.
{: shortdesc}

```
 ibmcloud coligo build run --name BUILDRUN_NAME --builddef BUILDDEF_NAME
```
{: pre}

**Command Options**  
<dl>
<dt>`-bdf`, `--builddef`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
<dt>`-n`, `--name`</dt>
<dd>A detailed explanation. Print this to the docs rather than the CLIDescription. This value is required. 
</dd>
</dl>

{[cli-build-run-example.md]}  

