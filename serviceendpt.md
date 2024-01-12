---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-11"

keywords: endpoints, virtual private endpoints, public endpoints, private endpoints, service endpoints

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Using service endpoints with {{site.data.keyword.codeengineshort}} 
{: #serviceendpt}

All {{site.data.keyword.codeenginefull}} projects offer integration with {{site.data.keyword.cloud}} service endpoints. This support gives you the ability to connect from your classic infrastructure  to {{site.data.keyword.codeengineshort}} workloads and stay within the {{site.data.keyword.cloud_notm}} network. 
{: shortdesc}

You can control the visibility of {{site.data.keyword.codeengineshort}} workloads and specify whether to expose the application or function to public or private endpoints. An application or function that is configured for `visibility = private`, is accessed through service endpoints.  Applications or functions that are accessed through a service endpoint do not leave the IBM network and stay within the {{site.data.keyword.cloud_notm}} network. 

## Public endpoints
{: #serviceendpt-public-endpoints}

Public endpoints provide a connection to your deployment on the public network. At provision time, a public endpoint is the default option for all deployments. Your environment needs to have internet access to connect to a deployment.

## Private endpoints
{: #serviceendpt-private-endpoints}

A deployment with a service endpoint on the private network gets an endpoint that is not accessible from the public internet. All traffic is routed to hardware dedicated to {{site.data.keyword.codeengineshort}} deployments and remains on the {{site.data.keyword.cloud_notm}} private network. All traffic to and from this endpoint is free and does not incur charges on the condition that the traffic remains in {{site.data.keyword.cloud_notm}}. After your environment has access to the {{site.data.keyword.cloud_notm}} private network, an internet connection is not required to connect to your deployment.

{{site.data.keyword.codeengineshort}} application deployments with private endpoints are reachable from any account within the private network and access to each instance requires authentication. To restrict this access to specific IP addresses, or ranges of IP addresses, configure [allowlists](/docs/cloud-databases?topic=cloud-databases-allowlisting). 
{: .important}

## Enabling service endpoints
{: #serviceendpt-enabling-service-endpoints}

If you want to use connections over the public internet, you do not have to enable service endpoints on your {{site.data.keyword.cloud_notm}} account. If you want to enable private networking on your deployments, you need to follow the instructions in the Service Endpoint documentation under [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

Currently, enabling service endpoints on your account is a manual step that is handled by support ticket. After you complete the [request](/docs/account?topic=account-vrf-service-endpoint#service-endpoint), you can check on the status of the ticket by going to your [Support](https://cloud.ibm.com/unifiedsupport/cases/manage) page on {{site.data.keyword.cloud_notm}}

## Managing {{site.data.keyword.codeengineshort}} resources securely by using service endpoints
{: #serviceendpt-ce-manageresources}


1. Specify a {{site.data.keyword.codeengineshort}} project to use the private endpoint. You can configure a {{site.data.keyword.codeengineshort}} project to use the private endpoint only with the CLI. To create a project, use the  [**`ibmcloud ce project create`**](/docs/codeengine?topic=codeengine-cli#cli-project-create) command with the `--endpoint=private` option.

    ```txt
    ibmcloud ce project create --name myproject --endpoint=private 
    ```
    {: pre}

    Wait until the project is in `active` status. With the CLI, you can confirm the project status by using the  [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command.

    If you want an existing {{site.data.keyword.codeengineshort}} project to use the private endpoint, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command with the `--endpoint=private` option.

    ```txt
    ibmcloud ce project select --name myproject --endpoint=private
    ```
    {: pre}

    For the **`project create`** and **`project select`** commands, if the `--endpoint` option is not explicitly specified, the behavior is determined by the system. If the {{site.data.keyword.cloud_notm}} CLI is connected to `private.cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `private`. If the {{site.data.keyword.cloud_notm}} CLI is connected to `cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `public`.
    {: important}

2. If you did not create a new project and you selected an existing project, and you want your app to only be visible to the private endpoint, confirm the existing project supports applications with private visibility. Use the  [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command to verify the output for `Application Private Visibility Supported` is set to `true`. If the value is `false`, [contact IBM support](/docs/codeengine?topic=codeengine-get-support) to enable this capability within your existing project.

    ```txt
    ibmcloud ce project get -n myproject
    ```
    {: pre}

    Example output

    ```txt 
    Getting project 'myproject'...
    OK

    Name:                                      myproject  
    ID:                         abcdabcd-abcd-abcd-abcd-f1de4aab5d5d
    Status:                                    active  
    Enabled:                                   true  
    Application Private Visibility Supported:  false  
    Selected:                                  true  
    Region:                                    us-south 
    Resource Group:             default
    Service Binding Service ID: ServiceId-1234abcd-abcd-abcd-1111-1a2b3c4d5e6f
    Age:                        52d 
    Created:                                   Tue, 28 Sep 2021 05:12:16 -0500  
    Updated:                                   Tue, 28 Sep 2021 05:12:19 -0500  

    Quotas:    
    Category                                  Used  Limit  
    App revisions                             1     60  
    Apps                                      1     20  
    Build runs                                1     100  
    Builds                                    2     100  
    Configmaps                                2     100  
    CPU                                       0     64  
    Ephemeral storage                         0     256G  
    Instances (active)                        0     250  
    Instances (total)                         0     2500  
    Job runs                                  0     100  
    Jobs                                      0     100  
    Memory                                    0     256G  
    Secrets                                   6     100  
    Subscriptions (cron)                      0     100  
    Subscriptions (IBM Cloud Object Storage)  0     100  
    Subscriptions (Kafka)                     0     100
    ```
    {: screen}

3. Create an application or function that is only visible to the private endpoint. Use the  [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or the [**`ibmcloud ce function create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create) command with the `--visibility=private` option. Alternatively, you can use the console to create or update an app or function and set the [visibility of your app](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).

    ```txt
    ibmcloud ce application create -n myapp --visibility=private
    ```
    {: pre}



## Accessing your app securely with service endpoints
{: #serviceendpt-ce-access-app}


1. From your {{site.data.keyword.codeengineshort}} project, confirm that your application is configured with a `visibility=private` setting. See [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-private). 

2. Retrieve the URL of the {{site.data.keyword.codeengineshort}} application that is exposed to the private network. The URL is in the following format: `<app>.<uuid>.private.<region>.codeengine.appdomain.cloud`.
    * From the {{site.data.keyword.codeengineshort}} console, go to the **Domain mappings** tab for your application to view the visibility of an app and its available URLs. 
    * From the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli), use the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command with the `--option url` option. In the following example, because the visibility of the `myapp` is set to  `visibility=private`, specifying `--option url` with this command outputs the URL to the private network. 

        ```txt
        ibmcloud ce application get -n myapp -output url
        ```
        {: pre}

        Example output

        ```txt 
        http://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
        ```
        {: screen}

3. Call the application. The `myapp` application is a simple Hello World application. When you curl the `myapp` app, `Hello World` is returned.

   ```txt
   curl http://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
    ```
   {: pre}


## Accessing your function securely with service endpoints
{: #serviceendpt-ce-access-fun}


1. From your {{site.data.keyword.codeengineshort}} project, confirm that your function is configured with a `visibility=private` setting. See [Deploying your function with a private endpoint](/docs/codeengine?topic=codeengine-fun-work#fun-endpoint-private). 

2. Retrieve the URL of the {{site.data.keyword.codeengineshort}} function that is exposed to the private network. The URL is in the following format: `<function>.<uuid>.private.<region>.codeengine.appdomain.cloud`.
    * From the {{site.data.keyword.codeengineshort}} console, go to the **Domain mappings** tab for your function to view the visibility of the function and its available URLs. 
    * From the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli), use the [**`ibmcloud ce function get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command. In the following example, because the visibility of the `myfunction` is set to  `visibility=private`, this command outputs the URL to the private network. 

        ```txt
        ibmcloud ce function get -n myfunction
        ```
        {: pre}

        Example output

        ```txt 
        http://myfunction.1abc23def19.private.us-south.codeengine.appdomain.cloud
        ```
        {: screen}










