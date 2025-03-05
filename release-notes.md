---

copyright:
  years: 2020, 2025
lastupdated: "2025-03-05"

keywords: release notes for code engine, updates in code engine, what's new in code engine, document changes in code engine, updates, release notes

subcollection: codeengine

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.codeengineshort}}
{: #codeengine-relnotes}

Use the release notes to learn about the latest changes to {{site.data.keyword.codeenginefull}} that are grouped by month.
{: shortdesc}

## March 2025
{: #codeengine-march25}

### 05 March 2025
{: #codeengine-march0525}
{: release-note}

CLI version 1.51.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).



## February 2025
{: #codeengine-february25}

### 25 February 2025
{: #codeengine-february2525}
{: release-note}

Added support for `run_build_params` property for builds and build runs.
:   - See [Go](https://github.com/IBM/code-engine-go-sdk){: external} version 4.23.1
    - See [Java](https://github.com/IBM/code-engine-java-sdk){: external} version 4.22.1
    - See [Node.js](https://github.com/IBM/code-engine-node-sdk){: external} version 4.24.0
    - See [Python](https://github.com/IBM/code-engine-python-sdk){: external} version 4.14.1

### 20 February 2025
{: #codeengine-february2025}
{: release-note}

CLI version 1.51.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 01 February 2025
{: #codeengine-february0125}
{: release-note}

Automatic deletion of completed jobs and build runs
:   Starting on 1 February 2025, all job and build runs will be automatically deleted 7 days after completion, whether successful or not.
    To access job and build run details before deletion, use the Code Engine console, CLI or API:
       - [Retrieving Job Information](https://cloud.ibm.com/docs/codeengine?topic=codeengine-ts-jobrun-learnmore)
       - [Retrieving Build Information](https://cloud.ibm.com/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettinglogs)
    Make sure that you save any information that requires long-term storage to IBM Cloud Logs.
    
: Note: Job runs that are created by subscriptions will still be deleted 10 minutes after completion.


## January 2025
{: #codeengine-january25}

### 28 January 2025
{: #codeengine-january2825}
{: release-note}

CLI version 1.50.10 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 January 2025
{: #codeengine-january1625}
{: release-note}

Updated SDK versions by adding jobrun index details property to the existing jobrun status_details property
:   - See [Go](https://github.com/IBM/code-engine-go-sdk){: external} version 4.18.0
    - See [Java](https://github.com/IBM/code-engine-java-sdk){: external} version 4.17.0
    - See [Node.js](https://github.com/IBM/code-engine-node-sdk){: external} version 4.19.0
    - See [Python](https://github.com/IBM/code-engine-python-sdk){: external} version 4.9.0

### 10 January 2025
{: #codeengine-january1025}
{: release-note}

Terraform support for {{site.data.keyword.codeengineshort}} allowed outbound destinations is available
:   See [Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce).

CLI version 1.50.9 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## December 2024
{: #codeengine-december24}

### 05 December 2024
{: #codeengine-december0524}
{: release-note}

CLI version 1.50.8 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
: See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## November 2024
{: #codeengine-november24}

### 21 November 2024
{: #codeengine-november2124}
{: release-note}

Updated SDK versions with support for allowed outbound destinations
:   - See [Go](https://github.com/IBM/code-engine-go-sdk){: external} version 4.14.1
    - See [Java](https://github.com/IBM/code-engine-java-sdk){: external} version 4.12.1
    - See [Node.js](https://github.com/IBM/code-engine-node-sdk){: external} version 4.14.1
    - See [Python](https://github.com/IBM/code-engine-python-sdk){: external} version 4.4.1

### 14 November 2024
{: #codeengine-november1424}
{: release-note}

CLI version 1.50.7 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
: See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

: Note: The default Java version is changing from `17` to `21`. You can continue to build your projects with Java 17 by adding a file called `.buildenv` to your source directory with the following content: `BP_JVM_VERSION=17`.

### 05 November 2024
{: #codeengine-november0524}
{: release-note}

CLI version 1.50.6 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## October 2024
{: #codeengine-october24}

### 28 October 2024
{: #codeengine-october2824}
{: release-note}

CLI version 1.50.5 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 24 October 2024
{: #codeengine-october2424}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 10 October 2024
{: #codeengine-october1024}
{: release-note}

Terraform support for {{site.data.keyword.codeengineshort}} functions is generally available
:   See [Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce).

### 03 October 2024
{: #codeengine-october0324}
{: release-note}

Updated SDK versions with support for functions
:   - See [Go](https://github.com/IBM/code-engine-go-sdk){: external} version 4.10.0
    - See [Java](https://github.com/IBM/code-engine-java-sdk){: external} version 4.10.0
    - See [Node.js](https://github.com/IBM/code-engine-node-sdk){: external} version 4.10.0
    - See [Python](https://github.com/IBM/code-engine-python-sdk){: external} version 4.1.1

## September 2024
{: #codeengine-september24}

### 12 September 2024
{: #codeengine-september1224}
{: release-note}

CLI version 1.50.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

## August 2024
{: #codeengine-august24}

### 23 August 2024
{: #codeengine-august2324}
{: release-note}

CLI version 1.50.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 August 2024
{: #codeengine-august1624}
{: release-note}

Updated information about supported versions of Knative
:   See [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

## July 2024
{: #codeengine-july24}

### 11 July 2024
{: #codeengine-july1124}
{: release-note}

CLI version 1.50.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


## June 2024
{: #codeengine-june24}

### 06 June 2024
{: #codeengine-june0624}
{: release-note}

CLI version 1.50.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## May 2024
{: #codeengine-may24}

### 24 May 2024
{: #codeengine-may2424}
{: release-note}

CLI version 1.49.12 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 17 May 2024
{: #codeengine-may1724}
{: release-note}

CLI version 1.49.11 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated information about supported versions of Knative
:   See [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

Added support for functions in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).

## April 2024
{: #codeengine-apr24}

### 25 April 2024
{: #codeengine-apr2524}
{: release-note}

CLI version 1.49.10 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 18 April 2024
{: #codeengine-apr1824}
{: release-note}

CLI version 1.49.9 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 11 April 2024
{: #codeengine-apr1124}
{: release-note}

CLI version 1.49.8 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


## March 2024
{: #codeengine-mar24}

### 21 March 2024
{: #codeengine-mar2124}
{: release-note}

CLI version 1.49.7 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated the value of `CE_API_BASE_URL` environment variable from `CE_API_BASE_URL=https://api.private.us-south.codeengine.cloud.ibm.com/` to `CE_API_BASE_URL=https://api.us-south.codeengine.cloud.ibm.com/` for applications and jobs
:   See [Automatically injected environment variables for apps](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-app).
:   See [Automatically injected environment variables for jobs](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-jobs).

Updated the default value for the `--max-scale` option on the **`app update`** command
:   See the [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) command in the {{site.data.keyword.codeengineshort}} CLI reference.

### 14 March 2024
{: #codeengine-mar1424}
{: release-note}

CLI version 1.49.6 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 11 March 2024
{: #codeengine-mar1124}
{: release-note}

Added `CE_REGION`, `CE_PROJECT`, and `CE_API_BASE_URL` environment variables for functions
:   See [Automatically injected environment variables for functions](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-fun).


## February 2024
{: #codeengine-feb24}

### 27 February 2024
{: #codeengine-feb2724}
{: release-note}

Added `CE_REGION`, `CE_PROJECT`, and `CE_API_BASE_URL` environment variables for applications and jobs
:   See [Automatically injected environment variables for apps](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-app).
:   See [Automatically injected environment variables for jobs](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-jobs).

### 22 February 2024
{: #codeengine-feb2224}
{: release-note}

CLI version 1.49.5 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 20 February 2024
{: #codeengine-feb2024}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 16 February 2024
{: #codeengine-feb1624}
{: release-note}

Updated the user experience for working with jobs and job runs in the console
:   {{site.data.keyword.codeengineshort}} has enhanced the user experience to simplify working with jobs and job runs in the console. A consolidated list of job runs is now provided. See [Accessing job details from the console](/docs/codeengine?topic=codeengine-access-job-details#access-jobdetails-ui).

Added more information about functions in {{site.data.keyword.codeengineshort}}
:   - See [Automatically injected environment variables for functions](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-fun).
:   - See [Function pricing](/docs/codeengine?topic=codeengine-pricing#functions-pricing).
:   - See [Options for visibility for a {{site.data.keyword.codeengineshort}} function](/docs/codeengine?topic=codeengine-fun-work#optionsvisibilityfun).
:   - See [Verifying the code bundle reference for my function](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-verifyimage).

Updated behavior change for image builds that are built with Cloud Native Buildpacks
:   Introduced a behavior change for {{site.data.keyword.codeengineshort}} image builds that are built with Buildpacks. Images that are built using Buildpacks no longer use the neutral timestamp of `Jan, 1st 1980` as their image creation timestamp. The timestamp of the input source is now used. See [Choosing a build strategy -  Cloud Native Buildpacks](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat).



### 14 February 2024
{: #codeengine-feb1424}
{: release-note}

Added the `ibm_codeengine_job_name` attribute to the `ibm_codeengine_jobruns` metric for monitoring job runs in {{site.data.keyword.codeengineshort}}
:   See [Monitoring for {{site.data.keyword.codeengineshort}} - Attributes for segmentation](/docs/codeengine?topic=codeengine-monitor#attributes).



### 09 February 2024
{: #codeengine-feb0924}
{: release-note}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: Madrid, Spain (`eu-es`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).


### 05 February 2024
{: #codeengine-feb0524}
{: release-note}

CLI version 1.49.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added troubleshooting information about displaying limits and current usage with the CLI
:   - See [Debugging apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-limits).
:   - See [Debugging builds](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-limits).
:   - See [Debugging functions](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-limits).
:   - See [Debugging jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-limits).

The `Build` and `BuildRun` Kubernetes API objects are available in a new version
:   The `Build` and `BuildRun` Kubernetes API objects are available as `v1beta1` version. The `v1alpha1` version of these objects is deprecated. If you use the Kubernetes API to manage these objects, update to use the `v1beta1` version.  No action is required if you use the {{site.data.keyword.codeengineshort}} API, CLI, or console. See [Source-to-image CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-s2i).

## January 2024
{: #codeengine-jan24}

Review the release notes for January 2024.
{: shortdesc}

### 30 January 2024
{: #codeengine-jan3024}
{: release-note}

Added support for the `build` and `buildrun` properties for jobs in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).

### 25 January 2024
{: #codeengine-jan2524}
{: release-note}

CLI version 1.49.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 22 January 2024
{: #codeengine-jan2224}
{: release-note}

Updated the user experience for making configuration changes to apps in the console
:   {{site.data.keyword.codeengineshort}} has enhanced the user experience to simplify deploying configuration changes for applications. When you work in the {{site.data.keyword.codeengineshort}} console, instead of specifically entering an edit mode before you can make configuration changes, you can make changes to your configuration settings and deploy to make your changes effective. You can also redeploy your application without changes to configuration settings, if needed. See [Update your application](/docs/codeengine?topic=codeengine-update-app).

Updated the user experience for creating secrets and configmaps in the console
:   {{site.data.keyword.codeengineshort}} has enhanced the user experience to simplify creating and working with secrets and configmaps in the console. See [Working with secrets](/docs/codeengine?topic=codeengine-secret) and [Working with configmaps](/docs/codeengine?topic=codeengine-configmap).


### 12 January 2024
{: #codeengine-jan1224}
{: release-note}

CLI version 1.49.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for the `scale_array_size_variable_override` property for job runs in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).


## December 2023
{: #codeengine-dec23}

Review the release notes for December 2023.
{: shortdesc}

### 12 December 2023
{: #codeengine-dec1223}
{: release-note}

Added information about testing functions locally
:    See [Testing Code Engine functions locally](/docs/codeengine?topic=codeengine-fun-test-local)?

Added troubleshooting information for builds with Dockerfiles
:    See [Why is my build from a Dockerfile failing with a no command specified error](/docs/codeengine?topic=codeengine-ts-build-nocmdspecified)?

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 07 December 2023
{: #codeengine-dec023}
{: release-note}

Added support for applications with gRPC
:   See [Implementing applications with gRPC](/docs/codeengine?topic=codeengine-app-grpc).

### 06 December 2023
{: #codeengine-dec0623}
{: release-note}

CLI version 1.49.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 05 December 2023
{: #codeengine-dec0523}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 01 December 2023
{: #codeengine-dec0123}
{: release-note}

Added support for providing a custom value to the `JOB_ARRAY_SIZE` environment variable
:   - See [Processing a subset of data by dynamically assigning work to parallel job run instances](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel-dynamic).
:   - See the [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) and [**`jobrun resubmit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit) commands in the {{site.data.keyword.codeengineshort}} CLI reference.

CLI version 1.49.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


## November 2023
{: #codeengine-nov23}

Review the release notes for November 2023.
{: shortdesc}

### 16 November 2023
{: #codeengine-nov1623}
{: release-note}

Updated support for multi-domain or wildcard certificates for custom domain mappings
:   {{site.data.keyword.codeengineshort}} supports multi-domain or wildcard certificates within multiple projects within the same region. Also, if you use multi-domain or wildcard certificates and you need to update the credentials, you must update the existing TLS secret that is associated with the domain mapping, instead of creating a different TLS secret for the domain mapping. See [Working with custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings).


### 13 November 2023
{: #codeengine-nov1323}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 09 November 2023
{: #codeengine-nov0923}
{: release-note}

Added `xxlarge` size for builds
:   See [Determining the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size).

CLI version 1.48.0 released
:   This CLI version adds support for `xxlarge` build sizes. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated information about adding authentication and authorization capabilities, and rotating TLS certificates for security
:   See [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).

Added information about a new project details page in the console
:    This update includes information such as the region, CRN, GUID, network addresses (public and private), and more! This page provides a convenient way to obtain project details when troubleshooting.
:    - See [How can I see details about a project](/docs/codeengine?topic=codeengine-manage-project#project-details)?
:    - See [Providing support case details](/docs/codeengine?topic=codeengine-get-support#support-case-details).

Added troubleshooting information for app connectivity when using a proxy
:    See [Why does my app connection fail when using a proxy](/docs/codeengine?topic=codeengine-ts-app-connection-failwithproxy)?

Added troubleshooting information for expired SSH keys during a build
:   See [Build fails in the source step](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-expiredsshkey)?



### 03 November 2023
{: #codeengine-nov0323}
{: release-note}

Added FAQ about access for roles that are applied to {{site.data.keyword.codeengineshort}} entities are scoped within a {{site.data.keyword.codeengineshort}} project
:    See [Does {{site.data.keyword.codeengineshort}} provide a way to limit access to a particular entity within a {{site.data.keyword.codeengineshort}} project](/docs/codeengine?topic=codeengine-faqs#limit-access-fun)?

Added troubleshooting information for creating an allowlist for {{site.data.keyword.codeengineshort}} functions
:   See [How can I add my {{site.data.keyword.codeengineshort}} app to an allowlist](/docs/codeengine?topic=codeengine-ts-allowlist-function)?

Added support for domain mappings in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).

## October 2023
{: #codeengine-oct23}

Review the release notes for October 2023.
{: shortdesc}

### 30 October 2023
{: #codeengine-oct3023}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 19 October 2023
{: #codeengine-oct1923}
{: release-note}

Added information about additional support for functions in {{site.data.keyword.codeengineshort}}
:   - See [Options for visibility for a Code Engine functions](/docs/codeengine?topic=codeengine-fun-work#optionsvisibilityfun).
:   - See [Can I keep my function instance alive longer](/docs/codeengine?topic=codeengine-fun-work#functions-scale)?
:   - See [Creating function workloads from existing code bundles](/docs/codeengine?topic=codeengine-fun-create-existing).
:   - See [Configuring custom domain mappings for your function](/docs/codeengine?topic=codeengine-fun-domainmapping).

CLI version 1.47.1 released
:   This CLI version adds support for custom domain mappings, configuring scale-down delay, and endpoint visibility settings for functions with the CLI. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added troubleshooting information about receiving `ECONNRESET` errors
:   See [Why am I getting ECONNRESET errors when connecting to an endpoint](/docs/codeengine?topic=codeengine-ts-other-econnreset)?

Added information about controlling access to {{site.data.keyword.registryshort}} for {{site.data.keyword.codeengineshort}} workloads
:   See [Controlling access to {{site.data.keyword.registryshort}} for {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-add-registry#control-cr-access).

Updated information about supported versions of Knative
:   See [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

Updated information about custom domain mappings with {{site.data.keyword.codeengineshort}} apps
:   - See [Working with custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings).
:   - See [Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-app-domainmapping).




### 09 October 2023
{: #codeengine-oct0923}
{: release-note}

CLI version 1.46.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 05 October 2023
{: #codeengine-oct0523}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## September 2023
{: #codeengine-sep23}

Review the release notes for September 2023.
{: shortdesc}

### 27 September 2023
{: #codeengine-sep2723}
{: release-note}

Added support for liveness and readiness probes for applications in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).


### 21 September 2023
{: #codeengine-sep2123}
{: release-note}

Added support for liveness and readiness probes for applications in {{site.data.keyword.codeengineshort}}
:   See [Working with liveness and readiness probes for your app](/docs/codeengine?topic=codeengine-app-probes).

CLI version 1.46.0 released
:   This CLI version adds support for liveness and readiness probes for applications. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added troubleshooting information for toolchain
:   See [Why is my toolchain package too large](/docs/codeengine?topic=codeengine-ts-toolchain-size)?

Added getting started information about working with the {{site.data.keyword.codeengineshort}} CLI
:   See [Getting started with the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-cecli-getstart).

### 19 September 2023
{: #codeengine-sep1923}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 12 September 2023
{: #codeengine-sep1223}
{: release-note}

CLI version 1.45.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 07 September 2023
{: #codeengine-sep0723}
{: release-note}

Updated {{site.data.keyword.codeengineshort}} architecture diagram
:   See [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).

## August 2023
{: #codeengine-aug23}

Review the release notes for August 2023.
{: shortdesc}

### 29 August 2023
{: #codeengine-aug2923}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Added getting started information about working with the {{site.data.keyword.codeengineshort}} API
:   See [Getting started with the {{site.data.keyword.codeengineshort}} REST API](/docs/codeengine?topic=codeengine-ceapi-getstart).

### 17 August 2023
{: #codeengine-aug1723}
{: release-note}

Added troubleshooting information about how to verify a container image reference
:   See [How can I verify my image reference](/docs/codeengine?topic=codeengine-ts-build-verify-image)?

### 10 August 2023
{: #codeengine-aug1023}
{: release-note}

Added troubleshooting information about application restarts
:   See [Why did my app restart](/docs/codeengine?topic=codeengine-ts-app-restart)?

Added troubleshooting information about open ports on an endpoint for a {{site.data.keyword.codeengineshort}} component
:   See [Why does my port scan show more open ports than expected](/docs/codeengine?topic=codeengine-ts-app-toomanyports)?

Added troubleshooting information about jobs that run indefinitely, but don't automatically restart
:   See [Why does my daemon job not automatically restart](/docs/codeengine?topic=codeengine-ts-jobrun-daemon)?

Added information about an approach for processing many files by running jobs
:   See [Running jobs in parallel](/docs/codeengine?topic=codeengine-job-run-parallel).


## July 2023
{: #codeengine-jul23}

Review the release notes for July 2023.
{: shortdesc}

### 26 July 2023
{: #codeengine-jul2623}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 1.45.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 20 July 2023
{: #codeengine-jul2023}
{: release-note}

Added support for displaying details of app instances
:   With the {{site.data.keyword.codeengineshort}} console, you can view details about app instances to aid in troubleshooting apps. See [Getting details about app instances](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-instancedetails).

Added troubleshooting information about app instances that do not scale down as expected
:   See [Why aren't my app instances scaling down as expected](/docs/codeengine?topic=codeengine-ts-app-domain-notscaledown)?


### 19 July 2023
{: #codeengine-jul1923}
{: release-note}

Updated environment variable information to include functions
:   See [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

Terraform support for {{site.data.keyword.codeengineshort}} service bind is generally available
:   See [Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce).

CLI version 1.45.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 06 July 2023
{: #codeengine-jul0623}
{: release-note}

Updated {{site.data.keyword.codeengineshort}} getting started information to include functions
:   - See [Getting started with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-getting-started).

Added information comparing {{site.data.keyword.codeengineshort}} apps, jobs, and functions
:   - See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).
:   - See [Application workloads](/docs/codeengine?topic=codeengine-ceapplications).
:   - See [Batch job workloads](/docs/codeengine?topic=codeengine-cebatchjobs).
:   - See [Function workloads](/docs/codeengine?topic=codeengine-cefunctions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 1.45.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 05 July 2023
{: #codeengine-jul0523}
{: release-note}

Added support for the scale-down delay autoscaling option in the console
:   See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

Added information about details to provide when you report a support case
:   See [Providing support case details](/docs/codeengine?topic=codeengine-get-support#support-case-details).

## June 2023
{: #codeengine-jun23}

Review the release notes for June 2023.
{: shortdesc}


### 29 June 2023
{: #codeengine-jun2923}
{: release-note}

New! Support for functions in {{site.data.keyword.codeengineshort}}
:   - [Get an overview of Functions](/docs/codeengine?topic=codeengine-cefunctions).
:   - [Take a tutorial](/docs/codeengine?topic=codeengine-fun-tutorial).
:   - [Dive deeper into Functions](/docs/codeengine?topic=codeengine-fun-work).

CLI version 1.45.0 released
:   This CLI version adds support for the **`function`** command group to manage {{site.data.keyword.codeengineshort}} Functions with the CLI. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 23 June 2023
{: #codeengine-jun2323}
{: release-note}

Added summary information for getting started with apps and batch jobs in {{site.data.keyword.codeengineshort}}
:   - See [Application workloads](/docs/codeengine?topic=codeengine-ceapplications).
:   - See [Batch job workloads](/docs/codeengine?topic=codeengine-cebatchjobs).

Added support for the scale-down delay autoscaling option
:   - See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).
:   - See the [**`app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) and [**`app update`**](/docs/codeengine?topic=codeengine-cli#cli-application-update) commands in the {{site.data.keyword.codeengineshort}} CLI reference.

CLI version 1.44.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for service binding operations in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).



### 13 June 2023
{: #codeengine-jun1323}
{: release-note}

Added troubleshooting information about deleting jobs and job runs when the limit is exceeded
:   See [I'm over my limit for jobs or job runs. How can I delete them](/docs/codeengine?topic=codeengine-ts-jobrun-deleteforquota)?

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 08 June 2023
{: #codeengine-jun0823}
{: release-note}

CLI version 1.43.7 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 01 June 2023
{: #codeengine-jun0123}
{: release-note}

Added troubleshooting information about stopping an app from receiving traffic
:   See [Can I stop my app](/docs/codeengine?topic=codeengine-ts-app-stop-traffic)?

Updated information about working with multi-line log data
:   See [Considerations for viewing logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-logs-considerations).

## May 2023
{: #codeengine-may23}

Review the release notes for May 2023.
{: shortdesc}

### 30 May 2023
{: #codeengine-may3023}
{: release-note}

Added support to get status details for a project in the {{site.data.keyword.codeengineshort}} V2 API
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).

### 25 May 2023
{: #codeengine-may2523}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated information about DDoS protection in {{site.data.keyword.codeengineshort}}
:   See [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos).

Added troubleshooting information for app connectivity
:   See [Why does my app connection fail](/docs/codeengine?topic=codeengine-ts-app-connection-fail)?

Updated information about applying filters on {{site.data.keyword.la_short}} data
:   See [Can I apply filters on {{site.data.keyword.la_short}} data](/docs/codeengine?topic=codeengine-logging&interface=ui#view-logs-filters)?


### 18 May 2023
{: #codeengine-may1823}
{: release-note}

Added troubleshooting information for job runs not starting
:   See [Why is my job run not starting](/docs/codeengine?topic=codeengine-ts-jobrun-notstart)?

Added troubleshooting information for unavailable details of service binding operations
:   See [Why can't I display details of my configured service binding operations](/docs/codeengine?topic=codeengine-ts-sb-projsettings-nodetails)?

### 16 May 2023
{: #codeengine-may1623}
{: release-note}

CLI version 1.43.5 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 10 May 2023
{: #codeengine-may1023}
{: release-note}

Terraform support for {{site.data.keyword.codeengineshort}} is generally available
:   See [Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce).

### 05 May 2023
{: #codeengine-may0523}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## April 2023
{: #codeengine-apr23}

Review the release notes for April 2023.
{: shortdesc}

### 27 April 2023
{: #codeengine-apr2723}
{: release-note}


CLI version 1.43.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 26 April 2023
{: #codeengine-apr2623}
{: release-note}

Added support for {{site.data.keyword.codeengineshort}} project-wide settings
:   Added support for configuring project-wide settings for service binding operations and access to {{site.data.keyword.registrylong_notm}} in the console. See [Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations).

Updated support for TLS secrets
:   Updated support for creating TLS secrets in the console to also permit the upload of a certificate chain and its private key from a file. See [Creating a TLS secret from the console](/docs/codeengine?topic=codeengine-secret#secret-create-ui-tls).

Added troubleshooting information for creating an allowlist for {{site.data.keyword.codeengineshort}} apps and jobs
:   - See [How can I add my {{site.data.keyword.codeengineshort}} app to an allowlist](/docs/codeengine?topic=codeengine-ts-allowlist-app)?
:   - See [How can I add my {{site.data.keyword.codeengineshort}} job to an allowlist](/docs/codeengine?topic=codeengine-ts-allowlist-job)?

Added troubleshooting information for deploying a Python app
:   See [Why does my Python app fail to deploy](/docs/codeengine?topic=codeengine-ts-build-python)?

### 19 April 2023
{: #codeengine-apr1923}
{: release-note}

Configuring a highly available application tutorial
:   See [Configuring a highly available application](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 14 April 2023
{: #codeengine-apr1423}
{: release-note}

CLI version 1.43.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 April 2023
{: #codeengine-apr1223}
{: release-note}


CLI version 1.43.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 05 April 2023
{: #codeengine-apr0523}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


## March 2023
{: #codeengine-mar23}

Review the release notes for March 2023.
{: shortdesc}


### 30 March 2023
{: #codeengine-mar3023}
{: release-note}

Added information about troubleshooting images
:   - See [Debugging images](/docs/codeengine?topic=codeengine-troubleshoot-images).
:   - See [Why can't {{site.data.keyword.codeengineshort}} pull an image](/docs/codeengine?topic=codeengine-image-cannot-pull)?

Added information about troubleshooting toolchains
:   - See [Debugging your {{site.data.keyword.codeengineshort}} toolchain](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce).
:   - See [Why does my build run in my toolchain time out](/docs/codeengine?topic=codeengine-ts-buildrun-timeout-toolchain)?

Updated documentation for API V2.0
:   See [API change log](/docs/codeengine?topic=codeengine-api-changelog).


### 27 March 2023
{: #codeengine-mar2723}
{: release-note}

Terraform support for {{site.data.keyword.codeengineshort}} beta release
:   See [Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce).


### 23 March 2023
{: #codeengine-mar2323}
{: release-note}

CLI version 1.43.0 released
:   This CLI version adds support for the **`domainmapping`** command group to manage domain mappings with the CLI. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for managing domain mappings with the CLI
:   Use the **`domainmapping`** command group to map your own custom domain to a {{site.data.keyword.codeengineshort}} application to route requests from your custom URL to your application from the CLI. With this support, you can manage domain mapping with the CLI, in addition to the {{site.data.keyword.codeengineshort}} console.
    * See [Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-domain-mappings).
    * See [{{site.data.keyword.codeengineshort}} CLI reference (`domainmapping` command)](/docs/codeengine?topic=codeengine-cli#cli-domainmapping).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 16 March 2023
{: #codeengine-mar1623}
{: release-note}

CLI version 1.42.0 released
:   This CLI version updates support for secrets in the CLI such that you can define and work with various formats of secrets with the **`secret`** command group. See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated support for secrets in the CLI
:   Formats of secrets include basic authentication, generic, registry, SSH, and TLS. While you can continue to use the **`registry`** and **`repo`** command groups, take advantage of the unified **`secret`** command group.
    * See [Working with secrets](/docs/codeengine?topic=codeengine-secret).
    * See [{{site.data.keyword.codeengineshort}} CLI reference (`secret` command)](/docs/codeengine?topic=codeengine-cli#cli-secret).

### 10 March 2023
{: #codeengine-mar1023}
{: release-note}

Added troubleshooting information for why apps stop running
:   See [Why did my app stop running](/docs/codeengine?topic=codeengine-ts-app-end)?

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 02 March 2023
{: #codeengine-mar0223}
{: release-note}

CLI version 1.41.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


## February 2023
{: #codeengine-feb23}

Review the release notes for February 2023.
{: shortdesc}

### 23 February 2023
{: #codeengine-feb2323}
{: release-note}

Important: Project limits for resources in a {{site.data.keyword.codeengineshort}} project is increased
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits#project_quotas). The following limits are changed.
    * Applications:   40 apps per project
    * Application revisions:  120 revisions per project
    * CPU: The total combination for all the app instances, running job instances, and running build instances cannot exceed 128 vCPU.
    * Domain mappings: 80 custom domain mappings per project
    * Ephemeral storage:  The total combination for all the app instances, running job instances, and running build instances cannot exceed 512 G of ephemeral storage.
    * Memory:  The total combination for all the app instances, running job instances, and running build instances cannot exceed 512 G of memory.

CLI version 1.41.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 17 February 2023
{: #codeengine-feb1723}
{: release-note}

Added FAQ for Migrating your Cloud Foundry app
:   Added information about migrating a global load balancer. See [I use a global load balancer with my Cloud Foundry app. Can I migrate it to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_glb)?

Updated troubleshooting information for apps that don't achieve a ready status
:   Added information about confirming the port value. See [Why doesn't my app ever become ready](/docs/codeengine?topic=codeengine-ts-app-neverready)?

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 1.41.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 09 February 2023
{: #codeengine-feb0923}
{: release-note}

Added information about troubleshooting job runs
:   See [How can I find information about my job run](/docs/codeengine?topic=codeengine-ts-jobrun-learnmore)?

CLI version 1.41.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).


### 03 February 2023
{: #codeengine-feb0323}
{: release-note}

Added information about troubleshooting service bindings
:   - See [Debugging service bindings](/docs/codeengine?topic=codeengine-troubleshoot-servicebindings).
    - See [Why do the service credentials in my service binding to {{site.data.keyword.cos_full_notm}} show as `REDACTED`](/docs/codeengine?topic=codeengine-ts-sb-cosredacted)?
    - See [Why does my service binding to a Db2 Enterprise instance fail](/docs/codeengine?topic=codeengine-ts-sb-db2createfails)?

CLI version 1.40.8 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).



## January 2023
{: #codeengine-jan23}

Review the release notes for January 2023.
{: shortdesc}

### 27 January 2023
{: #codeengine-jan2723}
{: release-note}

Updated SDK versions
:   - See [Node.js](https://github.com/IBM/code-engine-node-sdk){: external} version 2.0.0
    - See [Python](https://github.com/IBM/code-engine-python-sdk){: external} version 2.0.3
    - See [Java](https://github.com/IBM/code-engine-java-sdk){: external} version 2.0.5

### 26 January 2023
{: #codeengine-jan2623}
{: release-note}

{{site.data.keyword.codeengineshort}} supports service endpoints
:   Added support for integration of {{site.data.keyword.codeengineshort}} projects with {{site.data.keyword.cloud}} service endpoints. This support gives you the ability to connect from your classic infrastructure to {{site.data.keyword.codeengineshort}} applications and stay within the {{site.data.keyword.cloud_notm}} network. You can control the visibility of {{site.data.keyword.codeengineshort}} applications and specify whether to expose the application to public or private endpoints. See [Using service endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-serviceendpt).

CLI version 1.40.7 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 24 January 2023
{: #codeengine-jan2423}
{: release-note}

Added information about using {{site.data.keyword.codeengineshort}} with a toolchain
:   See [Integrating {{site.data.keyword.codeengineshort}} workloads with Continuous Delivery](/docs/codeengine?topic=codeengine-toolchain-ce).

### 20 January 2023
{: #codeengine-jan2023}
{: release-note}

CLI version 1.40.6 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated support for service bindings from the console, which provides more options for configuring service bindings
:   - See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).
    - See [Configuring access for a service binding](/docs/codeengine?topic=codeengine-configure-bindaccess).
    - See [Binding a service instance to a Code Engine app or job](/docs/codeengine?topic=codeengine-bind-services).


### 12 January 2023
{: #codeengine-jan1223}
{: release-note}

CLI version 1.40.5 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Added information about supported versions of Knative
:   See [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).


## December 2022
{: #codeengine-dec22}

Review the release notes for December 2022.
{: shortdesc}

### 14 December 2022
{: #codeengine-dec1422}
{: release-note}

CLI version 1.40.4 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Added information about environment variables for jobs
:   See [Automatically injected environment variables for jobs](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-jobs).

### 07 December 2022
{: #codeengine-dec0722}
{: release-note}

Added GitHub tutorial for sending events
:   See [Sending GitHub events to an application](/docs/codeengine?topic=codeengine-github-event-webhooks).

Added migration tutorial for Heroku apps
:   See [Migrating Heroku apps to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-heroku-migrate).

Added information about supported TLS versions and ciphers
:   See [Supported TLS versions and cipher suites](/docs/codeengine?topic=codeengine-secure#secure-tls).

CLI version 1.40.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 01 December 2022
{: #codeengine-dec0122}
{: release-note}

CLI version 1.40.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## November 2022
{: #codeengine-nov22}

Review the release notes for November 2022.
{: shortdesc}

### 17 November 2022
{: #codeengine-nov1722}
{: release-note}

Added more information about certificates and considerations when you use {{site.data.keyword.cis_short}} with custom domain mappings
:   See [How can I obtain a certificate for my custom domain?](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain-cert) and [Can I use {{site.data.keyword.cis_short}} for domain management when I am using custom domain mapping with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-domain-mappings#prepare-use-cis)

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 10 November 2022
{: #codeengine-nov1022}
{: release-note}

CLI version 1.40.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 03 November 2022
{: #codeengine-nov0322}
{: release-note}

Added support for custom domain mappings
:   {{site.data.keyword.codeengineshort}} adds support for mapping your own custom domain to a {{site.data.keyword.codeengineshort}} application to route requests from your custom URL to your application from the {{site.data.keyword.codeengineshort}} console.
    See [Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-domain-mappings).

## October 2022
{: #codeengine-oct22}

Review the release notes for October 2022.
{: shortdesc}


### 27 October 2022
{: #codeengine-oct2722}
{: release-note}

CLI version 1.40.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated support of ephemeral storage for apps and jobs
:   {{site.data.keyword.codeengineshort}} adds support for setting ephemeral storage for apps and jobs in the console. Added validation checks for ephemeral storage to clarify the relationship between ephemeral storage and memory. Ephemeral storage is bounded by the configured memory.
    * See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).
    * See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


### 20 October 2022
{: #codeengine-oct2022}
{: release-note}

CLI version 1.39.6 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Revised and improved descriptions of metrics for monitoring {{site.data.keyword.codeengineshort}}
:   See [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 17 October 2022
{: #codeengine-oct1722}
{: release-note}

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 06 October 2022
{: #codeengine-oct0622}
{: release-note}

CLI version 1.39.5 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

## September 2022
{: #codeengine-sep22}

Review the release notes for September 2022.
{: shortdesc}

### 21 September 2022
{: #codeengine-sep2122}
{: release-note}

New tutorial
:   Added a tutorial that demonstrates how to secure your application with an open source tool called Guard. See [Securing your application with Guard](/docs/codeengine?topic=codeengine-getting-started-with-guard).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 15 September 2022
{: #codeengine-sep1522}
{: release-note}

CLI version 1.39.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).


## August 2022
{: #codeengine-aug22}

Review the release notes for August 2022.
{: shortdesc}

### 31 August 2022
{: #codeengine-aug3122}
{: release-note}

CLI version 1.39.2 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

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
:   See [Creating and running a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon).

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
    * See [Building a container image](/docs/codeengine?topic=codeengine-plan-build).

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
:   - [Can I use a custom URL with Code Engine](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#customurl)?
    - [Why are my apps slow to respond](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_response)?

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
:   With {{site.data.keyword.codeengineshort}}, you can now go from source code to a running app or a configured job with a **single** command. The **`app create`** command automatically runs the container build and deploys your app in a single step. You don't even need to know about building container images or working with registries. Let {{site.data.keyword.codeengineshort}} handle all these processes for you.
    * If you are familiar with `push source code` platforms, such as Cloud Foundry, start by exploring the tutorial [Deploying Cloud Foundry applications in Code Engine: Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial).
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
:   Types include {{site.data.keyword.codeengineshort}} managed secrets and user-managed secrets. If no credentials are needed to access the registry, then the access is `None`. See [Types of registry access secrets](/docs/codeengine?topic=codeengine-add-registry#types-registryaccesssecrets).

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
:   CLI 1.27.0 introduces an improved service binding implementation, which is used for all new service bindings. Existing applications and jobs continue to function normally. However, if you want to bind another service instance to an app or job, you must first delete any existing service bindings from that app or job. You can then re-create those service bindings with the improved service binding implementation. See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).

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
:   See [Why is my job not completing](/docs/codeengine?topic=codeengine-ts-jobrun-doesnotcomplete)?

Added information about considerations when you use SSH keys for accessing your source repository
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

Added clarification for use of direct endpoints when you use private networking with services such as {{site.data.keyword.cos_full_notm}}
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

CLI version 1.23.3 released
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
:   Added support for monitoring security and compliance posture with {{site.data.keyword.codeengineshort}}. See [Monitoring security and compliance posture with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-secure).

### 06 December 2021
{: #codeengine-dec0621}
{: release-note}

Review the release notes for 06 December 2021.
{: shortdesc}

{{site.data.keyword.cos_full_notm}} subscriptions
:   Added support for {{site.data.keyword.cos_full_notm}} eventing subscriptions from the {{site.data.keyword.codeengineshort}} console. See [Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 01 December 2021
{: #codeengine-dec0121}
{: release-note}

Review the release notes for 01 December 2021.
{: shortdesc}

CLI version 1.23.2 released
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

CLI version 1.23.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 November 2021
{: #codeengine-nov1621}
{: release-note}

Review the release notes for 16 November 2021.
{: shortdesc}

{{site.data.keyword.codeengineshort}} supports virtual private endpoints
:   Added support for integration of {{site.data.keyword.codeengineshort}} projects with {{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for Virtual Private Cloud (VPC). You can use this support to connect from your VPC network to {{site.data.keyword.codeengineshort}} applications. See [Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe) and [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).

CLI version 1.23.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 04 November 2021
{: #codeengine-nov0421}
{: release-note}

Review the release notes for 04 November 2021.
{: shortdesc}

CLI version 1.22.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.codeengineshort}} is integrated with {{site.data.keyword.compliance_long}}
:   Added support for governing information {{site.data.keyword.codeengineshort}} resource configuration with {{site.data.keyword.compliance_long}}. See [Managing security and compliance with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-secure).

Updated versions for buildpacks
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

CLI version 1.21.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.cos_full_notm}} subscriptions
:  Removed restriction for {{site.data.keyword.codeengineshort}} subscriptions for {{site.data.keyword.cos_short}} event producers in the `ca-tor` region. {{site.data.keyword.cos_short}} event producers are supported in these [regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Added Python as a supported language for builds that use the Cloud Native Buildpacks strategy
:   See [Cloud Native Buildpacks](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).




### 21 October 2021
{: #codeengine-oct2121}
{: release-note}

Review the release notes for 21 October 2021.
{: shortdesc}

CLI version 1.21.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 15 October 2021
{: #codeengine-oct1521}
{: release-note}

Review the release notes for 15 October 2021.
{: shortdesc}

Added support for deploying apps with project-only endpoints
:   Workflows for application create and update from the console support `Project-only` visibility for app endpoints. Setting a project-only endpoint means that your app is not accessible from the public internet and network access is only possible from other {{site.data.keyword.codeengineshort}} components that are running in the same project (cluster-local). See [Deploying your app with a project-only endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly).

Added information about creating custom dashboards to monitor {{site.data.keyword.codeengineshort}} workloads
:   See [Creating custom dashboards to monitor {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor-custom).

### 07 October 2021
{: #codeengine-oct0721}
{: release-note}

Review the release notes for 07 October 2021.
{: shortdesc}

Creating builds no longer requires a value for the source branch
:   If the value is not provided and you leave the field empty, {{site.data.keyword.codeengineshort}} automatically determines the branch name. See [Building a container image](/docs/codeengine?topic=codeengine-plan-build).

CLI version 1.20.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 04 October 2021
{: #codeengine-oct0421}
{: release-note}

Review the release notes for 04 October 2021.
{: shortdesc}

Revised and improved the application configuration pages in the console
:   See [Updating your app](/docs/codeengine?topic=codeengine-update-app).

CLI version 1.20.0 released
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

CLI version 1.19.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 September 2021
{: #codeengine-sep1621}
{: release-note}

Review the release notes for 16 September 2021.
{: shortdesc}

CLI version 1.19.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated the Dockerfile build strategy to use the BuildKit tool
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 9 September 2021
{: #codeengine-sep0921}
{: release-note}

Review the release notes for 9 September 2021.
{: shortdesc}

CLI version 1.18.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated information about the roles that are required for using Kubernetes and Knative with {{site.data.keyword.codeengineshort}}
:   See [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes) and [Using Knative with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-knative).

### 2 September 2021
{: #codeengine-sep0221}
{: release-note}

Review the release notes for 2 September 2021.
{: shortdesc}

Added support for build logs in the {{site.data.keyword.codeengineshort}} console
:   See [Viewing build logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-build-ui).

Updated information about `reclamation` commands
:   See [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project). |

### 1 September 2021
{: #codeengine-sep0121}
{: release-note}

Review the release notes for 1 September 2021.
{: shortdesc}

CLI version 1.17.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added support for Periodic timer (cron) event producers in the {{site.data.keyword.codeengineshort}} console
:   See [Working with the Periodic timer (cron) event producer](/docs/codeengine?topic=codeengine-subscribe-cron).

Updated versions for buildpacks
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

CLI version 1.16.1 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 19 August 2021
{: #codeengine-aug1921}
{: release-note}

Review the release notes for 19 August 2021.
{: shortdesc}

CLI version 1.16.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Secrets
:   Updated information about viewing a list of all secrets, which includes secrets that are generated by {{site.data.keyword.codeengineshort}}, or viewing a list of secrets that are user-generated. See [Creating secrets from the console](/docs/codeengine?topic=codeengine-secret#secret-create-ui).

Updated information about headers and environment variables when you use subscriptions
:   See [Header and body information for {{site.data.keyword.cos_full_notm}} events delivered to applications](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos), [Environment variables for {{site.data.keyword.cos_full_notm}} events delivered to jobs](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-envir-variables-cos), [Header and body information for cron events delivered to applications](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron), and [Environment variables for cron events delivered to jobs](/docs/codeengine?topic=codeengine-subscribe-cron#sub-envir-variables-cron).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 16 August 2021
{: #codeengine-aug1621}
{: release-note}

Review the release notes for 16 August 2021.
{: shortdesc}

CLI version 1.15.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Troubleshooting subscriptions
:   Added information about troubleshooting subscriptions when a subscription shows errors when it delivers events. See [Why does my subscription show errors when it delivers events](/docs/codeengine?topic=codeengine-ts-subscription-deliveryerrors)?

Subscriptions for {{site.data.keyword.cos_full_notm}} event producers are not available in the Canada Toronto (`ca-tor`) region
:   See [Working with the {{site.data.keyword.cos_short}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 6 August 2021
{: #codeengine-aug0621}
{: release-note}

Review the release notes for 6 August 2021.
{: shortdesc}

CLI version 1.14.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Private repositories
:   Updated information about running {{site.data.keyword.codeengineshort}} builds that use source in private repos. See [Building a container image](/docs/codeengine?topic=codeengine-plan-build).

### 5 August 2021
{: #codeengine-aug0521}
{: release-note}

Review the release notes for 5 August 2021.
{: shortdesc}

Updated versions for buildpacks
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

CLI version 1.13.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 29 July 2021
{: #codeengine-jul2921}
{: release-note}

Review the release notes for 29 July 2021.
{: shortdesc}

Deleting projects
:   Added support in the console for restoring projects that are soft deleted and for permanently deleting projects. See [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project) and [Permanently deleting projects](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 27 July 2021
{: #codeengine-jul2721}
{: release-note}

Review the release notes for 27 July 2021.
{: shortdesc}

CLI version 1.12.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added overview topics for deploying apps and running jobs
:   See [Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads) and [Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan).

Updated versions for buildpacks
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

CLI version 1.11.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Subscription ping limits
:   Added information about limits for subscription ping data. See [Subscription ping limits](/docs/codeengine?topic=codeengine-limits#subscription-cron-limit).

Applications that use WebSockets
:   Added information about apps that use WebSockets need to reconnect before the session expires. See [Do Code Engine apps support WebSockets](/docs/codeengine?topic=codeengine-faqs#app-websockets)?

Updated versions for buildpacks
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

Updated versions for buildpacks
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

CLI version 1.10.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated app and app revision quotas for projects
:   The quota is revised to 20 apps per project and 60 revisions for all apps per project. See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits#project_quotas).

Added basic troubleshooting information
:   See [Troubleshooting overview](/docs/codeengine?topic=codeengine-troubleshooting_over).

{{site.data.keyword.cloud_notm}} and third-party integrations
:   Find out what {{site.data.keyword.cloud_notm}} and third-party integrations are supported by {{site.data.keyword.codeengineshort}}. See [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/codeengine?topic=codeengine-supported-integrations).

Added information about security and {{site.data.keyword.codeengineshort}}
:   See [{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 16 June 2021
{: #codeengine-jun1621}
{: release-note}

Review the release notes for 16 June 2021.
{: shortdesc}

CLI version 1.9.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Build size
:   Updated the size for `xlarge` builds to 4 CPU and 16 GB. See [Determine the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size).

Configmaps and secrets
:   Updated information about referencing existing and not-yet-created configmaps and secrets with the CLI. See [Referencing configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap#configmap-ref-cli) and [Referencing secrets with the CLI](/docs/codeengine?topic=codeengine-secret#secret-ref-cli).

Added information about updating jobs
:   See [Updating a job](/docs/codeengine?topic=codeengine-update-job).

### 10 June 2021
{: #codeengine-jun1021}
{: release-note}

Review the release notes for 10 June 2021.
{: shortdesc}

Important: Introduced a breaking change with {{site.data.keyword.codeengineshort}} memory and CPU combinations
:   With this version, applications and batch jobs are required to use a specific set of memory and CPU combinations for resource allocations. Existing running workloads are not impacted, but new and updated workloads are required to follow these requirements. For more information, see [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

CLI version 1.8.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Running job without job configuration
:   Updated information about running batch jobs to include running a job with the CLI without first defining a job configuration. See [Running a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withoutjobconfig).

Added support for private repositories from the console
:   See [Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Subscription support for jobs is generally available
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

Updated versions for buildpacks
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

CLI version 1.7.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated information about supported {{site.data.keyword.cos_full_notm}} buckets for subscriptions
:   See [Set up the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#setup-cosevent-producer).

Added information about specifying the `--path` option when you create a subscription to an application.
:   See [Subscribing to Ping events for an app](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app) and [Creating an {{site.data.keyword.cos_full_notm}} subscription for an application](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app).

Updated information about accessing container registries
:   See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry).

Added information about working with Kubernetes and {{site.data.keyword.codeengineshort}}
:   See [Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes).

### 18 May 2021
{: #codeengine-may1821}
{: release-note}

Review the release notes for 18 May 2021.
{: shortdesc}

Added information about working with environment variables in {{site.data.keyword.codeengineshort}}
:   See [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).

Working with secrets and configmaps
:   Added information about working with secrets and configmaps with the console and updated information about working with secrets and configmaps with the CLI. See [Working with secrets](/docs/codeengine?topic=codeengine-secret) or [Working with configmaps](/docs/codeengine?topic=codeengine-configmap).

CLI version 1.6.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 10 May 2021
{: #codeengine-may1021}
{: release-note}

Review the release notes for 10 May 2021.
{: shortdesc}

CLI version 1.5.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 7 May 2021
{: #codeengine-may0721}
{: release-note}

Review the release notes for 7 May 2021.
{: shortdesc}

Updated versions for buildpacks
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

CLI version 1.4.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 21 April 2021
{: #codeengine-apr2121}
{: release-note}

Review the release notes for 21 April 2021.
{: shortdesc}

`CloudEvents` specification
:   Added information about support for `CloudEvents` specification. See [Can I use other CloudEvents specifications](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)?

CLI version 1.3.0 released
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

CLI version 1.2.0 released
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

CLI version 1.1.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 1 April 2021
{: #codeengine-apr0121}
{: release-note}

Review the release notes for 1 April 2021.
{: shortdesc}

Added information about deploying apps across multiple regions that use a custom domain name.
:   See [Deploying an application across multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

CLI version 1.0.1 released
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

CLI version 1.0.0 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 30 March 2021
{: #codeengine-mar3021}
{: release-note}

Review the release notes for 30 March 2021.
{: shortdesc}

Updated information about setting the `port` value when you deploy apps
:   See [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).

Updated information about application scaling when apps connect to event producers
:   See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).


### 26 March 2021
{: #codeengine-mar2621}
{: release-note}

Review the release notes for 26 March 2021.
{: shortdesc}

CLI versions 0.6.2 and CLI 0.6.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added {{site.data.keyword.codeengineshort}} billing.
:   See [Pricing for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-pricing).

Updated CPU and memory limits for jobs and apps
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

### 25 March 2021
{: #codeengine-mar2521}
{: release-note}

Review the release notes for 25 March 2021.
{: shortdesc}

Added {{site.data.keyword.codeengineshort}} monitoring information
:   See [Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor).

Added information for determining CPU and memory combinations
:   See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).

{{site.data.keyword.codeengineshort}} Tutorial
:   See [{{site.data.keyword.codeengineshort}} Tutorial](/docs/solution-tutorials?topic=solution-tutorials-serverless-github-traffic-analytics).

### 23 March 2021
{: #codeengine-mar2321}
{: release-note}

Review the release notes for 23 March 2021.
{: shortdesc}

{{site.data.keyword.codeengineshort}} is supported in a new region: Asia Pacific (`jp-tok`)
:   See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Added {{site.data.keyword.codeengineshort}} high availability and disaster recovery documentation
:   See [Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-ha-dr).

### 22 March 2021
{: #codeengine-mar2221}
{: release-note}

Review the release notes for 22 March 2021.
{: shortdesc}

CLI version 0.6.1 releases
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 18 March 2021
{: #codeengine-mar1821}
{: release-note}

Review the release notes for 18 March 2021.
{: shortdesc}

CLI versions 0.6.0 and 0.5.25 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Automatically create registry access
:   From the console, {{site.data.keyword.codeengineshort}} can now automatically create registry access for {{site.data.keyword.registryshort}} instances that are in your account. When you push images, {{site.data.keyword.codeengineshort}} can even create a namespace in your container registry instance. See [Deploying an app that references an image in Container Registry with the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console), [Deploying your app from source code](/docs/codeengine?topic=codeengine-app-source-code), [Creating a job from images in Container Registry with the console](/docs/codeengine?topic=codeengine-create-job-crimage), and [Creating a job from source code](/docs/codeengine?topic=codeengine-run-job-source-code).

Added logging information for apps and jobs from the console
:   See [Viewing logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-logs-ui).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated limits for {{site.data.keyword.codeengineshort}}
:   See [Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits).

Updated API CRD information for subscriptions and jobs
:   See [Subscription CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-subscription) and [Job CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-batch).

[Using Kubernetes with {{site.data.keyword.codeengineshort}} - Serving CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-serving).

Updated information for troubleshooting your builds
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated service bind information
:   See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).

### 9 March 2021
{: #codeengine-mar0921}
{: release-note}

Review the release notes for 9 March 2021.
{: shortdesc}

CLI version 0.5.21 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Project reclamation
:   Updated **`project delete`** command to include information about project reclamation. See [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).

### 4 March 2021
{: #codeengine-mar0421}
{: release-note}

Review the release notes for 4 March 2021.
{: shortdesc}

Added {{site.data.keyword.codeengineshort}} architecture and workload isolation documentation
:   See [Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture).

Added HTTP headers and body information for subscriptions
:   See [HTTP headers and body information for {{site.data.keyword.cos_full_notm}} events](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos) and [HTTP headers and body information for Ping events](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron).

System events
:   Added information about viewing system events to troubleshooting information for apps and jobs. See [system event information for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent) and [system event information for job runs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent).

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 2 March 2021
{: #codeengine-mar0221}
{: release-note}

Review the release notes for 2 March 2021.
{: shortdesc}

CLI version 0.5.20 released
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

Updated versions for buildpacks
:   See [Choosing a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 0.5.19 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added notices file
:   See [{{site.data.keyword.codeengineshort}} notices](/docs/codeengine?topic=codeengine-notices).

### 23 February 2021
{: #codeengine-feb2321}
{: release-note}

Review the release notes for 23 February 2021.
{: shortdesc}

CLI version 0.5.18 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 February 2021
{: #codeengine-feb1621}
{: release-note}

Review the release notes for 16 February 2021.
{: shortdesc}

CLI version 0.5.17 released
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

CLI version 0.5.16 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Added information about potentially reaching Docker rate limits.
:   See [Accessing container registries](/docs/codeengine?topic=codeengine-add-registry) and [Planning your build](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 3 February 2021
{: #codeengine-feb0321}
{: release-note}

Review the release notes for 3 February 2021.
{: shortdesc}

Added planning for {{site.data.keyword.codeengineshort}} information
:   See [Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

Added information about working with configmaps and secrets as mounted files
:   See [Referencing secrets and configmaps as mounted files](/docs/codeengine?topic=codeengine-secretcm-reference-mountedfiles).

Updated FAQ to add information about differences between {{site.data.keyword.codeengineshort}} builds and Docker builds
:   See [What is the difference between a Docker build on my system and a build in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild)?

Added a tip for when you copy an entire Git repository and note about best practices for naming application directories
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

CLI version 0.5.15 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Environment variables
:   Added information about automatically injected environment variables for {{site.data.keyword.codeengineshort}} apps and jobs. See [Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars).

Revised subscription topic
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

CLI version 0.5.14 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 20 January 2021
{: #codeengine-jan2021}
{: release-note}

Review the release notes for 20 January 2021.
{: shortdesc}

New region!
:   {{site.data.keyword.codeengineshort}} is supported in a new region: EU Central (`eu-de`). See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).

Removed some beta limitations for Code Engine
:   From now on, projects, applications, and jobs do not expire after seven days. In addition, you are no longer limited to one project per region. See [Limits](/docs/codeengine?topic=codeengine-limits).

### 15 January 2021
{: #codeengine-jan1521}
{: release-note}

Review the release notes for 15 January 2021.
{: shortdesc}

Added a build tutorial
:   See [Tutorial: Building applications by using buildpacks](/docs/codeengine?topic=codeengine-build-app-tutorial).

Take a terminology quiz
:   See [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology).

Added a sitemap of {{site.data.keyword.codeengineshort}} topics
:   See [Sitemap for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-sitemap).

CLI version 0.5.13 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 12 January 2021
{: #codeengine-jan1221}
{: release-note}

Review the release notes for 12 January 2021.
{: shortdesc}

Updated information for troubleshooting your builds
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

New Activity tracker information
:   See [Auditing events for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-at_events).

Updated build information
:   See [Building a container image](/docs/codeengine?topic=codeengine-plan-build).

Added API CRD information for subscriptions
:   See [Subscription CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-subscription).

Updated task information for jobs
:   See [creating jobs with images from {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-create-job-crimage) and [creating jobs with images from a private repository](/docs/codeengine?topic=codeengine-create-job-private).

CLI version 0.5.11 and 0.5.12 released
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

Updated information for troubleshooting your builds
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated versions for buildpacks
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

Updated sizes for builds
:   See [build sizes](/docs/codeengine?topic=codeengine-plan-build#build-size).

CLI versions 0.5.8 and 0.5.9 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 December 2020
{: #codeengine-dec1420}
{: release-note}

Review the release notes for 14 December 2020.
{: shortdesc}

Learn more about scaling your applications
:   See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

CLI version 0.5.7 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 9 December 2020
{: #codeengine-dec0920}
{: release-note}

Review the release notes for 9 December 2020.
{: shortdesc}

Find Dockerfile build tips
See [Writing a Dockerfile for Code Engine](/docs/codeengine?topic=codeengine-dockerfile).

Updated troubleshooting tips for builds
:   See [Troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

Updated versions for buildpacks
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

CLI version 0.5.6 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 2 December 2020
{: #codeengine-dec0220}
{: release-note}

Review the release notes for 2 December 2020.
{: shortdesc}

CLI version 0.5.5 released
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

Updated user access information
:   See [Managing user access](/docs/codeengine?topic=codeengine-iam).

### 20 November 2020
{: #codeengine-nov2020}
{: release-note}

Review the release notes for 20 November 2020.
{: shortdesc}

CLI version 0.5.3 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

New logging topic
:   See [Viewing logs](/docs/codeengine?topic=codeengine-logging).

Tips for troubleshooting applications
:   See [Troubleshooting tips for apps](/docs/codeengine?topic=codeengine-troubleshoot-apps).

### 12 November 2020
{: #codeengine-nov1220}
{: release-note}

Review the release notes for 12 November 2020.
{: shortdesc}

CLI version 0.4.2592 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 11 November 2020
{: #codeengine-nov1120}
{: release-note}

Review the release notes for 11 November 2020.
{: shortdesc}

CLI version 0.4.2577 released
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

CLI version 0.4.2493 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Lithops
:   You can run a {{site.data.keyword.codeengineshort}} job by using Lithops framework. See [Running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops).

### 23 October 2020
{: #codeengine-oct2320}
{: release-note}

Review the release notes for 23 October 2020.
{: shortdesc}

CLI version 0.4.2439 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Project selected for current context
:   When you create a project, it is automatically selected as the current context. See [Creating a project with the CLI](/docs/codeengine?topic=codeengine-manage-project#create-project-cli).

Updated runtimes for buildpacks
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

CLI version 0.4.2397 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 14 October 2020
{: #codeengine-oct1420}
{: release-note}

Review the release notes for 14 October 2020.
{: shortdesc}

New troubleshooting information
:   See [Troubleshooting jobs](/docs/codeengine?topic=codeengine-troubleshoot-job) and [Troubleshooting builds](/docs/codeengine?topic=codeengine-troubleshoot-build).

### 6 October 2020
{: #codeengine-oct0620}
{: release-note}

Review the release notes for 6 October 2020
{: shortdesc}

CLI version 0.4.2365 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 5 October 2020
{: #codeengine-oct0520}
{: release-note}

Review the release notes for 5 October 2020.
{: shortdesc}

CLI version 0.4.2335 released
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

CLI version 0.4.2276 released
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

CLI version 0.4.2227 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Updated runtimes for buildpacks
:   See [build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy).

### 18 September 2020
{: #codeengine-sep1820}
{: release-note}

Review the release notes for 18 September 2020.
{: shortdesc}

CLI version 0.4.2217 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 16 September 2020
{: #codeengine-sep1620}
{: release-note}

Review the release notes for 16 September 2020.
{: shortdesc}

New! [{{site.data.keyword.codeenginefull_notm}} beta release](https://cloud.ibm.com/codeengine/overview)
:   With {{site.data.keyword.codeengineshort}}, you can,
    - [Build container images](/docs/codeengine?topic=codeengine-plan-build) and deploy them in apps and jobs.
    - [Pull from private repositories](/docs/codeengine?topic=codeengine-code-repositories).
    - [Connect to private registries](/docs/codeengine?topic=codeengine-add-registry).
    - [Work with configmaps](/docs/codeengine?topic=codeengine-configmap).
    - [Work with secrets](/docs/codeengine?topic=codeengine-secret).

CLI version 0.4.2192 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 4 September 2020
{: #codeengine-sep0420}
{: release-note}

Review the release notes for 4 September 2020.
{: shortdesc}

Application logs
:   Added [viewing application logs](/docs/codeengine?topic=codeengine-logging&interface=cli#view-applog-cli) information.

### 2 September 2020
{: #codeengine-sep0220}
{: release-note}

Review the release notes for 2 September 2020.
{: shortdesc}

CLI version 0.3.1973 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

{{site.data.keyword.codeengineshort}} batch CRDs updated to `v1beta1`
:   See [Batch CRDs](/docs/codeengine?topic=codeengine-kubernetes#api-crd-batch).

## August 2020
{: #codeengine-aug20}

Review the release notes for August 2020.
{: shortdesc}

### 21 August 2020
{: #codeengine-aug2120}
{: release-note}

Review the release notes for 21 August 2020.
{: shortdesc}

CLI version 0.3.1802 released
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

CLI version 0.3.1712 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

Ephemeral storage limit
:   Added ephemeral storage limit to [apps](/docs/codeengine?topic=codeengine-limits#limits_application) and [jobs](/docs/codeengine?topic=codeengine-limits#limits_job).

### 14 August 2020
{: #codeengine-aug1420}
{: release-note}

Review the release notes for 14 August 2020.
{: shortdesc}

CLI version 0.3.1675 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 4 August 2020
{: #codeengine-aug0420}
{: release-note}

Review the release notes for 4 August 2020.
{: shortdesc}

`array indices`
:   Updated job run tasks to use `array indices`, which replaced `array spec` when you run jobs from the console.

CLI version 0.3.1535 released
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

CLI version 0.3.1415 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 17 July 2020
{: #codeengine-jul1720}
{: release-note}

Review the release notes for 17 July 2020.
{: shortdesc}

CLI version 0.3.1363 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 10 July 2020
{: #codeengine-jul1020}
{: release-note}

Review the release notes for 10 July 2020.
{: shortdesc}

CLI version 0.2.1250 released
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

CLI version 0.2.1093 released
:   See [CLI version history](/docs/codeengine?topic=codeengine-cli_versions).

### 11 June 2020
{: #codeengine-jun1120}
{: release-note}

Review the release notes for 11 June 2020.
{: shortdesc}

Updates to service bind
:   - Bind an {{site.data.keyword.cloud_notm}} service instance to a job.
    - Information about using environment variables to connect.
    - Unbinding your services.

:   See [Integrating IBM Cloud services with service binding](/docs/codeengine?topic=codeengine-service-binding).

CLI version 0.2.966 released
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
:   With {{site.data.keyword.codeengineshort}}, you can build [applications](/docs/codeengine?topic=codeengine-application-workloads) in any language and then deploy them in seconds. Offload long-running and resource-hungry tasks to [asynchronous jobs](/docs/codeengine?topic=codeengine-create-job) that allow for optimized scale and cost efficiency. Learn how to get started with our [Deploying applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial) and [Running jobs](/docs/codeengine?topic=codeengine-run-job-tutorial) tutorials.
