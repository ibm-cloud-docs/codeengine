---

copyright:
  years: 2024
lastupdated: "2025-02-28"

keywords: code engine, data portability

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}



# Understanding data portability for {{site.data.keyword.codeengineshort}}
{: #data-portability}





Data portability involves a set of commands that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes commands for exporting the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.



For more information about your responsibilities for {{site.data.keyword.codeengineshort}}, see [Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce). 

## Data export procedures
{: #data-portability-procedures}

{{site.data.keyword.codeengineshort}} provides mechanisms to build container images from source code. Source code can be stored either locally or on Github. {{site.data.keyword.codeengineshort}} does not provide commands or tools to download such container images. Instead, customers need to download and store those images following the [data export procedures for {{site.data.keyword.registryfull_notm}}](/docs/Registry?topic=Registry-data_portability). 



{{site.data.keyword.codeengineshort}} provides mechanisms to export settings and configurations that are used to process the customer's content.



Configuration data for the following {{site.data.keyword.codeengineshort}} entities can be exported using the commands specified later in this section:
- Projects
- Applications
- Application revisions
- Builds
- Build runs
- Configmaps
- Secrets
- Domain mappings
- Event subscriptions ({{site.data.keyword.cos_full_notm}}, `cron`, and Kafka)
- Functions
- Jobs
- Job runs

### Tools required for exporting data
{: #ools}

For exporting {{site.data.keyword.codeengineshort}} data, you need to download and install the following commandline tools:

- The {{site.data.keyword.cloud_notm}} CLI client
    - Visit the {{site.data.keyword.cloud_notm}} CLI [Getting started page](/docs/cli?topic=cli-getting-started) to install the CLI client for your operating system.
- The {{site.data.keyword.codeengineshort}} CLI plug-in
    - Visit the [{{site.data.keyword.codeengineshort}} CLI page](/docs/codeengine?topic=codeengine-cli) which has instructions on how to install the {{site.data.keyword.codeengineshort}} plug-in for the {{site.data.keyword.cloud_notm}} CLI.
- The Kubernetes CLI client
    - Visit the [Kubernetes Install Tools page](https://kubernetes.io/docs/tasks/tools/#kubectl) to install the `kubectl` CLI client for your operating system.

### Exporting `project` configuration
{: #exporting}

A project in {{site.data.keyword.codeengineshort}} is a container of related configurations and workloads. If you want to export a project, use the following `ibmcloud resource` commands:

To list all {{site.data.keyword.codeengineshort}} projects use:
```text
ibmcloud resource service-instances --service-name codeengine
```
{: pre}

To list all {{site.data.keyword.codeengineshort}} projects in a specific region use:
```text
ibmcloud resource service-instances --service-name codeengine --location us-south
```
{: pre}

When you have identified the {{site.data.keyword.codeengineshort}} project you want to export use:
```text
ibmcloud resource service-instance <project-name> -o json >project-name.json
```
{: pre}

Exporting a {{site.data.keyword.codeengineshort}} project only exports configuration of the project entity itself. Contained configuration entities and workload entities need to be exported separately.
{: note}

### Exporting a `KUBECONFIG` to export project entities
{: #exporting-kubeconfig}

When you have identified a project you want to export, you have to export a `KUBECONFIG` environment variable to scope the `kubectl` commands described in this document to that project.

To obtain this `KUBECONFIG` environment variable, run the following commands

```text
ibmcloud code-engine project select -n <project-name>
ibmcloud code-engine project current
```
{: pre}

This selects the project and prints a statement similar to the following one:

```text
Getting the current project context...
OK

Name:       <project-name>
ID:         123a4cbc-567d-8e90-1f2b-032d33d931ba
Subdomain:  1abc2defi34
Domain:     us-south.codeengine.appdomain.cloud
Region:     us-south

Kubernetes Config:
Context:               1abc2defi34
Environment Variable:  export KUBECONFIG="/Users/<username>/.bluemix/plugins/code-engine/<project-name>-123a4cbc-567d-8e90-1f2b-032d33d931ba.yaml"
```
{: pre}

Copy the `export KUBECONFIG=xxx` statement to your terminal prompt and run it. All following `kubectl` commands are now scoped to this project.

### Exporting `application` configuration
{: #exporting-application}

To export the configuration of all applications in your project, run the following `kubectl` command:

```text
kubectl get service -o json >project-name_application-configurations.json
```
{: pre}

If you want to export the configuration of a single application, use the following `kubectl` command:

```text
kubectl get service <application-name> -o json >project-name-application-name_application-configuration.json
```
{: pre}

### Exporting `application revision` configuration
{: #exporting-application-revision}

To export the configuration of all application revisions in your project, run the following `kubectl` command:

```text
kubectl get revision -o json >project-name_application-revisions.json
```
{: pre}

If you want to export the configuration of a single application revision, use the following `kubectl` command:

```text
kubectl get revision <application-revision-name> -o json >project-name-application-revision-name_revision.json
```
{: pre}

### Exporting `build` configuration
{: #exporting-build}

To export the configuration of all builds in your project, run the following `kubectl` command:

```text
kubectl get build -o json >project-name_build-configurations.json
```
{: pre}

If you want to export the configuration of a single build, use the following `kubectl` command:

```text
kubectl get build <build-name> -o json >project-name-build-name_build-configuration.json
```
{: pre}

### Exporting `build run` configuration
{: #exporting-buid-run}

To export the configuration of all buildruns in your project, run the following `kubectl` command:

```text
kubectl get buildrun -o json >project-name_buildrun-configurations.json
```
{: pre}

If you want to export the configuration of a single buildrun, use the following `kubectl` command:

```text
kubectl get buildrun <buildrun-name> -o json >project-name-buildrun-name_buildrun-configuration.json
```
{: pre}

### Exporting `configmap` configuration
{: #exporting-configmap}

To export the content of all configmaps in your project, run the following `kubectl` command:

```text
kubectl get configmap -o json >project-name_configmaps.json
```
{: pre}

If you want to export the content of a single configmap, use the following `kubectl` command:

```text
kubectl get configmap <configmap-name> -o json >project-name-configmap-name_configmap.json
```
{: pre}

### Exporting `secret` configuration
{: #exporting-secret}

Do not export the contents of secrets to a file on a persistent storage.
{: note}

To export the content of all secrets in your project, run the following `kubectl` command:

```text
kubectl get secret -o json >project-name_secrets.json
```
{: pre}

If you want to export the content of a single secret, use the following `kubectl` command:

```text
kubectl get secret <secret-name> -o json >project-name-secret-name_secret.json
```
{: pre}

Values stored in {{site.data.keyword.codeengineshort}} secrets are usually copies of values managed in other systems, like {{site.data.keyword.secrets-manager_full_notm}}. Therefore, most of the time exporting secrets is not required. If you still require to export secrets from {{site.data.keyword.codeengineshort}}, you should choose exporting single secrets over exporting all secrets to avoid unintentional disclosure of sensitive information.
{: note}

### Exporting `domain mapping` configuration
{: #exporting-domain-mapping}

To export the configuration of all domain mappings in your project, run the following `kubectl` command:

```text
kubectl get domainmapping -o json >project-name_domainmappings.json
```
{: pre}

If you want to export the configuration of a single domain mapping, use the following `kubectl` command:

```text
kubectl get domainmapping <domainmapping-name> -o json >project-name-domainmapping-name_domainmapping.json
```
{: pre}

### Exporting `{{site.data.keyword.cos_full_notm}} event subscription` configuration
{: #exporting-cos-event-subscription}

To export the configuration of all {{site.data.keyword.cos_full_notm}} event subscriptions in your project, run the following `kubectl` command:

```text
kubectl get cossource -o json >project-name_cos-event-subscriptions.json
```
{: pre}

If you want to export the configuration of a single {{site.data.keyword.cos_full_notm}} event subscription, use the following `kubectl` command:

```text
kubectl get cossource <cos-event-subscription-name> -o json >project-name-cos-event-subscription-name_cos-event-subscription.json
```
{: pre}

### Exporting `cron event subscription` configuration
{: #exporting-cron-event-subscription}

To export the configuration of all `cron` event subscriptions in your project, run the following `kubectl` command:

```text
kubectl get pingsource -o json >project-name_cron-event-subscriptions.json
```
{: pre}

If you want to export the configuration of a single `cron` event subscription, use the following `kubectl` command:

```text
kubectl get pingsource <cron-event-subscription-name> -o json >project-name-cron-event-subscription-name_cron-event-subscription.json
```
{: pre}

### Exporting `Kafka event subscription` configuration
{: #exporting-kafka-event-subscription}

To export the configuration of all Kafka event subscriptions in your project, run the following `kubectl` command:

```text
kubectl get kafkasource -o json >project-name_kafka-event-subscriptions.json
```
{: pre}

If you want to export the configuration of a single Kafka event subscription, use the following `kubectl` command:

```text
kubectl get kafkasource <cron-event-subscription-name> -o json >project-name-kafka-event-subscription-name_kafka-event-subscription.json
```
{: pre}

### Exporting `function` configuration
{: #exporting-function}

To export the configuration of all functions in your project, run the following `kubectl` command:

```text
kubectl get function -o json >project-name_functions.json
```
{: pre}

If you want to export the configuration of a single function, use the following `kubectl` command:

```text
kubectl get function <function-name> -o json >project-name-function-name_function.json
```
{: pre}

### Exporting `job` configuration
{: #exporting-job}

To export the configuration of all jobs in your project, run the following `kubectl` command:

```text
kubectl get jobdefinition -o json >project-name_jobs.json
```
{: pre}

If you want to export the configuration of a single job, use the following `kubectl` command:

```text
kubectl get jobdefinition <function-name> -o json >project-name-job-name_job.json
```
{: pre}

### Exporting `job run` configuration
{: #exporting-job-run}

To export the configuration of all jobruns in your project, run the following `kubectl` command:

```text
kubectl get jobrun -o json >project-name_jobruns.json
```
{: pre}

If you want to export the configuration of a single jobrun, use the following `kubectl` command:

```text
kubectl get jobrun <function-name> -o json >project-name-jobrun-name_jobrun.json
```
{: pre}

## Exported data formats
{: #data-portability-data-formats}



{{site.data.keyword.codeengineshort}} supports the following data format and schema of the exported data, configuration, and application:
* JSON

**Example:** Exporting a ConfigMap with name `export-sample` and format `JSON` results in the following JSON output:

Command:
`kubectl get configmap export-sample -o json`

Output:
```text
{
    "apiVersion": "v1",
    "data": {
        "APP_OWNER": "John Doe",
        "NUM_DATASETS": "24",
        "foo": "bar"
    },
    "kind": "ConfigMap",
    "metadata": {
        "creationTimestamp": "2024-10-15T09:12:47Z",
        "name": "export-sample",
        "namespace": "7yuw2furi55",
        "resourceVersion": "9162003517",
        "uid": "12962640-a294-4e1f-a006-a875f119df43"
    }
}
```
{: codeblock}

All commands that use the `kubectl` command with the `-o json` option, produce a JSON output that is compatible with Kubernetes. The JSON produced by other commands, like `ibmcloud resource` or `ibmcloud code-engine` cannot be assumed to be compatible with Kubernetes as is.


{{site.data.keyword.codeengineshort}} doesn't support the export of the following data format and schema of the exported data, configuration, and application:
* YAML

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [{{site.data.keyword.cloud_notm}} Service Agreement](https://www.ibm.com/terms/?id=Z126-6304_WS).
