---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-09"

keywords: command-line interface, kubernetes and code engine cli, knative and code engine cli, kubectl and code engine cli, kubernetes, knative

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
{:audio: .audio}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: .ph data-hd-programlang='c#'}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: #curl .ph data-hd-programlang='curl'}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: .external target="_blank"}
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
{:middle: .ph data-hd-position='middle'}
{:navgroup: .navgroup}
{:new_window: target="_blank"}
{:node: .ph data-hd-programlang='node'}
{:note: .note}
{:objectc: .ph data-hd-programlang='Objective C'}
{:objectc: data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: .ph data-hd-programlang='PHP'}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:release-note: data-hd-content-type='release-note'}
{:right: .ph data-hd-position='right'}
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
{:step: data-tutorial-type='step'} 
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:topicgroup: .topicgroup}
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


# Using Kubernetes with {{site.data.keyword.codeengineshort}} 
{: #kubernetes}

{{site.data.keyword.codeenginefull}} is designed so that you do not need to interact with the underlying technology it is built upon. However, if you have existing tooling that is based upon Kubernetes or Knative, you can still use it with {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} supports the Kubernetes (and Knative) APIs as well as their CLI commands. For information about Knative, see [Using Knative with Code Engine](/docs/codeengine?topic=codeengine-knative).
{: shortdesc}

## Installing the Kubernetes command-line interface
{: #kubernetes-kubectl} 

To install the Kubernetes CLI, download and install the [`kubectl` CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/){: external}.
{: shortdesc}

Be sure to add the `kubectl` binary to your system's PATH environment variable. 
{: tip}

## Interacting with Kubernetes API
{: #kubectl-kubeconfig}


In order to interact with your project from the Kubernetes command-line interface, `kubectl`, or with Knative, `kn` you must set up your environment to interact with the Kubernetes API of {{site.data.keyword.codeengineshort}}.

**Before you begin**

- You must [create your project](/docs/codeengine?topic=codeengine-manage-project#create-a-project) and the project must be in `active` status.
- Install the [Kubernetes CLI (`kubectl`)](#knative-kubectl) and the [Knative CLI (`kn`)](#knative-kubectl).

You can set up your environment in the following ways. 

- You can add the `--kubecfg` option to your **`project select`** command. For example, 

    ```
    ibmcloud ce project select --name PROJECT_NAME --kubecfg
    ```
    {: pre}

- You can export the `kubeconfig` file directly. Run the **`ibmcloud ce project current`** command to find the project that you are currently targeting. This command also returns the **`export`** command for your `kubeconfig` file.  For example,

    ```
    ibmcloud ce project current
    ```
    {: pre}

    **Example output**

    ```
    Getting the current project context...
    OK

    Name:       myproject
    ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Subdomain:  aabon2dfwa0
    Domain:     us-south.codeengine.appdomain.cloud
    Region:     us-south
    Kubectl Context:  4svg40kna19

    Kubernetes Config:
    Context:             aabon2dfwa0
    Environment Variable: export KUBECONFIG=/user/myusername/.bluemix/plugins/code-engine/myproject-01234567-abcd-abcd-abcd-abcdabcd1111.yaml
    ```
    {: screen}

    Then, copy the export command, paste it into your command-line interface, and run it.

Verify that your environment is set correctly by running the **`kubectl config`** command.

```
kubectl config current-context
```
{: pre}

If the context is correctly set, the output matches the `Kubectl Context` value of your project. For example, if your `Kubectl Context` value of your project is `4svg40kna19`, the command returns `4svg40kna19`.

For more information about Kubernetes and how it works with {{site.data.keyword.codeengineshort}} architecture, see [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).
{: important}
  
## Required access authorities to work with Kubernetes API
{: #kubectl-api}

After you set up your environment, you can interact with Kubernetes API. You must have the correct level of authority for specific tasks. These roles are set in Identity and access management. See [{{site.data.keyword.cloud_notm}} service roles](/docs/codeengine?topic=codeengine-iam#service).

| Resource |  Manager Role | Writer Role | Reader Role |
| --------- | -------------- | ------------ | ------------ |
| `serviceaccounts` | get, list, watch | get, list, watch | None |
| `secrets` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | None |
| `configmaps` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | None |
| `events` | get, list, watch | get, list, watch | None |
| `pods/log` | get, list, watch | get, list, watch | get, list, watch |
| `pods` | get, list, watch, create, delete, patch, apply | get, list, watch, create, delete, patch, apply | get, list, watch |
| `services` | get, list, watch, create, delete, patch, apply | get, list, watch, create, delete, patch, apply | get, list, watch |
| `pods/exec` | create | create | None |
| `pods/portforward` | create | create | None |
| `pods/attach` | create | None | None |
| `pods/status` | get, list | get, list | None |
| `resourcequotas` | get, list, watch | get, list, watch | get, list, watch |
| `limitranges` | get, list, watch | get, list, watch | None |
| `deployments` | get, list, watch, create, delete, patch, apply | get, list, watch, create, delete, patch, apply | get, list, watch |
| `daemonset` | get, list, watch, create, delete, patch, apply | get, list, watch | get, list, watch |
| `pods.metrics.k8s.io` | list | list | list |
{: caption="Table 1. Kubernetes authorities" caption-side=ottom"}

