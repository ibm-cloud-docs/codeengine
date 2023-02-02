---

copyright:
  years: 2023
lastupdated: "2023-02-02"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials, secrets

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Debugging service bindings
{: #troubleshoot-servicebindings}
{: troubleshoot}

Use the tips to learn how to troubleshoot {{site.data.keyword.codeenginefull}} service bindings.
{: shortdesc}

## Limits to consider 
{: #ts-sb-limits}

When you create service bindings with {{site.data.keyword.codeengineshort}}, secrets are created. Every new service binding that does not reuse a service credential creates a secret. The maximum number of secrets per project is 100 secrets.

For more information about limits for secrets, see [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Be sure to also consider limits for the specific service instance that you are binding to.
{: important}

For more information about service bindings, see [Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding).

## Listing service bindings  
{: #ts-sb-listing}

You can list service bindings that are set for a {{site.data.keyword.codeengineshort}} app or job. 

From the console, use one of the following ways. 
* After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. From the Overview page, click **Service bindings**. This view displays all service bindings for the selected project. 
* View existing service bindings to a specific app or job from the specific {{site.data.keyword.codeengineshort}} app or job page in the console. To view service bindings within the context of your app or job, go to the **Service bindings** tab for your specific app or job. You can also work with service bindings for your app from this view. 

With the CLI, use the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command or the [**`ibmcloud ce job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to display service bindings from the context of your app or job. 

For example, suppose the `myapp` application is bound to an {{site.data.keyword.cos_full_notm}} service instance. Use the **`application get`** command to list the services that are bound to this app. 

```txt
ibmcloud ce application get -n myapp
```
{: pre}

Example output

```txt 
Run 'ibmcloud ce application events -n myapp' to get the system events of the application instances.
Run 'ibmcloud ce application logs -f -n myapp' to follow the logs of the application instances.
OK

Name:               myapp
ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
Project Name:       myproject
Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
Age:                26h  
Created:            2023-01-31T13:03:34-05:00 
URL:                https://myapp.4svg40kabcd.us-south.codeengine.appdomain.cloud
Cluster Local URL:  http://myapp.4svg40kabcd.svc.cluster.local
Console URL:        https://cloud.ibm.com/codeengine/project/us-south/01234567-abcd-abcd-abcd-abcdabcd1111/application/myapp/configuration
Status Summary:  Application deployed successfully

Environment Variables:    
  Type                   Name                                     Value  
  Secret full reference  CLOUD_OBJECT_STORAGE_=service-key-z2z59    
  Literal                CE_APP                                   myapp  
  Literal                CE_DOMAIN                                us-south.codeengine.appdomain.cloud  
  Secret key reference   CE_SERVICES                              ce-services.app_myapp  
  Literal                CE_SUBDOMAIN                             4svg40kabcd  
Image:                  icr.io/codeengine/helloworld  
Resource Allocation:
CPU:                1
Ephemeral Storage:  400M
Memory:             4G

Revisions:
  myapp-00002:    
    Age:                26h  
    Latest:             true  
    Traffic:            100%  
    Image:              icr.io/codeengine/helloworld (pinned to 1cee99)  
    Running Instances:  0 

Runtime:
    Concurrency:    100
    Maximum Scale:  10
    Minimum Scale:  0
    Timeout:        300

Conditions:
    Type                 OK    Age  Reason
    ConfigurationsReady  true  52s
    Ready                true  26s
    RoutesReady          true  26s

Service Bindings:    
  Name                     ID                                    Service Instance  Service Type          Role / Credential  Environment Variable Prefix  Age  
  ce-service-access-wcfap  e04f4cbe-abcd-abcd-abcd-0ec858d33b82  Blueprint-basic   cloud-object-storage  Writer             CLOUD_OBJECT_STORAGE         26h  
```
{: screen}



