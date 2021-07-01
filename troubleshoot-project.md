---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-01"

keywords: troubleshooting for code engine projects, projects, tips for projects, accessing projects, tips for creating project

subcollection: codeengine

content-type: troubleshoot

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
{:terraform: .ph data-hd-interface='terraform'}
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
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Debugging for projects
{: #troubleshoot-project}
{: troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot {{site.data.keyword.codeengineshort}} projects.
{: shortdesc}

To understand how to create, work with, and delete projects, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).

## Project limits to consider 
{: #ts-project-limits}

The maximum number of projects that you can create per region is 20. For more information about limits for projects, see [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

The maximum number of projects includes projects that are active and any projects that are not permanently deleted, such as projects that are soft deleted. Projects that are soft deleted can be restored within 7 days before it is permanently deleted. 

When working with the console, review your defined projects from the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}. This listing includes the region where your project lives. From this page, you can delete projects as needed. When you delete a project from the console, the project is soft deleted. The deleted project does not display from the **Projects** page. 

When working with the CLI, use the [**`project list`**](/docs/codeengine?topic=codeengine-cli#cli-project-list) command to display all of your projects. The output of this command displays the region where your project lives. 

Use the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command to delete a project. In the CLI, you can delete a project by specifying the name of the project or by specifying the `project id`. If you specify the `--name` of the project, you must be working in the same region where the project lives. If you specify the `--id` of the project, you are not required to be in the same project to issue the **`project delete`** command. 

The following example command soft deletes the `myproject` project so that it can be restored within 7 days, `ibmcloud ce project delete --name myproject -f`. The `-f` option specifies to force the delete without confirmation. Note, this soft deleted project still counts towards the project maximum until the project is permanently removed 7 days later. 

To permanently delete a project so that it cannot be restored, specify the `--hard` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command, for example, `ibmcloud ce project delete --name myproject2 --hard -f`.

For more information, see [deleting a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).

