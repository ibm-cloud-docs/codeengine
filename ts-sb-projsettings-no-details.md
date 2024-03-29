---

copyright:
  years: 2023
lastupdated: "2023-05-18"

keywords: troubleshooting for code engine service bindings, service bindings, binding, service credentials

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I display details of my configured service binding operations? 
{: #ts-sb-projsettings-nodetails}
{: troubleshoot}

When you configure project-wide settings with the Integrations page from the console, {{site.data.keyword.codeengineshort}} automatically sets up the necessary credentials so that {{site.data.keyword.codeengineshort}} can perform service binding operations for you. Sometimes, the service binding operations are configured, but details cannot be displayed about the settings.


After successfully configuring service binding operations, the status shows configured; however, you receive a warning message that details of the current service binding operations cannot be displayed. A warning that is similar to the following text appears on the **Project settings** > **Integrations**  > **Service binding operations** page, `Cannot display details of the current configuration`. 
{: tsSymptoms}

When you create the first service binding in a specific {{site.data.keyword.codeengineshort}} project, or you run the **`project update`** CLI command, {{site.data.keyword.codeengineshort}} creates the operator secret (`ibmcloud-operator-secret`) for service binding operations for the project. The operator secret is a {{site.data.keyword.codeengineshort}} generated and managed secret that includes the service ID and an autogenerated API key for it. {{site.data.keyword.codeengineshort}} uses the service ID to perform binding operations on behalf of the user, instead of using the identity of the user that is logged in. The service ID creates credentials for a specific {{site.data.keyword.cloud_notm}} service instance. After this operator secret is created, {{site.data.keyword.codeengineshort}} uses this secret for the life of the project for service binding operations. 
{: tsCauses}

However, the operator secret might not contain the necessary information about the service ID so that details about the service binding configuration cannot be displayed from the Integrations page for project-wide settings. 

The operator secret that was created because one of the following scenarios might not have the service ID information.

1. If the [**`project update`**](/docs/codeengine?topic=codeengine-cli#cli-project-update) CLI command was run with the `--binding-service-id` option.

2. If you created service bindings from the console or with the CLI for a {{site.data.keyword.codeengineshort}} app or job in a project that was created before the release of [project-wide settings in the console](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2623), the operator secret does not reference the service ID. Note that for projects that were created after the release of project-wide settings in the console, the operator secret contains information about the service ID. {{site.data.keyword.codeengineshort}} uses this information to display details about the service binding operations, including information about the operator secret and the service ID. 


Try one of these solutions.
{: tsResolve}

1. If you used a custom service ID that you created and manage with the **`project update`** command, and you know the specific service ID that was used, take the following steps to reconfigure the service binding operations to use your custom service ID.
    
    If you do not know the specific service ID that was used with the **`project update`** command, do not take the following steps. For this case, service binding operations are configured such that you can create and manage service bindings; however, the system cannot display details of service binding operations from the project-wide Integrations page and you continue to see the warning message.

    1. Review the list of service IDs in {{site.data.keyword.iamlong}} (IAM) to help you determine the custom service ID that was used with the **`project update`** command. From the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Service IDs**.
    2. After you identify the service ID that was used with the **`project update`** command, use the {{site.data.keyword.codeengineshort}} console to assign the same custom service ID to the operator secret. 
    3. Go to the Integrations page in the console. After you select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, click **Project settings** > **Integrations**. The configuration status is `Configured`.
    4. Click **Remove configuration**. This action removes the existing operator secret, and the configuration status is `Not Configured`. 
    5. Click **Configure** to configure service binding operations and select the option to use a custom service ID. 
    6. Select your custom service ID from the table. Use the custom service ID that you identified in the first step. 
    7. Click **Configure** to save this configuration. 

After service binding operations are configured with your custom service ID, you can view details of the configuration. 

2. If you created service bindings for an app or job in a {{site.data.keyword.codeengineshort}} project that was created before the release of [project-wide settings in the console](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2623), ignore the warning message. Service binding operations will continue to work because service bindings were previously created. Do not remove and reconfigure service binding operations configurations from the Integrations page in the console because this action does not delete the original service ID and can cause a security risk. 



For more information about working with service bindings, see [Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding) and [Configuring project-wide service binding operations](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb). 






