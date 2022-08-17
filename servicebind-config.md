---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-17"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Binding a service instance to a {{site.data.keyword.codeengineshort}} app or job
{: #bind-services}

You can integrate an {{site.data.keyword.cloud_notm}} service instance to resources in an {{site.data.keyword.codeenginefull}} project by using service bindings. 
{: shortdesc} 

Before you begin

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.

## Configuring access policies for a service binding
{: #configure-binding}

Before you can bind to a service instance, your {{site.data.keyword.codeengineshort}} project must be configured to create service bindings. {{site.data.keyword.codeengineshort}} uses a Service ID to access {{site.data.keyword.cloud_notm}} services with service bindings. For more information about service binding access requirements, see [Service Binding access](/docs/codeengine?topic=codeengine-service-binding#service-binding-access).

Consider the following cases to ensure you have access for working with service bindings.

* You can use the [default service binding access policies](#bind-auto-servid) and let {{site.data.keyword.codeengineshort}} automatically create the Service ID for you to access all services in the resource group of your project.

* You can [configure your project to use a custom Service ID](#bind-custom-servid) if you don't want to use the default service binding access policies to let {{site.data.keyword.codeengineshort}} automatically create the Service ID for you.

* You must [configure your project for access to a resource group](#bind-config-proj) if the {{site.data.keyword.cloud_notm}} resource that you want to bind to your {{site.data.keyword.codeengineshort}} app or job is in a resource group that is different than the resource group of your {{site.data.keyword.codeengineshort}} project for your app or job.

### Using the default service binding access policies
{: #bind-auto-servid}

By default, {{site.data.keyword.codeengineshort}} automatically creates a Service ID for accessing all services in the resource group of the {{site.data.keyword.codeengineshort}} project when your account that is used with your {{site.data.keyword.codeengineshort}} project has sufficient permissions.

The {{site.data.keyword.cloud_notm}} account that is used with your {{site.data.keyword.codeengineshort}} project must have `Reader` and `Writer` service access and `Viewer` and `Operator` platform access. With these permissions for your account, {{site.data.keyword.codeengineshort}} checks and automatically sets up a Service ID with `Operator` and `Manager` access for all services in the resource group of the {{site.data.keyword.codeengineshort}} project. {{site.data.keyword.codeengineshort}} uses this Service ID to access {{site.data.keyword.cloud_notm}} services with service bindings. 

If you have insufficient permissions to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you. If you want more control over access policies, you can set policies manually by [configuring your project for access to a resource group](#bind-config-proj) or [configure your project to use a custom Service ID](#bind-custom-servid).

For more information about {{site.data.keyword.codeengineshort}} service binding access requirements, see [What access do I need to create service bindings?](/docs/codeengine?topic=codeengine-service-binding#service-binding-access).

### Configuring a project with a custom service ID
{: #bind-custom-servid}

To configure a {{site.data.keyword.codeengineshort}} project for service binding with a custom Service ID, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the desired project.  Use the [**`ibmcloud ce project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to display all projects, including information for the selected project. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
{: note} 

1. Create a Service ID with the policies required for your service binding needs. For more information about working with Service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
2. Find the ID of your Service ID by clicking Details on your Service ID page or else run `ibmcloud iam service-ids`.
3. Run the **`ibmcloud ce project update`** command. For example, if the ID of your Service ID is `ServiceId-12a3456b-c78d-901e-f2a3b4cabcde`:

    ```txt
    ibmcloud ce project update --binding-service-id ServiceId-12a3456b-c78d-901e-f2a3b4cabcde
    ```
    {: pre}

### Configuring a project for access to a resource group
{: #bind-config-proj}

If the {{site.data.keyword.cloud_notm}} service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job is in a different resource group than the resource group of the {{site.data.keyword.codeengineshort}} project for your app or job, then you must update the project to access service instances in other resource groups before you can complete the binding. For example, if your {{site.data.keyword.codeengineshort}} project is in the `Default` resource group, and you want to bind to a service instance that exists in the `dev` resource group, you must update the {{site.data.keyword.codeengineshort}} project so that {{site.data.keyword.codeengineshort}} can access services instances in other resource groups.

To configure a {{site.data.keyword.codeengineshort}} project for service binding access for all service instances in a resource group, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the desired project.  Use the [**`ibmcloud ce project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to display all projects, including information for the selected project. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
{: note} 

* To configure service binding access for all service instances in the **Default** resource group,

    ```txt
    ibmcloud ce project update --binding-resource-group Default
    ```
    {: pre}

* To configure service binding access for all service instances in a resource group, by specifying the ID of the resource group,

    ```txt
    ibmcloud ce project update --binding-resource-group-id abcdabcdabcdabcdabcdabcdabcdabcd 
    ```
    {: pre}

    To get a list of your resource groups, including the resource group IDs, run **`ibmcloud resource groups`**.

* To configure service binding access for all service instances in _all_ resource groups:

    ```txt
    ibmcloud ce project update --binding-resource-group "*"
    ```
    {: pre}

When you run the **`project update`** command, a service ID is created for the project and is used to configure the current project for service bindings. If you do not have permission to create this Service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you. For more information about {{site.data.keyword.codeengineshort}} service binding access requirements, see [What access do I need to create service bindings?](/docs/codeengine?topic=codeengine-service-binding#service-binding-access).


## Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job
{: #bind}

Now that you have a service instance that you want to bind to a {{site.data.keyword.codeengineshort}} app or job, and your {{site.data.keyword.codeengineshort}} project is configured with access policies for a service binding, you are ready to bind your {{site.data.keyword.codeengineshort}} app or job to the service instance. 

### Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job from the console
{: #bind-ui}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* Create the service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.
* [Create an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) or [create a job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) to bind to your service instance. 

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}. 
2. From the Overview page, click **Service bindings**.
3. From the Service bindings page, click **Create service binding** to create your binding.  
4. From the Create service binding page, complete the following steps.
    1. Select the IBM service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.  
    2. Select the {{site.data.keyword.codeengineshort}} app or job that you want to bind to the service instance.
    3. (optional) Specify a custom prefix for the service binding. The prefix is for environment variables that are created for this service binding. 
5. Now that your service binding to your app or job is created from the console, go to the Service bindings page to view a listing of defined service bindings between service instances and {{site.data.keyword.codeengineshort}} apps and jobs.  

### Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job with the CLI
{: #bind-cli}

Before you begin

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project). 
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* Create the service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.

    For example, to create an {{site.data.keyword.cos_full_notm}} service instance (Lite plan):

    ```txt
    ibmcloud resource service-instance-create my-object-storage cloud-object-storage lite global -g Default
    ```
    {: pre}

* Create a {{site.data.keyword.codeengineshort}} application.

    For example, to create an application that is called `my-application` that uses the `icr.io/codeengine/hello` image:

    ```txt
    ibmcloud ce application create --name my-application --image icr.io/codeengine/hello
    ```
    {: pre}

#### Binding a service instance with a new credential
{: #bind-credentials}


To bind your new service instance to your {{site.data.keyword.codeengineshort}} application and generate a new service credential, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    Example output

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with the default service role. The default service role is either Manager or the first role that is provided by the service if Manager is not supported. The following example **`application bind`** command binds the `my-object-storage` service instance with the app called `my-application`. A new service credential with the Manager role is generated for this binding action.

    ```txt
    ibmcloud ce application bind --name my-application --service-instance my-object-storage
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the application to bind. This value is required. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the application. This value is required. |
    {: caption="Table 1. Command options" caption-side="bottom"}

    Example output

    ```txt
    Binding service instance...
    Status: Done
    Waiting for application revision to become ready...
    The Configuration is still working to reflect the latest desired specification.
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready.
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage     cloud-object-storag   Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}

#### Binding a service instance with a particular role
{: #bind-credentials-role}

To bind a service instance to your {{site.data.keyword.codeengineshort}} application and generate new service credentials with a particular role, use the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command. To bind your service instance to a {{site.data.keyword.codeengineshort}} job, use the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    Example output

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Bind your service instance to your {{site.data.keyword.codeengineshort}} application or job and generate a new service credential with a particular service role. For more information about IAM service roles, see [Service access roles](/docs/account?topic=account-userroles#service_access_roles). The following example **`application bind`** command binds the `my-object-storage` service instance to the app called `my-application` by using the Writer service role. A new service credential with the Writer role is generated for this binding action. By specifying the `--prefix` option, a prefix is added to the environment variables that are created by the service bindings.

    ```txt
    ibmcloud ce application bind --name my-application --service-instance my-object-storage --role Writer --prefix MyPrefix
    ```
    {: pre}

    The following table summarizes the options that are used with the **`application bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce application bind`**](/docs/codeengine?topic=codeengine-cli#cli-application-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the application to bind. This value is required. |
    | `--prefix` | The prefix for environment variables that are created for this service binding. For example, `--prefix MyPrefix` adds the `MyPrefix` prefix to any environment variables that are created for this service binding. For more information, see [using a prefix](/docs/codeengine?topic=codeengine-service-binding#prefix-method) with environment variables to access a bound service instance from an app or job. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the application. This value is required. |
    | `--role` | The name of a service role for the new service credential that is created for this service binding. Valid values include `Reader`, `Writer`, `Manager`, or a service-specific role. If the `--role` option is not specified, the default is `Manager` or the first role that is provided by the service if `Manager` is not supported. This option is ignored if `--service-credential` is specified. |
    {: caption="Table 2. Command options" caption-side="bottom"}

    Example output

    ```txt
    Binding service instance...
    Status: Done
    Waiting for application revision to become ready...
    The Configuration is still working to reflect the latest desired specification.
    Traffic is not yet migrated to the latest revision.
    Ingress has not yet been reconciled.
    Waiting for load balancer to be ready.
    OK
    ```
    {: screen}

3. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage  cloud-object-storage     Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}

#### Binding a service instance with existing credentials
{: #bind-existing-credentials}

If you already created a credential for your service instance and want to use it for your service binding, add the `--service-credentials` option.

1. Identify the name of the service instance that you want to bind to your app or job. You can find all the service instances that are in your account for your current resource group by running the **`ibmcloud resource service-instances`** command; for example, 

    ```txt
    ibmcloud resource service-instances
    ```
    {: pre}

    Example output

    ```txt
    Name                               Location   State    Type               Resource Group ID
    my-object-storage                  global     active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer1                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    tone_analyzer2                     us-south   active   service_instance   325d80be5d7945608f6d121712c96ee9
    ```
    {: screen}

2. Find the credentials of the service instance.

    ```txt
    ibmcloud resource service-keys --instance-name INSTANCENAME
    ```
    {: pre}
    
    Example output
    
    ```txt
    Name                State    Created At       
    my-cos-credential   active   Tue Mar  2 01:15:33 UTC 2021 
    ```
    {: screen}

    To see details of a service credential, run `ibmcloud resource service-key KEYNAME`. You can find all the service keys in your resource group by running `ibmcloud resource service-keys`.
    {: tip}

3. Bind the service instance to the application or job with existing credentials. For example, the following **`job bind`** command binds the `my-object-storage` service instance with existing service credentials called `my-cos-credential` to an existing job that is called `myjob`.

    ```txt
    ibmcloud ce job bind --name myjob --service-instance my-object-storage --service-credential my-cos-credential
    ```
    {: pre}

    The following table summarizes the options that are used with the **`job bind`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce job bind`**](/docs/codeengine?topic=codeengine-cli#cli-job-bind) command.

    | Option | Description |
    | --- | --- |
    | `--name` | The name of the job to bind. This value is required. |
    | `--service-instance` | Specify the name of an existing service instance to bind to the job. This value is required. |
    | `--service-credential` | The name of the existing service credential to bind. |
    {: caption="Table 3. Command options" caption-side="bottom"}

4. Verify that the credentials were generated by using the **`application get`** or the **`job get`** command. In the following example, verify that the credentials that were created in the previous example were created. 

    ```txt
    ibmcloud ce job get --name myjob
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Service Bindings:
    Name                                 ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    myjob-ce-service-binding-abcde       abcde645-d3f9-407d-b964-6c3ae69abcde  myfmo-object-storage  cloud-object-storage  my-cos-credential  CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen} 

## Unbinding service instances
{: #unbind}

Unbinding service instances from an application or job removes existing service bindings.

### Unbinding a service instance from the console
{: #unbind-ui}

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project. 
2. From the Overview page, click **Service bindings** to view a listing of defined service bindings. 
3. From the list of service bindings, delete the binding that you want to remove from your application or job.

### Unbinding a service instance with the CLI
{: #unbind-cli}

1. Find the service binding that you want to remove with the **`application get`** or **`job get`** command; for example, 

    ```txt
    ibmcloud ce application get --name my-application
    ```
    {: pre}

    Example output

    ```txt
    [...]
    Service Bindings:
    Name                                         ID                                    Service Instance      Service Type          Role / Credential  Environment Variable Prefix
    my-application-app-ce-service-binding-abcde  abcde5d3-dfc3-4f52-b133-b869b5eabcde  my-object-storage     cloud-object-storage  Writer             CLOUD_OBJECT_STORAGE
    [...]
    ```
    {: screen}

2. Remove the service binding by using the **`application unbind`** or the **`job unbind`** command.

    * To remove a single binding, specify the `--name` and `--binding` options. 

        ```txt
        ibmcloud ce application unbind --name APPLICATION_NAME --binding BINDING_NAME
        ```
        {: pre}

    * To unbind all service instances, use the `--all` option.

        ```txt
        ibmcloud ce job unbind --name JOB_NAME --all
        ```
        {: pre}



