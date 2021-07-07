---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-02"

keywords: troubleshooting for code engine, troubleshooting for apps in code engine, tips for apps in code engine, logs for apps in code engine, apps

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
{:terraform: .ph data-hd-interface='terraform'}
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


# Debugging apps 
{: #troubleshoot-apps}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} applications.
{: shortdesc}

When your app isn't behaving as expected, looking at logs and system events can provide information that might help you debug the problem. 

## App limits to consider 
{: #ts-app-limits}

The maximum number of apps that you can create per project is 20. You are limited to a total of 60 revisions for all apps per project. {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. See [Updating apps](/docs/codeengine?topic=codeengine-application-workloads#update-app).

For more information about limits for apps including memory and cpu, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

## Getting logs for my apps 
{: #ts-app-gettinglogs}

Logs can be helpful to troubleshoot problems when you run apps. You can view app logs from the console or with the CLI. 
{: shortdesc}

When you view logs from the console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} app. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your apps. You can view app logs after you add logging capabilities. For more information, see [viewing app logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui).

When working with the CLI, you can display logs of all of the instances of an app or display logs of a specific instance of an app. 

1. Use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all of your defined apps in your project; for example,
 
     ```
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,
 
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
  Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

  Status Summary:  Application deployed successfully

  Image:                ibmcom/hello
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  500Mi
    Memory:             4G

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

  * To display the logs of a specific instance of your app, use the [**`ibmcloud ce app logs --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,
  
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

  * To display the logs of all of the instances of your app, use the [**`app logs --application APP_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,
  
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

## Getting system event information for my apps 
{: #ts-app-gettingevent}

System event information can be helpful to troubleshoot problems when you run apps. You can view system event information with the CLI.  
{: shortdesc}

You can display system events of all of the instances of an app or display system events of a specific instance of an app. 

1. Use the [**`ibmcloud ce app list`**](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all of your defined apps; for example,
 
     ```
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to get the details of your app, including the name of the instances for the app; for example,
 
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
  Console URL:   https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration

  Status Summary:  Application deployed successfully

  Image:                ibmcom/hello
  Resource Allocation:
    CPU:                1
    Ephemeral Storage:  500Mi
    Memory:             4G

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

  Events:
    Type    Reason   Age    Source              Messages
    Normal  Created  3m55s  service-controller  Created Configuration "myapp"
    Normal  Created  3m54s  service-controller  Created Route "myapp"

  Instances:
    Name                                       Revision       Running  Status   Restarts  Age
    myapp-atfte-2-deployment-7cb45cdf67-qc7sb  myapp-atfte-2  2/2      Running  0         52s
    myapp-atfte-2-deployment-7cb45cdf67-sp9fr  myapp-atfte-2  2/2      Running  0         52s
  ```
  {: screen}

3. Display the system events of instances of your app. 

  * To display the events of a specific instance of your app, use the [**`ibmcloud ce app events --instance INSTANCE_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,
  
    ```
    ibmcloud ce app events --instance myapp-atfte-2-deployment-7cb45cdf67-qc7sb
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

  * To display events of all of the instances of your app, use the [**`ibmcloud ce app events --application APP_NAME`**](/docs/codeengine?topic=codeengine-cli#cli-application-events) command; for example,
  
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

