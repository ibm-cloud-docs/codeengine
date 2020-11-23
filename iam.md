---

copyright:
  years: 2020
lastupdated: "2020-11-23"

keywords: IAM access for code engine, permissions for code engine, identity and access management for code engine, roles for code engine, actions for code engine, assigning access for code engine

subcollection: codeengine
---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Managing user access
{: #iam}

Access to {{site.data.keyword.codeenginefull_notm}} service instances for users in your account is controlled by {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.codeengineshort}} service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. 
{: shortdesc}

*Policies* enable access to be granted at different levels.

*Roles* define the actions that a user or serviceID can run. There are different types of roles in the {{site.data.keyword.cloud_notm}}:

* *Platform management roles* enable users to perform tasks on service resources at the platform level, for example assign user access for the service, create or delete service IDs, create instances, assign policies for your service to other users, and bind instances to applications.
* *Service access roles* enable users to be assigned varying levels of permission for calling the service's API.

{{site.data.keyword.codeengineshort}} uses both the Platform and Service management roles. You can set policies about who can create a project at the platform level, and then use the service roles to manage interaction with the project itself. As the creator of a project, you do not need to set any IAM policies to view or work with your {{site.data.keyword.codeengineshort}} entities.

Want to learn more about IAM key concepts? Check out [What is IBM Cloud Identity and Access Management?](/docs/account?topic=account-iamoverview).
{: tip}

## How do I know which access policies have set for me?

You can see which access policies have been set for you in the [{{site.data.keyword.cloud}} catalog](https://cloud.ibm.com/catalog){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.

## Managing access by using access groups
{: #groups}

To manage access or assign new access for users by using access groups, you must be the account owner, administrator, or editor on all Identity and Access enabled services in the account, or the assigned Administrator or Editor for the IAM Access Groups Service. 

Choose any of the following actions to manage access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/account?topic=account-groups#create_ag).
* [Assigning access to a group](/docs/account?topic=account-groups#access_ag).


## Managing access by assigning policies directly to users
{: #users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance. 

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To grant permissions to a user, see [Assigning access](/docs/account?topic=account-assign-access-resources#assign_new_access).
* To revoke permissions, see [Removing access](/docs/account?topic=account-assign-access-resources#removing_access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/account?topic=account-assign-access-resources#review_your_access).

## {{site.data.keyword.cloud_notm}} platform roles
{: #platform}

Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service, create or delete instances, and bind instances to applications.

Use the following table to identify the platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:


| Platform actions                                                          | Administrator                                     | Editor | Operator | Viewer  |
|---------------------------------------------------------------------------|:-------------------------------------------------:|:-------:|:--------:|:------:|
| Grant other account members access to work with the service             | ![Check mark icon](images/confirm.png "Feature available") |         |          |        |
| Provision a service instance                                            | ![Check mark icon](images/confirm.png "Feature available") | ![Check mark icon](images/confirm.png "Feature available") |      |      |
| Delete a service instance                                              | ![Check mark icon](images/confirm.png "Feature available") | ![Check mark icon](images/confirm.png "Feature available")    |        |      |
| Update a service instance                                               | ![Check mark icon](images/confirm.png "Feature available")  | ![Check mark icon](images/confirm.png "Feature available")    |        |      |
| Create a service ID                                                    | ![Check mark icon](images/confirm.png "Feature available")  | ![Check mark icon](images/confirm.png "Feature available")    |        |      |
| View {{site.data.keyword.codeengineshort}} dashboard  | ![Check mark icon](images/confirm.png "Feature available")  | ![Check mark icon](images/confirm.png "Feature available")    | ![Check mark icon](images/confirm.png "Feature available")      |        |
| View details of a service instance                                      | ![Check mark icon](images/confirm.png "Feature available")  | ![Check mark icon](images/confirm.png "Feature available")    | ![Check mark icon](images/confirm.png "Feature available")      | ![Check mark icon](images/confirm.png "Feature available")    |
{: caption="Table 1. IAM user platform roles and actions" caption-side="top"}


## {{site.data.keyword.cloud_notm}} service roles
{: #service}

Use the following table to identify the service roles that you can grant a user to run any of the following service actions:

| Actions                                                                 | Manager                                           | Writer                     | Reader |
|-------------------------------------------------------------------------|:-------------------------------------------------:|:-----------------------------------:|:------:|
| Create items within a project                       | ![Check mark icon](images/confirm.png "Feature available") | ![Check mark icon](images/confirm.png "Feature available")                    |    |
| Update items within a project                                                | ![Check mark icon](images/confirm.png "Feature available")      | ![Check mark icon](images/confirm.png "Feature available")                    |    |
| Delete items within a project                                          | ![Check mark icon](images/confirm.png "Feature available")      | ![Check mark icon](images/confirm.png "Feature available")                    |    |
| List and view items within a project                                      | ![Check mark icon](images/confirm.png "Feature available")      | ![Check mark icon](images/confirm.png "Feature available")                    |     |
| View project details                                         | ![Check mark icon](images/confirm.png "Feature available")      | ![Check mark icon](images/confirm.png "Feature available")                    | ![Check mark icon](images/confirm.png "Feature available")    |
{: caption="Table 2. IAM service roles and actions" caption-side="top"}
