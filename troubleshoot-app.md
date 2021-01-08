---

copyright:
  years: 2021
lastupdated: "2021-01-08"

keywords: code engine, troubleshooting for code engine, app, application, tips. logs

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
There are several reasons why you might not be able to create an app.  

1. The name of your app is not unique within the project. You receive a similar error message that contains: `Application 'myapp' already exists within project 'myproj', please select a unique name.` 
2. The name of your app is not valid. You receive a similar error message that contains: `An application name must consist of lower case alphanumeric characters, '-' and must start with an alphabetic character and end with an alphanumeric character.` 
3. If the image that you referenced does not exist, the app create does not complete and an error occurs. You receive a similar error message that contains: `Unable to pull the image`.
4. If you do not have the permissions to access the referenced image, the app create does not complete and an error occurs. You receive a similar error message that contains:   `Unable to pull the image`. 
5. The memory or cpu setting is not valid. You receive a similar error message that contains: `memory parameter must be between 128Mi and 32Gi` or `cpu parameter must be between .01 and 8.0`.

{: tsResolve}
Try one of these solutions.

1. To determine if the name of your app is unique within the project, use the `ibmcloud ce app list` command to list all defined apps and check whether an app with the same name exists. If an app with the same name exists, use the `ibmcloud ce app  delete --name APP_NAME` to delete the old app. The name of the app must be unique within your project. 
2. To confirm that the name of your app is valid, check that the name of your app consists of lower case alphanumeric characters, '-', and that the name starts and ends with an alphabetic character. 
3. To confirm that the image for your app exists, review the error message for information about the failure.  

    a. To deploy applications in {{site.data.keyword.codeengineshort}}, you need to first create a container image that has all of the runtime artifacts your application needs in order to run, such as runtime libraries. You can use many different methods to create the image, including building your app from source code by using the [build container images](/docs/codeengine?topic=codeengine-plan-build) feature available in {{site.data.keyword.codeengineshort}}. Your image can be downloaded from either a public or private image registry. For more information about accessing private registries, see [Adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).

    b. If using the `app create` command in the {{site.data.keyword.codeengineshort}} CLI, specify the name of the image that is used for your application by using the format `REGISTRY/NAMESPACE/REPOSITORY:TAG` where `REGISTRY` and `TAG` are optional. If `REGISTRY` is not specified, the default is `docker.io`. If `TAG` is not specified, the default is `latest`. For more information about the format to use to specify the repository for your image, see the [`app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. 
    
4. To confirm that you have access the referenced image, verify the location of your image and confirm that you have permissions to access the image.  
  * If the image is located in a container image registry, such as Docker Hub or {{site.data.keyword.registryfull_notm}}, check that you have added registry access to {{site.data.keyword.codeengineshort}} and that you are using the correct image registry access secret.  For more information about working with images in a container image registry, see [adding access to a private container registry](/docs/codeengine?topic=codeengine-add-registry).  
  * If the image is located in a Git code repository, such as GitHub or GitLab, check that you have created your repository access and that you are using the correct Git repository access secret. For more information about working with images in a Git code repository, see [accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).
5. If you specify the `--memory` or `--cpu` option with the `app create` command , confirm that you are using valid values. In the following command, the values that are specified for `--memory` and `--cpu` are not valid; for example,  

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

    To fix the errors, set the `--memory` option between 128 Mi and 32 Gi, and set the `--cpu` option between .01 and 8.0 vCPU. 
    
For more information about deploying apps, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

## Why doesn't my app ever become ready?   
{: #ts-app-neverready}
{: troubleshoot}

{: tsSymptoms}
After you deploy an app, the app does not achieve a ready status.

{: tsCauses}
By default, {{site.data.keyword.codeengineshort}} apps listen for incoming connections on port `8080`. Your app might listen on a different port if you receive the following error message:

```
Internal error:
RevisionFailed: Revision "myapp-1" failed with message: Initial scale was never achieved
```
{: screen}

{: tsResolve}
If your app listens on a port other than port `8080`, deploy your app by using the [`ibmcloud ce app create`](/docs/codeengine?topic=codeengine-cli#cli-application-create) command in the CLI and use the `--port` option on this command to specify the port.

## How do I get logs for my app? (CLI) 
{: #ts-app-gettinglogs-cli}
{: troubleshoot}

{: tsSymptoms}
Your app isn't behaving as expected and you want to look at the logs to see if any messages are generated to help you debug the problem. 

{: tsCauses}
You can display the logs of an app to view app output. Logs can be helpful to troubleshoot problems when running apps.   

{: tsResolve}
You can display logs of all of the instances of an app or or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

1. Use the [`ibmcloud ce app list `](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to list all of your defined apps; for example,
 
     ```
    ibmcloud ce app list  
    ```
    {: pre}

2. Use the [`ibmcloud ce app get`](/docs/codeengine?topic=codeengine-cli#cli-application-list) command to get the details of your app, including the name of the instances for the app; for example,
 
  ```
  ibmcloud ce app get --name myapp  
  ```
  {: pre}

  **Example output** 

  ```
  Getting application 'myapp'...
  OK

  Name:          myapp

  URL:           https://myapp.23c3366c-68cf.us-south.codeengine.appdomain.cloud
  Console URL:   https://cloud.ibm.com/codeengine/project/us-south/23c3366c-68cf-4b22-a234-99f0b3f7aafc/application/myapp/configuration
  [...]

  Instances:
    Name                                       Running  Status   Restarts  Age
    myapp-abcd5-1-deployment-6fccbf7c7f-mj9mf  2/2      Running  0         26s
    myapp-abcd5-1-deployment-6fccbf7c7f-xvmt6  1/2      Running  0         3m
  ```
  {: screen}

3. Display the logs of your app. 

  * To display the logs of a specific instance of your app, use the [`ibmcloud ce app logs --instance INSTANCE_NAME`](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command; for example,
  
    ```
    ibmcloud ce app logs --instance myapp-abcd5-1-deployment-6fccbf7c7f-mj9mf
    ```
    {: pre} 
      
    **Example output** 

    ```
    Logging application instance 'myapp-abcd5-1-deployment-6fccbf7c7f-mj9mf'...
    OK

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
    Getting application 'myapp'...
    Getting revisions for application 'myapp'...
    Getting instances for application 'myapp'...
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-abcd5-1-deployment-6fccbf7c7f-mj9mf:
    Server running at http://0.0.0.0:8080/

    myapp-abcd5-1-deployment-6fccbf7c7f-xvmt6:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}



