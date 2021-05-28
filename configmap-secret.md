---

copyright:
  years: 2021
lastupdated: "2021-05-28"

keywords: configmaps with code engine, secrets with code engine, key references with code engine, key-value pair with code engine, setting up secrets with code engine, setting up configmaps with code engine, configmaps, secrets, environment variables

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



# Setting up and using secrets and configmaps 
{: #configmap-secret} 

Learn how to work with secrets and configmaps in {{site.data.keyword.codeengineshort}}. In {{site.data.keyword.codeengineshort}}, you can store your information as key-value pairs in secrets or configmaps that can be consumed by your job or application by using environment variables. 
{: shortdesc}

## What are secrets and configmaps and why would I use them? 
{: #configmapsec-whatwhy}

In {{site.data.keyword.codeengineshort}}, both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app or job portable. A configmap contains information in key-value pairs.

A secret provides a method to include sensitive configuration information, such as passwords or SSH keys, to your deployment. By referencing values from your secret, you can decouple sensitive information from your deployment to keep your app or job portable. Anyone who is authorized to your project can also view your secrets; be sure that you know that the secret information can be shared with those users. Secrets contain information in key-value pairs.

Since secrets and configmaps are similar entities (except secrets are stored more securely), the way you interact and work with secrets and configmaps is also similar. 

In {{site.data.keyword.codeengineshort}}, secrets that are used to store simple name-value pairs are called *generic* secrets. In contrast, secrets that store information about how to authenticate to a container registry are called [registry access secrets (`imagePullSecret`)](/docs/codeengine?topic=codeengine-add-registry). Secrets that store information about how to access and authenticate to a Git repository are called [Git repository access secrets](/docs/codeengine?topic=codeengine-code-repositories#create-code-repo-console).

## Creating configmaps
{: #configmap-create}

Create configmaps with {{site.data.keyword.codeengineshort}}.
{: shortdesc}

### Creating a configmap from the console
{: #configmap-create-ui}

Create configmaps with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Overview page, click **Secrets and configmaps**.
3. From the Secrets and configmaps page, click **Create** to create your configmap.  
4. From the Create config page:
   1. Select the **Configmap** option.  
   2. Provide a name; for example, `myconfigmap`.
   3. Click **Add key-value pair**. Specify one or more key-value pairs for this configmap. For example, specify one key as `key1` with the value of `value1` and specify another key as `key2` with the value of `value2`. Notice that you can specify values on one or more lines. The name that you choose for your key does not need to be the same as the name of your environment variable.
   4. Click **Create** to create the configmap. 
5. Now that your configmap is created from the console, go to the Secrets and configmaps page to view a listing of your defined secrets and configmaps.

### Creating a configmap with the CLI
{: #configmap-create-cli}

Create configmaps with the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

You can populate a configmap in several ways. You can populate it by specifying the key-value pairs directly on the command line, or you can point to a file. 

**Before you begin**
   * Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
   * [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

When you create (or update) a configmap from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when you use a file to specify configmap values, *all* of the contents within the file become the value for the key-value pair. When you use the option format of `--from-file KEY=FILE`, the `KEY` is name of the environment variable that is known to your job or app. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job or app. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. 
{: important}

1. Create a configmap with the **`configmap create`** command in one of the following ways: 

    * Create a configmap directly on the command line by using the `--from-literal` option in `KEY=VALUE` format. For example,

        ```sh
        ibmcloud ce configmap create --name myliteralconfigmap --from-literal TARGET=Sunshine 
        ```
        {: pre}

    * Create a configmap by using the `--from-file` option to point to a file. By using this option, all of the contents of the file become the value for the key-value pair. For this example, use a file that is named `colors.txt`, which contains the text `blue, green, red`. 

        * The following example uses the `--from-file KEY=FILE` format with the **`configmap create`** command:  

            ```sh
            ibmcloud ce configmap create --name mycolorconfigmap --from-file TARGET=colors.txt
            ```
            {: pre}

        * The following example command uses the `--from-file FILE` format with the **`configmap create`** command. In this example, `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to the example `myjob` job.

            ```sh
            ibmcloud ce configmap create --name mycolorconfigmap2  --from-file TARGET
            ```
            {: pre}

    * Create a configmap by using the `--from-env-file` option to point to a file that contains one or more lines that match the format `KEY=VALUE`. Each line from the specified file is added as a key-value pair. For this example, let's use a file that is named `colors_multi.txt` that contains the key-value pairs: `color1=yellow`, `color2=orange`, and `color3=purple`. 

        ```sh
        ibmcloud ce configmap create --name mycolorconfigmapmulti --from-env-file colors_multi.txt
        ```
        {: pre}

2. Now that the configmap is created, use the **`configmap list`** command to list all configmaps in your project or use the **`configmap get`** command to display details about a specific configmap. For example,

    ```sh
    ibmcloud ce configmap get --name mycolorconfigmap
    ```
    {: pre}

   **Example output**
   
   ```
    Getting configmap 'mycolorconfigmap'...
    OK

    Name:          mycolorconfigmap
    ID:            abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           11s
    Created:       2020-10-14 14:10:57 -0400 EDT

    Data:
    ---
    TARGET: blue, green, red
   ```
   {: screen}

## Updating configmaps 
{: #configmap-update}

You can change key-value pairs for existing configmaps.
{: shortdesc}

### Updating configmaps from the console 
{: #configmap-update-ui}

You can update an existing configmap and its key-value pairs from the console. 
{: shortdesc}

1. You can update key-value pairs for your defined configmaps from the console in one of the following ways. 

   * Go to the Secrets and configmaps page for your project and locate the configmap that you want to update. Click the name of the configmap that you want to update to open it. 
   * If your configmap is referenced by an app or job, then use the links in the environment variables table on the **Environmental variables** tab of your app or job. These links take you directly to your secret or configmap. 
2. Click **Edit** and make the updates for your configmap. 
3. Click **Save** to save the changes to your configmap.

If your updated configmap is referenced by a job or app, then your job or app must be restarted for the new data to take effect.
* Apps: From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated configmap.
* Jobs: From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated configmap.

### Updating configmaps with the CLI 
{: #configmap-update-cli}
 
You can update an existing configmap and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a configmap, use the [`configmap update`](/docs/codeengine?topic=codeengine-cli#cli-configmap-update) command. Let's update the `myliteralconfigmap` configmap to change the value of the `TARGET` key from `Sunshine` to `Stranger`.

    ```sh
    ibmcloud ce configmap update --name myliteralconfigmap --from-literal "TARGET=Stranger"
    ```
    {: pre}

2. Now that your configmap is updated, use the **`configmap get`** command to display details about a specific secret. For example,

    ```sh
    ibmcloud ce configmap get --name myliteralconfigmap
    ```
    {: pre}

   **Example output**
   
   ```
    Getting generic secret 'myliteralconfigmap'...
    OK

    Name:          myliteralconfigmap
    ID:            abcdefgh-abcd-abcd-abcd-c88e2775388e
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           21m
    Created:       2021-05-14T07:57:11-04:00

    Data:
    ---
    TARGET: Stranger
   ```
   {: screen}

## Referencing configmaps  
{: #configmap-ref}

Your apps or jobs can consume and use the information that is stored in a configmap by using environment variables.  
{: shortdesc}

### Referencing configmaps from the console 
{: #configmap-ref-ui}

You can use the console to create environment variables for your apps and jobs that fully reference a configmap or reference individual keys in a configmap. 
{: shortdesc}

Before you can reference a configmap, it must exist. See [create a configmap](/docs/codeengine?topic=codeengine-configmap-secret#configmap-create-ui).

From the console, you can reference only one individual key of a defined configmap or secret per environment variable.  If you need to reference more than one key of a configmap or secret, then repeat the steps to define another environment variable that references a different key.
{: note}

1. To reference a defined configmap from your app or job, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing configmap or reference an individual key in an existing configmap.
2. After you create environment variables, you must restart your app or job for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs, submit your job to update the job with the environment variables that you defined. 

To update an environment variable that references a configmap, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations when updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a configmap, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Referencing configmaps with the CLI 
{: #configmap-ref-cli}
 
To use configmaps with apps and jobs, you can set environment variables that fully reference a configmap or reference individual keys in a configmap with the CLI.
{: shortdesc}

Before you can reference a configmap, it must exist. See [create a configmap](/docs/codeengine?topic=codeengine-configmap-secret#configmap-create-cli).
Let's use the configmaps that were previously defined with the CLI with an application. 

1. [Deploy an app](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cli). For this example, create an app that uses the [`Hello`](https://hub.docker.com/r/ibmcom/hello) image in Docker Hub. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. 

    ```sh
    ibmcloud ce app create --name myhelloapp --image ibmcom/hello 
    ```
    {: pre}

   When you call the `myhelloapp` app, the output is `Hello World`.  

2. Update the app to reference the previously defined `mycolorconfigmap` configmap. 

    From the CLI, to use a defined configmap with an application, specify the `--env-from-configmap` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) commands. Similarly, to use a configmap with a job, specify the `--env-from-configmap` option on the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 
    {: tip}

    ```sh
    ibmcloud ce app update --name myhelloapp --env-from-configmap mycolorconfigmap
    ```
    {: pre}

    **Example output**
   
   ```
    Updating application 'myhelloapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myhelloapp' to check the application status. 
    OK

    https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

3. Call the application again. This time, the app returns `Hello blue, green, red`, which is the value for the `TARGET` key that is specified in the `mycolorconfigmap` configmap.

    ```sh
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

   **Example output**
   
   ```
    Hello blue, green, red
   ```
   {: screen}

4. Update the app again to use the `myliteralconfigmap` configmap. 

   When you update an application or job with an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
   {: note}

    ```sh
    ibmcloud ce app update --name myhelloapp --env-from-configmap myliteralconfigmap
    ```
    {: pre}

   **Example output**
   
   ```
    Updating application 'myhelloapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myhelloapp' to check the application status.
    OK 

    https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
   ```
   {: screen}

5. Call the application again. This time, the app returns `Hello Stranger`, which is the value that is specified in the `myliteralconfigmap` configmap.

    ```sh
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

   **Example output**
   
   ```
    Hello Stranger
     ```
   {: screen}

6. Update the `myliteralconfigmap` to change the key-value pair.  

    ```sh
    ibmcloud ce configmap update --name myliteralconfigmap --from-literal "TARGET=Happy day"
    ```
    {: pre}

    Run the `**ibmcloud ce configmap get -n myliteralconfigmap`** command to display details of the configmap. 

   **Example output**
   
   ```
    Name:          myliteralconfigmap
    [...]
    Data:
    ---
    TARGET: Happy day
     ```
   {: screen}

7. Restart the application for the new data to take effect. 

    ```sh
    ibmcloud ce app update --name myhelloapp 
    ```
    {: pre}
8. Call the application again. This time, the app returns `Hello Happy day`, which is the value that is specified in the `myliteralconfigmap` configmap.

    ```sh
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

   **Example output**
   
   ```
    Hello Happy day
     ```
   {: screen}

For more detailed scenarios about fully referencing secrets and configmaps as environment variables, referencing individual keys of a secret or configmap, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).

You can also reference secrets and configmaps as mounted files in the CLI. For more information, see [Referencing secrets and configmaps as mounted files](/docs/codeengine?topic=codeengine-secretcm-reference-mountedfiles).

## Creating secrets
{: #secret-create}

Use secrets to provide sensitive information to your apps or jobs. Secrets are defined in key-value pairs and the data that is stored in secrets is encoded.
{: shortdesc}

### Creating a secret from the console
{: #secret-create-ui}

Learn how to create secrets from the {{site.data.keyword.codeengineshort}} console that can be consumed by jobs or apps as environment variables.
{: shortdesc}

Before you begin, [create a project](/docs/codeengine?topic=codeengine-manage-project).

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Components page, click **Secrets and configmaps**.
3. From the Secrets and configmaps page, click **Create** to create your secret.
4. From the Create config page:
   1. Select the **Secret** option.  
   2. Provide a name; for example, `mysecret`.
   3. Click **Add key-value pair**. Specify one or more key-value pairs for this secret. For example, specify one key as `secret1` with the value of `mysecret1` and specify another key as `secret2` with the value of `mysecret2`. The name that you choose for your key does not need to be the same as the name of your environment variable. Notice that the value for the key is hidden, but it can be viewed if needed. 
4. Click **Create** to create the secret. 
5. Now that your secret is created from the console, go to the Secrets and configmaps page to view a listing of your defined secrets and configmaps.  

### Creating a secret with the CLI
{: #secret-create-cli}
 
Learn how to create secrets with the {{site.data.keyword.codeengineshort}} CLI that can be consumed by jobs or apps as environment variables.

With the CLI, you can create a secret where the data is pulled from a file, or specified directly with the **`secret create`** command. 

**Before you begin**

   * Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
   * [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

When you create (or update) a secret from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when you use the `--from-file` option to specify secret values, *all* of the contents within the file is the value for the key-value pair. When you use the option format of `--from-file KEY=FILE` the `KEY` is name of the environment variable that is known to your job or app. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job or app. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. 
{: important}

1. Create a secret with the **`secret create`** command in one of the following ways:   

    * Create a secret directly from the command line by using the `--from-literal` option in `KEY=VALUE` format. For example, 

        ```sh
        ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My literal secret"
        ```
        {: pre}

    * Create a secret by using the `--from-file` option to point to a file. By using this option, all of the contents of the file become the value for the key-value pair. For this example, use a file that is named `secrets.txt`, which contains `my little secret1`. 
    
        * The following example uses the `--from-file KEY=FILE` format with the **`secret create`** command:  

            ```sh
            ibmcloud ce secret create --name mysecretmsg1 --from-file TARGET=secrets.txt
            ```
            {: pre}

        * The following example command uses the `--from-file FILE` format with the **`secret create`** command. In this example, `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to the job.

            ```sh
            ibmcloud ce secret create --name mysecretmsg2  --from-file TARGET
            ```
            {: pre}

    * Create a secret by using the `--from-env-file` option to point to a file that contains one or more lines that match the format `KEY=VALUE`. Each line from the specified file is added as a key-value pair. For this example, let's use a file that is named `secrets_multi.txt` which contains the key-value pairs: `sec1=mysec1`, `sec2=mysec2`, and `sec3=mysec3`. 

        ```sh
        ibmcloud ce secret create --name mysecretmulti --from-env-file secrets_multi.txt
        ```
        {: pre}
        
2. Now that secrets are created, use the **`secret list`** command to list all secrets in your project or use the **`secret get`** command to display details about a specific secret. For example,

    ```sh
    ibmcloud ce secret get --name mysecretmsg2
    ```
    {: pre}

   **Example output**
   
   ```
    Getting generic secret 'mysecretmsg2'...
    OK

    Name:          mysecretmsg2
    ID:            abcdefgh-abcd-abcd-abcd-c88e2775388e
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           9s
    Created:       2020-10-14 14:12:55 -0400 EDT

    Data:
    ---
    TARGET: bXkgYmlnIHNlY3JldDI=
   ```
   {: screen}

Notice that the value of the key `TARGET` for this secret is encoded. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command. 

## Updating secrets 
{: #secret-update}

You can change key-value pairs for existing secrets.
{: shortdesc}

### Updating secrets from the console 
{: #secret-update-ui}

You can update key-value pairs for your defined secrets from the console. 
{: shortdesc}

1. You can update key-value pairs for your defined secrets from the console in one of the following ways. 

   * Go to the Secrets and configmaps page for your project and locate the secret that you want to update. Click the name of the secret that you want to update to open it.
   * If your secret is referenced by an app or job, then use the links in the environment variables table on the **Environmental variables** tab of your app or job. These links take you directly to your secret or configmap. Alternatively, you can also go to the Secrets and configmaps page for your project and locate the secret that you want to update. Click the name of the secret that you want to update to open it.

2. Click **Edit** and make the updates for your secret. 

3. Click **Save** to save the changes to your secret.

If your updated secret is referenced by a job or app, then your job or app must be restarted for the new data to take effect. 
* Apps: From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated secret.
* Jobs: From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated secret.

### Updating secrets with the CLI 
{: #secret-update-cli}
 
You can update an existing secret and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a defined secret, use the [**`secret update`**](/docs/codeengine?topic=codeengine-cli#cli-secret-update) command. Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My literal secret` to `My new literal secret`.

    ```sh
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new literal secret"
    ```
    {: pre}

2. Now that your secret is updated, use the **`secret get`** command to display details about a specific secret. For example,

    ```sh
    ibmcloud ce secret get --name myliteralsecret
    ```
    {: pre}

   **Example output**
   
   ```
    Getting generic secret 'myliteralsecret'...
    OK

    Name:          myliteralsecret
    ID:            abcdefgh-abcd-abcd-abcd-c88e2775388e
    Project Name:  myproject
    Project ID:    01234567-abcd-abcd-abcd-abcdabcd1111
    Age:           21m
    Created:       2021-05-14T07:57:11-04:00

    Data:
    ---
    TARGET: TXkgbmV3IGxpdGVyYWwgc2VjcmV0
   ```
   {: screen}

Notice that the value of the key `TARGET` for this secret is encoded. To display the secret data as decoded, use the `--decode` option with the **`secret get`** command. 


## Referencing secrets 
{: #secret-ref}

Your apps or jobs can consume and use the information that is stored in a secret by using environment variables. 
{: shortdesc}

### Referencing secrets from the console 
{: #secret-ref-ui}

You can use the console to create environment variables for your apps and jobs that fully reference a secret or reference individual keys in a secret. 
{: shortdesc}

Before you can reference a secret, it must exist. See [create a secret](/docs/codeengine?topic=codeengine-configmap-secret#secret-create-ui). For this example, create a secret that is named `mysecret2` with the key-value pair of `TARGET=Sunshine`.

1. To reference a defined secret from your app or job, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing secret or reference an individual key in an existing secret.
2. After you create environment variables, you must restart your app or job for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs, submit your job to update the job with the environment variables that you defined. 

To update an environment variable that references a secret, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations when updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a secret, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

For example, let's use the previously defined `mysecret` secret that you defined from the console with a job and fully reference this secret with an environment variable. 

1. [Create and run a job ](/docs/codeengine?topic=codeengine-job-deploy). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the [`docker.io/ibmcom/codeengine`](https://hub.docker.com/r/ibmcom/codeengine){: external} image. This `hello-world` app includes the `TARGET` environment variable, and the app prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    From the Jobs page: 
    1. Create a job; for example, `myjob`.
    2. Specify `docker.io/ibmcom/codeengine` as the image reference.
    3. Click **Create** to create the job. 

    If your app or job that you want to use with the secret is already defined in {{site.data.keyword.codeengineshort}}, go to the Applications or Jobs page and then click the name of your app or job to open the component. 

2. When the job is created, from the Jobs page, click the name of your job to open it. 

3. Update the job to add a secret as an environment variable. Click **Environment variables** to open the tab and click **Add** to add your environment variable. 

4. From the Add environment variable page:
   1. To use the previously defined secret, select **Reference full secret**.
   2. From the menu, select the name of the secret that you want; for example, `mysecret2`.
   3. Click **Done** to save the environment variable. 
   4. Click **Save** to save the changes to your job. 

5. To run the job with the environment variable that references a secret, click **Submit job**. For this example, the logs of the `myjob` job run display `Hello Sunshine from {{site.data.keyword.codeengineshort}}` and the prints the environment variables, including any values of secrets that are referenced with environment variables. 

### Referencing secrets with the CLI 
{: #secret-ref-cli}
 
To use secrets with apps and jobs, you can set environment variables that fully reference a secret or reference individual keys in a secret with the CLI.
{: shortdesc}

Before you can reference a secret, it must exist. See [create a secret](/docs/codeengine?topic=codeengine-configmap-secret#secret-create-cli).
Let's use the secrets that were previously defined with the CLI with a job. 

To use a secret with a job with the CLI, specify the `--env-from-secret` option on the **`job create`**, **`job update`**, **`jobrun submit`**, or **`jobrun resubmit`** commands. Similarly, to reference a secret from an application with the CLI, specify the **`--env-from-secret`** option on the **`app create`** or **`app update`** commands.  

This scenario uses the CLI to run a job that references a secret. 

1. [Create and run a job ](/docs/codeengine?topic=codeengine-job-deploy). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the [`ibmcom/codeengine`](https://hub.docker.com/r/ibmcom/codeengine){: external} image in Docker Hub and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    ```sh
    ibmcloud ce job create --name myjob --image ibmcom/codeengine --array-indices 1-3
    ```
    {: pre}

2. Run the `myjob` job. 

    ```sh
    ibmcloud ce jobrun submit --name myjobrun --job myjob
    ```
    {: pre}

3. Display the logs of the `myjobrun` job run. You can display logs of all of the instances of a job run or display logs of a specific instance of a job run. In this example, the job run log displays the output of `Hello World from {{site.data.keyword.codeengineshort}}`. Use the **`jobrun get`** command to display the details of the job run, including its running instances. The following command displays the logs of `myjobrun-2-0` (the second instance of this job run) where `myjobrun` is the name of the job run, `2` is the second instance of the job run, and the `0` is the `retryindex` value of the job run.

    ```sh
    ibmcloud ce jobrun logs --instance myjobrun-2-0
    ```
    {: pre}

   **Example output**
   
   ```
    Getting logs for job run instance 'myjobrun-2-0'...
    OK

    myjobrun-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2
    Hello World from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)

    Some Env Vars:
    --------------
    HOME=/root
    HOSTNAME=myjobrun-2-0
    JOB_INDEX=2
    KUBERNETES_PORT=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
    KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
    KUBERNETES_PORT_443_TCP_PORT=443
    KUBERNETES_PORT_443_TCP_PROTO=tcp
    KUBERNETES_SERVICE_HOST=172.21.0.1
    KUBERNETES_SERVICE_PORT=443
    KUBERNETES_SERVICE_PORT_HTTPS=443
    PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    PWD=/
    SHLVL=1
   ```
   {: screen}

4. Update the configuration of the job to reference the previously defined `mysecretmsg2` secret. 

    ```sh
    ibmcloud ce job update --name myjob --env-from-secret mysecretmsg2
    ```
    {: pre}

5. Run the updated `myjob` job. The name of the job run must be unique. 

    ```sh
    ibmcloud ce jobrun submit --name myjobrun2 --job myjob
    ```
    {: pre}

6.  Use the **`jobrun get`** command to display details of the job run, including the instances of the job run. 

    ```sh
    ibmcloud ce jobrun get --name myjobrun2
    ```
    {: pre}

   **Example output**
   
   ```
    Getting jobrun 'myjobrun2'...
    Getting instances of jobrun 'myjobrun2'...
    Getting events of jobrun 'myjobrun2'...

    Name:               myjobrun2
    [...]

    Running Instances:
        Name           Ready  Status     Restarts  Age
        myjobrun2-1-0  0/1    Succeeded  0         4m
        myjobrun2-2-0  0/1    Succeeded  0         4m
        myjobrun2-3-0  0/1    Succeeded  0         4m
   ```
   {: screen}

7. Display the logs of the `myjobrun2` job run. You can display logs of all of the instances of a job run or display logs of a specific instance of a job run. This time, display the logs of the all the instances of the job run. The log displays `Hello my big secret2!`, which was specified by using an environment variable with a secret. Note, for this job that is defined with the `ibmcom/codeengine` image, the output of the job run prints the environment variables, including any values of secrets that are referenced with environment variables. 

    ```sh
    ibmcloud ce jobrun logs --jobrun myjobrun2
    ```
    {: pre}

   **Example output**
   
   ```
    Getting logs for all instances of job run 'myjobrun2'...
    Getting jobrun 'myjobrun2'...
    Getting instances of jobrun 'myjobrun2'...
    OK

    myjobrun2-1-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 1

    Hello my big secret2 from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)
    [...]
    TARGET=my big secret2

    myjobrun2-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2

    Hello my big secret2 from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)
    [...]
    TARGET=my big secret2

    myjobrun2-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello my big secret2 from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)
    [...]
    TARGET=my big secret2

   ```
   {: screen}

8. Resubmit the job run and specify to use the `myliteralsecret` secret for this job run.  

    ```sh
    ibmcloud ce jobrun resubmit  --jobrun myjobrun2  --name myjobrun2resubmit  --env-from-secret myliteralsecret
    ```
    {: pre}

    When you update a job or app with an environment variable that fully references a secret to fully reference a different secret, full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
    {: note}

9. Display the job run logs of an instance of the `myjobrun2resubmit` job run. This time, display the logs of the third instance of the job run. The log displays `Hello My literal secret!!`, which is the value that is specified in the `myliteralsecret` secret. Use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. 

    ```sh
    ibmcloud ce jobrun logs --instance myjobrun2resubmit-3-0
    ```
    {: pre}

   **Example output**
   
   ```
    Getting logs for job run instance 'myjobrun2resubmit-3-0'...
    OK

    myjobrun2resubmit-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello My literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)
    [...]
    TARGET=My literal secret
   ```
   {: screen}

10. To change the value of key-value pair in a secret, use the **`secret update`** command. Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My literal secret` to `My new literal secret`.

    ```sh
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new literal secret"
    ```
    {: pre}

11. For the new data to take effect, run your job again. Resubmit the job run again and specify to use the `myliteralsecret` secret for this job run. 

    ```sh
    ibmcloud ce jobrun resubmit  --jobrun myjobrun2  --name myjobrun2resubmit-b --env-from-secret myliteralsecret 
    ```
    {: pre}

12. Display the logs of the `myjobrun2resubmit-b` job run. This time, the job log displays `Hello My new literal secret!`, which is the value in the updated `myliteralsecret` secret. You can use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. Display the logs for any running instance of the job run.

    ```sh
    ibmcloud ce jobrun logs --instance myjobrun2resubmit-b-1-0
    ```
    {: pre}

   **Example output**
   
   ```
    Getting logs for job run instance 'myjobrun2resubmit-b-1-0'...
    OK

    myjobrun2resubmit-b-1-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 1

    Hello My new literal secret from:
    . ___  __  ____  ____
    ./ __)/  \(    \(  __)
    ( (__(  O )) D ( ) _)
    .\___)\__/(____/(____)
    .____  __ _   ___  __  __ _  ____
    (  __)(  ( \ / __)(  )(  ( \(  __)
    .) _) /    /( (_ \ )( /    / ) _)
    (____)\_)__) \___/(__)\_)__)(____)
    [...]
   ```
   {: screen}

To summarize, you completed basic scenarios to demonstrate how to use secrets with a job by referencing a full secret and updating keys within a secret.

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


## Deleting secrets and configmaps 
{: #configmapsecret-delete}

When you no longer need a configmap or secret, you can delete it. 
{: #shortdesc} 

### Deleting secrets and configmaps from the console
{: #configmapsecret-delete-ui}
 
1. To delete a secret or configmap from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the configmap or secret that you want to delete to open its page. 
    3. From the page for the specific configmap or secret, click **Actions > Delete secret** or **Actions > Delete configmap**. 
2. To delete a key-value pair for a specific secret or configmap from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the configmap or secret that you want to change to open its page. 
    3. From the page for the specific configmap or secret, delete the key-value pair that you want to remove. 

You can also delete defined environment variables that reference secrets and configmaps. To delete a defined environment variable, from the **Environment variables** tab of your job or app and delete the environment variable that you want to delete. After you delete a defined environment variable, be sure to click **Save** to save the changes to your app or job. For more information, see [delete an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Deleting secrets and configmaps with the CLI
{: #configmapsecret-delete-cli}
 
* To delete a configmap with the CLI, use the [**`configmap delete`**](/docs/codeengine?topic=codeengine-cli#cli-configmap-delete) command; for example, 

    ```sh
    ibmcloud ce configmap delete --name myliteralconfigmap -f
    ```
    {: pre}

    **Example output**

    ```
    Deleting configmap 'myliteralconfigmap'...
    OK
    ```
    {: screen}

* To delete a secret with the CLI, use the [**`secret delete`**](/docs/codeengine?topic=codeengine-cli#cli-secret-delete) command; for example, 

    ```sh
    ibmcloud ce secret delete --name myliteralsecret -f
    ```
    {: pre}

    **Example output**

    ```
    Deleting secret myliteralsecret...
    OK
    ```
    {: screen}

You can also [delete environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-cli) that reference secrets and configmaps from the CLI. 

## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}:  Automatically added configmaps
{: #inside-configmaps}
	
{{site.data.keyword.codeengineshort}} automatically creates the following configmaps in your namespace: `istio-ca-root` and `kube-root-ca`.

{{site.data.keyword.codeengineshort}} uses these configmaps internally and if you delete these configmaps, {{site.data.keyword.codeengineshort}} automatically recreates them.

