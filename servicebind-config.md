---

copyright:
  years: 2020, 2022
lastupdated: "2022-10-10"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Binding a service instance to a {{site.data.keyword.codeengineshort}} app or job
{: #bind-services}

You can integrate an {{site.data.keyword.cloud_notm}} service instance to resources in an {{site.data.keyword.codeenginefull}} project by using service bindings. 
{: shortdesc} 

## Configuring access policies for a service binding
{: #configure-binding}

Service bindings in {{site.data.keyword.codeengineshort}} use a service ID to access {{site.data.keyword.cloud_notm}} services. A service ID contains the credentials to communicate with a service instance on behalf of your {{site.data.keyword.codeengineshort}} project.

Access policies must be configured before you can [bind a service instance to a {{site.data.keyword.codeengineshort}} application or job](#bind).
{: important}

Before you can bind your app or job to a specific {{site.data.keyword.cloud_notm}} service instance, determine whether you want to [create and manage your own service ID](/docs/account?topic=account-serviceids), or if you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for you. Based on your choice, assign the proper access policies. {{site.data.keyword.codeengineshort}} uses one service ID per project to work with service bindings. 

* If you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for you, then configure [default service binding access policies](#bind-auto-servid). Ensure that proper access policies are assigned to the {{site.data.keyword.cloud_notm}} account that is used with your {{site.data.keyword.codeengineshort}} project. If your {{site.data.keyword.codeengineshort}} project is in the *same* resource group from the service instance that you want to bind to, then no additional configuration is required. If your {{site.data.keyword.codeengineshort}} project is in a *different* resource group from the service instance that you want to bind to, then instead of configuring default service binding access policies, you must use the **`project update --binding-resource-group`** command to [configure your project for access to a resource group](#bind-config-proj). When you configure your project for access to a different resource group, this action also automatically creates a service ID for you.

* If you want to use your own custom service ID that you configured in your service instance, outside of {{site.data.keyword.codeengineshort}}, then you must use the **`project update --binding-service-id`** command to [configure your project to use a custom service ID](#bind-custom-servid). In this case, assign access policies to your custom service ID.

### Using the default service binding access policies
{: #bind-auto-servid}

By default, {{site.data.keyword.codeengineshort}} automatically creates a service ID for accessing all services in the resource group of the {{site.data.keyword.codeengineshort}} project when your account that is used with your project has sufficient permissions. The service ID is created during the first service binding operation. 

The {{site.data.keyword.cloud_notm}} account that is used with your {{site.data.keyword.codeengineshort}} project must have `Reader` and `Writer` service access and `Viewer` and `Operator` platform access. With these permissions for your account, {{site.data.keyword.codeengineshort}} checks and automatically sets up a service ID with `Operator` and `Manager` access for all services in the resource group of the {{site.data.keyword.codeengineshort}} project. {{site.data.keyword.codeengineshort}} uses this service ID to access {{site.data.keyword.cloud_notm}} services with service bindings. 

If you have insufficient permissions to create this service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you. If you want more control over access policies, you can set policies manually by [configuring your project for access to a resource group](#bind-config-proj) or [configure your project to use a custom service ID](#bind-custom-servid).

For more information about {{site.data.keyword.codeengineshort}} service binding access requirements, see [What access do I need to create service bindings?](/docs/codeengine?topic=codeengine-service-binding#service-binding-access)

### Configuring a project for access to a resource group
{: #bind-config-proj}

If the {{site.data.keyword.cloud_notm}} service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job is in a different resource group than the resource group of the {{site.data.keyword.codeengineshort}} project for your app or job, then you must update the project to access service instances in other resource groups before you can complete the binding. For example, if your {{site.data.keyword.codeengineshort}} project is in the `Default` resource group, and you want to bind to a service instance that exists in the `dev` resource group, you must update the {{site.data.keyword.codeengineshort}} project so that {{site.data.keyword.codeengineshort}} can access services instances in other resource groups.

To configure a {{site.data.keyword.codeengineshort}} project for service binding access for all service instances in a resource group, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the desired project.  Use the [**`ibmcloud ce project current`**](/docs/codeengine?topic=codeengine-cli#cli-project-current) command to display details of the project that is currently targeted. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
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

When you run the **`project update`** command, a service ID is created for the project, and is used to configure the current project for service bindings. If you do not have permission to create this service ID, then you receive an error and the service binding is not created. Talk to your account administrator about your access policies, or ask them to configure the {{site.data.keyword.codeengineshort}} project for you. For more information about {{site.data.keyword.codeengineshort}} service binding access requirements, see [What access do I need to create service bindings?](/docs/codeengine?topic=codeengine-service-binding#service-binding-access)

### Configuring a project with a custom service ID
{: #bind-custom-servid}

To configure a {{site.data.keyword.codeengineshort}} project for service binding with a custom service ID, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command.

The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the desired project.  Use the [**`ibmcloud ce project current`**](/docs/codeengine?topic=codeengine-cli#cli-project-current) command to display details of the project that is currently targeted. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
{: note}




1. Create a service ID with the [access policies](/docs/codeengine?topic=codeengine-service-binding#service-binding-access) that are required for your service binding needs. For more information about working with service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).
2. Find the ID of your service ID by clicking Details on your service ID page or else run `ibmcloud iam service-ids`.
3. Run the **`ibmcloud ce project update`** command. For example, if the ID of your service ID is `ServiceId-12a3456b-c78d-901e-f2a3b4cabcde`:

    ```txt
    ibmcloud ce project update --binding-service-id ServiceId-12a3456b-c78d-901e-f2a3b4cabcde
    ```
    {: pre}

Whenever you run the **`project update --binding-service-id`** command, {{site.data.keyword.codeengineshort}} replaces any existing service ID and uses this service ID for service bindings.  

## Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job (updated info)
{: #bind}

Now that you have a service instance that you want to bind to a {{site.data.keyword.codeengineshort}} app or job, and your {{site.data.keyword.codeengineshort}} project is configured with access policies for a service binding, you are ready to bind the service instance to your {{site.data.keyword.codeengineshort}} app or job. 

[Access policies](#configure-binding) must be configured before you can bind a service instance to a {{site.data.keyword.codeengineshort}} application or job.
{: important}

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console) or [create a job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) to bind to your service instance. The app or job that you want to bind to the service instance must exist.
* Create the service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.


When you bind a service instance to an app or job, {{site.data.keyword.codeengineshort}} uses a *service access secret* to store the credential of the specified {{site.data.keyword.cloud_notm}} service instance. This type of secret is the key mechanism in a service binding that connects the {{site.data.keyword.cloud_notm}} service instance to a particular {{site.data.keyword.codeengineshort}} app or job. {{site.data.keyword.codeengineshort}} creates and manages this secret for you.

When you create your {{site.data.keyword.cloud_notm}} service instance, you can create the service credential for that service instance. Or, when you create a service binding, you can choose for {{site.data.keyword.codeengineshort}} to automatically create the service instance credential for you if you configured [access policies](#configure-binding).

Whether you choose for {{site.data.keyword.codeengineshort}} to automatically create the service credential for you or you manually create the service credential for a particular service instance, you must specify the Identity and Access Management (IAM) role for the service credential. The role that you specify defines the interaction that is allowed with the particular service instance.

### Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job from the console (updated)
{: #bind-ui}

You can create a service binding that binds an existing service instance to a {{site.data.keyword.codeengineshort}} app or job by using console.
#### Binding a service instance with a new credential (auto-generated)
{: #bind-credential-ui-newauto}

Let's create a service binding to bind a service instance to an app or job with a new service credential that is automatically generated by {{site.data.keyword.codeengineshort}}. This scenario creates a service binding from the console from the **Service bindings** page. For this example, create a service binding for the `myapp` application and choose for {{site.data.keyword.codeengineshort}} to automatically create the service credential to an {{site.data.keyword.cloud_notm}} service instance.
1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. From the Overview page, click **Service bindings**.
3. From the Service bindings page, click **Add service binding** to create the binding.
4. Select the IBM service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.
5. Select the {{site.data.keyword.codeengineshort}} app or job that you want to bind to the service instance; for example, choose the `myapp` application.
6. Specify the service access secret to use with this binding. The service access secret stores the credential for the service binding. Notice that any previously defined service credential for your specific service instance, which is not associated with the app or job that you selected, is listed. For this scenario, select **New secret** to specify to use a new credential for the service access secret. To use a new credential for the service access secret for this binding, select **New secret**. Complete the following steps.
    1. Select the **Role** for the service instance credential.
    2. Expand **Advanced options**.
    3. For {{site.data.keyword.codeengineshort}} to automatically create the service credential to an {{site.data.keyword.cloud_notm}} service instance, select `Auto-generate`.
    4. (optional) Specify a custom prefix for the service binding. If you do not specify a custom prefix, {{site.data.keyword.codeengineshort}} automatically generates a prefix. The prefix is used to distinguish environment variables that are created for this service binding.
7. Click **Add** to create the service binding.
8. Now that your service binding to your app or job is created from the console, you can view a list of all defined service bindings between service instances and {{site.data.keyword.codeengineshort}} apps and jobs from the Service bindings page.

#### Binding a service instance with a new credential (bring your own)
{: #bind-credential-ui-newbringyourown}

Let's create a service binding to bind a service instance to an app with a new service credential where you use a custom service ID. This scenario creates a service binding from the console from the **Service bindings** page. For this example, create a service binding for the `myapp` application and use a custom service ID that you generated for your {{site.data.keyword.cloud_notm}} service instance.

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. From the Overview page, click **Service bindings**.
3. From the Service bindings page, click **Add service binding** to create your binding.
4. Select the IBM service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.
5. Select the {{site.data.keyword.codeengineshort}} app or job that you want to bind to the service instance; for example, choose the `myapp` application.
6. Specify the service access secret to use with this binding. The service access secret stores the credential for the service binding. Notice that any previously defined service credential for your specific service instance, which is not associated with the app or job that you selected, is listed. For this scenario, select **New secret** to specify to use a new credential for the service access secret. sComplete the following steps.
    1. Select the **Role** for the service instance credential.
    2. Expand **Advanced options**.
    3. For {{site.data.keyword.codeengineshort}} to automatically create the access secret to an {{site.data.keyword.cloud_notm}} service instance, select the service credential that you previously created.
    4. (optional) Specify a custom prefix for the service binding. If you do not specify a custom prefix, {{site.data.keyword.codeengineshort}} automatically generates a prefix. The prefix is used to distinguish environment variables that are created for this service binding.
7. Click **Add** to create the service binding.
8. Now that your service binding to your app or job is created from the console, you can view a list of all defined service bindings between service instances and {{site.data.keyword.codeengineshort}} apps and jobs from the Service bindings page.


#### Binding a service instance with an existing credential
{: #bind-credential-ui-existing}

Suppose you want to use an existing credential in your service binding. You can reuse service access secrets. However, since the credential is stored within the service access secret, it is important to consider the following points:

* You can have more than one application or job that is bound to the same {{site.data.keyword.cloud_notm}} service instance with the same service access secret.

* A service access secret cannot be reused in a service binding for an app or job. However, you can reuse the same service access secret in a different app or job.

* Because a service access secret is associated with a specific {{site.data.keyword.cloud_notm}} service instance, you can reuse only the service access secret in a different application, or job if you are binding to the same service instance.

Let's create a service binding to bind a service instance to a job that uses an existing service access secret. For example, create a service binding for the `myjob` job and choose an existing service access secret for a particular service instance.

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. From the Overview page, click **Service bindings**.
3. From the Service bindings page, click **Add service binding** to create your binding.
4. Select the IBM service instance that you want to bind to your {{site.data.keyword.codeengineshort}} app or job.
5. Select the {{site.data.keyword.codeengineshort}} app or job that you want to bind to the service instance.
6. Because we have service bindings that exist to a particular service instance, we can use an existing credentials for the service access secret. Select **Existing secret**. Notice that any previously defined service credential for your specific service instance is listed, which are not associated with the app or job that you selected. Complete the following steps.
    1. Review the list of existing secrets and select the secret that you want to use with this service binding.
    2. (optional) Specify a custom prefix for the service binding. If you do not specify a custom prefix, {{site.data.keyword.codeengineshort}} automatically generates a prefix. The prefix is used to distinguish environment variables that are created for this service binding.
7. Click **Add** to create the service binding.
8. Now that your service binding to your app or job is created from the console, you can view a list of all defined service bindings between service instances and {{site.data.keyword.codeengineshort}} apps and jobs from the Service bindings page.

Alternatively, you can add a service binding from the page for your job. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project, and click **Jobs** to open a listing of your jobs. Click the name of your job. From the **Service bindings** tab within the **Configuration** section, you can manage service bindings for this job.

### Binding a service instance to a {{site.data.keyword.codeengineshort}} application or job with the CLI
{: #bind-cli}
You can create a service binding that binds an existing service instance to a {{site.data.keyword.codeengineshort}} app or job with the CLI. 

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
    | `--prefix` | The prefix for environment variables that are created for this service binding. For example, `--prefix MyPrefix` adds the `MyPrefix` prefix to any environment variables that are created for this service binding. For more information, see [prefix method](/docs/codeengine?topic=codeengine-service-binding#prefix-method). |
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

You can only manage service bindings to apps from the console by using this page. 

Alternatively for jobs, you can remove a service binding from the page for your job. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, click the name of your project, and click **Jobs** to open a listing of your jobs. Click the name of your job. From the **Service bindings** tab within the **Configuration** section, you can manage service bindings for this job.

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



