---

copyright:
  years: 2020
lastupdated: "2020-07-15"

keywords: code engine

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

# Setting up the CLI 
{: #kn-install-cli}

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

## Installing Knative 
{: #knative-install}

Install the latest version of the Knative command line interface, `kn`. 
{:shortdesc}

1. Download and install the [Knative CLI]](https://github.com/knative/client/blob/master/docs/README.md){: external}. 

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

## Installing `kubectl` 
{: #kube-install}

Install the latest version of the Kubernetes command line interface, `kubectl`.
{:shortdesc}

**Before you begin**

When you installed the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started), `kubectl` might have been installed. To check, type `kubectl version`. If `kubectl` is already installed, the command will output your current version information.  If `kubectl` is already installed, you do not need to complete the following steps to install `kubectl`. 

1. Download and install the [kubectl CLI]](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external}. 

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

## Installing the {{site.data.keyword.codeengineshort}} CLI plug-in
{: #kn-install-cli-plugin}

Now that you have installed {{site.data.keyword.cloud_notm}} CLI, `kn`, and `kubectl`, you are ready to install {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} uses `kubectl` to interact with your Kubernetes clusters and uses `kn` to manage your knative applications and jobs on those clusters. 



Complete the following steps to install the {{site.data.keyword.codeengineshort}} CLI plug-in.

1. Install the {{site.data.keyword.codeengineshort}} plug-in.

  ```
  ibmcloud plugin install code-engine
  ```
  {: pre}

2. Use the `ibmcloud plugin show code-engine` command to verify that the plug-in is installed.

  ```
  ibmcloud plugin list
  ```
  {: pre}

  **Example output**

  ```
  Plugin Name                              coligo/coligo-cli
  Plugin Version                           0.1.503
  Plugin SDK Version                       0.3.0
  Minimal IBM Cloud CLI version required   0.13.1
  ```
  {: screen}

3. To run {{site.data.keyword.codeengineshort}}} commands, use `ibmcloud code-engine` or `ibmcloud ce`. To see everything that you can do with the {{site.data.keyword.codeengineshort}} plug-in, run `ibmcloud ce` with no arguments.

  ```
  ibmcloud ce
  ```
  {: pre}
  
4. Optionally, install [`jq`](https://stedolan.github.io/jq){: external} to process JSON in the command line. This package enables you to view and parse JSON responses in the command line.

For more information about {{site.data.keyword.codeengineshort}} commands, see the [`ibmcloud ce` commands](/docs/codeengine?topic=codeengine-kn-cli).

## Updating the {{site.data.keyword.codeengineshort}} CLI
{: #kn-update-cli}

Update the CLI periodically to take advantage of new features.

1. View your current plug-in list by running the `ibmcloud plugin list` command.

   ```
   ibmcloud plugin list
   ```
   {: pre}
   
   **Example output**
   
   ```
   Plugin Name                                 Version   Status        
   code-engine                              1.0       Update Available   
   cloud-object-storage                        1.1.0        
   container-registry                          0.1.437      
   container-service/kubernetes-service        0.4.51       
   ```
   {: screen}

2. If an update is available, run the `ibmcloud plugin update` command.

   ```
   ibmcloud plugin update code-engine
   ```
   {: pre}


## Uninstalling the CLI
{: #kn-uninstall-cli}

If you no longer need the CLI, you can uninstall it.

To uninstall the CLI:

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
