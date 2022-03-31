---

copyright:
  years: 2022
lastupdated: "2022-03-31"

keywords: IAM access for code engine, permissions for code engine, identity and access management for code engine, roles for code engine, actions for code engine, assigning access for code engine, user access, access, platform roles, service roles

subcollection: codeengine
---

{{site.data.keyword.attribute-definition-list}}

# Managing user access
{: #iam}

Access to {{site.data.keyword.codeenginefull}} service instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.codeengineshort}} service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. 
{: shortdesc}

*Policies* enable access to be granted at different levels.

*Roles* define the actions that a user or service ID can run. There are different types of roles in the {{site.data.keyword.cloud_notm}}:

* *Platform management roles* enable users to perform tasks on {{site.data.keyword.codeengineshort}} resources at the platform level, for example assign user access for {{site.data.keyword.codeengineshort}}, create or delete service IDs, create projects, and assign policies for {{site.data.keyword.codeengineshort}} to other users.
* *Service access roles* enable users to be assigned varying levels of permission for calling the {{site.data.keyword.codeengineshort}} API.

{{site.data.keyword.codeengineshort}} uses both the Platform and Service management roles. You can set policies about who can create a project at the platform level, and then use the service roles to manage interaction with the project itself. As the creator of a project, you do not need to set any IAM policies to view or work with your {{site.data.keyword.codeengineshort}} entities.

Want to learn more about IAM key concepts? Check out [What is IBM Cloud Identity and Access Management?](/docs/account?topic=account-iamoverview).
{: tip}

## How do I know which access policies are set for me?
{: #iam-accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud}} catalog](https://cloud.ibm.com/catalog){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.

## Managing access by using access groups
{: #groups}

To manage access or assign new access for users by using access groups, you must be the account owner, administrator, or editor on all Identity and Access enabled services in the account, or the assigned **Administrator** or **Editor** for the IAM Access Groups Service. 

Choose any of the following actions to manage access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/account?topic=account-groups#create_ag).
* [Assigning access to a group](/docs/account?topic=account-groups#access_ag).

For more information about IAM commands, see the [IAM CLI reference docs](/docs/account?topic=cli-ibmcloud_commands_iam).

## Managing access by assigning policies directly to users
{: #users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To grant permissions to a user, see [Assigning access](/docs/account?topic=account-assign-access-resources#assign-new-access).
* To revoke permissions, see [Removing access](/docs/account?topic=account-assign-access-resources#removing-access-console).
* To review a user's permissions, see [Reviewing your assigned access](/docs/account?topic=account-assign-access-resources#review-your-access-console).

For more information about IAM commands, see the [IAM CLI reference docs](/docs/account?topic=cli-ibmcloud_commands_iam).

## {{site.data.keyword.cloud_notm}} platform roles
{: #platform}

Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service, create or delete instances, and bind instances to applications.

In {{site.data.keyword.codeengineshort}}, [`projects`](/docs/codeengine?topic=codeengine-manage-project) are service instances. 
{: note}

Use the following table to identify the platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:


| Platform actions   | Administrator   | Editor | Operator | Viewer  |
|--------------------------|:--------------------------:|:-------:|:--------:|:------:|
| Grant other account members access to work with the service. | ![Checkmark icon.](images/confirm.png "Feature available") |         |          |        |
| Create a project.                                           | ![Checkmark icon.](images/confirm.png "Feature available") | ![Checkmark icon.](images/confirm.png "Feature available") |      |      |
| Delete a project.                                              | ![Checkmark icon.](images/confirm.png "Feature available") | ![Checkmark icon.](images/confirm.png "Feature available")    |        |      |
| Update a project.                                               | ![Checkmark icon.](images/confirm.png "Feature available")  | ![Checkmark icon.](images/confirm.png "Feature available")    |        |      |
| View {{site.data.keyword.codeengineshort}} dashboard.  | ![Checkmark icon.](images/confirm.png "Feature available")  | ![Checkmark icon.](images/confirm.png "Feature available")    | ![Checkmark icon.](images/confirm.png "Feature available")      |        |
| View details of a service instance.                                      | ![Checkmark icon.](images/confirm.png "Feature available")  | ![Checkmark icon.](images/confirm.png "Feature available")    | ![Checkmark icon.](images/confirm.png "Feature available")      | ![Checkmark icon.](images/confirm.png "Feature available")    |
{: caption="Table 1. IAM user platform roles and actions" caption-side="top"}


## {{site.data.keyword.cloud_notm}} service roles
{: #service}

Use the following table to identify the service roles that you can grant a user to run any of the following service actions:

| Actions                                                          | Manager                                    | Writer                 | Reader |
|-------------------------------------------------------------------------|:-------------------------------------------------:|:-----------------------------------:|:------:|
| Create items within a project.                       | ![Checkmark icon.](images/confirm.png "Feature available") | ![Checkmark icon.](images/confirm.png "Feature available")                    |    |
| Update items within a project.                                                | ![Checkmark icon.](images/confirm.png "Feature available")      | ![Checkmark icon.](images/confirm.png "Feature available")                    |    |
| Delete items within a project.                                          | ![Checkmark icon.](images/confirm.png "Feature available")      | ![Checkmark icon.](images/confirm.png "Feature available")                    |    |
| List and view items within a project.                                      | ![Checkmark icon.](images/confirm.png "Feature available")      | ![Checkmark icon.](images/confirm.png "Feature available")                    |     |
| View project details.                                         | ![Checkmark icon.](images/confirm.png "Feature available")      | ![Checkmark icon.](images/confirm.png "Feature available")                    | ![Checkmark icon.](images/confirm.png "Feature available")    |
{: caption="Table 2. IAM service roles and actions" caption-side="top"}

## {{site.data.keyword.codeengineshort}} service binding access requirements
{: #service-binding-access-req}

For more information about {{site.data.keyword.codeengineshort}} service binding access requirements, see the [What access do I need to create service bindings?](/docs/codeengine?topic=codeengine-service-binding#service-binding-access).

## {{site.data.keyword.codeengineshort}} CLI access requirements
{: #cli-access-req}

To work with a {{site.data.keyword.codeengineshort}} project with the CLI, you must first target a resource group. To target a resource group with the CLI, you need Viewer access to the resource group.


