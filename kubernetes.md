---

copyright:
  years: 2021
lastupdated: "2021-05-21"

keywords: command-line interface for code engine, cli, cli for code engine, install cli for code engine, configuring code engine cli, kubernetes and code engine cli, knative and code engine cli, kubectl and code engine cli

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


# Using Kubernetes with Code Engine
{: #kubernetes}

{{site.data.keyword.codeenginefull}} is designed so that you do not need to interact with the underlying technology it is built upon. However, if you have existing tooling that is based upon Kubernetes or Knative, you can still use it with {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} supports the Kubernetes and Knative APIs as well as their respective CLIs. The following sections provide instructions for how to install and configure your environment to use these tools.
{: shortdesc}

## Installing the Knative and Kubernetes command-line interface
{: #knative-kubectl}

To install Knative (`kn`), download and install the [Knative CLI)(https://github.com/knative/client/blob/main/docs/README.md){: external}. 

To install Kubernetes (`kubectl`), download and install the [`kubectl` CLI]](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external}. 

Be sure to add the `kn` and `kubectl` binaries to your system's PATH environment variable. 
{: tip}

## Interacting with Kubernetes API
{: #kubectl-kubeconfig}
  
In order to interact with your project from the Kubernetes command-line interface, `kubectl`, or with Knative, `kn` you must set up your environment to interact with the Kubernetes API of {{site.data.keyword.codeengineshort}}.

**Before you begin**

- You must [create your project](/docs/codeengine?topic=codeengine-manage-project#create-a-project) and the project must be in `active` status.
- Install the [Kubernetes CLI (`kubectl`)](#knative-kubectl) and the [Knative CLI (`kn`)](#knative-kubectl).

You can set up your environment in the following ways. 

- You can add the `--kubecfg` option to your `project select` command. For example, 

  ```sh
  ibmcloud ce project select --name PROJECT_NAME --kubecfg
  ```
  {: pre}

- You can export the `kubeconfig` file directly. Run the **`ibmcloud ce project current`** command to find the project that you are currently targeting. This command also returns the **`export`** command for your `kubeconfig` file.  For example,

  ```sh
  ibmcloud ce project current
  ```
  {: pre}

  **Example output**

  ```
  Getting the current project context...
  OK

  Project Name:     myproject  
  Project ID:       01234567-abcd-abcd-abcd-abcdabcd1111
  Region:           us-south 
  Kubectl Context:  4svg40kna19 

  To use kubectl with your project, run the following command:
  export KUBECONFIG=/Users/email@us.ibm.com/.bluemix/plugins/code-engine/myproject-01234567-abcd-abcd-abcd-abcdabcd1111.yaml
  ```
  {: screen}

  Then, copy the export command, paste it into your command-line interface, and run it.

Verify that your environment is set correctly by running the **`kubectl config`** command.

```sh
kubectl config current-context
```
{: pre}

If the context is correctly set, the output matches the `Kubectl Context` value of your project. For example, if your `Kubectl Context` value of your project is `4svg40kna19`, the command returns `4svg40kna19`.

For more information about Kubernetes and how it works with {{site.data.keyword.codeengineshort}} architecture, see [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).
{: important}
