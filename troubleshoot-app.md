---

copyright:
  years: 2021
lastupdated: "2021-03-04"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine

subcollection: codeengine

content-type: troubleshoot

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


# Troubleshooting tips for apps
{: #troubleshoot-apps}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} apps.
{: shortdesc}

## Why is my app create failing?    
{: #ts-app-create-fails}
{: troubleshoot}

{: tsSymptoms}
You cannot create an app. When you run the `ibmcloud ce app create` command in the CLI or deploy an app in the console, the application create does not complete successfully and displays a `failed` or `revision failed` error message.   

{: tsCauses}
If you cannot create an app, determine whether one of the following cases is true.  

1. The name of your app is not unique within the project. You receive an error message that contains `Application 'myapp' already exists within project 'myproj', please select a unique name.` 
2. The name of your app is not valid. You receive an error message that contains `An application name must consist of lowercase alphanumeric characters, '-' and must start with an alphabetic character and end with an alphanumeric character.` 
3. If the image that you referenced does not exist, the app create does not complete and an error occurs. You receive an error message that contains `Unable to pull the image`.
4. If you do not have the permissions to access the referenced image, the app create does not complete and an error occurs. You receive an error message that contains `Unable to pull the image`. 
5. The memory or cpu setting is not valid. You receive an error message that contains `memory parameter must be between 128Mi and 32Gi` or `cpu parameter must be between .01 and 8.0`.

{: tsResolve}
Try one of these solutions.

1. To determine whether the name of your app is unique within the project, use the `ibmcloud ce app list` command to list all defined apps and check whether an app with the same name exists. If an app with the same name exists, use the `ibmcloud ce app  delete --name APP_NAME` to delete the old app. The name of the app must be unique within your project. 
2. To confirm that the name of your app is valid, check that the name of your app consists of lowercase alphanumeric characters, '-', and that the name starts and ends with an alphabetic character. 
3. To confirm that the image for your app exists, review the error message for information about the failure.  

    a. To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application needs in order to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

    b. If you use the `app create` command in the {{site.data.keyword.codeengineshort}} CLI, specify the name of the image that is used for your application by using the format `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. For more information about the format to use to specify the repository for your image, see the [`app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. 
    
4. To confirm that you can access the referenced image, verify the location of your image and confirm that you have permissions to access the image.  

  If the image is located in a container image registry, such as Docker Hub or {{site.data.keyword.registryfull_notm}}, check that you added registry access to {{site.data.keyword.codeengineshort}} and that you are using the correct image registry access secret.  For more information about working with images in a container image registry, see [adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).  

5. If you specify the `--memory` or `--cpu` option with the `app create` command, confirm that you are using valid values. In the following command, the values that are specified for `--memory` and `--cpu` are not valid; for example,  

    ```
    ibmcloud ce app create --name myapp --memory 50Gi --cpu 20
    ```
    {: pre}

    **Example output**

    ```
    Creating application 'myapp'...
    FAILED
    memory parameter must be between 128Mi and 32Gi
    cpu parameter must be between .01 and 8.0
    ```
    {: screen}

    To fix the errors, set the `--memory` option between 128 Mi and 32 Gi, and set the `--cpu` option between 0.01 and 8.0 vCPU. 
    
For more information about deploying apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

## Why doesn't my app ever become ready?   
{: #ts-app-neverready}
{: troubleshoot}

{: tsSymptoms}
After you deploy an app, the app does not achieve a ready status.

{: tsCauses}
By default, {{site.data.keyword.codeengineshort}} apps listen for incoming connections on port `8080`. Your app might listen on a different port if you receive the following error message,

```
Internal error:
RevisionFailed: Revision "myapp-1" failed with message: Initial scale was never achieved
```
{: screen}

{: tsResolve}
If your app listens on a port other than port `8080`, deploy your app by using the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command in the CLI and use the `--port` option on this command to specify the port.

## How do I get logs for my app instances? (CLI) 
{: #ts-app-gettinglogs-cli}

Your app isn't behaving as expected and you want to look at the logs to see whether any messages are generated to help you debug the problem. Logs can be helpful to troubleshoot problems when you run apps. 

You can display logs of all of the instances of an app or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

1. Use the [`ibmcloud ce app list `](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all of your defined apps; for example,
 
     ```
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [`ibmcloud ce app get`](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,
 
  ```
  ibmcloud ce app get --name myapp  
  ```
  {: pre}

  **Example output** 

  ```
  OK

  Name:          myapp
  [...]

  Created:       2021-02-23T07:32:16-05:00
  URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
  Console URL:   https://cloud.ibm.com/codeengine/project/us-south/cd09cfe1-8e62-4a64-b382-0f8a8a1d0ddf/application/myapp/configuration

  Image:                ibmcom/hello
  Resource Allocation:
    CPU:                0.1
    Ephemeral Storage:  500Mi
    Memory:             1Gi

  Revisions:
    myapp-atfte-2:
      Age:                51s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to e69c88)
      Running Instances:  2

  Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  2
    Timeout:        300

  Conditions:
    Type                 OK    Age  Reason
    ConfigurationsReady  true  36s
    Ready                true  10s
    RoutesReady          true  10s

  Instances:
    Name                                       Revision       Running  Status   Restarts  Age
    myapp-atfte-2-deployment-7cb45cdf67-qc7sb  myapp-atfte-2  2/2      Running  0         52s
    myapp-atfte-2-deployment-7cb45cdf67-sp9fr  myapp-atfte-2  2/2      Running  0         52s
  ```
  {: screen}

3. Display the logs of instances of your app. 

  * To display the logs of a specific instance of your app, use the [`ibmcloud ce app logs --instance INSTANCE_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,
  
    ```
    ibmcloud ce app logs --instance myapp-atfte-2-deployment-7cb45cdf67-qc7sb
    ```
    {: pre} 
      
    **Example output** 

    ```
    Getting logs for application instance 'myapp-atfte-2-deployment-7cb45cdf67-qc7sb'...
    OK

    myapp-atfte-2-deployment-7cb45cdf67-qc7sb/user-container:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

  * To display the logs of all of the instances of your app, use the [`ibmcloud ce app logs --application APP_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,
  
    ```
    ibmcloud ce app logs --app myapp 
    ```
    {: pre} 
    
    **Example output** 

    ```
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-atfte-2-deployment-7cb45cdf67-qc7sb/user-container:
    Server running at http://0.0.0.0:8080/

    myapp-atfte-2-deployment-7cb45cdf67-sp9fr/user-container:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

For more information, see [Viewing application logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-applog-cli).

## How do I get system event information for my app instances? (CLI) 
{: #ts-app-gettingevent-cli}

Your app isn't behaving as expected and you want to look at the system event information to see whether any messages are generated to help you debug the problem. System event information can be helpful to troubleshoot problems when you run apps.

You can display system events of all of the instances of an app or display system events of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

1. Use the [`ibmcloud ce app list `](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all of your defined apps; for example,
 
     ```
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [`ibmcloud ce app get`](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,
 
  ```
  ibmcloud ce app get --name myapp  
  ```
  {: pre}

  **Example output** 

  ```
  OK

  Name:          myapp
  [...]

  Created:       2021-02-23T07:32:16-05:00
  URL:           https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
  Console URL:   https://cloud.ibm.com/codeengine/project/us-south/cd09cfe1-8e62-4a64-b382-0f8a8a1d0ddf/application/myapp/configuration

  Image:                ibmcom/hello
  Resource Allocation:
    CPU:                0.1
    Ephemeral Storage:  500Mi
    Memory:             1Gi

  Revisions:
    myapp-atfte-2:
      Age:                51s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to e69c88)
      Running Instances:  2

  Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  2
    Timeout:        300

  Conditions:
    Type                 OK    Age  Reason
    ConfigurationsReady  true  36s
    Ready                true  10s
    RoutesReady          true  10s

  Instances:
    Name                                       Revision       Running  Status   Restarts  Age
    myapp-atfte-2-deployment-7cb45cdf67-qc7sb  myapp-atfte-2  2/2      Running  0         52s
    myapp-atfte-2-deployment-7cb45cdf67-sp9fr  myapp-atfte-2  2/2      Running  0         52s
  ```
  {: screen}

3. Display the system events of instances of your app. 

  * To display the events of a specific instance of your app, use the [`ibmcloud ce app events --instance INSTANCE_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,
  
    ```
    ibmcloud ce app events --instance myapp-atfte-1-deployment-5dc989d584-nvmml
    ```
    {: pre} 
      
    **Example output** 

    ```
    Getting events for application instance 'myapp-atfte-2-deployment-7cb45cdf67-qc7sb'...
    OK

    myapp-atfte-2-deployment-7cb45cdf67-qc7sb:
      Type    Reason     Age  Source                 Messages
      Normal  Scheduled  46m  default-scheduler      Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-qc7sb to 10.240.64.20
      Normal  Pulling    45m  kubelet, 10.240.64.20  Pulling image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
      Normal  Pulled     45m  kubelet, 10.240.64.20  Successfully pulled image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.64261536s
      Normal  Created    45m  kubelet, 10.240.64.20  Created container user-container
      [...]
    ```
    {: screen}

  * To display events of all of the instances of your app, use the [`ibmcloud ce app events --application APP_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,
  
    ```
    ibmcloud ce app events --app myapp 
    ```
    {: pre} 
    
    **Example output** 

    ```
    Getting events for all instances of application 'myapp'...
    OK

    myapp-atfte-2-deployment-7cb45cdf67-qc7sb:
      Type    Reason     Age  Source                 Messages
      Normal  Scheduled  47m  default-scheduler      Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-qc7sb to 10.240.64.20
      Normal  Pulling    47m  kubelet, 10.240.64.20  Pulling image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
      Normal  Pulled     47m  kubelet, 10.240.64.20  Successfully pulled image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.64261536s
      Normal  Created    46m  kubelet, 10.240.64.20  Created container user-container
      Normal  Started    46m  kubelet, 10.240.64.20  Started container user-container
      [...]

    myapp-atfte-2-deployment-7cb45cdf67-sp9fr:
      Type    Reason     Age  Source                Messages
      Normal  Scheduled  47m  default-scheduler     Successfully assigned 4svg40kna19/myapp-atfte-2-deployment-7cb45cdf67-sp9fr to 10.240.0.24
      Normal  Pulling    47m  kubelet, 10.240.0.24  Pulling image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980"
      Normal  Pulled     47m  kubelet, 10.240.0.24  Successfully pulled image "index.docker.io/ibmcom/hello@sha256:e69c88d7f33778b8266cd480b79522f13968c72aca1287f47603ab711208c980" in 3.682464554s
      Normal  Created    46m  kubelet, 10.240.0.24  Created container user-container
      Normal  Started    46m  kubelet, 10.240.0.24  Started container user-container
      [...] 
    ```
    {: screen}

