---

copyright:
  years: 2021
lastupdated: "2021-06-03"

keywords: data encryption in code engine, data storage for code engine, bring your own keys for code engine, BYOK for code engine, key management for code engine, key encryption for code engine, personal data in code engine, data deletion for code engine, data in code engine, data security in code engine, encrypted

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


# Securing your data in {{site.data.keyword.codeengineshort}}
{: #mng-data}

{{site.data.keyword.codeengineshort}} provides a platform to unify the deployment of all of your container-based applications. Whether those applications are functions, traditional 12-factor apps, batch workloads or any other container-based workloads, if they can be bundled into a container image, then {{site.data.keyword.codeengineshort}} can host and manage them for you - all on a Kubernetes-based infrastructure. And {{site.data.keyword.codeengineshort}} does this without the need for you to learn, or even know about, Kubernetes.  As {{site.data.keyword.codeengineshort}} is not a data service, it does not store personal or sensitive data. 
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.codeengineshort}}
{: #data-storage}

While {{site.data.keyword.codeengineshort}} does not store personal or sensitive data, when running {{site.data.keyword.codeengineshort}}, the data that is stored by {{site.data.keyword.codeengineshort}} includes references to container images where you run the images as {{site.data.keyword.codeengineshort}} applications or batch jobs.  {{site.data.keyword.codeengineshort}} does not store the container image data. Instead, it uses the pointer that you provide to where your container image repository is located, which might be a public repository like DockerHub or a private IBM Container Registry. Therefore, encryption of your data in your container images is implemented and managed as part of your container image repository. 

Some data, like DockerHub credentials, batch job templates and IBM container registry APIKey are stored as part of your namespace in {{site.data.keyword.codeengineshort}}, within an underlying Kubernetes secret map (within your Kubernetes etcd data). For more information, see [Securing information in Kubernetes](/docs/containers?topic=containers-encryption). 
 

## Deleting your data in {{site.data.keyword.codeengineshort}}
{: #data-delete}

Data in images is deleted within your container image repository. 

To delete data that is stored within {{site.data.keyword.codeengineshort}}, such as DockerHub credentials, batch job templates, or an IBM container registry APIKey, [delete your {{site.data.keyword.codeengineshort}} project](/docs/codeengine?topic=codeengine-manage-project#delete-project). 

When you delete a project, it is soft deleted and can be restored within 7 days before it is permanently deleted. You can restore a soft deleted project by using the {{site.data.keyword.cloud_notm}} CLI [**`ibmcloud resource reclamation-restore`**](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamation_restore) command. You must restore your project within 7 days or it is permanently deleted. For more information, see [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project). 

To delete a project so that it cannot be restored, use the `--hard` option with the **`project delete`** CLI command to specify to immediately delete the project.  

By using the `--force` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command, the delete is forced without confirmation.  

**Example**

```sh
ibmcloud ce project delete --name myproject --force
```
{: pre}

**Example output**

```
Deleting project `myproject`
OK
```
{: screen}  
