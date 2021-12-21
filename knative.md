---

copyright:
  years: 2020, 2021
lastupdated: "2021-12-20"

keywords: command-line interface, kubernetes and code engine cli, knative and code engine cli, kubectl and code engine cli, kubernetes, knative

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Using Knative with Code Engine
{: #knative}

{{site.data.keyword.codeenginefull}} is designed so that you do not need to interact with the underlying technology it is built upon. However, if you have existing tooling that is based on Knative, you can still use it with {{site.data.keyword.codeengineshort}}. {{site.data.keyword.codeengineshort}} supports the Knative APIs (and Kubernetes) and their CLI commands. For more information about Kubernetes, see [Using Kubernetes with Code Engine](/docs/codeengine?topic=codeengine-kubernetes).
{: shortdesc}

## Installing the Knative command-line interface
{: #knative-kubectl}

To install Knative (`kn`), download and install the [Knative CLI](https://github.com/knative/client/blob/main/docs/README.md){: external}.

To use Knative with {{site.data.keyword.codeengineshort}}, you must first set up your environment to interact with the Kubernetes API of {{site.data.keyword.codeengineshort}}. For more information, see [Installing the Kubernetes command-line interface](/docs/codeengine?topic=codeengine-kubernetes#kubernetes-kubectl).

For more information about Kubernetes and Knative and how they work with {{site.data.keyword.codeengineshort}} architecture, see [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).
{: important}

## Interacting with Kubernetes API
{: #kubectl-kubeconfig-knative}


To interact with your project from the Kubernetes command-line interface, `kubectl`, or with Knative, `kn` you must set up your environment to interact with the Kubernetes API of {{site.data.keyword.codeengineshort}}.

Before you begin

- You must [create your project](/docs/codeengine?topic=codeengine-manage-project#create-a-project) and the project must be in `active` status.
- Install the [Kubernetes CLI (`kubectl`)](#knative-kubectl) and the [Knative CLI (`kn`)](#knative-kubectl).

You can set up your environment in the following ways. 

- You can add the `--kubecfg` option to your **`project select`** command. For example, 

    ```sh
    ibmcloud ce project select --name PROJECT_NAME --kubecfg
    ```
    {: pre}

- You can export the `kubeconfig` file directly. Run the **`ibmcloud ce project current`** command to find the project that you are currently targeting. This command also returns the **`export`** command for your `kubeconfig` file. For example,

    ```sh
    ibmcloud ce project current
    ```
    {: pre}

    **Example output**

    ```sh
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

```sh
kubectl config current-context
```
{: pre}

If the context is correctly set, the output matches the `Kubectl Context` value of your project. For example, if your `Kubectl Context` value of your project is `4svg40kna19`, the command returns `4svg40kna19`.

For more information about Kubernetes and how it works with {{site.data.keyword.codeengineshort}} architecture, see [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).
{: important}
  
## Required access authorities to work with Knative API
{: #knative-api}

After you set up your environment, you can interact with Knative API. You must have the correct level of authority for specific tasks. These roles are set in Identity and access management. See [{{site.data.keyword.cloud_notm}} service roles](/docs/codeengine?topic=codeengine-iam#service).

| Resource |  Manager Role | Writer Role | Reader Role |
| --------- | -------------- | ------------ | ------------ |
| `services.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
| `configurations.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
| `routes.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
| `revisions.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit  | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
| `pingsource.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
| `kafkasource.serving.knative.dev` | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch, create, delete, update, patch, apply, edit | get, list, watch |
{: caption="Table 1. Knative authorities" caption-side=ottom"}

