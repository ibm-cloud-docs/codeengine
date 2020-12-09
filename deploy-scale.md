---

copyright:
  years: 2020
lastupdated: "2020-12-09"

keywords: code engine, application, app, http requests

subcollection: codeengine

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
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Configuring application scaling
{: #app-scale}


  
## Scaling your application with the CLI
{: #scale-app-cli}

You can control the maximum and minimum number of running instances of your app by changing the values of the `--min-scale` and `--max-scale` options by using the `application create` or `application update` command.

To observe application scaling from the {{site.data.keyword.codeengineshort}} CLI,

1. Call the application. 

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

2. Run the `application get` command to display the status of your application. Look for the value for `Running instances`. In this example, the app has `1` running instance. For example,

    ```
    ibmcloud ce application get -name myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
      Age:                46s
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  30s
      Ready                true  27s
      RoutesReady          true  27s

   Instances:
   Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-1-deployment-75b46dcf64-jp8fp  2/2      Running  0         80s
      myapp-a5yp2-2-deployment-65766594d4-qp8sv  2/2      Running  0         47s
   ```
   {: screen}

  Wait a few minutes, as it can take a few minutes for your app to scale to zero. 
  {: note}

3. Run the `application get` command again and notice that the value for `Running instances` scaled to zero. When the application is finished running, the number of running instances automatically scales to zero, if the `--min-scale` option is set to `0`, which is the default value. For example,

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]

   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
    Age:                12m
    Traffic:            100%
    Image:              ibmcom/hello (pinned to 548d5c)
    Running Instances:  0

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  10m
      Ready                true  10m
      RoutesReady          true  10m

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-2-deployment-65766594d4-lnpgk  1/2      Running  0         5m38s
   ```
   {: screen}

4. Call the application again to scale from zero:

   ```
   curl https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   ```
   {: pre}

5. Run the `application get` command again and notice that the value for `Running instances` scaled up from zero. For example,

    ```
    ibmcloud ce application get -n myapp
    ```
    {: pre}

   **Example output**
   
   ```
   Getting application 'myapp'...
   OK

   Name:          myapp
   [...]
 
   URL:           https://myapp.a4e12aca-b35f.us-south.codeengine.appdomain.cloud
   Console URL:   https://cloud.ibm.com/codeengine/project/us-south/abcd2aca-abcd-abcd-bd08-57cb7fe8396a/application/myapp/configuration

   Environment Variables:
      Type     Name    Value
      Literal  TARGET  Stranger
   Image:                  ibmcom/hello
   Resource Allocation:
      CPU:     1
      Memory:  1Gi

   Revisions:
   myapp-a5yp2-2:
      Age:                13m
      Traffic:            100%
      Image:              ibmcom/hello (pinned to 548d5c)
      Running Instances:  1

   Runtime:
      Concurrency:         100
      Maximum Scale:       10
      Minimum Scale:       0
      Timeout:             300

   Conditions:
      Type                 OK    Age  Reason
      ConfigurationsReady  true  13m
      Ready                true  13m
      RoutesReady          true  13m

   Instances:
      Name                                       Running  Status   Restarts  Age
      myapp-a5yp2-2-deployment-65766594d4-hj6c5  2/2      Running  0         22s
   ```
   {: screen}
