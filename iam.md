---

copyright:
  years: 2020
lastupdated: "2020-07-15"

keywords: IAM access for code engine, permissions for code engine, identity and access management for code engine, roles for code engine, actions for code engine, assigning access for code engine

subcollection: codeengine
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Managing user access
{: #knative-iam}

Access to {{site.data.keyword.codeenginefull_notm}} service instances for users in your account is controlled by {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.codeengineshort}} service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.Bluemix_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. 
{: shortdesc}

{{site.data.keyword.codeengineshort}} uses both the Platform and Service management roles. You can set policies about who can create a project at the platform level, and use the service roles to manage interaction with the project itself. As the creator of a project, you do not need to set any IAM policies to view or work with your {{site.data.keyword.codeengineshort}} entities.

## How do I set IAM policies so that others can work with my project?
{: #iam_project_policies}

In order for others to work with entities in your project, you must set the appropriate [IAM policies in the console](https://cloud.ibm.com/iam/overview){: external} or the [IAM CLI](#cli-pol-set). 

The minimum Platform level access is Viewer. The minimum Service level access is Reader. For more information about Platform and Service level access roles, see [Platform management roles](#iam_platform_roles) and [Service-specific roles](#service_specific_roles).

Want to learn more about IAM key concepts? Check out [the IAM concepts](/docs/iam?topic=iam-iamoverview) or the [Best practices for assigning access](/docs/iam?topic=iam-account_setup).
{: tip}

## How do I set IAM policies so that others can create a project in my account?

In order to allow other users to manage {{site.data.keyword.codeengineshort}} properties, including creating properties, you must set the following access policies for those users.

  * The user's **Platform role** must be set to Administrator. This policy applies to all resources of {{site.data.keyword.codeengineshort}}.
  * The user's **Service role**  must be set to Manager. This policy applies to all resources of {{site.data.keyword.codeengineshort}}.

## How do I know which access policies have set for me?

You can see which access policies have been set for you in the [{{site.data.keyword.Bluemix}} catalog](https://cloud.ibm.com/catalog){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.

## Assigning access roles
{: #iam_access_roles}

Policies enable access to be granted at different levels. Some of the options include the following levels of access: 

* Access across all instances of the service in your account
* Access to an individual service instance in your account
* Access to a specific resource within an instance

After you define the scope of the access policy, you assign a role, which determines the user's level of access. Review the following tables that outline what actions each role allows within the {{site.data.keyword.codeengineshort}} service.

### Platform management roles
{: #iam_platform_roles}

The following table details actions that are mapped to platform management roles. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service, create or delete instances, and bind instances to applications.

| Platform management role | Description of actions | 
|--------------------------|------------------------|
| Viewer                   | View dashboard            |
| Editor                   | View dashboard            |
| Operator                 | View dashboard            | 
| Administrator            | View dashboard            |
{: caption="Table 1. IAM user roles and actions" caption-side="top"}

### Service-specific roles
{: #service_specific_roles}

The following table details actions that are mapped to service access roles. Service access roles enable users access to `service name` and the ability to call the `service name's` API.

| Service access role | Description of actions | 
|---------------------|------------------------|
| Reader              | Read tenant and tenant entities, but cannot modify            | 
| Writer              | Create, read, update, and delete tenant entities; read tenant            |
| Manager             | Create, read, update, and delete tenant entities; read tenant            | 
{: caption="Table 2. IAM service access roles and actions" caption-side="top"}


For more information about assigning user roles in the console, see [Managing access to resources](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

### Setting access policies for a user with the CLI
You can set access policies for a specific user by using the following command. In this example `name@example.com` is assigned the Viewer role for {{site.data.keyword.codeengineshort}}. By assigning the Viewer role to a user, this action enables the user with this role to access all of your {{site.data.keyword.codeengineshort}} properties.
{: #cli-pol-set}

```
ibmcloud iam user-policy-create name@example.com --roles Viewer --service-name code-engine
```
{: pre}

</br>

<table>
  <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the <code>ibmcloud iam service-policy-create</code> command components</th>
  </thead>
  <tbody>
    <tr>
      <td><code>&lt;namespace_service_ID&gt;</code></td>
      <td>The service ID for the project. To see all service IDs, run <code>ibmcloud iam service-ids</code>.</td>
    </tr>
    <tr>
      <td>`--roles` <code>&lt;IAM_role&gt;</code></td>
      <td>The type of IAM service access role that the action must have to use the target service. To see the supported roles for the other service, run <code>ibmcloud iam roles --service SERVICE_NAME</code>. For more information, see [IAM access roles](/docs/iam?topic=iam-userroles#service_access_roles).</td>
    </tr>
    <tr>
      <td>`--service-name` <code>&lt;other_service_name&gt;</code></td>
      <td>The name of the other {{site.data.keyword.cloud_notm}} service name.</td>
    </tr>
    <tr>
      <td>`--service-instance` <code>&lt;other_service_GUID&gt;</code></td>
      <td>The GUID of the other service instance that you want the action to have access to. To get the service instance GUID, run <code>ibmcloud resource service-instance &lt;other_service_instance_name&gt;</code>.</td>
    </tr>
  </tbody>
</table>

For more information about IAM commands, see the [IAM CLI reference docs](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create).
