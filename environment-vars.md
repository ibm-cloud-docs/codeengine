---

copyright: 
  years: 2023
lastupdated: "2023-03-17"

keywords: environment variables with code engine, environment variables, creating environment variables, working with environment variables, key-value pair

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with environment variables  
{: #envvar} 

Learn how to work with environment variables (`env variables`) in {{site.data.keyword.codeengineshort}}. You can set environment variables as key-value pairs that can be used by your application or job. 
{: shortdesc}

## Creating and updating environment variables
{: #envvar-create}

Create and manage environment variables with {{site.data.keyword.codeengineshort}}.
{: shortdesc}

You can define environment variables as literal values or you can reference an existing secret or configmap. {{site.data.keyword.codeengineshort}} uses environment variables to enable [secrets](/docs/codeengine?topic=codeengine-secret) or [configmaps](/docs/codeengine?topic=codeengine-configmap) to be used by your job or application. 

### Creating environment variables from the console
{: #envvar-create-ui}

Create and update environment variables with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

You can define environment variables when you create your app or job, or when you update an existing app or job from the console.

Before you begin

- You must [create your project](/docs/codeengine?topic=codeengine-manage-project#create-a-project) and the [project](https://cloud.ibm.com/codeengine/projects){: external} must be in `active` status.
- Determine whether you want to create a literal environment variable or create an environment variable that references an existing secret or configmap. If you want your environment variable to fully reference an existing secret or configmap or reference individual keys in an existing secret or configmap, the secret or configmap must exist. See [create a secret](/docs/codeengine?topic=codeengine-secret#secret-create-ui) or [create a configmap](/docs/codeengine?topic=codeengine-configmap#configmap-create-ui) to define your secret or configmap before proceeding.


1. To open the dialog to define your environment variable on the Add environment variable page, complete one of the following choices.
    * If you are [creating an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console), from the Create application page, expand the **Environment variables (optional)** section. You can add one or more environment variables to the app that you are creating. Click **Add** to open the Add environment variable page. 
    * If you are [creating a job](/docs/codeengine?topic=codeengine-create-job#create-job-ui), from the Create job page, expand the **Environment variables (optional)** section. Click **Add** to open the Add environment variable page. 
    * If you are updating an existing app or job to add environment variables, go to the existing app or job and click the **Environment variables** tab. Click **Add** to open the Add environment variable page. 

2. From the Add environment variable page, create an environment variable in one of the following ways, 
    * To create a _literal_ environment variable, choose `Literal value`, specify the name for the literal environment variable, and provide a value. Notice that the `Resulting definition` section displays the name of the environment variable and its value.  
    * To create an environment variable that _fully references a configmap_, choose `Reference full configmap`, and then select the existing configmap. For this case, all keys of the selected configmap are referenced as part of the environment variable. Notice that the `Resulting definition` section displays the name of the keys in the configmap, but does not display the actual values of the keys that are referenced within the configmap.
    * To create an environment variable that _references an individual key of a defined configmap_, choose `Reference key in configmap`, select the existing configmap that you want, and then select the key to reference as part of the environment variable. After you select the individual key in the configmap that you want to reference, notice that the `Resulting definition` section displays the name of the selected key in the configmap, but does not display the actual value of the key that is referenced within the configmap.
    * To create an environment variable that _fully references a secret_, choose `Reference full secret`, and then select the existing secret. For this case, all keys of the selected secret are referenced as part of the environment variable. Notice that the `Resulting definition` section displays the name of the keys in the secret, but does not display the actual values of the keys that are referenced within the secret.
    * To create an environment variable that _references an individual key of a defined secret_, choose `Reference key in secret`, select the existing secret that you want, and then select the key to reference as part of the environment variable. After you select the individual key in the secret that you want to reference, notice that the `Resulting definition` section displays the name of the selected key in the secret, but does not display the actual value of the key that is referenced within the secret.

    From the console, you can reference only one individual key of a defined configmap or secret per environment variable. If you need to reference more than one key of a configmap or secret, then repeat the steps to define another environment variable that references a different key.
    {: note}

3. Click **Done** to save your changes. This action adds your environment variable to the table on the **Environment variables** tab. To continue adding environment variables, click **Add**. 
4. Complete the create or update for your app or job with the defined environment variable. 
    - If you are creating an app or job, when you click **Create**, the app or job is deployed with your environment variables.
    - If you are updating an existing app or job to add an environment variable, click **Save and deploy** to update the app or click **Save** to update your job with the new environment variables. 
5. When your app or job is in `Ready` state, your app or job is updated with your environment variables.

The following table describes information about your environment variables.  

| Heading                     |         Description         |
| --------------------------- | --------------------------- |
| `Name`                      | The name of your environment variable. |
| `Defined by`                | Specifies whether the environment variable is of type `literal`, or whether the environment variable is a fully referenced configmap or secret, or whether specific keys of a secret or configmap are referenced. |
| `Value or reference`        | Displays the literal value, the fully referenced configmap or secret, or the referenced keys of a configmap or secret. |
{: caption="Table of environment variables"}


For example, let's create an app and set environment variables for the app. 

1. [Create an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) that is named `myapp`, which uses the `icr.io/codeengine/codeengine` image. This `hello-world` app includes the `TARGET` environment variable, and the app prints `Hello ${TARGET} from {{site.data.keyword.codeengineshort}}` and prints a listing of environment variables. If the `TARGET`environment variable is empty, `Hello World from {{site.data.keyword.codeengineshort}}` is returned. 
2. Go to this app in the console. 
3. When the app is in `Ready` state, you can test your app. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. The `myapp` app returns a `Hello World from {{site.data.keyword.codeengineshort}}` response and prints the environment variables that are included in this app. 
4. Click the **Environment variables** tab.  
5. Create the following environment variables.
    * Click **Add** to open the Add environment variable page and create a _literal_ environment variable. For example, create a literal environment variable with the name `literalenvvar` and with the value of `This is my literal`. Click **Done** to save your changes.
    * Click **Add** to open the Add environment variable page and create an environment variable that _fully references a configmap_. Before you can reference a configmap, it must exist. For this example, a configmap with the name `mycolorconfigmap` exists and contains the following key-value pairs: `key1=blue`, `key2=green`, and `key3=yellow`. Create an environment variable that fully references the `mycolorconfigmap` configmap, including all its key-value pairs. Notice that the `Resulting definition` section displays the name of the keys in the configmap, but does not display the actual values of the keys that are referenced within the configmap. Click **Done** to save your changes.
    * Click **Add** to open the Add environment variable page and create another environment variable that _references an individual key of a defined secret_. Before you can reference a secret, it must exist. For this example, a secret with the name `mynewsecret` exists and contains the following key-value pairs: `newsec1=mynewsecret1`, `newsec2=mynewsecret2`, and `newsec3=mynewsecret3`. Create an environment variable that references the `newsec2` key of the `mynewsecret` secret. Notice the `Resulting definition` section displays the name of the selected key in the secret, but does not display the actual value of the key that is referenced within the secret. Click **Done** to save your changes.
6. Click **Save and create** to update the app with the new environment variables. 
7. When the app is in `Ready` state, your app is updated with your environment variables. 
8. To test your app, click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.  With this app revision, this app outputs `Hello World from {{site.data.keyword.codeengineshort}}` and the output includes the names of the environment variables, which were added in the previous steps.  

When you set environment variables in your app or job, this action adds a new environment variable or overrides an existing environment variable. If you have an environment variable with the same *Name*, and specify a different *value* than the previously defined environment variable, then the updated environment variable overrides the existing value. For example, if you have a defined environment variable that is named `envvar1` and its value is `myenvar1`, and you define another environment variable that is also named `envvar1` and specify its value as `mynewenvvar1`, then after you save and deploy your updated app or you save your updated job, your running app, or job uses the `envvar1` environment variable with value `mynewenvvar1`.
{: note}


### Updating environment variables from the console 
{: #envvar-update-ui}

1. To update an existing environment variable, go to your app or job that includes the environment variable that you want to change and click the **Environment variables** tab to display your table of environment variables. 
2. From the table of environment variables, click the environment variable that you want to update.
3. From the Edit environment variable page, make your update and click **Done** to save your changes. When you edit your environment variable, you can change the **Defined by** value and its corresponding required fields.
4. Click **Save and deploy** to deploy your application with your changes or click **Save** to run your job with your changes. When your app or job is in `Ready` state, your app or job is updated with your environment variables.  

### Creating and updating environment variables with the CLI
{: #envvar-create-cli}

Create and manage environment variables with the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

You can define environment variables when you create your app or job, or when you update an existing app or job with the CLI. 

When you create an environment variable with the CLI, you can reference configmaps or secrets, or you can create a literal environment variable. These instructions describe creating and updating *literal* environment variables with the CLI. 

For detailed scenarios about referencing full secrets and configmaps as environment variables, overriding references, and removing references in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).

Before you begin

* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).


#### Create and update environment variables for your app
{: #envvar-create-cli-app}

Create and update environment variables for your app as follows,   

* To create and set an environment variable for your app, use the `--env` option with the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) or [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. The following example creates the `myapp` application that uses the `icr.io/codeengine/codeengine` image, and defines the `envA` and `envB` environment variables.

    ```txt
    ibmcloud ce application create --name myapp --image icr.io/codeengine/codeengine --env envA=A --env envB=B
    ```
    {: pre}

* To update environment variables for an existing application, use the `--env` option with the [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. The following example updates the `myapp` application to overwrite the value of `envA` and adds the `envC` environment variable. 

    ```txt
    ibmcloud ce application update --name myapp  --env envA=AA --env envC=C
    ```
    {: pre}
    
#### Create and update environment variables for your job
{: #envvar-create-cli-job}

Set and update environment variables for your job as follows,  

* To create and set an environment variable for your job, use the `--env` option with the [**`job create`**](/docs/codeengine?topic=codeengine-cli#cli-job-create), [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command. The following example creates the `myjob` job that uses the `icr.io/codeengine/codeengine` image, and defines the `envA` environment variable.

    ```txt
    ibmcloud ce job create --name myjob --image icr.io/codeengine/codeengine --env envA=A 
    ```
    {: pre}

* To update environment variables for an existing job, use the `--env` option with the [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update), [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit), or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command.

Example 1

The following example updates the `myjob` job to overwrite the value of `envA` and adds the `envB` environment variable. 

```txt
ibmcloud ce job update --name myjob  --env envA=AA --env envB=B
```
{: pre}

Run the **`job get`** command to display details of the job, including its environment variables.  

```txt
ibmcloud ce job get --name myjob
```
{: pre}

Example output

```txt
Getting job 'myjob'...
OK

Name:          myjob
[...]
Environment Variables:
    Type     Name  Value
    Literal  envA  AA
    Literal  envB  B
Image:                  icr.io/codeengine/codeengine
[...]
```
{: screen}

Example 2

The following example runs the `myjob` job, overwrites the value of `envA`, and adds the `envD` environment variable for this job run. 

```txt
ibmcloud ce jobrun submit --job myjob  --name myjobrun1 --env envB=BB --env envC=C
```
{: pre}

Run the **`jobrun get`** command to display details of the job run, including its environment variables.  

```txt
ibmcloud ce jobrun get --name myjobrun1
```
{: pre}

Example output

```txt
[...]
Name:          myjobrun1
[...]
Job Ref:                myjob
Environment Variables:
    Type     Name  Value
    Literal  envA  AA
    Literal  envB  BB
    Literal  envC  C
Image:                  icr.io/codeengine/codeengine
[...]

Instances:
Name           Running  Status   Restarts  Age
myjobrun1-0-0  0/1      Succeeded  0         17s
```
{: screen}

## Considerations for updating apps or jobs with environment variables 
{: #envvar-upd-consider}

Consider the following information when you update an app or job that has an environment variable that references configmaps or secrets. 
* When you update an app or job that has an environment variable that fully references a configmap (or secret) to fully reference a different configmap (or secret), full references override other full references in the order in which they are set (the last referenced set overrides the first set).
* When you update an app or job that has an environment variable that references a key in one configmap (or secret) to reference the same key in a different configmap (or secret), then the last referenced key is used.  
* When you update an app or job that has an environment variable that fully references a configmap (or secret) to add a reference to a specific key, then the specific key reference overrides the full configmap (or secret) reference. 
{: note}

## Deleting environment variables 
{: #envvar-delete}

When you no longer need an environment variable, you can delete it. 
{: shortdesc}

### Deleting environment variables from the console
{: #envvar-delete-ui}

1. From the console, go to the app or job that has the environment variable that you want to delete. Click the **Environment variables** tab. 
2. From the table of environment variables, delete the environment variable that you want to remove from the app or job.
3. Click **Save and deploy** to update the app or click **Save** to update your job with the new environment variables. When your app or job is in `Ready` state, your app or job is updated with your current environment variables.  


### Deleting environment variables with the CLI
{: #envvar-delete-cli}

When you work with environment variables with the CLI, you can reference existing configmaps or secrets, or you can work with literal environment variables. These instructions describe deleting *literal* environment variables with the CLI. 

For detailed scenarios about removing references to full secrets and configmaps in the CLI, see [Referencing secrets and configmaps](/docs/codeengine?topic=codeengine-secretcm-reference).

#### Delete environment variables for your app 
{: #envvar-delete-cli-app}

To remove an environment variable for your app, use the `--env-rm` option with the [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command. The following example updates the `myapp` application to delete the `envA` environment variable.

```txt
ibmcloud ce application update --name myapp --env-rm envA
```
{: pre}


#### Delete environment variables for your job 
{: #envvar-delete-cli-job}  

To remove an environment variable for your job, use the `--env-rm` option with the [**`job update`**](/docs/codeengine?topic=codeengine-cli#cli-job-update) or [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) command. 

Use the `--env-rm` option with the **`job update`** command to remove environment variables set on the job. Use the `--env-rm` option with the **`jobrun resubmit`** command to remove environment variables set on a specified job run.
{: note}

* The following example updates the `myjob` job to delete the `envA` environment variable. 

    ```txt
    ibmcloud ce job update --name myjob  --env-rm envA 
    ```
    {: pre}

    Use the [**`job get`**](/docs/codeengine?topic=codeengine-cli#cli-job-get) command to display details of the job, including its environment variables. 

* The following example resubmits the `myjobrun1` job run and deletes the `envC` environment variable. 

    ```txt
    ibmcloud ce jobrun resubmit --jobrun myjobrun1  --name jobrun2resuba--env-rm envC
    ```
    {: pre}

    Run the **`jobrun get`** command to display details of the job run, including its environment variables.  

    ```txt
    ibmcloud ce jobrun get --name jobrun2resuba
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'jobrun2resuba'...
    Getting instances of jobrun 'jobrun2resuba'...
    Getting events of jobrun 'jobrun2resuba'...
    [...]

    Name:          jobrun2resuba
    [...]
    Job Ref:                myjob
    Environment Variables:
        Type     Name  Value
        Literal  envB  BB
    Image:                  icr.io/codeengine/codeengine
    [...]

    Instances:
    Name               Running  Status     Restarts  Age
    jobrun2resuba-0-0  0/1      Succeeded  0         21s
    ```
    {: screen}


