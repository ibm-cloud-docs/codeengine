---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-18"

keywords: configmaps with code engine, secrets with code engine, key references with code engine, key-value pair with code engine, setting up secrets with code engine, setting up configmaps with code engine, configmaps, secrets, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}


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

## I see configmaps that I didn't create. Can I delete them?
{: #inside-configmaps}

No. {{site.data.keyword.codeengineshort}} automatically creates the following configmaps in your namespace: `istio-ca-root` and `kube-root-ca`.  {{site.data.keyword.codeengineshort}} uses these configmaps internally. If you delete these configmaps, {{site.data.keyword.codeengineshort}} automatically re-creates them.

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
4. From the Create config page, complete the following steps.
    1. Select the **Configmap** option.  
    2. Provide a name; for example, `myconfigmap`.
    3. Click **Add key-value pair**. Specify one or more key-value pairs for this configmap. For example, specify one key as `key1` with the value of `value1` and specify another key as `key2` with the value of `value2`. Notice that you can specify values on one or more lines. The name that you choose for your key does not need to be the same as the name of your environment variable.
    4. Click **Create** to create the configmap. 
5. Now that your configmap is created from the console, go to the Secrets and configmaps page to view a listing of defined secrets and configmaps.

### Create a configmap with the CLI
{: #configmap-create-cli}

Create configmaps with the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

You can populate a configmap in several ways. You can populate it by specifying the key-value pairs directly on the command line, or you can point to a file. 

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

When you create (or update) a configmap from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when you use a file to specify configmap values, *all* the contents within the file become the value for the key-value pair. When you use the option format of `--from-file KEY=FILE`, the `KEY` is name of the environment variable that is known to your job or app. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job or app. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. Any lines in the specified file that are empty or begin with `#` are ignored. 
{: important}

#### Creating a configmap with the CLI
{: #configmap-creating-cli}

Create a configmap with the **`configmap create`** command in one of the following ways, 

* Create a configmap directly on the command line by using the `--from-literal` option in `KEY=VALUE` format. For example,

    ```txt
    ibmcloud ce configmap create --name myliteralconfigmap --from-literal TARGET=Sunshine 
    ```
    {: pre}

* Create a configmap by using the `--from-file` option to point to a file. By using this option, all the contents of the file become the value for the key-value pair. For this example, use a file that is named `colors.txt`, which contains the text `blue, green, red`. 
     
    * The following example uses the `--from-file KEY=FILE` format with the **`configmap create`** command:  

        ```txt
        ibmcloud ce configmap create --name mycolorconfigmap --from-file TARGET=colors.txt
        ```
        {: pre}

    * The following example command uses the `--from-file FILE` format with the **`configmap create`** command. In this example, `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to the example `myjob` job.

        ```txt
        ibmcloud ce configmap create --name mycolorconfigmap2  --from-file TARGET
        ```
        {: pre}

* Create a configmap by using the `--from-env-file` option to point to a file that contains one or more lines that match the format `KEY=VALUE`. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. For this example, use a file that is named `colors_multi.txt` that contains the key-value pairs: `color1=yellow`, `color2=orange`, and `color3=purple`. 

    ```txt
    ibmcloud ce configmap create --name mycolorconfigmapmulti --from-env-file colors_multi.txt
    ```
    {: pre}

#### Listing configmaps with the CLI
{: #configmap-list-cli}

Now that the configmap is created, use the **`configmap list`** command to list all configmaps in your project or use the **`configmap get`** command to display details about a specific configmap. For example,

```txt
ibmcloud ce configmap get --name mycolorconfigmap
```
{: pre}

Example output

```txt
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
* Apps - From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated configmap.
* Jobs - From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated configmap.

### Updating configmaps with the CLI 
{: #configmap-update-cli}

You can update an existing configmap and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a configmap, use the [`configmap update`](/docs/codeengine?topic=codeengine-cli#cli-configmap-update) command. Let's update the `myliteralconfigmap` configmap to change the value of the `TARGET` key from `Sunshine` to `Stranger`.

    ```txt
    ibmcloud ce configmap update --name myliteralconfigmap --from-literal "TARGET=Stranger"
    ```
    {: pre}

2. Now that your configmap is updated, use the **`configmap get`** command to display details about a specific secret. For example,

    ```txt
    ibmcloud ce configmap get --name myliteralconfigmap
    ```
    {: pre}

    Example output

    ```txt
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

From the console, you can reference only one individual key of a defined configmap or secret per environment variable. If you need to reference more than one key of a configmap or secret, then repeat the steps to define another environment variable that references a different key.
{: note}

1. To reference a defined configmap from your app or job, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing configmap or reference an individual key in an existing configmap. For example, let's fully reference the `myconfigmap` configmap from the `myapp` application. When you fully reference a configmap (or secret), you can optionally specify a `prefix`. By using a prefix such as `myconfigmap_`, each key is prefixed with `myconfigmap_`. 

2. After you create environment variables, you must restart your app or job for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs, submit your job to update the job with the environment variables that you defined. 

3. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. In this `myapp` example, because we specified a prefix for the fully referenced `myconfigmap` configmap, all the keys of this configmap are referenced as environment variables and are prefixed with `myconfigmap_`. For example, these environment variables display as `myconfigmap_key1=value1` and `myconfigmap_key2=value2`.

To update an environment variable that references a configmap, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations for updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a configmap, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Referencing configmaps with the CLI 
{: #configmap-ref-cli}

To use configmaps with apps and jobs, you can set environment variables that fully reference a configmap or reference individual keys in a configmap with the CLI.
{: shortdesc}

#### Referencing existing configmaps with the CLI 
{: #configmap-ref-existing-cli}

To use a configmap with an app with the CLI, specify the  `--env-from-configmap` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) commands. Similarly, to reference a configmap from a job with the CLI, specify the `--env-from-configmap` option on the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

The following example describes how to reference an existing configmap with an app by using the CLI. 

1. Use the **`configmap create`** command to create the following two configmaps for this scenario.  

    ```txt
    ibmcloud ce configmap create --name myliteralconfigmap --from-literal TARGET=Sunshine 
    ```
    {: pre}

    ```txt
    ibmcloud ce configmap create --name myliteralconfigmap2 --from-literal TARGET=Stranger 
    ```
    {: pre}     

2. [Deploy an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-cli) and reference the `myliteralconfigmap` configmap. For this example, create an app that uses the `hello` image. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. Reference the `myliteralconfigmap` configmap. For more information about the code that is used for this example, see [`hello`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.

    ```txt
    ibmcloud ce app create --name myhelloapp --image icr.io/codeengine/hello --env-from-configmap myliteralconfigmap
    ```
    {: pre}

3. Call the application. The app returns `Hello Sunshine`, which is the value for the `TARGET` key that is specified in the `myliteralconfigmap` configmap.

    ```txt
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: pre}

    Example output

    ```txt
    Hello Sunshine
    ```
    {: screen}

4. Update the app again to use the `myliteralconfigmap2` configmap. 

    When you update an application or job with an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
    {: note}

    ```txt
    ibmcloud ce app update --name myhelloapp --env-from-configmap myliteralconfigmap2
    ```
    {: pre}

    Example output

    ```txt
    Updating application 'myhelloapp' to latest revision.
    [...]
    Run 'ibmcloud ce application get -n myhelloapp' to check the application status.
    OK 

    https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

5. Call the application again. This time, the app returns `Hello Stranger`, which is the value that is specified in the `myliteralconfigmap2` configmap.

    ```txt
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

    Example output

    ```txt
    Hello Stranger
    ```
    {: screen}

6. Update the `myliteralconfigmap2` to change the key-value pair.  

    ```txt
    ibmcloud ce configmap update --name myliteralconfigmap2 --from-literal "TARGET=Happy day"
    ```
    {: pre}

    Run the **`ibmcloud ce configmap get -n myliteralconfigmap2`** command to display details of the configmap. 

    Example output

    ```txt
    Name:          myliteralconfigmap2
    [...]
    Data:
    ---
    TARGET: Happy day
    ```
    {: screen}

7. Restart the application for the new data to take effect. 

    ```txt
    ibmcloud ce app update --name myhelloapp 
    ```
    {: pre}

8. Call the application again. This time, the app returns `Hello Happy day`, which is the value that is specified in the `myliteralconfigmap2` configmap.

    ```txt
    curl https://myhelloapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

    Example output

    ```txt
    Hello Happy day
    ```
    {: screen}

#### Referencing configmaps that are not yet defined with the CLI 
{: #configmap-ref-not-existing-cli}

If a configmap does not exist before it is referenced, an app does not deploy successfully and a job does not run successfully until the referenced configmap is created.  

If you are working with an app or a job and the referenced configmap is not yet defined, you can use the `--force` option to avoid verification of the existence of the referenced configmap. The `--force` option can be used with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update), [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or  [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

When you use the `--force` option with these commands, the action to create, update, or run the app or job completes; however, the app or job will not run successfully until the referenced configmap exists. If you add the `--no-wait` option in addition to the `--force` option to the command, the system completes the action and does not wait for the app or job to successfully run. 

The following example describes how to reference a configmap that is not yet defined with an app by using the CLI. 

1. [Create an app](/docs/codeengine?topic=codeengine-application-workloads) and reference the undefined `myliteralconfigmap3` configmap. For this example, create a {{site.data.keyword.codeengineshort}} app that uses the `icr.io/codeengine/hello` image. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. Reference the `myliteralconfigmap3` configmap. For more information about the code that is used for this example, see [`hello`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.

    By using the `--no-wait` option with the **`app create`** command, the app is created and does not wait for the app to be ready. 

    ```txt
    ibmcloud ce app create --name myapp --image icr.io/codeengine/hello --env-from-configmap myliteralconfigmap3 --force --no-wait
    ```
    {: pre}

2. Use the **`app get`** command to display details of the job run, including the environment variable information. Notice that the app is created, but is not yet fully deployed. 

    ```txt
    ibmcloud ce app get --name myapp
    ```
    {: pre}

    Example output

    ```txt
    Name:            myapp
    [...]
    Status Summary:  Application is deploying

    Environment Variables:
        Type                      Name                 Value
        ConfigMap full reference  myliteralconfigmap3
    Image:                  icr.io/codeengine/hello
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Runtime:
        Concurrency:    100
        Maximum Scale:  10
        Minimum Scale:  0
        Timeout:        300

    Conditions:
        Type                 OK     Age  Reason
        ConfigurationsReady  false  10s
        Ready                false  10s  RevisionMissing : Configuration "myapp" is waiting for a Revision to become ready.
        RoutesReady          false  10s  RevisionMissing : Configuration "myapp" is waiting for a Revision to become ready.

    Events:
        Type    Reason   Age  Source              Messages
        Normal  Created  12s  service-controller  Created Configuration "myapp"
        Normal  Created  12s  service-controller  Created Route "myapp"

    Instances:
        Name                                      Revision      Running  Status   Restarts  Age
        myapp-00001-deployment-566d5c79b9-wttqs  myapp-00001  0/2      Pending  0         11s
    ```
    {: screen}

3. Create the configmap.  

    ```txt
    ibmcloud ce configmap create --name myliteralconfigmap3 --from-literal TARGET=Everyone 
    ```
    {: pre}

4. Restart the application for the new data to take effect. 

    ```txt
    ibmcloud ce app update --name myapp
    ```
    {: pre}

5. Call the application. The app returns `Hello Everyone`, which is the value that is specified in the `myliteralconfigmap3` configmap.

    ```txt
    curl https://myapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

    Example output

    ```txt
    Hello Everyone
    ```
    {: screen}

6. Update the app to reference the existing `myliteralconfigmap2` configmap. The `myliteralconfigmap2` is defined with the value `TARGET=Stranger`. Updating the app restarts the app for the new data to take effect. 

    When you update an application or job with an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
    {: note}

    ```txt
    ibmcloud ce app update --name myapp --env-from-configmap myliteralconfigmap2
    ```
    {: pre}

7. Call the application again. This time, the app returns `Hello Stranger`, which is the value that is specified in the `myliteralconfigmap2` configmap. 

    ```txt
    curl https://myapp.d484a5d6-d10d.us-south.codeengine.appdomain.cloud  
    ```
    {: pre}

    Example output

    ```txt
    Hello Stranger
    ```
    {: screen}

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).

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
4. From the Create config page, complete the following steps:
    1. Select the **Secret** option.  
    2. Provide a name; for example, `mysecret`.
    3. Click **Add key-value pair**. Specify one or more key-value pairs for this secret. For example, specify one key as `secret1` with the value of `mysecret1` and specify another key as `secret2` with the value of `target-secret`. The name that you choose for your key does not need to be the same as the name of your environment variable. Notice that the value for the key is hidden, but it can be viewed if needed. 
5. Click **Create** to create the secret. 
6. Now that your secret is created from the console, go to the Secrets and configmaps page to view a listing of defined secrets and configmaps. For secrets, you can display a list of user-generated secrets or a list of all secrets, which includes secrets that are generated by {{site.data.keyword.codeengineshort}}. 

### Create a secret with the CLI
{: #secret-create-cli}

Learn how to create secrets with the {{site.data.keyword.codeengineshort}} CLI that can be consumed by jobs or apps as environment variables.

With the CLI, you can create a secret where the data is pulled from a file, or specified directly with the **`secret create`** command. 

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

When you create (or update) a secret from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when you use the `--from-file` option to specify secret values, *all* the contents within the file is the value for the key-value pair. When you use the option format of `--from-file KEY=FILE` the `KEY` is name of the environment variable that is known to your job or app. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job or app. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. Any lines in the specified file that are empty or begin with `#` are ignored. 
{: important}

#### Creating a secret with the CLI
{: #secret-creating-cli}

Create a secret with the **`secret create`** command in one of the following ways:   

* Create a secret directly from the command line by using the `--from-literal` option in `KEY=VALUE` format. For example, 

    ```txt
    ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My literal secret"
    ```
    {: pre}

* Create a secret by using the `--from-file` option to point to a file. By using this option, all the contents of the file become the value for the key-value pair. For this example, use a file that is named `secrets.txt`, which contains `my little secret1`. 


    * The following example uses the `--from-file KEY=FILE` format with the **`secret create`** command:  

        ```txt
        ibmcloud ce secret create --name mysecretmsg1 --from-file TARGET=secrets.txt
        ```
        {: pre}

    * The following example command uses the `--from-file FILE` format with the **`secret create`** command. In this example, `TARGET` (no extension) is the name of the file, which is the same as the name of the environment variable that is known to the job.

        ```txt
        ibmcloud ce secret create --name mysecretmsg2  --from-file TARGET
        ```
        {: pre}

* Create a secret by using the `--from-env-file` option to point to a file that contains one or more lines that match the format `KEY=VALUE`. Each line from the specified file is added as a key-value pair. Any lines in the specified file that are empty or begin with `#` are ignored. For this example, use a file that is named `secrets_multi.txt`, which contains the key-value pairs: `sec1=mysec1`, `sec2=mysec2`, and `sec3=mysec3`. 

    ```txt
    ibmcloud ce secret create --name mysecretmulti --from-env-file secrets_multi.txt
    ```
    {: pre}
  
#### Listing secrets with the CLI
{: #secret-list-cli}

Now that secrets are created, use the **`secret list`** command to list the secrets in your project or use the **`secret get`** command to display details about a specific secret. For example,

```txt
ibmcloud ce secret get --name mysecretmsg2
```
{: pre}

Example output

```txt
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

* Apps - From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated secret.
* Jobs - From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated secret.

### Updating secrets with the CLI 
{: #secret-update-cli}

You can update an existing secret and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a defined secret, use the [**`secret update`**](/docs/codeengine?topic=codeengine-cli#cli-secret-update) command. Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My literal secret` to `My new literal secret`.

    ```txt
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new literal secret"
    ```
    {: pre}

2. Now that your secret is updated, use the **`secret get`** command to display details about a specific secret. For example,

    ```txt
    ibmcloud ce secret get --name myliteralsecret
    ```
    {: pre}

    Example output

    ```txt
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

Before you can reference a secret, it must exist. See [create a secret](/docs/codeengine?topic=codeengine-configmap-secret#secret-create-ui). For this example, create a secret that is named `target-secret` with the key-value pair of `TARGET=Sunshine`.

1. To reference a defined secret from your app or job, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing secret or reference an individual key in an existing secret. When you fully reference a secret (or configmap), you can optionally specify a `prefix`. For example, if you fully reference the `mysecret` secret from the `myapp` application and use the `mysecret_` prefix, each key in the secret is prefixed with `mysecret_`. 

2. After you create environment variables, you must restart your app or job for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs, submit your job to update the job with the environment variables that you defined. 

3. After the app or job status changes to **Ready**, you can test the application or run the job. For an app, click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. In the `myapp` example, because we specified a prefix for the fully referenced `mysecret` secret, all the keys of this secret are referenced as environment variables and are prefixed with `mysecret_`. For example, these environment variables display as `mysecret_secret1=mysecret1` and `mysecret_secret2=mysecret2`. 

To update an environment variable that references a secret, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations for updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a secret, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

For example, let's use the previously defined `mysecret` secret that you defined from the console with a job and fully reference this secret with an environment variable. 

1. [Create and run a job](/docs/codeengine?topic=codeengine-job-plan). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    From the Jobs page,
    1. Create a job; for example, `myjob`.
    2. Specify `icr.io/codeengine/codeengine` as the image reference.
    3. Click **Create** to create the job. 

    If your app or job that you want to use with the secret is already defined in {{site.data.keyword.codeengineshort}}, go to the Applications or Jobs page and then click the name of your app or job to open the component. 

2. When the job is created, from the Jobs page, click the name of your job to open it. 

3. Update the job to add a secret as an environment variable. Click **Environment variables** to open the tab and click **Add** to add your environment variable. 

4. From the Add environment variable page,
    1. To use the previously defined secret, select **Reference full secret**.
    2. From the menu, select the name of the secret that you want; for example, `target-secret`.
    3. Click **Add** to add the environment variable. 
    4. Click **Save** to save the changes to your job. 

5. To run the job with the environment variable that references a secret, click **Submit job**. For this example, the logs of the `myjob` job run display `Hello Sunshine from {{site.data.keyword.codeengineshort}}` and the prints the environment variables, including any values of secrets that are referenced with environment variables. 

### Referencing secrets with the CLI 
{: #secret-ref-cli}

To use secrets with apps and jobs, you can set environment variables that fully reference a secret or reference individual keys in a secret with the CLI.
{: shortdesc}

#### Referencing existing secrets with the CLI 
{: #secret-ref-existing-cli}

To use a secret with an app with the CLI, specify the  `--env-from-secret` option on the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) commands. Similarly, to reference a secret from a job with the CLI, specify the `--env-from-secret` option on the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

The following example describes how to reference an existing secret with a job by using the CLI. 

1. Use the **`secret create`** command to create the following two secrets for this scenario.  

    ```txt
    ibmcloud ce secret create --name myliteralsecret --from-literal "TARGET=My big literal secret"
    ```
    {: pre}

    ```txt
    ibmcloud ce secret create --name myliteralsecret2 --from-literal "TARGET=My little literal secret"
    ```
    {: pre}       

2. [Create a job](/docs/codeengine?topic=codeengine-job-plan) and reference the `myliteralsecret` secret. For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine --array-indices 2-3 --env-from-secret myliteralsecret
    ```
    {: pre}

3. Run the `myjob` job. 

    ```txt
    ibmcloud ce jobrun submit --name myjobrun --job myjob
    ```
    {: pre}

4. Use the **`jobrun get`** command to display details of the job run, including the instances of the job run. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    Getting events of jobrun 'myjobrun'...
    Run 'ibmcloud ce jobrun events -n myjobrun' to get the system events of the job run instances.
    Run 'ibmcloud ce jobrun logs -f -n myjobrun' to follow the logs of the job run instances.
    OK

    Name:               myjobrun
    [...]
    Job Ref:                myjob
    Environment Variables:
        Type                   Name          Value
        Secret full reference  myliteralsecret
    Image:                  icr.io/codeengine/codeengine
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  4G
        Memory:             4G

    Runtime:
        Array Indices:       2-3
        Max Execution Time:  7200
        Retry Limit:         3

    Status:
        Completed:          9s
        Instance Statuses:
            Succeeded:  2
        Conditions:
            Type      Status  Last Probe  Last Transition
            Pending   True    13s         13s
            Running   True    9s          9s
            Complete  True    9s          9s

    Events:
        Type    Reason     Age                Source                Messages
        Normal  Updated    10s (x4 over 14s)  batch-job-controller  Updated JobRun "myjobrun"
        Normal  Completed  10s                batch-job-controller  JobRun completed successfully

    Instances:
        Name          Running  Status     Restarts  Age
        myjobrun-2-0  0/1      Succeeded  0         14s
        myjobrun-3-0  0/1      Succeeded  0         14s
    ```
    {: screen}

5. Display the logs of the `myjobrun` job run. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. This time, display the logs of the all the instances of the job run. The log displays `Hello my big literal secret!`, which was specified by using an environment variable with a secret. Note, for this job that is defined with the `icr.io/codeengine/codeengine` image, the output of the job run prints the environment variables, including any values of secrets that are referenced with environment variables. 

    ```txt
    ibmcloud ce jobrun logs --jobrun myjobrun
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of job run 'myjobrun'...
    Getting jobrun 'myjobrun'...
    Getting instances of jobrun 'myjobrun'...
    OK

    myjobrun-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2

    Hello My big literal secret from:
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
    TARGET=My big literal secret

    myjobrun-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello My big literal secret from:
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
    HOSTNAME=myjobrun-3-0
    JOB_INDEX=3
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
    TARGET=My big literal secret
    ```
    {: screen}

6. Resubmit the job run and specify to use the `myliteralsecret2` secret for this job run.  

    ```txt
    ibmcloud ce jobrun resubmit  --jobrun myjobrun  --name myjobrunresubmit  --env-from-secret myliteralsecret2
    ```
    {: pre}

    When you update a job or app with an environment variable that fully references a secret to fully reference a different secret, full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
    {: note}

7. Use the **`jobrun get`** command to display details of the job run, including the instances of the job run. Notice that the job run references both `myliteralsecret` and `myliteralsecret2` secrets.

    ```txt
    ibmcloud ce jobrun get --name myjobrunresubmit
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrunresubmit'...
    Getting instances of jobrun 'myjobrunresubmit'...
    Getting events of jobrun 'myjobrunresubmit'...
    [...]

    Name:          myjobrunresubmit
    ID:            79f01367-932b-4a76-be18-b1e68790a85b
    Project Name:  fmotestproject4
    Project ID:    841f0f38-420d-4388-b5d8-f230657d7dc6
    Age:           14s
    Created:       2021-06-15T21:15:37-04:00

    Job Ref:                myjob
        Environment Variables:
        Type                   Name              Value
        Secret full reference  myliteralsecret
        Secret full reference  myliteralsecret2
    Image:                  icr.io/codeengine/codeengine
        Resource Allocation:
        CPU:                1
        Ephemeral Storage:  4G
        Memory:             4G

    Runtime:
        Array Indices:       2-3
        Max Execution Time:  7200
        Retry Limit:         3

    Status:
        Completed:          11s
        Instance Statuses:
            Succeeded:  2
        Conditions:
            Type      Status  Last Probe  Last Transition
            Pending   True    14s         14s
            Running   True    12s         12s
            Complete  True    11s         11s

    Events:
        Type    Reason     Age                Source                Messages
        Normal  Updated    13s (x4 over 16s)  batch-job-controller  Updated JobRun "myjobrunresubmit"
        Normal  Completed  13s                batch-job-controller  JobRun completed successfully

    Instances:
        Name                  Running  Status     Restarts  Age
        myjobrunresubmit-2-0  0/1      Succeeded  0         16s
        myjobrunresubmit-3-0  0/1      Succeeded  0         16s
    ```
    {: screen}

8. Display the job run logs of an instance of the `myjobrunresubmit` job run. This time, display the logs of the `myjobrunresubmit-3-0` instance. The log displays `Hello My little literal secret!`, which is the value that is specified in the `myliteralsecret2` secret. Use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. 

    ```txt
    ibmcloud ce jobrun logs --instance myjobrunresubmit-3-0
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for job run instance 'myjobrunresubmit-3-0'...
    OK

    myjobrunresubmit-3-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 3

    Hello My little literal secret from:
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
    HOSTNAME=myjobrunresubmit-3-0
    JOB_INDEX=3
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
    TARGET=My little literal secret
    ```
    {: screen}

9. To change the value of key-value pair in a secret, use the **`secret update`** command. Let's update the `myliteralsecret` secret to change the value of the `TARGET` key from `My big literal secret` to `My new big literal secret`.

    ```txt
    ibmcloud ce secret update --name myliteralsecret --from-literal "TARGET=My new big literal secret"
    ```
    {: pre}

10. For the new data to take effect, run your job again. Resubmit the job run again and specify to use the `myliteralsecret` secret for this job run. 

    ```txt
    ibmcloud ce jobrun resubmit  --jobrun myjobrun  --name myjobrunresubmit2 --env-from-secret myliteralsecret 
    ```
    {: pre}

11. Display the logs of the `myjobrunresubmit2` job run. This time, the job log displays `Hello My new big literal secret!`, which is the value in the updated `myliteralsecret` secret. You can use the **`jobrun get`** command to display the details of the job run, including the running instances of the job run. Display the logs for any running instance of the job run.

    ```txt
    ibmcloud ce jobrun logs --instance myjobrunresubmit2-2-0
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for job run instance 'myjobrunresubmit2-2-0'...
    OK

    myjobrunresubmit2-2-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 2

    Hello My new big literal secret from:
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
    HOSTNAME=myjobrunresubmit2-2-0
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
    TARGET=My new big literal secret
    ```
    {: screen}

To summarize, you completed basic scenarios to demonstrate how to use secrets with a job by referencing an existing full secret and updating keys within a secret.

#### Referencing secrets that are not yet defined with the CLI 
{: #secret-ref-notyetdefined-cli}

If a secret does not exist before it is referenced, an app will not deploy successfully and a job will not run successfully until the referenced secret is created.  

If you are working with an app or a job and the referenced secret is not yet defined, use the `--force` option to avoid verification of the existence of the referenced secret. The `--force` option can be used with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create), [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update), [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or  [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands. 

When you use the `--force` option with these commands, the action to create, update, or run the app or job completes. However, the app or job will not run successfully until the referenced secret exists. If you add the `--no-wait` option in addition to the `--force` option to the command, the system completes the action and does not wait for the app or job to run successfully. 

The following example describes how to reference a secret that is not yet defined with a job by using the CLI. 

1. [Create a job](/docs/codeengine?topic=codeengine-job-plan). For this example, create a {{site.data.keyword.codeengineshort}} job that uses the `icr.io/codeengine/codeengine` image and then run the job. When a request is sent to this sample job, the job reads the `TARGET` environment variable, and the job prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine 
    ```
    {: pre}

2. Use the **`jobrun submit`** command to run the `myjob` job. Note that the `mynewliteralsecret` does not exist. By using the `--no-wait` option with the **`jobrun submit`** command, the job run is submitted and does not wait for the instances of this job run to complete. 

    ```txt
    ibmcloud ce jobrun submit --name myjobrun1 --job myjob --env-from-secret mynewliteralsecret --force --no-wait
    ```
    {: pre}

3. Use the **`jobrun get`** command to display details of the job run, including the environment variable information. Notice that the job run is in `pending` status. 

    ```txt
    ibmcloud ce jobrun get --name myjobrun1
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'myjobrun1'...
    Getting instances of jobrun 'myjobrun1'...
    Getting events of jobrun 'myjobrun1'...
    [...]

    Name:          myjobrun1
    [...]

    Job Ref:                myjob
    Environment Variables:
        Type                   Name                Value
        Secret full reference  mynewliteralsecret
    Image:                  icr.io/codeengine/codeengine
    Resource Allocation:
        CPU:                1
        Ephemeral Storage:  400M
        Memory:             4G

    Runtime:
        Array Indices:       0
        Max Execution Time:  7200
        Retry Limit:         3

    Status:
        Instance Statuses:
            Pending:  1
        Conditions:
            Type     Status  Last Probe  Last Transition
            Pending  True    100s        100s

    Events:
        Type    Reason   Age                   Source                Messages
        Normal  Updated  108s (x5 over 2m29s)  batch-job-controller  Updated JobRun "myjobrun1"

    Instances:
        Name           Running  Status   Restarts  Age
        myjobrun1-0-0  0/1      Pending  0         2m29s
    ```
    {: screen}

4. Create the secret.  

    ```txt
    ibmcloud ce secret create --name mynewliteralsecret --from-literal "TARGET=Fun secret"
    ```
    {: pre}

5. Run the `myjobrun1` job run again. 

    ```txt
    ibmcloud ce jobrun resubmit --jobrun myjobrun1 --name myjobrunresubmit1
    ```
    {: pre}

    Run the **`ibmcloud ce jobrun get -n myjobrunresubmit1`** command to check the status of this job run.

6. Display the logs of the `myjobrunresubmit1` job run. The logs display `Hello Fun secret from {{site.data.keyword.codeengineshort}}`, which confirms the job run referenced the `myliteralsecret` secret. 

    ```txt
    ibmcloud ce jobrun logs --jobrun myjobrunresubmit1
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of job run 'myjobrunresubmit1'...
    Getting jobrun 'myjobrunresubmit1'...
    Getting instances of jobrun 'myjobrunresubmit1'...
    OK

    myjobrunresubmit1-0-0/myjob:
    Hello from helloworld! I'm a batch job! Index: 0

    Hello Fun secret from:
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
    HOSTNAME=myjobrunresubmit1-0-0
    JOB_INDEX=0
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
    TARGET=Fun secret
    ```
    {: screen}

For more detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).


## Deleting secrets and configmaps 
{: #configmapsecret-delete}

When you no longer need a configmap or secret, you can delete it. 
{: shortdesc} 

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

    ```txt
    ibmcloud ce configmap delete --name myliteralconfigmap -f
    ```
    {: pre}

    Example output

    ```txt
    Deleting configmap 'myliteralconfigmap'...
    OK
    ```
    {: screen}

* To delete a secret with the CLI, use the [**`secret delete`**](/docs/codeengine?topic=codeengine-cli#cli-secret-delete) command; for example, 

    ```txt
    ibmcloud ce secret delete --name myliteralsecret -f
    ```
    {: pre}

    Example output

    ```txt
    Deleting secret myliteralsecret...
    OK
    ```
    {: screen}

You can also [delete environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-cli) that reference secrets and configmaps from the CLI.

