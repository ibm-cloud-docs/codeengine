---

copyright:
  years: 2020, 2022
lastupdated: "2022-08-18"

keywords: release notes for code engine, updates in code engine, what's new in code engine, document changes in code engine, updates, release notes

subcollection: codeengine

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes 
{: #codeengine-relnotes}

Use the release notes to learn about the latest changes to {{site.data.keyword.codeenginefull}} that are grouped by month. 
{: shortdesc}

## August 2022
{: #codeengine-aug22}

Review the release notes for August 2022.
{: shortdesc}

### 18 August 2022
{: #codeengine-aug1822}
{: release-note}

CLI version 1.39.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for working with service bindings from the console 
:   - See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding)
    - See [Binding a service instance to a Code Engine app or job](/docs/codeengine?topic=codeengine-bind-services)

Updated the default maximum execution time for jobs 
:   The default maximum execution time for jobs is revised to 24 hours. See [Job defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_job).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 4 August 2022
{: #codeengine-aug0422}
{: release-note}

CLI version 1.38.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

New tutorial
:   See [Building applications that store information in IBM Cloudant](/docs/codeengine?topic=codeengine-tutorial-cloudant-local).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## July 2022
{: #codeengine-jul22}

Review the release notes for July 2022.
{: shortdesc}

### 29 July 2022
{: #codeengine-jul2922}
{: release-note}

CLI version 1.38.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated CPU and memory limits and maximums for jobs and apps
:   {{site.data.keyword.codeengineshort}} adds support for new CPU and memory ratio combinations. Also, this version adds support for increased default maximums for CPU, memory, and ephemeral-storage for {{site.data.keyword.codeengineshort}} apps and jobs.
    * See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
    * See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

Added support for jobs that can run indefinitely
:   See [Creating and running a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon)

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 21 July 2022
{: #codeengine-jul2122}
{: release-note}

CLI version 1.38.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 15 July 2022
{: #codeengine-jul1522}
{: release-note}

CLI version 1.37.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 8 July 2022
{: #codeengine-jul722}
{: release-note}

New! Context-based restrictions for {{site.data.keyword.codeengineshort}}
:   See [Protecting {{site.data.keyword.codeengineshort}} resources with context-based restrictions](/docs/codeengine?topic=codeengine-cbr).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## June 2022
{: #codeengine-jun22}

Review the release notes for June 2022.
{: shortdesc}

### 30 June 2022
{: #codeengine-jun3022}
{: release-note}

New! Tutorial for how to subscribe to Kafka events with {{site.data.keyword.codeengineshort}}
:   See [Subscribing to Kafka events](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial).

### 24 June 2022
{: #codeengine-jun2422}
{: release-note}

CLI version 1.36.0 released
:   This CLI version adds support for Kafka event subscriptions. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for Kafka event subscriptions with the console and CLI
:   See [Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer).


### 16 June 2022
{: #codeengine-jun1622}
{: release-note}

CLI version 1.35.0 released
:   - See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).
    - See [Supported environments for Code Engine CLI](/docs/codeengine?topic=codeengine-install-cli#cli-env).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 09 June 2022
{: #codeengine-jun0922}
{: release-note}

CLI version 1.34.0 released
:   This version of the CLI updates the **`buildrun submit`** command so that the `--build` option is no longer required. This update means that you can now use this single command to build a container image from a Git repository or local source without having to reference a build configuration. 
    * See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).
    * See [Building a container image with stand-alone build commands (CLI)](/docs/codeengine?topic=codeengine-build-standalone).



### 02 June 2022
{: #codeengine-jun0222}
{: release-note}

CLI version 1.33.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated available metrics for monitoring {{site.data.keyword.codeengineshort}}
:   No longer providing the following metrics:
    * `ibm_codeengine_application_request_duration_milliseconds_sum`
    * `ibm_codeengine_application_request_duration_milliseconds_count`
    * `ibm_codeengine_application_per_namespace_service_count`

    See [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor).

Revised and improved topic organization of {{site.data.keyword.codeengineshort}} limits and quotas
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).


## May 2022
{: #codeengine-may22}

Review the release notes for May 2022.
{: shortdesc}

### 26 May 2022
{: #codeengine-may2622}
{: release-note}

CLI version 1.33.0 released
:   This version of the CLI updates the **`build create`** command so that the `--image` and `--registry-secret` options are no longer required. This update means that you can choose to let {{site.data.keyword.codeengineshort}} take care of building the image for you from your source and storing the image in {{site.data.keyword.registrylong_notm}} with automatic access, or you can choose to specify registry details with a registry access secret for your build output. 
    * See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).
    * See [Building a container image](/docs/codeengine?topic=codeengine-build-image).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 19 May 2022
{: #codeengine-may1922}
{: release-note}

CLI version 1.32.0 released
:   - See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).
    - See [Supported environments for Code Engine CLI](/docs/codeengine?topic=codeengine-install-cli#cli-env).

Added more information about access authorities for image registries
:   - See [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry).


### 12 May 2022
{: #codeengine-may1222}
{: release-note}

CLI version 1.31.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 05 May 2022
{: #codeengine-may0522}
{: release-note}

CLI version 1.31.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added new FAQ topics to Migrating Cloud Foundry information
:   - [Can I use a custom URL with Code Engine?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#customurl)
    - [Why are my apps slow to respond?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_response)

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## April 2022
{: #codeengine-apr22}

Review the release notes for April 2022.
{: shortdesc}

### 29 April 2022
{: #codeengine-apr2922}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 27 April 2022
{: #codeengine-apr2722}
{: release-note}

New! Deploying apps and running jobs with {{site.data.keyword.codeengineshort}} is even easier!
:   With {{site.data.keyword.codeengineshort}}, you can now go from source code to a running app or a configured job with a **single** command. The **`app create`** command automatically runs the container build and deploys your app in a single step. You don't even need to know about building container images or working with registries. Just let {{site.data.keyword.codeengineshort}} handle all these processes for you.
    * If you are familiar with "push source code" platforms, such as Cloud Foundry, start by exploring the tutorial [Deploying Cloud Foundry applications in Code Engine: Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial). 
    * If you are familiar with {{site.data.keyword.codeengineshort}}, see [Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code), [Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code), [Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code), and [Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code).

CLI version 1.30.0 released
:   This version of the CLI supports deploying apps and configuring jobs from local or repository source code with a **single** command. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 21 April 2022
{: #codeengine-apr2122}
{: release-note}

CLI version 1.29.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 14 April 2022
{: #codeengine-apr1422}
{: release-note}

CLI version 1.29.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 April 2022
{: #codeengine-apr1222}
{: release-note}

CLI version 1.29.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

New! Tutorial for creating a serverless web application with {{site.data.keyword.codeengineshort}}
:   See [Serverless web application and API with {{site.data.keyword.codeengineshort}} Tutorial](/docs/solution-tutorials?topic=solution-tutorials-serverless-webapp).

### 7 April 2022
{: #codeengine-apr0722}
{: release-note}

CLI version 1.29.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 1 April 2022
{: #codeengine-apr0122}
{: release-note}

New! Tutorials for migrating Cloud Foundry apps to {{site.data.keyword.codeengineshort}}
:    [Deploying Cloud Foundry applications in {{site.data.keyword.codeengineshort}}: Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial)
:    [Migrating your service binding](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind)

CLI version 1.29.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## March 2022
{: #codeengine-mar22}

Review the release notes for March 2022.
{: shortdesc}

### 31 March 2022
{: #codeengine-mar3122}
{: release-note}

Review the release notes for 31 March 2022.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: Brazil Sao Paulo (`br-sao`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

### 23 March 2022
{: #codeengine-mar2322}
{: release-note}

Review the release notes for 23 March 2022.
{: shortdesc}

CLI version 1.28.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 18 March 2022
{: #codeengine-mar1822}
{: release-note}

Review the release notes for 18 March 2022.
{: shortdesc}

CLI version 1.28.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions). 

Added information about registry access secret types
:   Types include {{site.data.keyword.codeengineshort}} managed secrets and user managed secrets. If no credentials are needed to access the registry, then the access is `None`.  See [Types of registry access secrets](/docs/codeengine?topic=codeengine-add-registry#types-registryaccesssecrets).

Added information about setting max-scale = 0
:   Max scale is the maximum number of instances that can be used for an app. If you set this value to 0, the application scales as needed and is limited only by the resource quota for the project of your app. See [Scaling boundaries](/docs/codeengine?topic=codeengine-app-scale#app-scale-boundaries).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 04 March 2022
{: #codeengine-mar0422}
{: release-note}

Review the release notes for 04 March 2022.
{: shortdesc}

CLI version 1.27.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions). 

### 02 March 2022
{: #codeengine-mar0222}
{: release-note}

Review the release notes for 02 March 2022.
{: shortdesc}

CLI version 1.27.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).  

Improved service binding implementation 
:   CLI 1.27.0 introduces an improved service binding implementation, which is used for all new service bindings. Existing applications and jobs continue to function normally. However, if you want to bind an additional service instance to an app or job, you must first delete any existing service bindings from that app or job. You can then re-create those service bindings with the improved service binding implementation. See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).

## February 2022
{: #codeengine-feb22}

Review the release notes for February 2022.
{: shortdesc}

### 24 February 2022
{: #codeengine-feb2422}
{: release-note}

Review the release notes for 24 February 2022.
{: shortdesc}

CLI version 1.26.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 22 February 2022
{: #codeengine-feb2222}
{: release-note}

Review the release notes for 22 February 2022.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: US East (`us-east`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

### 17 February 2022
{: #codeengine-feb1722}
{: release-note}

Review the release notes for 17 February 2022.
{: shortdesc}

CLI version 1.26.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 10 February 2022
{: #codeengine-feb1022}
{: release-note}

Review the release notes for 10 February 2022.
{: shortdesc}

CLI version 1.25.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 03 February 2022
{: #codeengine-feb0322}
{: release-note}

Review the release notes for 03 February 2022.
{: shortdesc}

CLI version 1.25.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## January 2022
{: #codeengine-jan22}

Review the release notes for January 2022.
{: shortdesc}

### 27 January 2022
{: #codeengine-jan2722}
{: release-note}

Review the release notes for 27 January 2022.
{: shortdesc}

CLI version 1.25.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added more information for troubleshooting jobs when job runs do not complete 
:   See [Why is my job not completing?](/docs/codeengine?topic=codeengine-ts-jobrun-doesnotcomplete) 

Added information about considerations when using SSH keys for accessing your source repository
:   See [Choosing an SSH key for code repository](/docs/codeengine?topic=codeengine-code-repositories#choose-ssh-key).

### 20 January 2022
{: #codeengine-jan2022}
{: release-note}

Review the release notes for 20 January 2022.
{: shortdesc}

CLI version 1.25.0 released
:   This CLI version adds support for creating a build that pulls source from a local directory. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added information about considerations for HTTP handling with {{site.data.keyword.codeengineshort}} apps and jobs
:   See [Considerations for HTTP handling](/docs/codeengine?topic=codeengine-application-workloads#considerationshttphandlingapp). 

### 14 January 2022
{: #codeengine-jan1422}
{: release-note}

Review the release notes for 14 January 2022
{: shortdesc}

Added clarification for use of direct endpoints when using private networking with services such as {{site.data.keyword.cos_full_notm}}
:   See [How can I access a bound service instance from an app or job?](/docs/codeengine?topic=codeengine-service-binding#access-bound-service) and [Setting up the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#setup-cosevent-producer).

### 13 January 2022
{: #codeengine-jan1322}
{: release-note}

Review the release notes for 13 January 2022.
{: shortdesc}

CLI version 1.24.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 January 2022
{: #codeengine-jan1222}
{: release-note}

Review the release notes for 12 January 2022.
{: shortdesc}

Sample images are stored in {{site.data.keyword.registrylong}}
:   {{site.data.keyword.codeengineshort}} sample images that are built from the [{{site.data.keyword.codeenginefull_notm}} samples repository on GitHub](https://github.com/IBM/CodeEngine){: external} are available in {{site.data.keyword.registrylong}} in the public `icr.io/codeengine` namespace.

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## December 2021
{: #codeengine-dec21}

Review the release notes for December 2021.
{: shortdesc}

### 15 December 2021
{: #codeengine-dec1521}
{: release-note}

Review the release notes for 15 December 2021.
{: shortdesc}

CLI version 1.23.3 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 December 2021
{: #codeengine-dec1421}
{: release-note}

Review the release notes for 14 December 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: Australia Sydney (`au-syd`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

### 08 December 2021
{: #codeengine-dec0821}
{: release-note}

Review the release notes for 08 December 2021.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports monitoring security and compliance with {{site.data.keyword.compliance_long}}.
:   Added support for monitoring security and compliance posture with {{site.data.keyword.codeengineshort}}. See [Monitoring security and compliance posture with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-manage-security-compliance#monitor-security-compliance).

### 06 December 2021
{: #codeengine-dec0621}
{: release-note}

Review the release notes for 06 December 2021.
{: shortdesc}

{{site.data.keyword.cos_full_notm}} subscriptions
:   Added support for {{site.data.keyword.cos_full_notm}} eventing subscriptions from the {{site.data.keyword.codeengineshort}} console. See [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 01 December 2021
{: #codeengine-dec0121}
{: release-note}

Review the release notes for 01 December 2021.
{: shortdesc}

CLI version 1.23.2 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## November 2021
{: #codeengine-nov21}

Review the release notes for November 2021.
{: shortdesc}

### 19 November 2021
{: #codeengine-nov1921}
{: release-note}

Review the release notes for 19 November 2021.
{: shortdesc}

CLI version 1.23.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 November 2021
{: #codeengine-nov1621}
{: release-note}

Review the release notes for 16 November 2021.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports virtual private endpoints.
:   Added support for integration of {{site.data.keyword.codeengineshort}} projects with {{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for Virtual Private Cloud (VPC). You can use this support to connect from your VPC network to {{site.data.keyword.codeengineshort}} applications. See [Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe) and [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).

CLI version 1.23.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 04 November 2021
{: #codeengine-nov0421}
{: release-note}

Review the release notes for 04 November 2021.
{: shortdesc}

CLI version 1.22.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.codeengineshort}} is integrated with {{site.data.keyword.compliance_long}}.
:   Added support for governing information {{site.data.keyword.codeengineshort}} resource configuration with {{site.data.keyword.compliance_long}}. See [Managing security and compliance with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-manage-security-compliance).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


## October 2021
{: #codeengine-oct21}

Review the release notes for October 2021.
{: shortdesc}

### 28 October 2021
{: #codeengine-oct2821}
{: release-note}

Review the release notes for 28 October 2021.
{: shortdesc}

CLI version 1.21.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.cos_full_notm}} subscriptions
:  Removed restriction for {{site.data.keyword.codeengineshort}} subscriptions for {{site.data.keyword.cos_short}} event producers in the `ca-tor` region. {{site.data.keyword.cos_short}} event producers are supported in these [regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Added Python as a supported language for builds that use the Cloud Native Buildpacks strategy. 
:   See [Cloud Native Buildpacks](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).




### 21 October 2021
{: #codeengine-oct2121}
{: release-note}

Review the release notes for 21 October 2021.
{: shortdesc}

CLI version 1.21.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 15 October 2021
{: #codeengine-oct1521}
{: release-note}

Review the release notes for 15 October 2021.
{: shortdesc}

Added support for deploying apps with project-only endpoints.  
:   App create and update workflows from the console support `Project-only` visibility for app endpoints. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local). See [Deploying your app with a project-only endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly).

Added information about creating custom dashboards to monitor {{site.data.keyword.codeengineshort}} workloads.
:   See [Creating custom dashboards to monitor {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor-custom).

### 07 October 2021
{: #codeengine-oct0721}
{: release-note}

Review the release notes for 07 October 2021.
{: shortdesc}

Creating builds no longer requires a value for the source branch.  
:   If the value is not provided and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically determines the branch name. See [Building a container image](/docs/codeengine?topic=codeengine-build-image).

CLI version 1.20.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 04 October 2021
{: #codeengine-oct0421}
{: release-note}

Review the release notes for 04 October 2021.
{: shortdesc}

Revised and improved the application configuration pages in the console. 
:   See [Updating your app](/docs/codeengine?topic=codeengine-update-app).

CLI version 1.20.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## September 2021
{: #codeengine-sep21}

Review the release notes for September 2021.
{: shortdesc}

### 23 September 2021
{: #codeengine-sep2321}
{: release-note}

Review the release notes for 23 September 2021.
{: shortdesc}

CLI version 1.19.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 September 2021
{: #codeengine-sep1621}
{: release-note}

Review the release notes for 16 September 2021.
{: shortdesc}

CLI version 1.19.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated the Dockerfile build strategy to use the BuildKit tool. 
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 9 September 2021
{: #codeengine-sep0921}
{: release-note}

Review the release notes for 9 September 2021.
{: shortdesc}

CLI version 1.18.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated information about the roles that are required for using Kubernetes and Knative with {{site.data.keyword.codeengineshort}}. 
:   See [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes) and [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

### 2 September 2021
{: #codeengine-sep0221}
{: release-note}

Review the release notes for 2 September 2021.
{: shortdesc}

Added support for build logs in the {{site.data.keyword.codeengineshort}} console.
:   See [Viewing build logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-build-ui).

Updated information about `reclamation` commands.
:   See [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project).</li></ul>|

### 1 September 2021
{: #codeengine-sep0121}
{: release-note}

Review the release notes for 1 September 2021.
{: shortdesc}

CLI version 1.17.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for Periodic timer (cron) event producers in the {{site.data.keyword.codeengineshort}} console. 
:   See [Working with the Periodic timer (cron) event producer](/docs/codeengine?topic=codeengine-subscribe-cron).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## August 2021
{: #codeengine-aug21}

Review the release notes for August 2021.
{: shortdesc}

### 24 August 2021
{: #codeengine-aug2421}
{: release-note}

Review the release notes for 24 August 2021.
{: shortdesc}

CLI version 1.16.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 19 August 2021
{: #codeengine-aug1921}
{: release-note}

Review the release notes for 19 August 2021.
{: shortdesc}

CLI version 1.16.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Secrets
:   Updated information about viewing a list of all secrets, which includes secrets that are generated by {{site.data.keyword.codeengineshort}}, or viewing a list of secrets that are user-generated. See [Creating secrets from the console](/docs/codeengine?topic=codeengine-configmap-secret#secret-create-ui).

Updated information about headers and environment variables when using subscriptions.
:   See [Header and body information for {{site.data.keyword.cos_full_notm}} events delivered to applications](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos), [Environment variables for {{site.data.keyword.cos_full_notm}} events delivered to jobs](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-envir-variables-cos), [Header and body information for cron events delivered to applications](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron), and [Environment variables for cron events delivered to jobs](/docs/codeengine?topic=codeengine-subscribe-cron#sub-envir-variables-cron).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 16 August 2021
{: #codeengine-aug1621}
{: release-note}

Review the release notes for 16 August 2021.
{: shortdesc}

CLI version 1.15.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Troubleshooting subscriptions
:   Added information about troubleshooting subscriptions when a subscription shows errors when it delivers events. See [Why does my subscription show errors when it delivers events?](/docs/codeengine?topic=codeengine-ts-subscription-deliveryerrors)

Subscriptions for {{site.data.keyword.cos_full_notm}} event producers are not available in the Canada Toronto (`ca-tor`) region.
:   See [Working with the {{site.data.keyword.cos_short}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 6 August 2021
{: #codeengine-aug0621}
{: release-note}

Review the release notes for 6 August 2021.
{: shortdesc}

CLI version 1.14.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Private repositories
:   Updated information about running {{site.data.keyword.codeengineshort}} builds that use source in private repos. See [Building a container image](/docs/codeengine?topic=codeengine-build-image).

### 5 August 2021
{: #codeengine-aug0521}
{: release-note}

Review the release notes for 5 August 2021.
{: shortdesc}

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## July 2021
{: #codeengine-jul21}

Review the release notes for July 2021.
{: shortdesc}

### 30 July 2021
{: #codeengine-jul3021}
{: release-note}

Review the release notes for 30 July 2021.
{: shortdesc}

CLI version 1.13.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 29 July 2021
{: #codeengine-jul2921}
{: release-note}

Review the release notes for 29 July 2021.
{: shortdesc}

Deleting projects
:   Added support in the console for restoring projects that are soft deleted and for permanently deleting projects. See [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project) and [Permanently deleting projects](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 27 July 2021
{: #codeengine-jul2721}
{: release-note}

Review the release notes for 27 July 2021.
{: shortdesc}

CLI version 1.12.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added overview topics for deploying apps and running jobs.
:   See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads) and [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 20 July 2021
{: #codeengine-jul2021}
{: release-note}

Review the release notes for 20 July 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: Canada Toronto (`ca-tor`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

### 15 July 2021
{: #codeengine-jul1521}
{: release-note}

Review the release notes for 15 July 2021.
{: shortdesc}

CLI version 1.11.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Subscription ping limits
:   Added information about limits for subscription ping data. See [Subscription ping limits](/docs/codeengine?topic=codeengine-limits#subscription-cron-limit).

Applications that use WebSockets
:   Added information about apps that use WebSockets need to reconnect before the session expires. See [Do Code Engine apps support WebSockets?](/docs/codeengine?topic=codeengine-faqs#app-websockets)

Updated versions for buildpacks. 
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 7 July 2021
{: #codeengine-jul0721}
{: release-note}

Review the release notes for 7 July 2021.
{: shortdesc}

Environment variables
:   Updated information about automatically injected environment variables for {{site.data.keyword.codeengineshort}} apps and jobs. See [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

Troubleshooting overview topics
:   Added troubleshooting overview topics for apps, builds, jobs, projects, and subscriptions. See [Debugging apps](/docs/codeengine?topic=codeengine-troubleshoot-apps), [Debugging builds](/docs/codeengine?topic=codeengine-troubleshoot-build), [Debugging jobs](/docs/codeengine?topic=codeengine-troubleshoot-job), [Debugging projects](/docs/codeengine?topic=codeengine-troubleshoot-project), [Debugging subscriptions](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions).

{{site.data.keyword.cos_short}} buckets
:   {{site.data.keyword.codeengineshort}} supports {{site.data.keyword.cos_short}} buckets that are located in the `jp-osa` region. See [Set up the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#setup-cosevent-producer).

## June 2021
{: #codeengine-jun21}

Review the release notes for June 2021.
{: shortdesc}

### 30 June 2021
{: #codeengine-jun3021}
{: release-note}

Review the release notes for 30 June 2021.
{: shortdesc}

Iter8 tutorial
:   Added a tutorial that demonstrates how to validate your {{site.data.keyword.codeengineshort}} application with an open source tool called Iter8. See [Validating your application code and latency with Iter8](/docs/codeengine?topic=codeengine-slovalidationtut).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 29 June 2021
{: #codeengine-jun2921}
{: release-note}

Review the release notes for 29 June 2021.
{: shortdesc}

Application revisions
:   Introduced a behavior change for app revisions. {{site.data.keyword.codeengineshort}} retains only the latest inactive revision of your application in addition to your active app revision. Older revisions are deleted. See [Updating apps](/docs/codeengine?topic=codeengine-update-app).

Job runs that are created by subscriptions
:   Updated information that job runs that are created by subscriptions are deleted after 10 minutes. See [Running a job](/docs/codeengine?topic=codeengine-run-job).

### 23 June 2021
{: #codeengine-jun2321}
{: release-note}

Review the release notes for 23 June 2021.
{: shortdesc}

CLI version 1.10.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated app and app revision quotas for projects.
:   The quota is revised to 20 apps per project and 60 revisions for all apps per project. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits#project_quotas).

Added basic troubleshooting information.
:   See [Troubleshooting overview](/docs/codeengine?topic=codeengine-troubleshooting_over).

{{site.data.keyword.cloud_notm}} and third-party integrations
:   Find out what {{site.data.keyword.cloud_notm}} and third-party integrations are supported by {{site.data.keyword.codeengineshort}}. See [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/codeengine?topic=codeengine-supported-integrations).

Added information about security and {{site.data.keyword.codeengineshort}}. 
:   See [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 16 June 2021
{: #codeengine-jun1621}
{: release-note}

Review the release notes for 16 June 2021.
{: shortdesc}

CLI version 1.9.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Build size
:   Updated the size for `xlarge` builds to 4 CPU and 16 GB. See [Determine the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size).

Configmaps and secrets
:   Updated information about referencing existing and not-yet-created configmaps and secrets with the CLI. See [Referencing configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap-secret#configmap-ref-cli) and [Referencing secrets with the CLI](/docs/codeengine?topic=codeengine-configmap-secret#secret-ref-cli).

Added information about updating jobs.
:   See [Updating a job](/docs/codeengine?topic=codeengine-update-job).

### 10 June 2021
{: #codeengine-jun1021}
{: release-note}

Review the release notes for 10 June 2021.
{: shortdesc}

Important: Introduced a breaking change with {{site.data.keyword.codeengineshort}} memory and CPU combinations.
:   With this version, applications and batch jobs are required to use a specific set of memory and CPU combinations for resource allocations. Existing running workloads are not impacted, but new and updated workloads are required to follow these requirements. For more information, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

CLI version 1.8.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Running job without job configuration
:   Updated information about running batch jobs to include running a job with the CLI without first defining a job configuration. See [Running a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withoutjobconfig).

Added support for private repositories from the console.
:   See [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Subscription support for jobs is generally available.
:   See [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events), [Working with the Ping event producer](/docs/codeengine?topic=codeengine-subscribe-cron), and [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

### 8 June 2021
{: #codeengine-jun0821}
{: release-note}

Review the release notes for 8 June 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: Asia Pacific Osaka (`jp-osa`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

### 3 June 2021
{: #codeengine-jun0321}
{: release-note}

Review the release notes for 3 June 2021.
{: shortdesc}

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Deleting data
:   Added information about hard and soft deletes of data in {{site.data.keyword.codeengineshort}} projects. See [Deleting your data in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-mng-data#data-delete).

## May 2021
{: #codeengine-may21}

Review the release notes for May 2021.
{: shortdesc}

### 27 May 2021
{: #codeengine-may2721}
{: release-note}

Review the release notes for 27 May 2021.
{: shortdesc}

CLI version 1.7.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated information about supported {{site.data.keyword.cos_full_notm}} buckets for subscriptions.
:   See [Set up the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#setup-cosevent-producer).

Added information about specifying the `--path` option when you create a subscription to an application.
:   See [Subscribing to Ping events for an app](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) and [Creating an {{site.data.keyword.cos_full_notm}} subscription for an application](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).

Updated information about accessing container registries.
:   See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

Added information about working with Kubernetes and {{site.data.keyword.codeengineshort}}.
:   See [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes).

### 18 May 2021
{: #codeengine-may1821}
{: release-note}

Review the release notes for 18 May 2021.
{: shortdesc}

Added information about working with environment variables in {{site.data.keyword.codeengineshort}}.
:   See [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

Working with secrets and configmaps
:   Added information about working with secrets and configmaps with the console and updated information about working with secrets and configmaps with the CLI. See [Setting up and using secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret).

CLI version 1.6.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 10 May 2021
{: #codeengine-may1021}
{: release-note}

Review the release notes for 10 May 2021.
{: shortdesc}

CLI version 1.5.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 7 May 2021
{: #codeengine-may0721}
{: release-note}

Review the release notes for 7 May 2021.
{: shortdesc}

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 4 May 2021
{: #codeengine-may0421}
{: release-note}

Review the release notes for 4 May 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: EU Great Britain (`eu-gb`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

## April 2021
{: #codeengine-apr21}

Review the release notes for April 2021.
{: shortdesc}

### 29 April 2021
{: #codeengine-apr2921}
{: release-note}

Review the release notes for 29 April 2021.
{: shortdesc}

Added metrics for `jobruns` to information about monitoring in {{site.data.keyword.codeengineshort}}.
:   See [Monitoring for {{site.data.keyword.codeengineshort}} - Total number of `jobruns`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_jobruns).

CLI version 1.4.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 21 April 2021
{: #codeengine-apr2121}
{: release-note}

Review the release notes for 21 April 2021.
{: shortdesc}

`CloudEvents` specification
:   Added information about support for `CloudEvents` specification. See [Can I use other CloudEvents specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)

CLI version 1.3.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 April 2021
{: #codeengine-apr1421}
{: release-note}

Review the release notes for 14 April 2021.
{: shortdesc}

New! Subscription support for jobs as a beta function.
:   Revised subscription information to describe how your {{site.data.keyword.codeengineshort}} applications or jobs can receive events by subscribing to event producers. See [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events), [Working with the Ping event producer](/docs/codeengine?topic=codeengine-subscribe-cron), and [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

Project limits
:   Updated project limit information. See [Limits and quotas for project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

Project deletions
:   Updated information about project deletions and how these deletions can affect the maximum number of projects in a region. See [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).
  
CLI version 1.2.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 8 April 2021
{: #codeengine-apr0821}
{: release-note}

Review the release notes for 8 April 2021.
{: shortdesc}

Learning paths
:   Added curated {{site.data.keyword.codeengineshort}} learning path information to help guide you from planning to working with your deployments. See [Learning paths for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-learning-paths).

Pending reclamation
:   Updated information about how to discover deleted projects that are pending reclamation. See [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).

Environment variables
:   Updated information about automatically injected environment variables for {{site.data.keyword.codeengineshort}} apps and jobs. See [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

CLI version 1.1.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 1 April 2021
{: #codeengine-apr0121}
{: release-note}

Review the release notes for 1 April 2021.
{: shortdesc}

Added information about deploying apps across multiple regions that use a custom domain name.
:   See [Deploying an application across multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

CLI version 1.0.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


## March 2021
{: #codeengine-mar21}

Review the release notes for March 2021.
{: shortdesc}

### 31 March 2021
{: #codeengine-mar3121}
{: release-note}

Review the release notes for 31 March 2021.
{: shortdesc}

New! General availability of {{site.data.keyword.codeenginefull_notm}}
:   {{site.data.keyword.codeengineshort}} is now generally available. To get started, see [Getting started with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-getting-started).

CLI version 1.0.0 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 30 March 2021
{: #codeengine-mar3021}
{: release-note}

Review the release notes for 30 March 2021.
{: shortdesc}

Updated information about setting the `port` value when you deploy apps. 
:   See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Updated information about application scaling when apps connect to event producers. 
:   See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).


### 26 March 2021
{: #codeengine-mar2621}
{: release-note}

Review the release notes for 26 March 2021.
{: shortdesc}

CLI versions 0.6.2 and CLI 0.6.3 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added {{site.data.keyword.codeengineshort}} billing.
:   See [Pricing for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-pricing).

Updated CPU and memory limits for jobs and apps. 
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

### 25 March 2021
{: #codeengine-mar2521}
{: release-note}

Review the release notes for 25 March 2021.
{: shortdesc}

Added {{site.data.keyword.codeengineshort}} monitoring information.
:   See [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor).

Added information for determining CPU and memory combinations.
:   See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

{{site.data.keyword.codeengineshort}} Tutorial
:   See [{{site.data.keyword.codeengineshort}} Tutorial](/docs/solution-tutorials?topic=solution-tutorials-serverless-github-traffic-analytics).

### 23 March 2021
{: #codeengine-mar2321}
{: release-note}

Review the release notes for 23 March 2021.
{: shortdesc}

{{site.data.keyword.codeengineshort}} is supported in a new region: Asia Pacific (`jp-tok`). 
:   See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Added {{site.data.keyword.codeengineshort}} high availability and disaster recovery documentation. 
:   See [Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-ha-dr).

### 22 March 2021
{: #codeengine-mar2221}
{: release-note}

Review the release notes for 22 March 2021.
{: shortdesc}

CLI version 0.6.1 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 18 March 2021
{: #codeengine-mar1821}
{: release-note}

Review the release notes for 18 March 2021.
{: shortdesc}

CLI versions 0.6.0 and 0.5.25 released. 
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Automatically create registry access
:   From the console, {{site.data.keyword.codeengineshort}} can now automatically create registry access for {{site.data.keyword.registryshort}} instances that are in your account. When you push images, {{site.data.keyword.codeengineshort}} can even create a namespace in your container registry instance. See [Deploying an app that references an image in Container Registry with the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console), [Deploying your app from source code](/docs/codeengine?topic=codeengine-app-source-code), [Creating a job from images in Container Registry with the console](/docs/codeengine?topic=codeengine-create-job-crimage), and [Creating a job from source code](/docs/codeengine?topic=codeengine-run-job-source-code).

Added logging information for apps and jobs from the console.
:   See [Viewing logs from the console](/docs/codeengine?topic=codeengine-view-logs#view-logs-ui).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated limits for {{site.data.keyword.codeengineshort}}.
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Updated API CRD information for subscriptions and jobs.
:   See [Subscription CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-subscription) and [Job CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-batch).

Updated information for troubleshooting your builds.
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated service bind information.
:   See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).

### 9 March 2021
{: #codeengine-mar0921}
{: release-note}

Review the release notes for 9 March 2021.
{: shortdesc}

CLI version 0.5.21 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Project reclamation
:   Updated **`project delete`** command to include information about project reclamation. See [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).

### 4 March 2021
{: #codeengine-mar0421}
{: release-note}

Review the release notes for 4 March 2021.
{: shortdesc}

Added {{site.data.keyword.codeengineshort}} architecture and workload isolation documentation.
:   See [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).

Added HTTP headers and body information for subscriptions.
:   See [HTTP headers and body information for {{site.data.keyword.cos_full_notm}} events](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos) and [HTTP headers and body information for Ping events](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron).

System events
:   Added information about viewing system events to troubleshooting information for apps and jobs. See [system event information for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent) and [system event information for job runs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 2 March 2021
{: #codeengine-mar0221}
{: release-note}

Review the release notes for 2 March 2021.
{: shortdesc}

CLI version 0.5.20 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

New responsibilities for {{site.data.keyword.codeengineshort}} topic.
:   See [Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce).

## February 2021
{: #codeengine-feb21}

Review the release notes for February 2021.
{: shortdesc}

### 26 February 2021
{: #codeengine-feb2621}
{: release-note}

Review the release notes for 26 February 2021.
{: shortdesc}

Commands and arguments
:   Added information for defining commands and arguments for your apps and jobs. See [Defining commands and arguments for your {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-cmd-args).

Updated versions for buildpacks.
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 0.5.19 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added notices file.
:   See [{{site.data.keyword.codeengineshort}} notices](/docs/codeengine?topic=codeengine-notices).

### 23 February 2021
{: #codeengine-feb2321}
{: release-note}

Review the release notes for 23 February 2021.
{: shortdesc}

CLI version 0.5.18 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 February 2021
{: #codeengine-feb1621}
{: release-note}

Review the release notes for 16 February 2021.
{: shortdesc}

CLI version 0.5.17 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 February 2021
{: #codeengine-feb1221}
{: release-note}

Review the release notes for 12 February 2021.
{: shortdesc}

Added an {{site.data.keyword.cos_short}} subscription tutorial.
:   See [Tutorial: Subscribing to {{site.data.keyword.cos_short}} events](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial).

Added troubleshooting information for subscriptions. 
:   See [Troubleshooting tips for subscriptions](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions).

Added an FAQ for WebSocket support. 
:   See [Do {{site.data.keyword.codeengineshort}} apps support WebSockets](/docs/codeengine?topic=codeengine-faqs#app-websockets)?

Updated application limits.
:   See [Application limits](/docs/codeengine?topic=codeengine-limits#limits_application).

### 9 February 2021
{: #codeengine-feb0921}
{: release-note}

Review the release notes for 9 February 2021.
{: shortdesc}

CLI version 0.5.16 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added information about potentially reaching Docker rate limits. 
:   See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry) and [Planning your build](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 3 February 2021
{: #codeengine-feb0321}
{: release-note}

Review the release notes for 3 February 2021.
{: shortdesc}

Added planning for {{site.data.keyword.codeengineshort}} information. 
:   See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

Added information about working with configmaps and secrets as mounted files.
:   See [Referencing secrets and configmaps as mounted files](/docs/codeengine?topic=codeengine-secretcm-reference-mountedfiles).

Updated FAQ to add information about differences between {{site.data.keyword.codeengineshort}} builds and Docker builds. 
:   See [What is the difference between a Docker build on my system and a build in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild)?

Added a tip for when you copy an entire Git repository and note about best practices for naming application directories. 
:   See [Dockerfile basics](/docs/codeengine?topic=codeengine-dockerfile#dockerfile-basics).

## January 2021
{: #codeengine-jan21}

Review the release notes for January 2021.
{: shortdesc}

### 29 January 2021
{: #codeengine-jan2921}
{: release-note}

Review the release notes for 29 January 2021.
{: shortdesc}

CLI version 0.5.15 released. 
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Environment variables
:   Added information about automatically injected environment variables for {{site.data.keyword.codeengineshort}} apps and jobs. See [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

Revised subscription topic. 
:   See [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events).

Ping subscription tutorial
:   Added a ping subscription tutorial. See [Tutorial: Subscribing to ping events](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial).

Getting support
:   Added information about reviewing forums such as Stack Overview. See [Getting support](/docs/codeengine?topic=codeengine-get-support).

### 21 January 2021
{: #codeengine-jan2121}
{: release-note}

Review the release notes for 21 January 2021.
{: shortdesc}

CLI version 0.5.14 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 20 January 2021
{: #codeengine-jan2021}
{: release-note}

Review the release notes for 20 January 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: EU Central (`eu-de`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Removed some beta limitations for Code Engine. 
:   From now on, projects, applications, and jobs do not expire after seven days. In addition, you are no longer limited to one project per region. See [Limits](/docs/codeengine?topic=codeengine-limits).

### 15 January 2021
{: #codeengine-jan1521}
{: release-note}

Review the release notes for 15 January 2021.
{: shortdesc}

Added a build tutorial.
:   See [Tutorial: Building applications by using buildpacks](/docs/codeengine?topic=codeengine-build-app-tutorial).

Take a terminology quiz. 
:   See [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology).

Added a sitemap of {{site.data.keyword.codeengineshort}} topics.
:   See [Sitemap for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-sitemap).

CLI version 0.5.13 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 January 2021
{: #codeengine-jan1221}
{: release-note}

Review the release notes for 12 January 2021.
{: shortdesc}

Updated information for troubleshooting your builds.
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

New Activity tracker information. 
:   See [Auditing events for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-at_events).

Updated build information.
:   See [Building a container image](/docs/codeengine?topic=codeengine-build-image).

Added API CRD information for subscriptions.
:   See [Subscription CRD methods](/docs/codeengine?topic=codeengine-api#api-crd-subscription).

Updated task information for jobs
:   See [creating jobs with images from {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-create-job-crimage) and [creating jobs with images from a private repository](/docs/codeengine?topic=codeengine-create-job-private).

CLI version 0.5.11 and 0.5.12 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 7 January 2021
{: #codeengine-jan0721}
{: release-note}

Review the release notes for 7 January 2021.
{: shortdesc}

Updated task information for applications
:   Updated information for [deploying apps with images from {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-deploy-app-crimage) and [deploying apps with images from a private repository](/docs/codeengine?topic=codeengine-deploy-app-private).

## December 2020
{: #codeengine-dec20}

Review the release notes for December 2020.
{: shortdesc}

### 17 December 2020
{: #codeengine-dec1720}
{: release-note}

Review the release notes for 17 December 2020.
{: shortdesc}

Updated information for troubleshooting your builds. 
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated versions for buildpacks. 
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated sizes for builds.
:   See [build sizes](/docs/codeengine?topic=codeengine-plan-build#build-size).

CLI version 0.5.8 and 0.5.9 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 December 2020
{: #codeengine-dec1420}
{: release-note}

Review the release notes for 14 December 2020.
{: shortdesc}

Learn more about scaling your applications. 
:   See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

CLI version 0.5.7 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 9 December 2020
{: #codeengine-dec0920}
{: release-note}

Review the release notes for 9 December 2020.
{: shortdesc}

Find Dockerfile build tips.
See [Writing a Dockerfile for Code Engine](/docs/codeengine?topic=codeengine-dockerfile).

Updated troubleshooting tips for builds. 
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated versions for buildpacks.
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 0.5.6 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 2 December 2020
{: #codeengine-dec0220}
{: release-note}

Review the release notes for 2 December 2020.
{: shortdesc}

CLI version 0.5.5 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## November 2020
{: #codeengine-nov20}

Review the release notes for November 2020.
{: shortdesc}

### 30 November 2020
{: #codeengine-nov3020}
{: release-note}

Review the release notes for 30 November 2020.
{: shortdesc}

Updated user access information. 
:   See [Managing user access](/docs/codeengine?topic=codeengine-iam).

### 20 November 2020
{: #codeengine-nov2020}
{: release-note}

Review the release notes for 20 November 2020.
{: shortdesc}

CLI version 0.5.3 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

New logging topic. 
:   See [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).

Tips for troubleshooting applications. 
:   See [Troubleshooting tips for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps).

### 12 November 2020
{: #codeengine-nov1220}
{: release-note}

Review the release notes for 12 November 2020.
{: shortdesc}

CLI version 0.4.2592 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 11 November 2020
{: #codeengine-nov1120}
{: release-note}

Review the release notes for 11 November 2020.
{: shortdesc}

CLI version 0.4.2577 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

SDK documentation published
:   See [SDK documentation](https://cloud.ibm.com/apidocs/codeengine){: external}.

## October 2020
{: #codeengine-oct20}

Review the release notes for October 2020.
{: shortdesc}

### 30 October 2020
{: #codeengine-oct3020}
{: release-note}

Review the release notes for 30 October 2020.
{: shortdesc}

CLI version 0.4.2493 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Lithops
:   You can run a {{site.data.keyword.codeengineshort}} job by using Lithops framework. See [Running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops).

### 23 October 2020
{: #codeengine-oct2320}
{: release-note}

Review the release notes for 23 October 2020.
{: shortdesc}

CLI version 0.4.2439 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Project selected for current context
:   When you create a project, it is automatically selected as the current context. See [Creating a project with the CLI](/docs/codeengine?topic=codeengine-manage-project#create-project-cli).

Updated runtimes for buildpacks.
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 19 October 2020
{: #codeengine-oct1920}
{: release-note}

Review the release notes for 19 October 2020.
{: shortdesc}

Troubleshooting build information
:   Updated troubleshooting build resolution information for [Ephemeral storage limit is reached](/docs/codeengine?topic=codeengine-ts-build-ephemeral-limit) and [Memory limit is reached](/docs/codeengine?topic=codeengine-ts-build-memory-limit) to use `build update` command.

### 15 October 2020
{: #codeengine-oct1520}
{: release-note}

Review the release notes for 15 October 2020.
{: shortdesc}

CLI version 0.4.2397 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 October 2020
{: #codeengine-oct1420}
{: release-note}

Review the release notes for 14 October 2020.
{: shortdesc}

New troubleshooting information. 
:   See [Troubleshooting jobs](/docs/codeengine?topic=codeengine-troubleshoot-job) and [Troubleshooting builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

### 6 October 2020
{: #codeengine-oct0620}
{: release-note}

Review the release notes for 6 October 2020.
{: shortdesc}

CLI version 0.4.2365 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 5 October 2020
{: #codeengine-oct0520}
{: release-note}

Review the release notes for 5 October 2020.
{: shortdesc}

CLI version 0.4.2335 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## September 2020
{: #codeengine-sep20}

Review the release notes for September 2020.
{: shortdesc}

### 28 September 2020
{: #codeengine-sep2820}
{: release-note}

Review the release notes for 28 September 2020.
{: shortdesc}

CLI version 0.4.2276 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 24 September 2020
{: #codeengine-sep2420}
{: release-note}

Review the release notes for 24 September 2020.
{: shortdesc}

New tutorial
:   Added [{{site.data.keyword.codeengineshort}} Tutorial](/docs/solution-tutorials?topic=solution-tutorials-text-analysis-code-engine){: external}.

### 21 September 2020
{: #codeengine-sep2120}
{: release-note}

Review the release notes for 21 September 2020.
{: shortdesc}

CLI version 0.4.2227 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated runtimes for buildpacks.
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 18 September 2020
{: #codeengine-sep1820}
{: release-note}

Review the release notes for 18 September 2020.
{: shortdesc}

CLI version 0.4.2217 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 September 2020
{: #codeengine-sep1620}
{: release-note}

Review the release notes for 16 September 2020.
{: shortdesc}

New! [{{site.data.keyword.codeenginefull_notm}} beta release](https://cloud.ibm.com/codeengine/overview)
:   With {{site.data.keyword.codeengineshort}}, you can,
    - [Build container images](/docs/codeengine?topic=codeengine-build-image) and deploy them in apps and jobs.
    - [Pull from private repositories](/docs/codeengine?topic=codeengine-code-repositories).
    - [Connect to private registries](/docs/codeengine?topic=codeengine-add-registry).
    - [Work with configmaps and secrets](/docs/codeengine?topic=codeengine-configmap-secret).
  
CLI version 0.4.2192 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 4 September 2020
{: #codeengine-sep0420}
{: release-note}

Review the release notes for 4 September 2020.
{: shortdesc}

Application logs
:   Added [viewing application logs](/docs/codeengine?topic=codeengine-view-logs#view-applog-cli) information.

### 2 September 2020
{: #codeengine-sep0220}
{: release-note}

Review the release notes for 2 September 2020.
{: shortdesc}

CLI version 0.3.1973 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.codeengineshort}} batch CRDs updated to `v1beta1`. 
:   See [Batch CRDs](/docs/codeengine?topic=codeengine-api#api-crd-batch).

## August 2020
{: #codeengine-aug20}

Review the release notes for August 2020.
{: shortdesc}

### 21 August 2020
{: #codeengine-aug2120}
{: release-note}

Review the release notes for 21 August 2020.
{: shortdesc}

CLI version 0.3.1802 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated example
:   Updated `ibmcom/hello` sample source in [Tutorial Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial).

Project quotas
:   Added project quotas to [Limits and quotas](/docs/codeengine?topic=codeengine-limits#project_quotas) topic.

### 17 August 2020
{: #codeengine-aug1720}
{: release-note}

Review the release notes for 17 August 2020.
{: shortdesc}

CLI version 0.3.1712 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Ephemeral storage limit
:   Added ephemeral storage limit to [apps](/docs/codeengine?topic=codeengine-limits#limits_application) and [jobs](/docs/codeengine?topic=codeengine-limits#limits_job).

### 14 August 2020
{: #codeengine-aug1420}
{: release-note}

Review the release notes for 14 August 2020.
{: shortdesc}

CLI version 0.3.1675 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 4 August 2020
{: #codeengine-aug0420}
{: release-note}

Review the release notes for 4 August 2020.
{: shortdesc}

`array indices`
:   Updated job run tasks to use `array indices`, which replaced `array spec` when you run jobs from the console.

CLI version 0.3.1535 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## July 2020
{: #codeengine-jul20}

Review the release notes for July 2020.
{: shortdesc}

### 30 July 2020
{: #codeengine-jul3020}
{: release-note}

Review the release notes for 30 July 2020.
{: shortdesc}

`array spec`
:   Updated job run tasks to use `array spec`, which replaced `array size` when you run jobs from the console.

Example application
:   Example application `ibmcom/helloworld` is now called `ibmcom/hello`.

### 22 July 2020
{: #codeengine-jul2220}
{: release-note}

Review the release notes for 22 July 2020.
{: shortdesc}

Updates to application docs
:   Updated information about updating and scaling your app to [Tutorial: Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) and [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

CLI version 0.3.1415 released. 
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 17 July 2020
{: #codeengine-jul1720}
{: release-note}

Review the release notes for 17 July 2020.
{: shortdesc}

CLI version 0.3.1363 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 10 July 2020
{: #codeengine-jul1020}
{: release-note}

Review the release notes for 10 July 2020.
{: shortdesc}

CLI version 0.2.1250 released.
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## June 2020
{: #codeengine-jun20}

Review the release notes for June 2020.
{: shortdesc}

### 19 June 2020
{: #codeengine-jun1920}
{: release-note}

Review the release notes for 19 June 2020.
{: shortdesc}

CLI version 0.2.1093 released. 
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 11 June 2020
{: #codeengine-jun1120}
{: release-note}

Review the release notes for 11 June 2020.
{: shortdesc}

Updates to service bind.
:   - Bind an {{site.data.keyword.cloud_notm}} service instance to a job.
    - Information about using environment variables to connect.
    - Unbinding your services.

:   See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).
    
CLI version 0.2.966 released. 
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## May 2020
{: #codeengine-may20}

Review the release notes for May 2020.
{: shortdesc}

### 19 May 2020
{: #codeengine-may1920}
{: release-note}

Review the release notes for 19 May 2020.
{: shortdesc}

Service bind
:   You can now bind an {{site.data.keyword.cloud_notm}} service instance to your {{site.data.keyword.codeengineshort}} application. For more information, see [Binding services to applications](/docs/codeengine?topic=codeengine-service-binding).

### 18 May 2020
{: #codeengine-may1820}
{: release-note}

Review the release notes for 18 May 2020.
{: shortdesc}

New! [{{site.data.keyword.codeenginefull_notm}} experimental release](https://cloud.ibm.com/codeengine/overview){: external}
:   With {{site.data.keyword.codeengineshort}}, you can build [applications](/docs/codeengine?topic=codeengine-application-workloads) in any language and then deploy them in seconds. Offload long running and resource hungry tasks to [asynchronous jobs](/docs/codeengine?topic=codeengine-create-job) that allow for optimized scale and cost efficiency. Learn how to get started with our [Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) and [Running jobs](/docs/codeengine?topic=codeengine-run-job-tutorial) tutorials.
