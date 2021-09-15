---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-15"

keywords: tutorial code engine, tutorial cloud object storage for code engine, tutorial cloud object storage, subscribing cloud object storage, subscribing cloud object storage for code engine, object storage, events, app, subscription, code engine

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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


# Subscribing to {{site.data.keyword.cos_short}} events
{: #subscribe-cos-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

With this tutorial, you can learn how to subscribe to {{site.data.keyword.cos_short}} events by using the {{site.data.keyword.codeenginefull}} CLI. 
{: shortdesc}

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. Event information is received as POST HTTP requests for applications and as environment variables for jobs.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports two types of event producers. 

**Cron**: The cron event producer is based on cron and generates an event at regular intervals. Use a cron event producer when an action needs to be taken at well-defined intervals or at specific times.

**{{site.data.keyword.cos_full_notm}}**: The {{site.data.keyword.cos_short}} event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform an action based on that change, perhaps consuming that new object.

**Before you begin**

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

The {{site.data.keyword.cos_short}} subscription event producer is not available in the `ca-tor` region. See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions) for more information about regions where {{site.data.keyword.codeengineshort}} is available.
{: important} 

Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage.
{: note}

## Determine your {{site.data.keyword.cos_short}} bucket and region 
{: #determine-cos-bucket-and-region}
{: step}

The {{site.data.keyword.cos_short}} event producer generates events based on operations on objects in {{site.data.keyword.cos_full_notm}} buckets. 
{: shortdesc}

To see the buckets and their associated regions by using the CLI,

1. Install the {{site.data.keyword.cos_short}} plug-in CLI.
   
    ```
    ibmcloud plugin install cloud-object-storage
    ```
    {: pre}

2. Create an {{site.data.keyword.cos_short}} resource instance. For example, create an {{site.data.keyword.cos_short}} resource that is named `mycloud-object-storage` using the IBM Cloud lite plan. 

    ```
    ibmcloud resource service-instance-create mycloud-object-storage cloud-object-storage lite global
    ```
    {: pre}

3. Display the details of the {{site.data.keyword.cos_short}} resource instance that you created. Use the details to get the CRN (Cloud Resource Name) number from your {{site.data.keyword.cos_short}} instance. The CRN number identifies which {{site.data.keyword.cos_short}} instance you want to use. The CRN number is the value of the `ID` field in the output of the `ibmcloud resource service-instance COS_INSTANCE_NAME` command. 

    ```
    ibmcloud resource service-instance mycloud-object-storage
    ```
    {: pre}

    **Example output**

    ```
    Name:                  mycloud-object-storage  
    ID:                    crn:v1:bluemix:public:cloud-object-storage:global:a/ab9d57f699655f028880abcd2ccdb524:910b727b-abcd-4a73-abcd-77c68bfeabcd::   
    GUID:                  910b727b-abcd-4a73-abcd-77c68bfeabcd   
    Location:              global   
    Service Name:          cloud-object-storage   
    Service Plan Name:     lite   
    Resource Group Name:   Default   
    State:                 active   
    Type:                  service_instance   
    Sub Type:                 
    Created at:            2020-10-14T19:09:22Z   
    Created by:            user@us.ibm.com   
    Updated at:            2020-10-14T19:09:22Z   
    ...
    ```
    {: screen}

    If you do not know your {{site.data.keyword.cos_short}} instance name, run `ibmcloud resource service-instances --service-name cloud-object-storage` to see a list of {{site.data.keyword.cos_short}} instances.

    If you do not have an {{site.data.keyword.cos_short}} instance, [create one](/docs/cloud-object-storage).

4. Configure your {{site.data.keyword.cos_short}} CRN that you found with the previous step to specify an {{site.data.keyword.cos_short}} instance to work with. Be sure to copy the entire number, starting with `crn:`.

    ```
    ibmcloud cos config crn --crn CRN_NUMBER
    ```
    {: pre}

    **Example output**

    ```
    Saving new Service Instance ID...
    OK
    Successfully stored your service instance ID.
    ```
    {: screen}

5. Identify a bucket to subscribe to. To see a list of buckets that are associated with your {{site.data.keyword.cos_short}} instance,

    ```
    ibmcloud cos buckets
    ```
    {: pre}


    To create a bucket,

        ```
    ibmcloud cos  bucket-create -bucket BUCKET_NAME
    ```
    {: pre}

6. Identify the location and plan of the {{site.data.keyword.cos_short}} bucket,
   
    ```
    ibmcloud cos bucket-location-get --bucket BUCKET_NAME
    ```
    {: pre}

    **Example output**

    ```
    Details about bucket mybucket:
    Region: us-south
    Class: Standard
    ```
    {: screen}

Your {{site.data.keyword.cos_short}} bucket must be a regional bucket located in the same region as your {{site.data.keyword.codeengineshort}} project.
{: note}

## Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}
{: #notify_mgr}
{: step}

Before you can create an {{site.data.keyword.cos_short}} subscription, you must assign the Notifications Manager role to a {{site.data.keyword.codeengineshort}} project. As a Notifications Manager, {{site.data.keyword.codeengineshort}} can view, modify, and delete notifications for an {{site.data.keyword.cos_short}} bucket.
{: shortdesc}

Only account administrators can assign the Notifications Manager role.
{: note}

1. Identify the {{site.data.keyword.codeengineshort}} project that you want to use. You can use the [**`ibmcloud ce project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command to display a list of projects. Use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context. For example, to select a project named `myproject`

    ```
    ibmcloud ce project select -n myproject
    ```
    {: pre}


2. Assign the Notification Manager role by using the [**`ibmcloud iam authorization-policy-create`**](/docs/account?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.

    For example, to assign the Notifications Manager role to a project named `myproject` for an {{site.data.keyword.cos_short}} instance named `mycosinstance`,

    ```
    ibmcloud iam authorization-policy-create codeengine cloud-object-storage "Notifications Manager" --source-service-instance-name PROJECT --target-service-instance-name COS-INSTANCE
    ```
    {: pre}

    After you assign the Notifications Manager role to your project, you can then create {{site.data.keyword.cos_short}} subscriptions for any regional buckets in your {{site.data.keyword.cos_short}} instance that are in the same region as your project. 

    The following table summarizes the options that are used with the **`iam authorization-policy-create`** command in this example. For more information about the command and its options, see the [**`ibmcloud iam authorization-policy-create`**](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create) command.

    | Command option           | Description      | 
    |------------------|------------------|
    | `codeengine` | The source service that can be authorized to access. |
    | `cloud-object-storage` | The target service that the source service can be authorized to access. |
    | `Notifications Manager` | The roles that provide access for the source service. |
    | `source-service-instance-name` | The name of the `codeengine` project that you want to authorize to access. |
    | `target-service-instance-name` | The name of the `cloud-object-storage` instance that you want to access. |
    {: caption="iam authorization-policy-create command components" caption-side="top"}

3. Verify that the Notifications Manager role is set.

    ```
    ibmcloud iam authorization-policies
    ```
    {: pre}

    **Example output**

    ```
    ID:                        abcd1234-a123-b456-bdd9-849e337c4460   
    Source service name:       codeengine   
    Source service instance:   1234abcd-b456-c789-a7c5-ef82e56fb24c   
    Target service name:       cloud-object-storage   
    Target service instance:   a1b2c3d4-cbad-567a-8cea-77c68bfe97c9   
    Roles:                     Notifications Manager 
    ```
    {: screen}

## Create your app
{: #create-app-cos}
{: step}

Create an application that is named `cos-app` with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command by using an image that is called `cos-listen`. To always have a running instance of `cos-app`, specify the `--min-scale=1` option. This app logs each event as it arrives.
{: shortdesc}

```
ibmcloud ce app create --name cos-app --image ibmcom/cos-listen --min-scale=1
```
{: pre}

Run `ibmcloud ce application get --name cos-app` to verify that your app is in a `Ready` state. The application is in a ready state if the status summary reflects that the application deployed successfully.

For more information about this app, see the [{{site.data.keyword.cos_full_notm}} readme file](https://github.com/IBM/CodeEngine/tree/main/cos-event){: external}.

## Create a subscription
{: #create-subscription-cos}
{: step}

After your app is ready, you can create an {{site.data.keyword.cos_short}} subscription so you can start receiving {{site.data.keyword.cos_short}} events with the [**`ibmcloud ce sub cos create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create) command.
{: shortdesc}

For example, create an {{site.data.keyword.cos_short}} subscription that is called `cos-sub`. This subscription forwards any type of bucket operation to an application that is called `cos-app`.

```
ibmcloud ce sub cos create --name cos-sub --destination cos-app --bucket mybucket --event-type all
```
{: pre}

Run the `ibmcloud ce sub cos get -n cos-sub` command to find information about your subscription.

**Example output**

By default, the [**`ibmcloud ce sub cos get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command returns two parts. The first part includes {{site.data.keyword.cos_short}} subscription-related information such as subscription name, destination, prefix, suffix, and event type. The second part includes resource-related event information about the {{site.data.keyword.cos_short}} subscription that can be used for debugging purposes. By default, event information is available for one hour after it occurs.

```
Getting COS event subscription 'cos-sub'...
OK
Name:          cos-sub
ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f   
Project Name:  myproject
Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111  
Age:           4m16s  
Created:       2021-02-01T13:11:31-05:00  
Destination:  App:cos-app 
Bucket:       mybucket  
EventType:    all       
Ready:        true  

Conditions:    
    Type            OK    Age  Reason  
    CosConfigured   true  38s    
    Ready           true  38s    
    ReadyForEvents  true  38s    
    SinkProvided    true  38s    

Events:        
    Type    Reason          Age  Source                Messages  
    Normal  CosSourceReady  39s  cossource-controller  CosSource is ready 
   
```
{: screen}


## Testing your subscription
{: #test-subscription-cos}
{: step}

1. Upload a `.txt` file to your bucket. You can use the [**`ibmcloud cos object-put`**](/docs/cloud-object-storage?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-upload-object) command to upload an object to a bucket or use the {{site.data.keyword.cos_short}} console.

   
    ```
    ibmcloud cos object-put --bucket BUCKET_NAME --key KEY
    ```
    {: pre}

2. View the processed event by using the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command.

    ```
    ibmcloud ce app logs --name cos-app
    ```
    {: pre}

    **Example output**

    This command returns log files that include information about the event that was forwarded to your destination app. From the following output, you can see that a `Write` operation was performed on the `.txt` object in the bucket named `mybucket`.

    ```
    Body: {"bucket":"mybucket","endpoint":"","key":"info_instruction.txt","notification":{"bucket_name":"mybucket","content_type":"text/plain","event_type":"Object:Write","format":"2.0","object_length":"1960","object_name":"info_instruction.txt","request_id":"103dd6f7-dd7b-4f49-86db-c2ff4b678b0a","request_time":"2021-02-11T16:57:42.373Z"},"operation":"Object:Write"} 
    ```
    {: screen}


By default, the **`subscription cos create`** command first checks to see whether the destination application exists. If the destination check fails because the app name that you provided does not exist in your project, the **`subscription cos create`** command returns an error. If you want to create a subscription without first creating the application, use the `--force` option. By using the `--force` option, the command bypasses the destination check. Note that the `Ready` field of the subscription shows `false` until the destination app is created. Then, the subscription moves to a `Ready: true` state automatically.

After the subscription is created, but before the **`subscription cos create`** command reports any results, the **`subscription cos create`** command repeatedly polls the subscription for its status to verify its readiness. This continuous polling for status lasts for 15 seconds by default before it times out. If the subscription status returns as `Ready:true`, it reports success, otherwise it reports an error. You can change the amount of time that the **`subscription cos create`** command waits before it times out by using the `--wait-timeout` option. You can also bypass the status polling by setting the `--no-wait` option to `false`.

For more information about headers and body, see [HTTP headers and body information for events](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos).

Note that subscriptions can affect how an application scales. For more information, see [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).


## Update your {{site.data.keyword.cos_short}} subscription
{: #update-subscription-cos}
{: step}

Now you know that your {{site.data.keyword.cos_short}} subscription was created successfully and that the {{site.data.keyword.cos_short}} subscription is ready to serve events, you can update the {{site.data.keyword.cos_short}} subscription with the [**`ibmcloud ce sub cos update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-update) command. For example, you can change your subscription to run only when specific operations happen on a subset of objects in the bucket.
{: shortdesc}

1. Update the {{site.data.keyword.cos_short}} subscription to forward events only when `delete` operations happen on files with a name prefix of `test`.

    ```
    ibmcloud ce sub cos update --name cos-sub --event-type delete --prefix test
    ```
    {: pre}

2. Run the [**`ibmcloud ce sub cos get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get) command to find information about your subscription.

    ```
    ibmcloud ce sub cos get --name cos-sub 
    ```
    {: pre}

    **Example output**

    In this output, you can see that the updated values for `Prefix` and `EventType` are displayed.

    ```
    Getting COS event subscription 'cos-sub'...
    OK
    Name:          cos-sub
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f   
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           4m16s  
    Created:       2021-02-01T13:11:31-05:00  
    Destination:  App:cos-app 
    Bucket:       mybucket  
    EventType:    delete 
    Prefix:       test 
    Ready:        true  

    Conditions:    
        Type            OK    Age  Reason  
        CosConfigured   true  24m    
        Ready           true  24m    
        ReadyForEvents  true  24m    
        SinkProvided    true  24m    

    Events:        
        Type    Reason          Age               Source                Messages  
        Normal  CosSourceReady  9s (x2 over 24m)  cossource-controller  CosSource is ready  
    
    ```
    {: screen}

3. Delete an object from your bucket that has the `test` prefix. For example, delete a file with `test2.txt` for the name (or key). You can use the [**`ibmcloud cos object-delete`**](/docs/cloud-object-storage?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-delete-object) command to delete an object from your bucket or use the {{site.data.keyword.cos_short}} console.

4. View the processed event by using the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) command.

    ```
    ibmcloud ce app logs --name cos-app
    ```
    {: pre}

    **Example output**

    This command returns log files that include information about the event that was forwarded to your destination app. From the following output, you can see that a `Write` operation was performed on the `.txt` object in the bucket named `mybucket`.

    ```
    Body: {"bucket":"mybucket","endpoint":"",""key":"test2.txt","notification":{"bucket_name":"mybucket","event_type":"Object:Delete","format":"2.0","object_length":"41","object_name":"test2.txt","request_id":"c1099857-f1f3-4d74-9ac4-8d374582f77d","request_time":"2021-09-15T15:22:01.205Z"},"operation":"Object:Delete"}
    ```
    {: screen}

## Clean up for {{site.data.keyword.cos_short}} tutorial
{: #clean-subscription-cos}
{: step}

Ready to delete your {{site.data.keyword.cos_short}} subscription and your app? You can use the [**`ibmcloud ce app delete`**](/docs/codeengine?topic=codeengine-cli#cli-application-delete) and the [**`ibmcloud ce sub cos delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete) commands.

To remove your subscription,

```
ibmcloud ce sub cos delete --name cos-sub
```
{: pre}

To remove your application,

```
ibmcloud ce app delete --name cos-app
```
{: pre}

