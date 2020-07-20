---

copyright:
  years: 2020
lastupdated: "2020-07-16"

keywords: code engine

subcollection: codeengine

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


# {{site.data.keyword.codeenginefull_notm}} CLI 
{: #kn-cli}

Run these commands to manage the entities that make up {{site.data.keyword.codeenginefull_notm}} (or "{{site.data.keyword.codeengineshort}}").
{: shortdesc}

## Project commands
{: #cli-project}

A project is a container for components, such as applications and job definitions. Projects enable you to manage resources and provide access to components in the project. Use project commands to create, display details, and delete projects.
{: shortdesc}

You can use either `project` or `proj` in your project commands. 
To see CLI help for the project command, run `ibmcloud ce proj`. 
{: tip}

### `ibmcloud ce project create`
{: #cli-project-create}

Create a project.
{: shortdesc}

```
ibmcloud ce project create --name PROJECT_NAME  [--tag TAG] [--target]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required. Use a name that is unique to your region. The name must be 128 characters or fewer and can contain:
<ul>
  <li>Any Unicode character </li>
  <li>Only these special characters:  spaces ( ), periods (.), colons (:), underscores (_), and hyphens (-)</li>
</ul>
</dd>
<dt>`-t`, `--tag`</dt>
<dd>A label to assign to your resource.  This value is optional. The label must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. Specify one label per `--tag` flag.  To specify more than one label, use more than one `--tag` flag; for example, `--tag tagA --tag tagB`.</dd>
<dt>`--tg`, `--target`</dt>
<dd>Specify this option to target this project after it is created. The default value is `false`. This value is optional.</dd>
<dt>`-p`, `--project-api`</dt>
<dd>Specifies an alternate URL to use for project queries. Use this option only if the `target` option is also specified.</dd>
</dl>

**Example**

```
ibmcloud ce project create --name myproject  
```
{: pre}

**Example output**

```
Successfully created project myproject
```
{: screen}


### `ibmcloud ce project current`
{: #cli-project-current}

Display the details of the project that is currently targeted. 
{: shortdesc}

```
ibmcloud ce project current
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


### `ibmcloud ce project delete`
{: #cli-project-delete}

Delete a project.
{: shortdesc}

```
ibmcloud ce project delete --name PROJECT_NAME [--force]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required.</dd>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
</dl>

**Example**

```
ibmcloud ce project delete --name myproject
```
{: pre}

**Example output**

```
Deleted project myproject
```
{: screen}


### `ibmcloud ce project get`
{: #cli-project-get}

Display the details of a single project.
{: shortdesc}

```
ibmcloud ce project get --name PROJECT_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required.</dd>
</dl>

**Example**

```
ibmcloud ce project get --name myproject
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


### `ibmcloud ce project list`
{: #cli-project-list}

List available projects.
{: shortdesc}

```
ibmcloud ce project list
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


## Target command
{: #cli-target}

To work with a {{site.data.keyword.codeengineshort}} project, target the project. Before using the target command, you must have a project created. By targeting a project, the commands that you run are run within the specified project.  

{: shortdesc}

To see CLI help for the target command, run `ibmcloud ce target`. 
{: tip}

### `ibmcloud ce target`
{: #cli-targetcmd}

Target a project for context.
{: shortdesc}

```
ibmcloud ce target --name PROJECT_NAME [--project-api PROJECTAPI]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the project. This value is required.</dd>

<dt>`-p`, `--project-api`</dt>
<dd>Specifies an alternate URL to use for project queries. This value is optional.</dd>
</dl>

{[cli-target-project-example.md]}

## Application commands
{: #cli-application}

Before using application commands, you must be targeting a [project](#cli-project).  An application runs your code to serve HTTP requests. The application has a URL for incoming requests. Use application commands to create, display details, and update, and delete applications. 
{: shortdesc}

You can use either `application` or `app` in your application commands. 
To see CLI help for the application command, run `ibmcloud ce app`. 
{: tip}

### `ibmcloud ce application create`
{: #cli-application-create}

Create an application.
{: shortdesc}

```
ibmcloud ce application create --image IMAGE_REF --name APP_NAME  [--registry-secret SECRET] [--cpu CPU] [--memory MEMORY] [--timeout TIMEOUT] [--concurrency REQUESTS] [--minscale MIN_NUM] [--maxscale MAX_NUM] [--argument ARGUMENT] [--command COMMAND] [--env ENV] [--env-from-secret SECRETNAME:KEYNAME] [--env-from-configmap CONFIGMAPNAME:KEYNAME] [--quiet] [--no-wait | --wait-timeout] [--cluster-local]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. This value is required. For images in <a href="https://hub.docker.com" target="_blank" class="external">Docker Hub</a>, you can specify the image with `NAMESPACE/REPOSITORY`. For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`--rs`, `--registry-secret`</dt>
<dd>The name of the secret that is used to authenticate with a private registry when downloading the container image. This value is optional.</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the instance of the application. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the instance of the application. Use `Mi` for mebibytes or `Gi` for gibibytes. The default value is `1024Mi`. This value is optional.</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</dd>
<dt>`--cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently per instance. The default value is 1. This value is optional.</dd>
<dt>`--min`, `--minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. This option is useful to ensure no instances are running when not needed. The default value is 0. This value is optional.</dd>
<dt>`--max`, `--maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. The default value is 10. This value is optional.</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set any arguments for the application. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value is optional.</dd>
<dt>`-c`, `--command`</dt>
<dd>Override the default command that is specified within the container image. This value is optional.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environment variables to pass to the application. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`--env-sec`, `--env-from-secret`</dt>
<dd>Provides the application environment variable that is taken from a secret, in the format `secretName:keyName`. This value is optional.</dd>
<dt>`--env-cm`, `--env-from-configmap`</dt>
<dd>Indicates the application environment variable that is taken from a configmap, in the format `configmapName:keyName`. This value is optional.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
<dt>`--nw`, `--no-wait`</dt>
<dd>Create the application asynchronously. This value is optional. The default value is `false`.</dd> 
<dt>`--wto`, `--wait-timeout`</dt>
<dd> The length of time in seconds to wait for the application to start. This value is ignored when `no-wait` is specified. This value is optional. The default value is 300 seconds.</dd> 
<dt>`--cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. This value is optional. The default value is `false`.</dd> 
</dl>

{[cli-app-create-example.md]}

### `ibmcloud ce application bind`
{: #cli-application-bind}

Bind an {{site.data.keyword.cloud_notm}} service to an application in a {{site.data.keyword.codeengineshort}} project. 
{:shortdesc}

```
ibmcloud ce application bind --name APPLICATION_NAME --service-instance SERVICE_NAME [--service-credentials CREDENTIALS] [--prefix] [--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`--si`, `--service-instance`</dt>
<dd>Specifies the service instance name to bind to the application. This value is required.</dd> 
<dt>`--sc`, `--service-credential`</dt>
<dd>Provides the service instance credential for binding the service to the application. This value is optional. If you do not specify a service instance credential, new credentials are generated during the bind action.</dd>
<dt>`-p`, `--prefix`</dt>
<dd>Provides a prefix for any environment variables that are created for this service binding. The prefix must be 35 characters or fewer and cannot start with a number, and can only contain only uppercase letters, numbers, and underscores (_). This value is optional. </dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
</dl>

{[cli-app-bind-example.md]}

### `ibmcloud ce application delete`
{: #cli-application-delete}

Delete an application.
{: shortdesc}

```
ibmcloud ce application delete --name APP_NAME [--force] [--wait-timeout]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
<dt>`--wto`, `--wait-timeout`</dt>
<dd> The length of time in seconds to wait for the application to be deleted. This value is optional. The default value is 300 seconds.</dd>
</dl>

{[cli-app-delete-example.md]}

### `ibmcloud ce application get`
{: #cli-application-get}

Display the details of an application.
{: shortdesc}

```
ibmcloud ce application get --name APP_NAME [--more-details]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`--md`, `--more-details`</dt>
<dd>Specify this option to print more details about the application. The default value is `false`. This value is optional.</dd>
</dl>

{[cli-app-get-example.md]}

### `ibmcloud ce application unbind`
{: #cli-app-unbind}

Unbinding an {{site.data.keyword.cloud_notm}} service from an application removes existing service bindings from the application. 
{: shortdesc}

```
ibmcloud ce application unbind (--name APP_NAME --service-instance | --all) [--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`--si`, `--service-instance`</dt>
<dd>Specifies the service instance name to unbind from the application. This value is required if `--all` is not specified.</dd> 
<dt>`--all`</dt>
<dd>Specifies to unbind all service credentials from the application. This value is required if `--service-instance` is not specified.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
</dl>

{[cli-app-unbind-example.md]}

### `ibmcloud ce application update`
{: #cli-app-update}

Update an application. Updating your application creates a revision. By default, when calls are made to the application, traffic is routed to the revision.
{: shortdesc}

```
ibmcloud ce application update --name APP_NAME --image IMAGE_REF [--registry-secret SECRET] [--cpu CPU] [--memory MEMORY] [--timeout TIMEOUT] [--concurrency REQUESTS] [--minscale MIN_NUM] [--maxscale MAX_NUM] [--argument ARGUMENT] [--command COMMAND] [--env ENV] [--cluster-local] [--env-from-secret SECRETNAME:KEYNAME] [--env-from-configmap CONFIGMAPNAME:KEYNAME] [--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the application. This value is required.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this application. This value is required. The format for the image must be `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`.</dd>
<dt>`--rs`, `--registry-secret`</dt>
<dd>The name of the secret for the image. This value is optional.</dd>
<dt>`-c`, `--cpu`</dt>
<dd>The amount of CPU set for the application. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>Specify to change the amount of memory set for the application. Use `Mi` for mebibytes or `Gi` for gibibytes. This value is optional.</dd>
<dt>`-t`, `--timeout`</dt>
<dd>The amount of time that can pass before the application must succeed or fail. The default value is 360 seconds. This value is optional.</dd>
<dt>`--cn`, `--concurrency`</dt>
<dd>The number of requests that can be processed concurrently. The default value is 1. This value is optional.</dd>
<dt>`--min`, `--minscale`, `--min-scale`</dt>
<dd>The minimum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`--max`, `--maxscale`, `--max-scale`</dt>
<dd>The maximum number of instances that can be used for this application. The default value is 1. This value is optional.</dd>
<dt>`-a`, `--argument`</dt>
<dd>Set any arguments for the application. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value is optional.</dd>
<dt>`-c`, `--command`</dt>
<dd>Override the default command that is specified within the container image. This value is optional.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environment variables to pass to the application. Variables use a `KEY=VALUE` format. This value is optional.</dd>
<dt>`--cl`, `--cluster-local`</dt>
<dd>Deploy the application with a private endpoint. This value is optional. The default value is `false`.</dd>
<dt>`--env-sec`, `--env-from-secret`</dt>
<dd>Provides the application environment variable that is taken from a secret, in the format `secretName:keyName`. This value is optional.</dd>
<dt>`--env-cm`, `--env-from-configmap`</dt>
<dd>Indicates the application environment variable that is taken from a configmap, in the format `configmapName:keyName`. This value is optional.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
</dl>

{[cli-app-update-example.md]}

### `ibmcloud ce application list`
{: #cli-application-list}

List all applications in a project. 
{: shortdesc}

```
ibmcloud ce application list
```
{: pre}

{[cli-app-list-example.md]}



## Job definition commands
{: #cli-jobdef}

Before using job definition commands, you must be targeting a [project](#cli-project). A job definition is a template that contains workload configuration information that is used to run [jobs](#cli-job-runcmd). After creating a job definition, one or more jobs can be submitted based on the job definition, optionally overwriting values of the job definition. Use job definition commands to create, display details, update, and delete applications. 

{: shortdesc}

You can use either `jobdef` or `jd` in your job definition commands. 
To see CLI help for the job definition command, run `ibmcloud ce jd`. 
{: tip}

### `ibmcloud ce jobdef create`
{: #cli-jobdef-create}

Create a job definition.
{: shortdesc}

```
ibmcloud ce jobdef create --name JOBDEFINITION_NAME --image IMAGE_REF [--argument ARGUMENT] [--command COMMAND] [--cpu CPU] [--memory MEMORY] [--env ENV] [--env-from-secret SECRETNAME:KEYNAME] [--env-from-configmap CONFIGMAPNAME:KEYNAME]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job definition. This value is required. For images in <a href="https://hub.docker.com" target="_blank" class="external">Docker Hub</a>, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. </dd>
<dt>`-a`, `--argument`</dt>
<dd>Set any arguments for the job definition. Specify one argument per `--argument` flag.  To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value is optional.</dd>
<dt>`-e`, `--env`</dt>
<dd>Set any environment variables to pass to the job definition. Variables use a `KEY=VALUE` format. This value is optional.</dd>
 <dt>`--env-sec`, `--env-from-secret`</dt>
<dd>Provides the job definition environment variable that is taken from a secret, in the format `secretName:keyName`. This value is optional.</dd>
<dt>`--env-cm`, `--env-from-configmap`</dt>
<dd>Indicates the job definition environment variable that is taken from a configmap, in the format `configmapName:keyName`. This value is optional.</dd>
<dt>`-c`, `--command`</dt>
<dd>Override the default command that is specified within the container image. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to be assigned to the job definition. The default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>The amount of memory set for the job definition. Use `Mi` for mebibytes or `Gi` for gibibytes. The default value is `128Mi`. This value is optional.</dd>
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


### `ibmcloud ce jobdef bind`
{: #cli-jobdef-bind}

Bind an {{site.data.keyword.cloud_notm}} service to an job definition in a {{site.data.keyword.codeengineshort}} project. 
{:shortdesc}

```
ibmcloud ce jobdef bind --name JOBDEFINITION_NAME --service-instance SERVICE_NAME [--service-credentials CREDENTIALS] [--prefix] [--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
<dt>`--si`, `--service-instance`</dt>
<dd>Specifies the service instance name to bind to the job definition. This value is required.</dd> 
<dt>`--sc`, `--service-credential`</dt>
<dd>Provides the service instance credential for binding the service to the job definition. This value is optional. If you do not specify a service instance credential, new credentials are generated during the bind action.</dd>
<dt>`-p`, `--prefix`</dt>
<dd>Provides a prefix for any environment variables that are created for this service binding. The prefix must be 35 characters or fewer and cannot start with a number, and can only contain only uppercase letters, numbers, and underscores (_). This value is optional. </dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
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


### `ibmcloud ce jobdef get`
{: #cli-jobdef-get}

Display the details of a job definition.
{: shortdesc}

```
ibmcloud ce jobdef get --name JOBDEFINITION_NAME
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
</dl>

**Example**

```
ibmcloud ce jobdef get --name myjobdef
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


### `ibmcloud ce jobdef unbind`
{: #cli-jobdef-unbind}

Unbinding an {{site.data.keyword.cloud_notm}} service from a job definiton removes existing service bindings from the job definition.  
{: shortdesc}

```
ibmcloud ce jobdef unbind (--name JOBDEFINITION_NAME --service-instance | --all) [--quiet]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
<dt>`--si`, `--service-instance`</dt>
<dd>Specifies the service instance name to unbind from the job definition. This value is required if `--all` is not specified.</dd> 
<dt>`--all`</dt>
<dd>Specifies to unbind all service credentials from the job definition. This value is required if `--service-instance` is not specified.</dd>
<dt>`-q`, `--quiet`</dt>
<dd>Specify this option to reduce the output of the command. The default value is `false`. This value is optional.</dd>
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




### `ibmcloud ce jobdef delete`
{: #cli-jobdef-delete}

Delete a job definition.
{: shortdesc}

```
ibmcloud ce jobdef delete --name JOBDEFINITION_NAME [--force]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job definition. This value is required.</dd>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
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
{: shortdesc}

```
ibmcloud ce jobdef list
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


## Job commands
{: #cli-job-runcmd}

A job runs your code to complete a task. Before using job commands, you must be targeting a [project](#cli-project) and have a [job definition](#cli-jobdef) created. Jobs are submitted based on a job definition. After a job definition is created, you can run one or more jobs that refer to the job definition, optionally overwriting values of the job definition. Use job commands to create, display details, and delete jobs. 
{: shortdesc}

To see CLI help for the job commands, run `ibmcloud ce job`. 
{: tip}

### `ibmcloud ce job run`
{: #cli-job-run}

Run a job based on a job definition.
{: shortdesc}

```
ibmcloud ce job run (--jobdef JOBDEFINITION_NAME  | --name JOBRUN_NAME  --image IMAGE_REF) [--cpu CPU] [--memory MEMORY] [--env ENV] [--env-from-secret SECRETNAME:KEYNAME] [--env-from-configmap CONFIGMAPNAME:KEYNAME] [--argument ARGUMENT] [--command COMMAND] [--arraysize ARRAY] [--retrylimit RETRY] [--maxexecutiontime MAXEXECUTIONTIME]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job to be run. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`--jd`, `--jobdef`</dt>
<dd>Identifies the job definition that contains the description of the job to be run. This value is required if you do not specify the `--name` and `image` values.</dd>
<dt>`-i`, `--image`</dt>
<dd>The name of the image used for this job. The `--name` and the `--image` values are required, if you do not specify the `--jobdef` value. For images in <a href="https://hub.docker.com" target="_blank" class="external">Docker Hub</a>, you can specify the image with `NAMESPACE/REPOSITORY`.  For other registries, use `REGISTRY/NAMESPACE/REPOSITORY` or `REGISTRY/NAMESPACE/REPOSITORY:TAG`. This value overrides any `--image` value that is assigned in the job definition.</dd>
<dt>`-e`, `--env`</dt>
<dd>Specifies any environment variables to pass to the image. Variables use a `KEY=VALUE` format. This value overrides any environment variables that are passed in the job definition. This value is optional. </dd>
<dt>`--env-sec`, `--env-from-secret`</dt>
<dd>Provides the job run environment variable that is taken from a secret, in the format `secretName:keyName`. This value is optional.</dd>
<dt>`--env-cm`, `--env-from-configmap`</dt>
<dd>Indicates the job run environment variable that is taken from a configmap, in the format `configmapName:keyName`. This value is optional.</dd>
<dt>`-a`, `--argument`</dt>
<dd>Sets any arguments for the container. To specify more than one argument, use more than one `--argument` flag; for example, `-a argA -a argB`. This value overrides any arguments passed in the job definition. This value is optional.</dd>  
<dt>`-c`, `--command`</dt>
<dd>Set a command. This value overrides any commands that are passed in the job definition. This value is optional.</dd>
<dt>`--cpu`</dt>
<dd>Specifies the number of CPUs to assign to the container that is running the image. This value overrides any `--cpu` value that is assigned in the job definition. If this value is not set in the job definition or the job run, the default value is 1. This value is optional.</dd>
<dt>`-m`, `--memory`</dt>
<dd>Specifies the amount of memory to assign to the container that is running the image. This value overrides any `--memory` value that is assigned in the job definition. Use `Mi` for mebibytes or `Gi` for gibibytes. The default value is `128Mi`. This value is optional.</dd>
<dt>`--as`, `--arraysize`</dt>
<dd>Specifies how many instances of the job definition to run. The default value is 1. This value is optional.</dd>
<dt>`-r`, `--retrylimit`</dt>
<dd>Specifies the number of times to retry the job. A job is retried when it gives an exit code other than zero. The default value is 3. This value is optional.</dd>
<dt>`--met`, `--maxexecutiontime`</dt>
<dd>Specifies the maximum execution time for the job.  The default value is 7200 seconds. This value is optional.</dd>
</dl>

**Example**

The following example creates three new pods to run the container image specified in the `hello` job definition. The resource limits and requests are applied per pod, so each of the pods gets 128 MB memory and 1 vCPU. This array job allocates 5 \* 128 MiB = 640 MiB memory and 5 \* 1 vCPU = 5 vCPUs.

```
ibmcloud ce job run --name myjobrun --jobdef myjobdef --arraysize 5 --retrylimit 2 --memory 128M --cpu 1
```
{: pre}

**Example output**

```
Creating Job 'myjobrun'...
OK
Successfully created Job 'myjobrun'
```
{: screen}


### `ibmcloud ce job list`
{: #cli-job-list}

List all running jobs in a project.
{: shortdesc}

```
ibmcloud ce job list
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


### `ibmcloud ce job get`
{: #cli-job-get}

Display the details of a job.
{: shortdesc}

```
ibmcloud ce job get --name JOBRUN_NAME 
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
</dl>

**Example**

```
ibmcloud ce job get --name hellojob
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


### `ibmcloud ce job logs`
{: #cli-job-logs}

Display the logs of one job.
{: shortdesc}

```
ibmcloud ce job logs --name JOBRUN_NAME [--pod POD]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
<dt>`-p`, `--pod`</dt>
<dd>The job pod index. The default value is 0. This value is optional. </dd>
</dl>

**Example**

```
ibmcloud ce job logs --name myjobrun
```
{: pre}

**Example output**

```
Logging Job 'myjobrun' on Pod 0...

Hello . ENV1 is , ENV2 is , ENV3 is

Command 'job logs' performed successfully
```
{: screen}


### `ibmcloud ce job delete`
{: #cli-job-delete}
Delete the job.
{: shortdesc}

```
ibmcloud ce job delete --name JOBRUN_NAME [--force]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the job. This value is required.</dd>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
</dl>

**Example**

```
ibmcloud ce job delete --name myjobrun
```
{: pre}

**Example output**

```
Deleting Job 'myjobrun'...

Deleted Job 'myjobrun'
```
{: screen}


## Secret commands
{: #cli-secrets}

Create {{site.data.keyword.codeengineshort}} secrets. 
{: shortdesc}

To see CLI help for the secret commands, run `ibmcloud ce secret`. 
{: tip}

### `ibmcloud ce secret create` (Generic)
{: #cli-secret-create-generic}

Create a generic secret from a value pair or from a file.
{: shortdesc}

```
ibmcloud ce secret create --name SECRETNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to create a generic secret from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to create a generic secret from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

{[cli-secret-create-generic-example.md]}

### `ibmcloud ce secret create` (Image pull)
{: #cli-secret-create-imgpull}

Create an image pull secret. Use image pull to access a container registry that stores the secrets.
{: shortdesc}

```
ibmcloud ce secret create --name SECRET_NAME --from-registry URL --username USERNAME --password PASSWORD
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-r`, `--from-registry`</dt>
<dd>Provide the URL of the image registry that contains the secret. This value is required.</dd>
<dt>`-u`, `--username`</dt>
<dd>Provide the username for the secret in the registry. This value is required.</dd>
<dt>`-p`, `--password`</dt>
<dd>Provide the password for the secret in the registry. This value is required.</dd>
</dl>

{[cli-secret-create-image-example.md]}

### `ibmcloud ce secret delete`
{: #cli-secret-delete}

Delete a secret.
{: shortdesc}

```
ibmcloud ce secret delete --name SECRETNAME [--force]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the secret. This value is required.</dt>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
</dl>

**Example**

```
ibmcloud ce secret delete --name mysecret
```
{: pre}

**Example output**

```
Deleting Secret mysecret...

Successfully deleted secret 'mysecret'.
```
{: screen}




## Configmap commands
{: #cli-configmap}

Use configmap commands to create, display details, and delete configmaps. 
{: shortdesc}

You can use either `configmap` or `cm` in your configmap commands. 
To see CLI help for the configmap commands, run `ibmcloud ce configmap`.
{: tip}

### `ibmcloud ce configmap create`
{: #cli-configmap-create}

Create a configmap.
{: shortdesc}

```
ibmcloud ce configmap create --name CONFIGMAPNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to create a configmap from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to create a configmap from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
</dl>

**Examples**

- The following example creates a configmap that is named `configmap-fromliteral` with a username and password value pair.

  ```
  ibmcloud ce configmap create --name configmap-fromliteral --from-literal username=devuser --from-literal password='S!B99d$Y2Ksb'
  ```
  {: pre}

  **Example output**

  ```
  Creating Configmap 'configmap-fromliteral'...

  Successfully created configmap 'configmap-fromliteral'. Run `ibmcloud ce configmap get -n 'configmap-fromliteral'` to see more details.
  ```
  {: screen}
  
- The following example creates a configmap that is named `configmap-fromfile` with values from a file.

  ```
  ibmcloud ce configmap create --name configmap-fromfile  --from-file ./username.txt --from-file ./password.txt
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
{: shortdesc}

```
ibmcloud ce configmap get --name CONFIGMAPNAME 
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required.</dd>
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
{: shortdesc}

```
ibmcloud ce configmap update --name CONFIGMAPNAME  --from-literal NAME=VALUE | --from-file PATH_TO_FILE
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required. Use a name that is unique within the project.
<ul>
  <li>  The name must begin with a lowercase letter. </li>
  <li>  The name must end with a lowercase alphanumeric character. </li>
  <li>  The name must be 35 characters or fewer and can contain letters, numbers, periods (.), and hyphens (-). </li>
</ul>
</dd>
<dt>`-f`, `--from-file value`</dt>
<dd>Include this flag to update a configmap from a file. You must provide the path to the file as a value. If you do not use this flag, you must use the `--from-literal` flag.</dd>
<dt>`-l`, `--from-literal`</dt>
<dd>Include this flag to update a configmap from a value pair. The format must be `NAME=VALUE`.  If you do not use this flag, you must use the `--from-file` flag.</dd>
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


### `ibmcloud ce configmap list`
{: #cli-configmap-list}

List all configmaps in a project.  
{: shortdesc}

```
ibmcloud ce configmap list
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


### `ibmcloud ce configmap delete`
{: #cli-configmap-delete}

Delete a configmap.
{: shortdesc}

```
ibmcloud ce configmap delete --name CONFIGMAPNAME [--force]
```
{: pre}

**Command options**
<dl>
<dt>`-n`, `--name`</dt>
<dd>The name of the configmap. This value is required.</dd>
<dt>`-f`, `--force`</dt>
<dd>Specifies to force the deletion without confirmation. This value is optional. The default value is `false`.</dd>
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
