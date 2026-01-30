---

copyright:
  years: 2020, 2026
lastupdated: "2026-01-27"

keywords: binding in code engine, service bind in code engine, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, adding credentials for service in code engine, service bind, access, prefix, CE_SERVICES, bind, bound, unbinding, project, integrating service with function in code engine

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring access for service bindings
{: #configure-bindaccess}

Service bindings in {{site.data.keyword.codeengineshort}} use a service ID to access {{site.data.keyword.cloud_notm}} services. A service ID contains the credentials to communicate with a service instance on behalf of your {{site.data.keyword.codeengineshort}} project. Before you can bind a service instance to a {{site.data.keyword.codeengineshort}} workload, you must configure access for bindings that is based on whether you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for you or whether you want to use a service ID that you manage.
{: shortdesc}


Interested in configuring your project such that all users of the project can create and delete service bindings? With sufficient permissions, you can use the Project integrations pages in the console to configure service binding operations from a single page. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions. See [Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations). 
{: note}


Before you can bind your app, job, or function to a specific {{site.data.keyword.cloud_notm}} service instance, determine whether you want to [create and manage your own service ID](/docs/account?topic=account-serviceids), or if you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for you. Based on your choice, assign the proper access policies. {{site.data.keyword.codeengineshort}} uses one service ID per project to work with service bindings.

* If you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for you, then configure [default service binding access policies](#bind-auto-servid). Ensure that proper access policies are assigned to the {{site.data.keyword.cloud_notm}} account that is used with your {{site.data.keyword.codeengineshort}} project.
    * If your {{site.data.keyword.codeengineshort}} project is in the *same* resource group as the service instance that you want to bind to, then you need to configure [default service binding access policies](#bind-auto-servid).
    * If your {{site.data.keyword.codeengineshort}} project is in a *different* resource group from the service instance that you want to bind to, you'll need to configure [default service binding access policies](#bind-auto-servid) for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings, and you need to [configure your project to bind services in a different resource group](#bind-config-proj).

* If you want more control over access policies, you can choose to [use a custom service ID for service bindings](#bind-custom-servid) that is configured in your service instance. In this case, assign access policies to the custom service ID. You'll need to configure your project to use the custom service ID.

## Using the default service binding access policies
{: #bind-auto-servid}

By default, {{site.data.keyword.codeengineshort}} automatically creates a service ID for accessing all services in the resource group of the {{site.data.keyword.codeengineshort}} project when your account that is used with your project has sufficient permissions. The service ID is created during the first service binding operation.

To use default service binding access policies when your {{site.data.keyword.codeengineshort}} project is in the *same* resource group as the service instance that you want to bind to, [configure access for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings](#bind-auto-servid-access).


### Configuring access for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings
{: #bind-auto-servid-access}

If your service instance is in the same resource group as your {{site.data.keyword.codeengineshort}} project, and you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service binding for you, then the {{site.data.keyword.cloud_notm}} account that is used with your {{site.data.keyword.codeengineshort}} project must have `Writer` service access and `Operator` platform access, at minimum.

With these permissions set for your account, when you create a service binding, {{site.data.keyword.codeengineshort}} checks and automatically sets up a service ID with `Operator` and `Manager` access for all services in the resource group of the {{site.data.keyword.codeengineshort}} project. {{site.data.keyword.codeengineshort}} uses this service ID to access {{site.data.keyword.cloud_notm}} services with service bindings.

Whenever {{site.data.keyword.codeengineshort}} creates the service ID that is used for service bindings for your project, this service ID is reused with subsequent service bindings within the same project, unless you run the `project update` CLI command to [configure your project to bind services in a different resource group](#bind-config-proj) or you run the `project update` CLI command to use a [custom service ID with access permissions for {{site.data.keyword.codeengineshort}} service bindings](#bind-auto-servid-access-custom).

For example, suppose you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings for an {{site.data.keyword.cloudant}} service instance. Also, suppose that the `my-user` account that is used with your {{site.data.keyword.codeengineshort}} project and the {{site.data.keyword.cloudant}} service instance are both in the same resource group.

The following steps describe one way to setup the required access permissions so that {{site.data.keyword.codeengineshort}} can automatically create and manage the service ID for service bindings for `my-user`. The account owner for the service instance completes the following steps to assign permissions for `my-user`.

1. [Create an IAM resource group](/docs/account?topic=account-rgs&interface=ui#create_rgs) for users who create {{site.data.keyword.codeengineshort}} service bindings.
    1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
    2. Select **Manage** > **Account** > **Resource Groups** > **Create resource group**.
    3. Create a resource group; for example, `CodeEngine_servicebindings_resourcegroup`.

2. Create the service instances that you want to bind to in the same resource group. For this example, create an {{site.data.keyword.cloudant}} service instance in the `CodeEngine_servicebindings_resource group` resource group.

3. [Create an IAM access group](/docs/account?topic=account-groups&interface=ui) for users who create {{site.data.keyword.codeengineshort}} service bindings.
    1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
    2. Select **Manage** > **Access(IAM)** > **Access groups**.
    3. Create a group; for example, `CodeEngine_servicebindings_accessgroup`.
    4. From within this new access group, click the **Access** tab and assign the following two access policies to the access group. For the first access policy,
        * For Service, select `All Identity and Access enabled services`.
        * For Resources, select the specific resource group that you created in the previous step; for example, `CodeEngine_servicebindings_resourcegroup`.
        * For Resource group access, select `Viewer`.
        * For Roles and actions, select Platform access of `Administrator`.
        * Click **Add** to add the access policy to this access group.

    5. Assign the second access policy for this access group.
        * For Service, select `Code Engine`.
        * For Resources, select the specific resource group that you created in the previous step; for example, `CodeEngine_servicebindings_resourcegroup`.
        * For Resource group access, select `Viewer`.
        * For Roles and actions, select Service access of `Writer` and Platform access of `Operator`.
        * Click **Add** to add the access policy to this access group.
    6. Click **Assign** to assign the access policies to this access group.

4. Add the `my-user` user to this access group.


Now you are ready to create service bindings in {{site.data.keyword.codeengineshort}} where {{site.data.keyword.codeengineshort}} automatically creates a service ID with sufficient permissions to create service credentials to your specified service instances. See [bind a service instance to an app, job, or function workload](/docs/codeengine?topic=codeengine-bind-services).

### Configuring a project to bind services in a different resource group
{: #bind-config-proj}

By default, {{site.data.keyword.codeengineshort}} automatically creates a service ID for accessing all services in the resource group of the {{site.data.keyword.codeengineshort}} project when your account that is used with your project has sufficient permissions. The service ID is created during the first service binding operation.

However, if the {{site.data.keyword.cloud_notm}} service instance that you want to bind to your {{site.data.keyword.codeengineshort}} workload is in a *different* resource group than the resource group of the {{site.data.keyword.codeengineshort}} project for your workload, and you want {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service binding for you, then you must complete the following actions before you create the service binding.

* [Configure access for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings](#bind-auto-servid-access).
* [Update the project to access service instances in other resource groups](#bind-auto-servid-update-project).

For example, if your {{site.data.keyword.codeengineshort}} project is in the `Default` resource group, and you want to bind to a service instance that exists in the `dev` resource group, you must update the {{site.data.keyword.codeengineshort}} project so that {{site.data.keyword.codeengineshort}} can access services instances in other resource groups.

#### Update the project to access service instances in other resource groups
{: #bind-auto-servid-update-project}

When the resources that you want to bind to are in a different resource group, configure your {{site.data.keyword.codeengineshort}} project with the CLI so that it can access resources in the different resource group. Use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) command and specify the `--binding-resource-group` option to configure a {{site.data.keyword.codeengineshort}} project for service binding access for all service instances in a resource group. This command tells your {{site.data.keyword.codeengineshort}} project which resource group that it can bind to. You can update your project to bind services to a different resource group only with the CLI.


The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the project that you want.  Use the [**`ibmcloud ce project current`**](/docs/codeengine?topic=codeengine-cli#cli-project-current) command to display details of the project that is currently targeted. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
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

* To configure service binding access for all service instances in all resource groups:

    ```txt
    ibmcloud ce project update --binding-resource-group "*"
    ```
    {: pre}

When you run the **`project update`** command, a service ID is created for the project, and is used to configure the current project for service bindings. If you do not have permission to create this service ID, then you receive an error that your project is not ready to work with service bindings. Talk to your account administrator about your access policies, or ask the administrator to [configure access for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings](#bind-auto-servid-access).

## Using a custom service ID for service bindings
{: #bind-custom-servid}

If you want more control over access policies or resource groups, you can create a custom service ID for your service instance.

Your organization might choose to use a custom service ID for accessing a specific service instance if the account owner doesn't want to grant `Administrator` access for a user to the **All Identity and Access enabled services** within a resource group, which is required for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings. The account owner might want to scope the user access to a specific service type or service instance. In these cases, a custom service ID provides this control.

To use a custom service ID for service bindings,
* [Create a custom service ID with access permissions for {{site.data.keyword.codeengineshort}} service bindings](#bind-auto-servid-access-custom).
* [Configure your project to use the custom service ID](#bind-custom-servid-project).

### Creating a custom service ID with access permissions for {{site.data.keyword.codeengineshort}} service bindings
{: #bind-auto-servid-access-custom}

When you are using a custom service ID, you must give the custom service ID `Operator` platform access so that this service ID can create the service credentials for service bindings.

For example, suppose you want to create a service binding to bind a {{site.data.keyword.codeengineshort}} workload to an {{site.data.keyword.cloudant}} service instance. Yet, you do not want to give the user `Administrator` access for all **All Identity and Access enabled services** within a resource group. However, you want to give the user access to a specific instance of {{site.data.keyword.cloudant}}.

The following steps describe one way to setup a custom service ID with the required access permissions so that {{site.data.keyword.codeengineshort}} can create service bindings for `my-user`. The account owner for the service instance completes the following steps to create a custom service ID.

1. [Create an IAM resource group](/docs/account?topic=account-rgs&interface=ui#create_rgs) for users who create {{site.data.keyword.codeengineshort}} service bindings.
    1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
    2. Select **Manage** > **Account** > **Resource Groups** > **Create resource group**.
    3. Create a resource group; for example, `CodeEngine_servicebindings_resourcegroup`.

2. Create the service instances that you want to bind to in the same resource group. For this example, create an {{site.data.keyword.cloudant}} service instance in the `CodeEngine_servicebindings_resource group` resource group.

3. [Create an IAM access group](/docs/account?topic=account-groups&interface=ui) for users who create {{site.data.keyword.codeengineshort}} service bindings.
    1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
    2. Select **Manage** > **Access(IAM)** > **Access groups**.
    3. Create a group; for example, `CodeEngine_servicebindings_accessgroup`.
    4. From within this new access group, click the **Access** tab and assign the following access policy for the {{site.data.keyword.codeengineshort}} service.
        * For Service, select **Code Engine**.
        * For Resources, select the specific resource group that you created in the previous step; for example, `CodeEngine_servicebindings_resourcegroup`.
        * For Resource group access, select `Viewer`.
        * For Roles and actions, select Service access of `Writer` and Platform access of `Operator`.
        * Click **Add** to add the access policy to this access group.
    5. Click **Assign** to assign the access policies to this access group.
    6. Create the service instances that you want to bind to in the same resource group. For this example, create an {{site.data.keyword.cloudant}} service instance in the `CodeEngine_servicebindings_resource group` resource group.

4. Add the `my-user` user to this access group.

5. Create a service ID for the service instance that you want to bind to.
    1. Launch [Access (IAM) Overview](https://cloud.ibm.com/iam/overview){: external}.
    2. Select **Manage** > **Access(IAM)** > **Service IDs**.
    3. Create a service ID; for example, `CodeEngine_servicebindings_serviceid`.
    4. From within this new service ID, click the **Assign group**. From the Assign access page, select **Access policy**. Do not select **Access groups**. Assign the following access policy,
        * For Service, select the service instance that you want to bind to; for example, {{site.data.keyword.cloudant}} service instance.
        * For Resources, select the specific resource group that you created for users that can create service bindings to this service.
        * For Resource group access, select `Viewer`.
        * For Roles and actions, select Service access of `Manager` and Platform access of `Operator`.
        * Click **Add** to add the access policy to this service ID.
    5. Click **Assign** to assign the access policies to this service ID.

Now that you have a custom service ID for service bindings, you must configure your {{site.data.keyword.codeengineshort}} project to use the custom service ID.

### Configuring a project to use a custom service ID
{: #bind-custom-servid-project}

To configure a {{site.data.keyword.codeengineshort}} project for service binding to use a custom service ID that you manage, use the [**`ibmcloud ce project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) CLI command and specify the `--binding-service-id` option. You can update your project to use a custom service ID only with the CLI.

The **`project update`** command works within the project that is selected as the current context. Before you use the **`project update`** command, confirm that you are in the project that you want.  Use the [**`ibmcloud ce project current`**](/docs/codeengine?topic=codeengine-cli#cli-project-current) command to display details of the project that is currently targeted. If needed, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command to select your project as the current context.
{: note}




1. Find the ID of your custom service ID by clicking Details on your service ID page from the console, or else run the `ibmcloud iam service-ids` CLI command.
2. Run the **`ibmcloud ce project update`** command. For example, if the ID of your service ID is `ServiceId-12a3456b-c78d-901e-f2a3b4cabcde`:

    ```txt
    ibmcloud ce project update --binding-service-id ServiceId-12a3456b-c78d-901e-f2a3b4cabcde
    ```
    {: pre}

Whenever you run the **`project update --binding-service-id`** command, {{site.data.keyword.codeengineshort}} replaces any existing service ID and uses this service ID for service bindings.



## Next steps
{: #service-bindings-access-nextsteps}

Now that access for service bindings is configured, you are ready to [bind a service instance to an app, job, or function workload](/docs/codeengine?topic=codeengine-bind-services).
