
---

copyright:
  years: 2020
lastupdated: "2020-09-09"

keywords: code engine, configmap, secret

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Setting up and using secrets and configmaps
{: #configmap-secret} 

Learn how to work with secrets and configmaps in {{site.data.keyword.codeengineshort}}. In {{site.data.keyword.codeengineshort}}, you can store your information as key-value pairs in secrets or configmaps that can be consumed by your job or application by using environment variables. 
{: shortdesc}

## What are secrets and configmaps and why would I use them? 
{: #configmapsec-whatwhy}

In {{site.data.keyword.codeengineshort}}, both secrets and configmaps are key-value pairs and when mapped to environment variables, are set such that they have a name that corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

A *configmap* provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment so that updates to the values can be made without changing your apps or jobs. You can create and work with configmaps from the console or from the CLI.

A *secret* provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. With secrets, you get the same decoupling that configmaps offer, but unlike configmaps, secrets are stored securely to ensure that your information remains private. Note that anyone who is authorized to your project can also view your secrets so be sure that you know the secret information is shared with those users. Secrets contain information in key-value pairs. You can create and work with secrets from the console or from the CLI.

Since secrets and configmaps are similar entities (except secrets are stored more securely), the way you interact and work with secrets and configmaps is also very similar.  

## Creating configmaps
{: #configmap-create}

Create configmaps with {{site.data.keyword.codeengineshort}}.
{: shortdesc}



### Creating a configmap with the CLI
{: #configmap-create-cli}

Create configmaps with the  {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

There are multiple ways to populate a configmap. You can do it by specifying the key-value pairs directly on the command line, or you can point to a file. 

Before you begin:
   * Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
   * [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).


1. Create a configmap with the `configmap create` command in one of the following ways: 

    * Create a configmap directly on the command line by using the `--from-literal` option. For example: 

        ```
        ibmcloud ce configmap create --name myliteralconfigmap --from-literal TARGET=yellow
        ```
        {: pre}

    * Create a configmap by pointing to a file that contains the key-value pair using the `--from-file` option. For this example, let's use a file that is named `configmapcolors.txt` which contains the text `blue, green, red`. The following example command uses the `--from-file KEY=FILE` format with the `configmap create` command: 

        ```
        ibmcloud ce configmap create --name mycolorconfigmap --from-file TARGET=configmapcolors.txt
        ```
        {: pre}

    When creating (or updating) a configmap from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when using a file to specify configmap values, *all* of the contents within the file is the value for the key-value pair. When using the option format of `--from-file KEY=FILE` the `KEY` is name of the environment variable that is known to your job or app. When using the option format of `--fromfile FILE`, where `FILE` is the name of the environment variable that is known to your job or app. 
    {: important}

2. Now that configmaps are created, use the `configmap list` command to list all configmaps in your project or use the `configmap get` command to display details about a specific configmap. For example:

    ```
    ibmcloud ce configmap get --name mycolorconfigmap
    ```
    {: pre}

   **Example output**
   
   ```
    Successfully retrieved configmap 'mycolorconfigmap'.

    Name:        mycolorconfigmap
    ...
    Data:
    ---
    TARGET: blue, green, red
   ```
   {: screen}

## Using configmaps 
{: #configmap-using}

After defining a configmap, your jobs or apps can consume and use the information stored in the configmap. 
{: shortdesc}



### Using configmaps with the CLI 
{: #configmap-using-cli}

Use defined configmaps with jobs or apps. Let's use the configmaps that were previously defined with the CLI with an application.

1. [Deploy an app](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cli). For this example, create an app that uses the [`Hello`](https://hub.docker.com/r/ibmcom/hello) image in Docker Hub. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `"Hello ${TARGET}"`. If this environment variable is empty, `"Hello World"` is returned. 

    ```
    ibmcloud ce app create --name myhelloapp --image ibmcom/hello 
    ```
    {: pre}

   When you call the `myhelloapp` app, the output is `Hello World`.  

2. Update the app to use the previously defined `mycolorconfigmap` configmap. 

    From the CLI, to use a defined configmap with an application, specify the `--env-fromconfigmap` option on the `app create` or `app update` CLI commands. Similarly, to use a configmap with a job, specify the `--env-fromconfigmap` option on the `jobdef create`, `jobdef update`, `job run`, or `job update` CLI commands. 
    {: tip}

    ```
    ibmcloud ce app update --name myhelloapp --env-from-configmap mycolorconfigmap
    ```
    {: pre}

3. Call the application again. This time, the app returns `Hello blue, green, red` which is the value specified in the `mycolorconfigmap` configmap.

    ```
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    Hello blue, green, red
   ```
   {: screen}

5. Update the app again to use the `myliteralconfigmap` configmap. 

   When updating an application or job with an environment variable that fully references a configmap to fully reference a different configmap, full references override other full references in the order in which they are set (the last referenced set overrides the first set).
   {: note}

    ```
    ibmcloud ce app update --name myhelloapp --env-from-configmap myliteralconfigmap
    ```
    {: pre}

   **Example output**
   
   ```
    Updating application 'myhelloapp'
    Application 'myhelloapp' updated to latest revision and is available at URL:
    https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

6. Call the application again. This time, the app returns `Hello yellow` which is the value specified in the `myliteralconfigmap` configmap.

    ```
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    Hello yellow
     ```
   {: screen}

7. To change the value of a key-value pair in a configmap, use the `configmap update` command. Let's update the `configmap-fromlit` configmap to change the value of the `TARGET` key from `Sunshine` to `Stranger`.

    ```
    ibmcloud ce configmap update --name myliteralconfigmap --from-literal "TARGET=Stranger"
    ```
    {: pre}

8. Restart the application and call the application again.  This time, the app returns `Hello Stranger` which is the updated value specified in the `myliteralconfigmap` configmap.

    ```
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    Hello Stranger
   ```
   {: screen}

To summarize, you have completed basic scenarios to demonstrate using configmaps with an app by referencing a full configmap and updating keys within a configmap.

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


## Creating secrets
{: #secret-create}

Use secrets to provide sensitive information to your apps or jobs. Secrets are defined in key-value pairs and the data stored in secrets is encoded.
{: shortdesc}



### Creating a secret with the CLI
{: #secret-create-cli}

There are multiple ways to populate a secret. You can do it by specifying the key-value pairs directly on the command line, or you can point to a file. 

With the CLI, you can create a secret where the data is pulled from a file, or specified directly  with the `secret create` command. Secrets that are used to store simple name-value pairs are called *generic secrets*. Secrets that store information about how to authenticate to a container registry are called [registry access secrets (`imagePullSecret`)](/docs/codeengine?topic=codeengine-plan-image).

This section describes creating generic secrets that can be consumed by jobs or apps as environment variables.

Before you begin:

   * Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kn-install-cli) environment.
   * [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. Create a generic secret with the `secret create` command in one of the following ways:   

    * Create a secret directly on the command line by using the `--from-literal` option. For example: 

        ```
        ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My literal secret"
        ```
        {: pre}

    * Create a secret by pointing to a file that containes the key-value pair using the `--from-file` option. For this example, let's use a file that is named `secrets.env` which contains `my little secret1`. 
    
        * The following example uses the `--from-file KEY=FILE` format with the `secret create` command:  

            ```
            ibmcloud ce secret create --name mysecretmsg --from-file TARGET=secrets.env
            ```
            {: pre}

        * The following example command uses the `--from-file FILE` format with the `secret create` command.  In this example `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to our job.

            ```
            ibmcloud ce secret create --name mysecretmsg2  --from-file TARGET
            ```
            {: pre}

    When creating (or updating) a secret from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when using a file to specify secret values, *all* of the contents within the file is the value for the key-value pair. When using the option format of `--from-file KEY=FILE` the `KEY` is name of the environment variable that is known to your job or app. When using the option format of `--fromfile FILE`,  where `FILE` is the name of the environment variable that is known to your job or app.
    {: important}

3.  Now that secrets are created, use the `secret list` command to list all secrets in your project or use the `secret get` command to display details about a specific secret. For example:

    ```
    ibmcloud ce secret get --name mysecretmsg2
    ```
    {: pre}

   **Example output**
   
   ```
    Successfully retrieved secret 'mysecretmsg2'.
    ...

    Data:
    ---
    TARGET: bXkgYmlnIHNlY3JldDI=
   ```
   {: screen}

Notice that the value of the key `TARGET` for this secret is encoded.  

## Using secrets 
{: #secret-using}

After defining your secret, your jobs or apps can consume and use the information stored in the secret. 
{: shortdesc}



### Using secrets with the CLI 
{: #secret-using-cli}

Use defined secrets with jobs or apps. Let's use secrets that were previously defined with the CLI with a job.

To use a secret with a job with the CLI, specify the `--env-fromsecret` option on the `jobdef create`, `jobdef update`, `job run` or `job update` commands. Similarly, to reference a secret from an application with the CLI, specify the `--env-from-secret` option on the `app create` or `app update` commands.  

This scenario uses the CLI to run a job that references a secret. 

1. [Create a job definition and run a job](/docs/codeengine?topic=codeengine-kn-job-deploy). For this example, create a {{site.data.keyword.codeengineshort}} job definition that uses the [`testjob`](https://hub.docker.com/r/ibmcom/testjob) image in Docker Hub and then run a job using the job definition. When a request is sent to this sample job, the job reads the environment variable `TARGET` and prints `"Hello ${TARGET}!"`. If this environment variable is empty, `"Hello World!"` is returned. 

    a. Create the job definition.

    ```
    ibmcloud ce jobdef create --name myjobdef1 --image ibmcom/testjob 
    ```
    {: pre}

2. Run the job based on the `myjobdef2` job definition. 

    ```
    ibmcloud ce job run --name myjob1 --jobdef myjobdef1
    ```
    {: pre}

3. Display the job logs of the `myjob1` job. In this example, the job logs display the output of `"Hello World!"`. 

    ```
    ibmcloud ce job logs --name myjob1
    ```
    {: pre}

   **Example output**
   
   ```
    Hello World!
   ```
   {: screen}

3. Update the job to reference the previously defined `mysecretmsg` secret. 

    ```
    ibmcloud ce job run --name myjob2 --jobdef myjobdef1 --env-from-secret mysecretmsg 
    ```
    {: pre}

4.  Display the job logs of the `myjob2` job. This time, the job logs display the output of `"Hello ${TARGET}!"` where the value for `TARGET` was specified by using an environment variable with a secret.

    ```
    ibmcloud ce job logs --name myjob2
    ```
    {: pre}

   **Example output**
   
   ```
    Hello my little secret1!
   ```
   {: screen}

5. Run the job again and specify to use the `myliteralsecret` secret for this job run.  

   When updating a job or app with an environment variable that fully references a secret to fully reference a different secret, full references override other full references in the order in which they are set (the last referenced set overrides the first set).
   {: note}

    ```
    ibmcloud ce job run --name myjob3 --jobdef myjobdef1 --env-from-secret myliteralsecret
    ```
    {: pre}

6. Display the job logs of the `myjob3` job. This time, the job logs display `Hello My literal secret!!` which is the value specified in the `mysecret-fromlit` secret.

    ```
    ibmcloud ce job logs --name myjob3
    ```
    {: pre}

   **Example output**
   
   ```
    Hello My literal secret!
     ```
   {: screen}

7. To change the value of key-value pair in a secret, use the `secret update` command.  Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My literal secret` to `My new literal secret`.

    ```
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new literal secret"
    ```
    {: pre}

8. Run the job again and then display the job logs of the `myjob4` job to view the result.  This time, the job returns `My new literal secret!!` which is the updated value specified in the `myliteralsecret` secret.

    ```
    ibmcloud ce job run --name myjob4 --jobdef myjobdef1 --env-from-secret myliteralsecret 
    ```
    {: pre}

   **Example output** (from the `job logs` command)
   
   ```
    Hello My new literal secret!
   ```
   {: screen}

To summarize, you have completed basic scenarios to demonstrate using secrets with a job by referencing a full secret and updating keys within a secret.

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


## Deleting secrets and configmaps 
{: #configmapsecret-delete}

When you no longer need a configmap or secret, you can delete it. 
{: #shortdesc} 



### Deleting secrets and configmaps with the CLI
{: #configmapsecret-delete-cli}

* To delete a configmap with the CLI, use the [`configmap delete`](/docs/codeengine?topic=codeengine-kn-cli#cli-configmap-delete) command. 

    ```
    ibmcloud ce configmap delete --name myconfigmap 
    ```
    {: pre}

    **Example output**

    ```
    Deleting configmap 'myconfigmap'...
    OK
    Successfully deleted configmap 'myconfigmap'
    ```
    {: screen}

* To delete a secret with the CLI, use the [`secret delete`](/docs/codeengine?topic=codeengine-kn-cli#cli-secret-delete) command. 

    ```
    ibmcloud ce secret delete --name mysecret 
    ```
    {: pre}

    **Example output**

    ```
    Deleting secret mysecret...
    OK
    Successfully deleted secret 'mysecret'.
    ```
    {: screen}

## Next steps
{: #configmapsecret-next}

When working with secrets and configmaps in the CLI, you can reference full secrets and configmaps or you can reference individual keys in secrets and configmaps. For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


