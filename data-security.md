---

copyright:
  years: 2022
lastupdated: "2022-02-10"

keywords: data encryption in code engine, data storage for code engine, bring your own keys for code engine, BYOK for code engine, key management for code engine, key encryption for code engine, personal data in code engine, data deletion for code engine, data in code engine, data security in code engine, encrypted

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in {{site.data.keyword.codeengineshort}}
{: #mng-data}

{{site.data.keyword.codeengineshort}} provides a platform to unify the deployment of all your container-based applications. Whether those applications are functions, traditional 12-factor apps, batch workloads or any other container-based workloads, if they can be bundled into a container image, then {{site.data.keyword.codeengineshort}} can host and manage them for you - all on a Kubernetes-based infrastructure. And {{site.data.keyword.codeengineshort}} does this without the need for you to learn, or even know about, Kubernetes. As {{site.data.keyword.codeengineshort}} is not a data service, it does not store personal or sensitive data. 
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.codeengineshort}}
{: #data-storage}

While {{site.data.keyword.codeengineshort}} does not store personal or sensitive data, when running {{site.data.keyword.codeengineshort}}, the data that is stored by {{site.data.keyword.codeengineshort}} includes references to container images where you run the images as {{site.data.keyword.codeengineshort}} applications or batch jobs. {{site.data.keyword.codeengineshort}} does not store the container image data. Instead, it uses the pointer that you provide to where your container image repository is located, which might be a public repository like DockerHub or a private IBM Container Registry. Therefore, encryption of your data in your container images is implemented and managed as part of your container image repository. 

Some data, like DockerHub credentials, batch job templates and IBM container registry APIKey are stored as part of your namespace in {{site.data.keyword.codeengineshort}}, within an underlying Kubernetes secret map (within your Kubernetes etcd data). For more information, see [Securing information in Kubernetes](/docs/containers?topic=containers-encryption). 


## Deleting your data in {{site.data.keyword.codeengineshort}}
{: #data-delete}

Data in images is deleted within your container image repository. 

To delete data that is stored within {{site.data.keyword.codeengineshort}}, such as DockerHub credentials, batch job templates, or an IBM container registry APIKey, [delete your {{site.data.keyword.codeengineshort}} project](/docs/codeengine?topic=codeengine-manage-project#delete-project). 

When you delete a project from the console or with the CLI, it is soft deleted and can be restored. You must restore your project within 7 days or it is permanently deleted. For more information about restoring projects, see [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project). To permanently delete a project, see [Permanently deleting projects](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project).

When you delete a project, any projects that are not permanently deleted count toward the maximum of 20 total projects per region that are allowed.
{: tip} 

By using the `--force` option with the [**`project delete`**](/docs/codeengine?topic=codeengine-cli#cli-project-delete) command, the delete is forced without confirmation.  

**Example**

```txt
ibmcloud ce project delete --name myproject --force
```
{: pre}

**Example output**

```txt
Deleting project `myproject`
OK
```
{: screen}  


