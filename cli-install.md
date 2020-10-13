---

copyright:
  years: 2020
lastupdated: "2020-10-13"

keywords: code engine

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
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
{:java: #java .ph data-hd-programlang='java'}
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
{:swift: #swift .ph data-hd-programlang='swift'}
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
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# Setting up the CLI 
{: #install-cli}

Install, update, and delete the required CLIs and set up your environment to use {{site.data.keyword.codeenginefull_notm}}. 
{: shortdesc}

## Installing the {{site.data.keyword.cloud_notm}} CLI 
{: #cli-setup}

Install the latest version of the {{site.data.keyword.cloud_notm}} CLI.
{:shortdesc}

**Before you begin**

You must create an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external}.

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

  This installation includes the following files: 
    * IBM Cloud Functions plug-in
    * IBM Cloud Object Storage plug-in
    * IBM Cloud Container Registry plug-in
    * IBM Cloud Kubernetes Service plug-in

  For more information, see [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). 

2. Log in to the {{site.data.keyword.cloud_notm}} CLI.

  ```
  ibmcloud login
  ```
  {: pre}

3. If you have more than one account, you are prompted to select which account to use. Follow the prompts or use the `target` command to select your {{site.data.keyword.cloud_notm}} account.

  ```
  ibmcloud target -c <account_id>
  ```
  {: pre}

4. You must also specify a region. You can use the `target` command to target or change regions.
  
  ```
  ibmcloud target -r <region>
  ```
  {: pre}

5. You must specify a resource group. To get a list of your resource groups, run the following command.

    ```
    ibmcloud resource groups
    ```
    {: pre}

    **Example output**

    ```
    Retrieving all resource groups under account <account_name> as email@ibm.com...
    OK
    Name      ID                                 Default Group   State   
    default   a8a12accd63b437bbd6d58fb8b462ca7   true            ACTIVE
    test      a8a12abbbd63b437cca6d58fb8b462ca7   false           ACTIVE
    ```
    {: screen}

6. Target a resource group by running the following command.

    ```
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    **Example output**

    ```
    Targeted resource group default
    ```
    {: screen}

## Installing the {{site.data.keyword.codeengineshort}} CLI plug-in
{: #install-cli-plugin}

Install the latest version of the {{site.data.keyword.codeengineshort}} CLI.
{: shortdesc}

Be sure that you installed the latest version of the {{site.data.keyword.cloud_notm}} CLI. Otherwise, your {{site.data.keyword.codeengineshort}} CLI installation might fail with a message similar to `Could not find compatible binary to install for plug-in code-engine`.
{: tip}



1. Install the {{site.data.keyword.codeengineshort}} plug-in.

  ```
  ibmcloud plugin install code-engine
  ```
  {: pre}

2. Use the `ibmcloud plugin show code-engine` command to verify that the plug-in is installed.

  ```
  ibmcloud plugin show code-engine
  ```
  {: pre}

  **Example output**

  ```
  Plugin Name                              code-engine/ce
  Plugin Version                           0.3.1350
  Plugin SDK Version                       0.3.0
  Minimal IBM Cloud CLI version required   1.0.0
  ```
  {: screen}

3. To run {{site.data.keyword.codeengineshort}}} commands, use `ibmcloud code-engine` or `ibmcloud ce`. To see everything that you can do with the {{site.data.keyword.codeengineshort}} plug-in, run `ibmcloud ce` with no arguments.

  ```
  ibmcloud ce
  ```
  {: pre}
  
Optionally, you can install the [`jq` package](https://stedolan.github.io/jq){: external}. Many {{site.data.keyword.codeengineshort}} commands include an option (`--output JSON`) to create JSON output. With this package, you can view and parse JSON responses from the command line.
{: tip}

For more information about {{site.data.keyword.codeengineshort}} commands, see the [`ibmcloud ce` commands](/docs/codeengine?topic=codeengine-kn-cli).

## Updating the {{site.data.keyword.codeengineshort}} CLI
{: #update-cli}

Update the CLI periodically to take advantage of new features.

1. View your current plug-in list by running the `ibmcloud plugin list` command.

   ```
   ibmcloud plugin list
   ```
   {: pre}
   
   **Example output**
   
   ```
   Plugin Name                            Version    Status
   code-engine/ce                         0.3.1350
   container-registry                     0.1.482
   container-service/kubernetes-service   1.0.118
   ```
   {: screen}

2. If an update is available, run the `ibmcloud plugin update` command.

   ```
   ibmcloud plugin update code-engine
   ```
   {: pre}


## Uninstalling the CLI
{: #uninstall-cli}

If you no longer need the CLI, you can uninstall it.

1. List the plug-ins that are installed.
   
   ```
   ibmcloud plugin list
   ```
   {: pre}
   
2. Uninstall the plug-ins. For example, to uninstall the {{site.data.keyword.codeengineshort}} CLI plug-in:
   
   ```
   ibmcloud plugin uninstall code-engine
   ```
   {: pre}
   
3. Verify the plug-ins were uninstalled by running the following command and checking the list of the plug-ins that are installed.

   ```
   ibmcloud plugin list
   ```
   {: pre}

The plug-ins that you deleted are not displayed in the results.

## <img src="images/kube.png" alt="Kubernetes icon"/> Inside {{site.data.keyword.codeengineshort}}: Knative and Kubernetes command-line interface
{: #knative-kubectl}

Many {{site.data.keyword.codeengineshort}} commands are based on Knative and Kubernetes commands. If you are interested in exploring these command-line interfaces, you must first install them.

### Installing Knative 
{: #knative-install}

Install the latest version of the Knative command-line interface, `kn`. 
{:shortdesc}

1. Download and install the [Knative CLI](https://github.com/knative/client/blob/master/docs/README.md){: external}. 

  Be sure to add the `kn` binary to your system's PATH environment variable. 
  {: tip}

2. Run the following command to confirm `kn` is installed:

  ```
  kn version
  ```
  {: pre}

  **Example output**

  ```
    Version:      v20200501-88805dc
    Build Date:   2020-05-01 02:05:19
    Git Revision: 88805dc
    Supported APIs:
    * Serving
      - serving.knative.dev/v1 (knative-serving v0.13.2)
    * Eventing
      - sources.eventing.knative.dev/v1 (knative-eventing v0.13.6)
      - eventing.knative.dev/v1 (knative-eventing v0.13.6)
  ```
  {: screen}

### Installing `kubectl` 
{: #kube-install}

Install the latest version of the Kubernetes command-line interface, `kubectl`. 
{:shortdesc}

When you installed the [{{site.data.keyword.cloud_notm}} CLI](#cli-setup), `kubectl` might also be installed. To check, type `kubectl version`. If `kubectl` is already installed, the command outputs your current version information and you do not need to install it again.

1. Download and install the [`kubectl` CLI]](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external}. 

  Be sure to add the `kubectl` binary to your system's PATH environment variable. 
  {: tip}

2. Run the following command to verify `kubectl` is installed:

  ```
  kubectl version --short
  ```
  {: pre}

  **Example output**

  ```
  Client Version: v1.18.0
  Server Version: v1.16.8+IKS
  ```
  {: screen}

### Next steps

In order to use `kubectl` or `kn` with {{site.data.keyword.codeengineshort}} projects, you must set up your environment to interact with the Kubernetes API. For more information, see [Inside {{site.data.keyword.codeengineshort}}: Interacting with Kubernetes API](/docs/codeengine?topic=codeengine-manage-project#kubectl-kubeconfig).
