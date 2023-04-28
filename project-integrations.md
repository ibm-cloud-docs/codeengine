---

copyright:
  years: 2020, 2023
lastupdated: "2023-04-28"

keywords: project, projects in code engine, providing access with projects in code engine, access control in code engine, iam access for projects in code engine, projects, code engine, binding in code engine, service binding in code engine, project settings, project integrations, configuring project-wide settings, service binding operations, integrating services in code engine, integrating service with app in code engine, integrating service with job in code engine, operator secret, ibmcloud-operator-secret, service bind, access, bind, bound, registries, container registry, image registry, apikey, API key, images, registry access, registry secret, service id, registry secret, registry access 

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring project-wide settings
{: #project-integrations}

By using the Project settings pages in the console, you can review and configure settings that apply to a specific project. Learn how to work with project-wide integrations. 
{: shortdesc} 

## What are project-wide integrations and why use them? 
{: #projectintegration-why}

Use the Integrations page in the console when you want to configure the project-wide settings in such a way that all users of the project can perform certain actions. With sufficient permissions, you can configure service binding operations or configure access to images in {{site.data.keyword.registrylong_notm}} from a single page. If you don't have sufficient permissions to perform these actions, you can use these pages to help you understand the required permissions. 
{: shortdesc} 

When you set project-wide settings with the Integrations page, {{site.data.keyword.codeengineshort}} automatically sets up the necessary credentials so that {{site.data.keyword.codeengineshort}} can perform service binding operations or access {{site.data.keyword.registryshort_notm}} for you, instead of using a personal user ID. You can view details about what {{site.data.keyword.codeengineshort}} does for you when you configure service binding operations or configure access to {{site.data.keyword.registryshort_notm}}. These details include information about the service ID and its access policies, the API key, and secret.

* If you want to configure settings for service binding operations, see [Configuring service binding operations](#projectintegration-sb).

* If you want to configure settings to control {{site.data.keyword.codeengineshort}} managed registry access to {{site.data.keyword.registrylong_notm}}, see [Configuring project-side access to {{site.data.keyword.registryshort_notm}}](#projectintegration-cr).


## Configuring project-wide service binding operations
{: #projectintegration-sb}

Use the Integrations page in the console to configure settings for service binding operations so that all users of a specific project can create and delete bindings without having to assign all necessary privileges to their personal user IDs.
{: shortdesc}  

In {{site.data.keyword.codeengineshort}}, service binding operations, which include creating, and deleting service bindings, are not performed with the identity of the user that is logged in. Instead, {{site.data.keyword.codeengineshort}} automatically creates a service ID that is used specifically for service binding operations. With sufficient permissions, you can configure service binding operations to automatically set up this service ID for service binding operations from the Integrations page. Or, you can choose to use your own custom service ID that you manage for service binding operations. 

### What access permissions are required to configure service binding operations? 
{: #projectintegration-sb-access}

The user of this Integrations page must have the following {{site.data.keyword.iamshort}} (IAM) access policies that are assigned to your user account to successfully configure service binding operations. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions.



* **Service:** All Identity and Access enabled services
    * **Resources:** Select from resource group, region, or access management tags.
    * **Resource group access:** `Viewer`
    * **Roles and actions:** `Administrator` platform access (no service access required)
* **Service:** {{site.data.keyword.codeengineshort}}
    * **Resources:** The resource group of this {{site.data.keyword.codeengineshort}} project
    * **Resource group access:** `Viewer`
    * **Roles and actions:** `Writer` service access and `Operator` platform access 

For {{site.data.keyword.codeengineshort}} to automatically generate a service ID for service binding operations, {{site.data.keyword.codeengineshort}} checks and automatically sets up a service ID with `Operator` platform access and `Manager` service access for all services in the resource group of the {{site.data.keyword.codeengineshort}} project. {{site.data.keyword.codeengineshort}} uses this service ID to access {{site.data.keyword.cloud_notm}} services with service bindings. 

If you use your own custom service ID, the custom service ID must provide `Operator` platform access and `Manager` service access for any {{site.data.keyword.cloud_notm}} services or service instances that you want to bind to {{site.data.keyword.codeengineshort}} apps or jobs. 

If this service ID does not exist, {{site.data.keyword.codeengineshort}} tries to automatically create this service ID whenever a service binding is created. The successful creation of this service ID for service binding operations depends on whether the user that is logged in to {{site.data.keyword.codeengineshort}} has sufficient permissions. If the operator secret is not created successfully, any attempt to create a service binding fails. For more information about {{site.data.keyword.codeengineshort}} access requirements for service binding operations, see [Configuring access for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess).


### What's the relationship between the service ID and the operator secret? 
{: #projectintegration-sb-relation}

When you configure service binding operations, you can view details about what {{site.data.keyword.codeengineshort}} does for you, including information about the service ID, API key, and secret. 

In {{site.data.keyword.codeengineshort}}, a *service binding* is the relationship between an app or job and another {{site.data.keyword.cloud_notm}} service. 

{{site.data.keyword.codeengineshort}} uses a *service ID* to perform binding operations on behalf of the user, instead of using the identity of the user that is logged in. The service ID creates credentials for a specific {{site.data.keyword.cloud_notm}} service instance. These service credentials are used by your bound {{site.data.keyword.codeengineshort}} apps and jobs to interact with the service instances. The *API key* for the service ID is stored in the operator secret. The access policies are the permissions that are given to the service ID. 

The *operator secret* or `ibmcloud-operator-secret` is a {{site.data.keyword.codeengineshort}} generated and managed secret that includes the service ID and an autogenerated API key for it. This secret is used with service binding operations and does not act as the current user's account. If the operator secret doesn't exist, it is automatically created when any one of the following scenarios is true.
* When the next service binding is created for the project (from the console or CLI).
* When you configure service binding operations from the Integrations page.
* When you run the **`project update`** command.  

When service binding operations are configured, the *service ID* and *operator secret* apply to your specific project. 

You can configure service binding operations and let {{site.data.keyword.codeengineshort}} [automatically generate the service ID](#projectintegration-sb-auto) or you can [configure service bindings with your own custom service ID](#projectintegration-sb-customserviceid).


### Configuring service bindings operations with a {{site.data.keyword.codeengineshort}} autogenerated service ID
{: #projectintegration-sb-auto}

You can configure service binding operations so that all users in the project can create and manage service bindings to {{site.data.keyword.cloud_notm}} services in the selected resource group from the {{site.data.keyword.codeengineshort}} console.
{: shortdesc} 

1. Go to the Integrations page. 
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. 
    2. Click  **Project settings** > **Integrations**. 
2. Click **Configure** in the **Service bindings** tile to configure service binding operations for all users of this project.  
3. From the "Configure service binding operations" page, specify the resource group that you want to use for service binding operations. You can choose an {{site.data.keyword.cloud}} resource group that contains the {{site.data.keyword.codeengineshort}} project and let {{site.data.keyword.codeengineshort}} create the necessary credentials. Or, you can choose to use a [custom service ID](#projectintegration-sb-customserviceid) that uses your service ID credentials.
4. (optional) Expand the **What {{site.data.keyword.codeengineshort}} does for you** section to view information about what {{site.data.keyword.codeengineshort}} automatically creates for you when you configure service binding operations. View information about the service ID and the access policies that are assigned to this service ID, the API key that {{site.data.keyword.codeengineshort}} automatically generates for the service ID, and the operator secret that is used for service bindings.
5. Click **Configure**.
6. (optional) Click **View details** to view details of the service binding operations configuration. From this page, you can view information about the service ID, API key, and operator secret that is used for service binding operations. 

Now that you configured service binding operations for the specified resource group, every user with writer or manager access to this {{site.data.keyword.codeengineshort}} project can create and delete service bindings. See [Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding).  

### Configuring service binding operations with a custom service ID
{: #projectintegration-sb-customserviceid}

You can configure service binding operations such that all users in the project can create and manage service bindings with a custom service ID to {{site.data.keyword.cloud_notm}} services from the {{site.data.keyword.codeengineshort}} console. 
{: shortdesc} 

When you use a custom service ID, the assigned IAM policies for the service ID determine the resource groups. 
{: note}

1. Go to the Integrations page. 
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. 
    2. Click  **Project settings** > **Integrations**. 
2. Click **Configure** in the **Service bindings** tile to configure service binding operations for all users of this project with your custom service ID. 
3. From the "Configure service binding operations" page, select **Use a custom service ID**.  
4. Choose the custom service ID that you want to use. 
5. (optional) Expand the **What {{site.data.keyword.codeengineshort}} does for you** section to view information about what {{site.data.keyword.codeengineshort}} automatically creates for you when you configure service binding operations. View information about the API key that {{site.data.keyword.codeengineshort}} automatically generates for the service ID and the operator secret that is used for service binding operations. 
6. Click **Configure**. After service binding operations are configured, the custom service ID for service binding operations is displayed. 
7. (optional) Click **View details** to view details of the service binding operations configuration. From this page, you can view information about the service ID, API key, and operator secret that is used for service binding operations.  

Now that you configured service binding operations with a custom service ID with required IAM permissions, every user with writer or manager access to this {{site.data.keyword.codeengineshort}} project can create and delete service bindings. See [Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding).

### Removing configured service binding operations 
{: #projectintegration-sb-remove}

If service binding operations are configured, you can also use the Integrations page to remove the ability for all users of the project to create or delete service bindings. This action removes the operator secret for service binding operations. 
{: shortdesc}  

1. Go to the Integrations page. 
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. 
    2. Click  **Project settings** > **Integrations**.    
2. If the status of Service binding operations is **Configured**, click **Remove configuration** to remove the operator secret. You are asked to confirm that you want to delete the operator secret.

When you receive a message that service binding operations are removed, the status for service binding operations is **Not configured**. 

If you remove configured service binding operations from the Integrations page, any existing service bindings remain. This means that for existing service bindings, when you run applications, run new application revisions, or run jobs, the bound app or job uses the existing service bindings and their credentials. However, new service bindings cannot be created without sufficient permissions, and existing bindings cannot be deleted.

If the operator secret doesn't exist, it is automatically created when any one of the following scenarios is true.
* When the next service binding is created for the project (from the console or CLI).
* When you configure service binding operations from the Integrations page.
* When you run the **`project update`** command. 


## Configuring project-wide access to {{site.data.keyword.registryshort_notm}}
{: #projectintegration-cr}

Use the Integrations page in the console to configure settings to set up and manage registry access to images in {{site.data.keyword.registrylong_notm}} so that all users of a specific {{site.data.keyword.codeengineshort}} project can store and access images in {{site.data.keyword.registryshort_notm}} without having to manually create registry secrets. 
{: shortdesc} 

When you use project integrations to control your {{site.data.keyword.codeengineshort}} managed access to {{site.data.keyword.registryshort_notm}}, {{site.data.keyword.codeengineshort}} doesn't use the identity of the user that is logged in. Instead, {{site.data.keyword.codeengineshort}} automatically creates registry access that is used specifically for accessing images in {{site.data.keyword.registrylong_notm}}. With sufficient permissions, you can configure this default registry access on a per location (region) basis. For more information about {{site.data.keyword.registryshort_notm}} regions, see [{{site.data.keyword.registrylong_notm}} regions](/docs/Registry?topic=Registry-registry_overview#registry_regions).

### What access permissions are required for {{site.data.keyword.codeengineshort}} managed access to {{site.data.keyword.registrylong_notm}}? 
{: #projectintegration-cr-access}

The user of this Integrations page must have the following {{site.data.keyword.iamlong}} (IAM) access policies that are assigned to your user account to successfully configure registry access for all users of the project. If you don't have sufficient permissions to perform these actions, you can use this page to help you understand the required permissions and actions you can take. 




* **Service:** {{site.data.keyword.registryshort_notm}}
    * **Resources:** Select from resource group, region, or access management tags.
    * **Resource group access:** `Viewer`
    * **Roles and actions:** `Administrator` platform access and `Reader`, `Writer`, and `Manager` service access
* **Service:** {{site.data.keyword.codeengineshort}}
    * **Resources:** The resource group of this {{site.data.keyword.codeengineshort}} project
    * **Resource group access:** `Viewer`
    * **Roles and actions:** `Operator` platform access and `Writer` service access 

For {{site.data.keyword.codeengineshort}} to automatically generate a service ID for accessing images in {{site.data.keyword.registryshort_notm}} in a specific location, {{site.data.keyword.codeengineshort}} sets up this service ID with the `Administrator` role for the IAM Identity service that is scoped to this service ID. Additionally, {{site.data.keyword.codeengineshort}} grants the `Manager` role for the {{site.data.keyword.registrylong_notm}} service that is scoped to the specified location (region). These roles and permissions are required so that {{site.data.keyword.codeengineshort}}  can use this service ID to access {{site.data.keyword.registryshort_notm}} on behalf of the user of the respective {{site.data.keyword.codeengineshort}} project. 

When {{site.data.keyword.codeengineshort}} configures this service ID with the `Administrator` platform access and `Manager` service access to {{site.data.keyword.registrylong_notm}}, the access is scoped to only this service ID.
{: important}


For more information about {{site.data.keyword.codeengineshort}} requirements for accessing images in a container registry, see [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry). 

### What's the relationship between the service ID and the registry secret? 
{: #projectintegration-cr-relation}


When you configure default registry access for a specific location, you can view details about what {{site.data.keyword.codeengineshort}} does for you, including information about the service ID and its access policies, API key, and registry secret. 

{{site.data.keyword.codeengineshort}} uses a *service ID* to enable registry access to {{site.data.keyword.registryshort_notm}}, on behalf of the user, instead of using the identity of the user that is logged in. 

The *registry secret* is a {{site.data.keyword.codeengineshort}} generated and managed registry secret that includes an autogenerated API key for it. This secret is used for accessing images in {{site.data.keyword.registryshort_notm}}. 

When default registry access is configured for a location (region), the *service ID* and *registry secret* apply to your specific project. 

### Configuring {{site.data.keyword.registryshort_notm}} access
{: #projectintegration-cr-config}

You can configure registry access such that all users in the project can access and work with images in {{site.data.keyword.registrylong_notm}} from the {{site.data.keyword.codeengineshort}} console. 
{: shortdesc} 

1. Go to the Integrations page. 
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. 
    2. Click  **Project settings** > **Integrations**.  
2. In the **{{site.data.keyword.registryshort_notm}}** tile, click the row for the location that you want to configure registry access.
3. From the "Configure default registry access" page, you can optionally expand the **What {{site.data.keyword.codeengineshort}} does for you** section to view information about what {{site.data.keyword.codeengineshort}} automatically creates for you when you configure default registry access to a specific location. View information about the service ID and the access policies that are assigned to this service ID, the API key that {{site.data.keyword.codeengineshort}} automatically generates for the service ID, and the registry secret that is used for this registry access.
4. Click **Configure** to configure the default registry access for a specific location. 
5. From the table, you can view configuration status by location and the autogenerated registry secret.
6. (optional) For more details, click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **View details**. You can view information about the service ID and the access policies that are assigned to this service ID, the API key that {{site.data.keyword.codeengineshort}} automatically generates for the service ID, and the registry secret that is configured for accessing {{site.data.keyword.registryshort_notm}}.

Now that you configured default registry access for a specific location to {{site.data.keyword.registryshort_notm}}, every user with writer or manager access to this {{site.data.keyword.codeengineshort}} project can use this registry access secret with their apps, jobs, and builds to access images in {{site.data.keyword.registryshort_notm}}. 


### Removing {{site.data.keyword.codeengineshort}} managed access to {{site.data.keyword.registryshort_notm}}
{: #projectintegration-cr-remove}

When you remove a {{site.data.keyword.codeengineshort}} managed registry access secret for a particular region, this project-wide registry access is deleted. The associated service ID, API key, and registry secret are deleted. You can continue to use manually created registry access secrets, or you can configure project-wide {{site.data.keyword.registryshort_notm}} access again.
{: shortdesc}  

1. Go to the Integrations page. 
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. 
    2. Click  **Project settings** > **Integrations**.  
2. From the row of the location (region) that you want to remove the registry access, click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **Remove configuration**. You are asked to confirm that you want to delete the registry access.

When you receive a message that registry access is removed, the status for registry access for a particular {{site.data.keyword.registryshort_notm}} location is **Not configured**. 




