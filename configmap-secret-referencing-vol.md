---

copyright:
  years: 2021
lastupdated: "2021-02-04"

keywords: configmaps with code engine, secrets with code engine, key references with code engine, key-value pair with code engine, referencing secrets with code engine, referencing configmaps with code engine

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
{:swift-ios: .ph data-hd-programlang='iOS Swift'}
{:swift-server: .ph data-hd-programlang='server-side Swift'}
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


# Referencing secrets and configmaps as mounted files 
{: #secretcm-reference-mountedfiles}

In {{site.data.keyword.codeengineshort}}, after you create secrets and configmaps, the information that is stored as key-value pairs can be consumed by your application as a mounted file. 
{: shortdesc}

You can work with configmaps and secrets with the CLI, but this capability is not currently available from the console.
{: important} 

Working with secrets and configmaps as mounted files is similar to working with secrets and configmaps as environment variables. 

When working with secrets, data is saved as an encoded string, but the data is unencoded when it is added to the environment as an environment variable or as a mounted file. 


## Referencing a secret as a mounted file with the CLI
{: #secret-reference-mount-file-cli}

In this scenario, let's create a secret and then reference the secret as a mounted file when running an application, which uses the `ibmcom/ce-secret-vol` image. 

The sample image, `ibmcom/ce-secret-vol`, reads each file in the `/mysecrets` directory and prints the name of the file and its contents to standard output for each request, so that the output is contained in the app logs. For more information about this sample application, see the [secrets as volumes (`secrets-vol`) sample in the {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/blob/master/secrets-vol/secret.go).

While this scenario uses a secret, you can use the same steps to reference a configmap as a mounted file by substituting `configmap` for `secret` in the commands. 
{: tip} 

1. Create a secret, named `mysecret`, and specify the key-value pairs for the secret by using the `--from-literal` option; for example: 

    ```
    ibmcloud ce secret create -n mysecret --from-literal apikey=abcdefgh 
    ```
    {: pre}

2. Create the `myapp` application that uses the `ibmcom/ce-secret-vol` image. Use the `--mount-secret` option to mount or add the contents of the `mysecret` secret to the app in the `/mysecrets` directory. By specifying `--min-scale=1`, the app always has an instance that is running and does not scale to zero, which is useful when you view logs. For example, 

    ```
    ibmcloud ce app create --name myapp --image ibmcom/ce-secret-vol --mount-secret /mysecrets=mysecret --min-scale 1
    ```
    {: pre}

    **Example output**
    
    ```
    Creating application 'myapp'...
    [...]
    Run 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe ce application get -n myapp' to check the application status.
    OK
    ```
    {: screen}

3. Copy the domain URL from the previous output and call the application with `curl`; for example:

    ```
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

4. View the logs from your application. Because the `myapp` app uses the sample image, `ibmcom/ce-secret-vol`, the app reads each file in the `/mysecrets` directory and prints the name of the file (`apikey` is the name of the file in this example) and its contents to standard output for each request, so that the output is contained in the app logs. 

    ```
    ibmcloud ce app logs --app myapp
    ```
    {: pre}

    **Example output**
    
    ```
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-b3gxd-1-deployment-6f45dcf7f4-nw59z/user-container:
    Listening on port 8080
    apikey: abcdefgh
    ```
    {: screen}

5. Update the `mysecret` secret to change the value for the `apikey` key-value pairs; for example:  

    ```
    ibmcloud ce secret update -n mysecret --from-literal apikey=qrst 
    ```
    {: pre}

6. Call the application again. 

    ```
    curl https://myapp.4svg40kna19.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

7. View the logs from your application.

    ```
    ibmcloud ce app logs --app myapp
    ```
    {: pre}

    **Example output**
    
    ```
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-b3gxd-1-deployment-6f45dcf7f4-nw59z/user-container:
    Listening on port 8080
    apikey: abcdefgh
    apikey: qrst
    ```
    {: screen}

You have now added data that is stored in secrets (or configmaps) to your app as a mounted file, and then updated the data stored in the secret. The app did not require a restart to use the updated referenced secret.
