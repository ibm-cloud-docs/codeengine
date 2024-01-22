---

copyright:
  years: 2020, 2024
lastupdated: "2024-01-19"

keywords: configmaps with code engine, key references with code engine, key-value pair with code engine, setting up configmaps with code engine, configmaps, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with configmaps 
{: #configmap} 

Learn how to work with configmaps in {{site.data.keyword.codeengineshort}}. In {{site.data.keyword.codeengineshort}}, you can store your information as key-value pairs in configmaps that can be consumed by your app, job, or function workload by using environment variables. 
{: shortdesc}

## What are configmaps and why would I use them? 
{: #configmap-whatwhy}

In {{site.data.keyword.codeengineshort}}, both secrets and configmaps are key-value pairs. When mapped to environment variables, the `NAME=VALUE` relationships are set such that the name of the environment variable corresponds to the "key" of each entry in those maps, and the value of the environment variable is the "value" of that key.

A configmap provides a method to include non-sensitive data information to your deployment. By referencing values from your configmap as environment variables, you can decouple specific information from your deployment and keep your app, job, or function portable. A configmap contains information in key-value pairs.


Because secrets and configmaps are similar entities (except secrets are stored more securely), the way you interact and work with secrets and configmaps is also similar. To learn more about secrets, see [Working with secrets](/docs/codeengine?topic=codeengine-secret).
{: note} 



## I see configmaps that I didn't create. Can I delete them?
{: #inside-configmaps}

No. {{site.data.keyword.codeengineshort}} automatically creates the `istio-ca-root` and `kube-root-ca` configmaps in your namespace. {{site.data.keyword.codeengineshort}} uses these configmaps internally. If you delete these configmaps, {{site.data.keyword.codeengineshort}} automatically re-creates them.

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
4. From the Create secret or configmap page, complete the following steps:
    1. Click **Configmap**, and click **Next**. 
    2. Provide a name; for example, `myconfigmap`.
    3. Click **Add key-value pair**. Specify one or more key-value pairs for this configmap. For example, specify one key as `key1` with the value of `value1` and specify another key as `key2` with the value of `value2`. Notice that you can specify values on one or more lines. The name that you choose for your key does not need to be the same as the name of your environment variable.
    4. Click **Create** to create the configmap. 

Now that your configmap is created from the console, go to the Secrets and configmaps page to view a list of defined secrets and configmaps. You can apply filters to customize the list to meet your needs.

### Create a configmap with the CLI
{: #configmap-create-cli}

Create configmaps with the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

You can populate a configmap in several ways. You can populate it by specifying the key-value pairs directly on the command line, or you can point to a file. 

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

When you create (or update) a configmap from a file, the format must be `--from-file FILE` or `--from-file KEY=FILE`. In {{site.data.keyword.codeengineshort}}, when you use a file to specify configmap values, *all* the contents within the file become the value for the key-value pair. When you use the option format of `--from-file KEY=FILE`, the `KEY` is name of the environment variable that is known to your app, job, or function workload. When you use the option format of `--from-file FILE`, `FILE` is the name of the environment variable that is known to your job, app, or function. If your file contains one or more key-value pairs, use the `--from-env-file` option to add an environment variable for each key-value pair in the specified file. Any lines in the specified file that are empty or begin with `#` are ignored. 
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
    * If your configmap is referenced by an app, job, or function workload, then use the links in the environment variables table on the **Environmental variables** tab of your workload. These links take you directly to your configmap. 
2. Click **Edit** and make the updates for your configmap. 
3. Click **Save** to save the changes to your configmap.

If your updated configmap is referenced by an app, job, or function workload, then your workload must be restarted for the new data to take effect.

* Apps - From the page for your app, click **New revision** and then **Save and deploy**. Alternatively, you can wait for your app to scale to zero and when the app scales up, the app uses the updated configmap.
* Jobs - From the page for your job, click **Submit job** to run your job, or you can rerun a job. This new job run uses the updated configmap.
* Function - Your function is restarted when it is called again. You can test your function by clicking **Test function** from the function page.


### Updating configmaps with the CLI 
{: #configmap-update-cli}

You can update an existing configmap and its key-value pairs with the CLI.
{: shortdesc}

1. To change the value of a key-value pair in a configmap, use the [`configmap update`](/docs/codeengine?topic=codeengine-cli#cli-configmap-update) command. Let's update the `myliteralconfigmap` configmap to change the value of the `TARGET` key from `Sunshine` to `Stranger`.

    ```txt
    ibmcloud ce configmap update --name myliteralconfigmap --from-literal "TARGET=Stranger"
    ```
    {: pre}

2. Now that your configmap is updated, use the **`configmap get`** command to display details about a specific configmap. For example,

    ```txt
    ibmcloud ce configmap get --name myliteralconfigmap
    ```
    {: pre}

    Example output

    ```txt
    Getting configmap 'myliteralconfigmap'...
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

Your app, job, or function workload can consume and use the information that is stored in a configmap by using environment variables.  
{: shortdesc}

### Referencing configmaps from the console 
{: #configmap-ref-ui}

You can use the console to create environment variables for your app, job, or function workload that fully reference a configmap or reference individual keys in a configmap. 
{: shortdesc}

Before you can reference a configmap, it must exist. See [create a configmap](#configmap-create).

From the console, you can reference only one individual key of a defined configmap per environment variable. If you need to reference more than one key of a configmap, then repeat the steps to define another environment variable that references a different key.
{: note}

1. To reference a defined configmap from your app, job, or function workload, [create an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui). The environment variable can fully reference an existing configmap or reference an individual key in an existing configmap. For example, let's fully reference the `myconfigmap` configmap from the `myapp` application. When you fully reference a configmap (or secret), you can optionally specify a `prefix`. By using a prefix such as `myconfigmap_`, each key is prefixed with `myconfigmap_`. 

2. After you create environment variables, you must restart your app, job, or function workload for the changes to take effect. For apps, save and deploy your app to update the app with the environment variables that you defined. For jobs and functions, your workload is updated the next time it is called with the environment variables that you defined. 

3. After the application status changes to **Ready**, you can test the application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. In this `myapp` example, because we specified a prefix for the fully referenced `myconfigmap` configmap, all the keys of this configmap are referenced as environment variables and are prefixed with `myconfigmap_`. For example, these environment variables display as `myconfigmap_key1=value1` and `myconfigmap_key2=value2`.

To update an environment variable that references a configmap, see [updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui) and [considerations for updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider).

To remove an environment variable that references a configmap, see [deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Referencing configmaps with the CLI 
{: #configmap-ref-cli}

To use configmaps with app, job, or function workloads, you can set environment variables that fully reference a configmap or reference individual keys in a configmap with the CLI.
{: shortdesc}

#### Referencing existing configmaps with the CLI 
{: #configmap-ref-existing-cli}

To use a configmap with an app, job, or function workload with the CLI, specify the  `--env-from-configmap` option on the following commands.

- [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)
- [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create)
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update)
- [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit)
- [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit)
- [**`fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create)
- [**`fn update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) 

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

2. [Deploy an app](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#deploy-app-cli) and reference the `myliteralconfigmap` configmap. For this example, create an app that uses the `hello` image. When a request is sent to this sample app, the app reads the environment variable `TARGET` and prints `Hello ${TARGET}`. If this environment variable is empty, `Hello World` is returned. Reference the `myliteralconfigmap` configmap. For more information about the code that is used for this example, see [`hello`](https://github.com/IBM/CodeEngine/tree/main/hello){: external}.

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

    When you update an app, job, or function with an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set). 
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

If a configmap does not exist before it is referenced, the app, job, or function workload does not deploy successfully and a job or function do not run successfully until the referenced configmap is created.  

If you are working with an app, job, or function workload and the referenced configmap is not yet defined, you can use the `--force` option to avoid verification of the existence of the referenced configmap. The `--force` option can be used with the following commands.

- [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create)
- [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update)
- [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create)
- [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update)
- [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit)
- [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit)
- [**`fn create`**](/docs/codeengine?topic=codeengine-cli#cli-function-create)
- [**`fn update`**](/docs/codeengine?topic=codeengine-cli#cli-function-update) 

When you use the `--force` option with these commands, the action to create, update, or run the workload completes; however, the app, job, or workload will not run successfully until the referenced configmap exists. If you add the `--no-wait` option in addition to the `--force` option to the command, the system completes the action and does not wait for the workload to successfully run. 

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

## Deleting configmaps 
{: #configmap-delete}

When you no longer need a configmap, you can delete it. 
{: shortdesc} 

### Deleting configmaps from the console
{: #configmaps-delete-ui}

1. To delete a configmap from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the configmap that you want to delete to open its page. 
    3. From the page for the specific configmap, click **Actions > Delete configmap**. 
2. To delete a key-value pair for a specific configmap from the console, 
    1. Go to the Secrets and configmaps page from your [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click the configmap that you want to change to open its page. 
    3. From the page for the specific configmap, delete the key-value pair that you want to remove. 

You can also delete defined environment variables that reference secrets and configmaps. To delete a defined environment variable, from the **Environment variables** tab of your app, job, or function and delete the environment variable that you want to delete. After you delete a defined environment variable, be sure to click **Save** to save the changes to your app, job, or function. For more information, see [Delete an environment variable](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui).

### Deleting configmaps with the CLI
{: #configmap-delete-cli}

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

You can also [delete environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete-cli) that reference secrets and configmaps from the CLI.



