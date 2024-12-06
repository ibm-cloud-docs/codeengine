---

copyright:
  years: 2024
lastupdated: "2024-12-06"

keywords: sitemap, code engine, about, tutorial, project, app, job, configmaps, secret, event, log, monitor, cli, api, troubleshoot, support, source code, faq, memory, cpu, commands, arguments, release notes

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Sitemap for {{site.data.keyword.codeengineshort}}
{: #sitemap}

Find what you are looking for in the compilation of {{site.data.keyword.codeenginefull}} topics.
{: shortdesc}





## Getting started with {{site.data.keyword.codeenginefull_notm}}
{: #sitemap_getting_started_with_}


[Getting started with {{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-getting-started#getting-started)

* [What are {{site.data.keyword.codeengineshort}} projects, applications, jobs, and functions?](/docs/codeengine?topic=codeengine-getting-started#term-summary)

* [Deploying your first {{site.data.keyword.codeengineshort}} app](/docs/codeengine?topic=codeengine-getting-started#app-hello)

* [Running your first {{site.data.keyword.codeengineshort}} job](/docs/codeengine?topic=codeengine-getting-started#first-job)

* [Running your first function](/docs/codeengine?topic=codeengine-getting-started#first-function)

* [Building your first container image from source code](/docs/codeengine?topic=codeengine-getting-started#build-image-gs)

* [Next steps for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-getting-started#nextsteps-getstart)


## About workloads
{: #sitemap_about_workloads}


[Learn about {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about#about)

* [Benefits of {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about#benefits)

* [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology)

[Application workloads](/docs/codeengine?topic=codeengine-ceapplications#ceapplications)

* [What are application workloads?](/docs/codeengine?topic=codeengine-ceapplications#ceapp-workloads)

* [How do apps compare to jobs and functions?](/docs/codeengine?topic=codeengine-ceapplications#ceapp-workloads-compare)

* [What are the key features of working with {{site.data.keyword.codeengineshort}} applications?](/docs/codeengine?topic=codeengine-ceapplications#ceapp-features)

    * [Isolation](/docs/codeengine?topic=codeengine-ceapplications#ceapp-isolation)

    * [Logging](/docs/codeengine?topic=codeengine-ceapplications#ceapp-logging)

    * [Running applications](/docs/codeengine?topic=codeengine-ceapplications#ceapp-runapp)

    * [Scaling](/docs/codeengine?topic=codeengine-ceapplications#ceapp-scaling)

    * [Security](/docs/codeengine?topic=codeengine-ceapplications#ceapp-security)

    * [Triggering applications with events](/docs/codeengine?topic=codeengine-ceapplications#ceapp-eventing)

    * [Visibility](/docs/codeengine?topic=codeengine-ceapplications#ceapp-visibility)

* [How can I get started with applications?](/docs/codeengine?topic=codeengine-ceapplications#ceapp-getstart)

[Batch job workloads](/docs/codeengine?topic=codeengine-cebatchjobs#cebatchjobs)

* [What are batch job workloads?](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-workloads)

    * [What is the lifecycle of a batch job?](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-lifecycle)

* [How do jobs compare to apps and functions?](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-compare)

* [What are the key features of working with {{site.data.keyword.codeengineshort}} batch jobs?](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-features)

    * [Isolation](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-isolation)

    * [Logging](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-logs)

    * [Queuing](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-queue)

    * [Retries](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-retries)

    * [Running batch jobs](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-run)

    * [Scaling](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-scaling)

    * [Status](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-status)

    * [Submitting similar batch jobs](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-reuse)

    * [Triggering batch jobs with events](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-eventing)

* [How can I get started with batch jobs?](/docs/codeengine?topic=codeengine-cebatchjobs#batchjob-getstart)

[Function workloads](/docs/codeengine?topic=codeengine-cefunctions#cefunctions)

* [Lifecycle of a function instance](/docs/codeengine?topic=codeengine-cefunctions#functions-lifecycle)

* [How do functions compare to apps and jobs?](/docs/codeengine?topic=codeengine-cefunctions#functions-work-compare)

* [What are key features of working with functions?](/docs/codeengine?topic=codeengine-cefunctions#functions-work-ce)

    * [Isolation](/docs/codeengine?topic=codeengine-cefunctions#cefun-isolation)

    * [Logging](/docs/codeengine?topic=codeengine-cefunctions#functions-logging)

    * [Runtimes](/docs/codeengine?topic=codeengine-cefunctions#functions-runtime)

    * [Running functions](/docs/codeengine?topic=codeengine-cefunctions#cefun-runfun)

    * [Security](/docs/codeengine?topic=codeengine-cefunctions#cefun-security)

    * [Invocation concurrency and scaling of function instances](/docs/codeengine?topic=codeengine-cefunctions#functions-concur-ce)

    * [Packaging your source code for a function](/docs/codeengine?topic=codeengine-cefunctions#functions-packaging)

* [How can I get started with functions?](/docs/codeengine?topic=codeengine-cefunctions#cefun-getstart)


## Release notes for {{site.data.keyword.codeengineshort}}
{: #sitemap_release_notes_for_}


[Release notes for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-relnotes)

* [December 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-december24)

    * [05 December 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-december0524)

        * CLI version 1.50.8 released

* [November 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-november24)

    * [21 November 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-november2124)

        * Updated SDK versions with support for allowed outbound destinations

    * [14 November 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-november1424)

        * CLI version 1.50.7 released

        * Updated versions for buildpacks

    * [05 November 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-november0524)

        * CLI version 1.50.6 released

* [October 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-october24)

    * [28 October 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-october2824)

        * CLI version 1.50.5 released

    * [24 October 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-october2424)

        * Updated versions for buildpacks

    * [10 October 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-october1024)

        * Terraform support for {{site.data.keyword.codeengineshort}} functions is generally available

    * [03 October 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-october0324)

        * Updated SDK versions with support for functions

* [September 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-september24)

    * [12 September 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-september1224)

        * CLI version 1.50.4 released

* [August 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-august24)

    * [23 August 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-august2324)

        * CLI version 1.50.3 released

    * [16 August 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-august1624)

        * Updated information about supported versions of Knative

* [July 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-july24)

    * [11 July 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-july1124)

        * CLI version 1.50.1 released

        * Updated versions for buildpacks

* [June 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-june24)

    * [06 June 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-june0624)

        * CLI version 1.50.0 released

        * Updated versions for buildpacks

* [May 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may24)

    * [24 May 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may2424)

        * CLI version 1.49.12 released

    * [17 May 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1724)

        * CLI version 1.49.11 released

        * Updated information about supported versions of Knative

        * Added support for functions in the {{site.data.keyword.codeengineshort}} V2 API

* [April 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr24)

    * [25 April 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2524)

        * CLI version 1.49.10 released

    * [18 April 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1824)

        * CLI version 1.49.9 released

    * [11 April 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1124)

        * CLI version 1.49.8 released

* [March 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar24)

    * [21 March 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2124)

        * CLI version 1.49.7 released

        * Updated the value of `CE_API_BASE_URL` environment variable from `CE_API_BASE_URL=https://api.private.us-south.codeengine.cloud.ibm.com/` to `CE_API_BASE_URL=https://api.us-south.codeengine.cloud.ibm.com/` for applications and jobs

        * Updated the default value for the `--max-scale` option on the **`app update`** command

    * [14 March 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1424)

        * CLI version 1.49.6 released

    * [11 March 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1124)

        * Added `CE_REGION`, `CE_PROJECT`, and `CE_API_BASE_URL` environment variables for functions

* [February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb24)

    * [27 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2724)

        * Added `CE_REGION`, `CE_PROJECT`, and `CE_API_BASE_URL` environment variables for applications and jobs

    * [22 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2224)

        * CLI version 1.49.5 released

    * [20 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2024)

        * Updated versions for buildpacks

    * [16 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1624)

        * Updated the user experience for working with jobs and job runs in the console

        * Added more information about functions in {{site.data.keyword.codeengineshort}}

        * Updated behavior change for image builds that are built with Cloud Native Buildpacks

    * [14 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1424)

        * Added the `ibm_codeengine_job_name` attribute to the `ibm_codeengine_jobruns` metric for monitoring job runs in {{site.data.keyword.codeengineshort}}

    * [09 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0924)

        * New region!

    * [05 February 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0524)

        * CLI version 1.49.4 released

        * Added troubleshooting information about displaying limits and current usage with the CLI

        * The `Build` and `BuildRun` Kubernetes API objects are available in a new version

* [January 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan24)

    * Review the release notes for January 2024.

    * [30 January 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan3024)

        * Added support for the `build` and `buildrun` properties for jobs in the {{site.data.keyword.codeengineshort}} V2 API

    * [25 January 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2524)

        * CLI version 1.49.3 released

    * [22 January 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2224)

        * Updated the user experience for making configuration changes to apps in the console

        * Updated the user experience for creating secrets and configmaps in the console

    * [12 January 2024](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1224)

        * CLI version 1.49.2 released

        * Added support for the `scale_array_size_variable_override` property for job runs in the {{site.data.keyword.codeengineshort}} V2 API

* [December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec23)

    * Review the release notes for December 2023.

    * [12 December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1223)

        * Added information about testing functions locally

        * Added troubleshooting information for builds with Dockerfiles

        * Updated versions for buildpacks

    * [07 December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec023)

        * Added support for applications with gRPC

    * [06 December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0623)

        * CLI version 1.49.1 released

    * [05 December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0523)

        * Updated versions for buildpacks

    * [01 December 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0123)

        * Added support for providing a custom value to the `JOB_ARRAY_SIZE` environment variable

        * CLI version 1.49.0 released

* [November 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov23)

    * Review the release notes for November 2023.

    * [16 November 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1623)

        * Updated support for multi-domain or wildcard certificates for custom domain mappings

    * [13 November 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1323)

        * Updated versions for buildpacks

    * [09 November 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov0923)

        * Added `xxlarge` size for builds

        * CLI version 1.48.0 released

        * Updated information about adding authentication and authorization capabilities, and rotating TLS certificates for security

        * Added information about a new project details page in the console

        * Added troubleshooting information for app connectivity when using a proxy

        * Added troubleshooting information for expired SSH keys during a build

    * [03 November 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov0323)

        * Added FAQ about access for roles that are applied to {{site.data.keyword.codeengineshort}} entities are scoped within a {{site.data.keyword.codeengineshort}} project

        * Added troubleshooting information for creating an allowlist for {{site.data.keyword.codeengineshort}} functions

        * Added support for domain mappings in the {{site.data.keyword.codeengineshort}} V2 API

* [October 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct23)

    * Review the release notes for October 2023.

    * [30 October 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct3023)

        * Updated versions for buildpacks

    * [19 October 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1923)

        * Added information about additional support for functions in {{site.data.keyword.codeengineshort}}

        * CLI version 1.47.1 released

        * Added troubleshooting information about receiving `ECONNRESET` errors

        * Added information about controlling access to {{site.data.keyword.registryshort}} for {{site.data.keyword.codeengineshort}} workloads

        * Updated information about supported versions of Knative

        * Updated information about custom domain mappings with {{site.data.keyword.codeengineshort}} apps

    * [09 October 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0923)

        * CLI version 1.46.1 released

    * [05 October 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0523)

        * Updated versions for buildpacks

* [September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep23)

    * Review the release notes for September 2023.

    * [27 September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2723)

        * Added support for liveness and readiness probes for applications in the {{site.data.keyword.codeengineshort}} V2 API

    * [21 September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2123)

        * Added support for liveness and readiness probes for applications in {{site.data.keyword.codeengineshort}}

        * CLI version 1.46.0 released

        * Added troubleshooting information for toolchain

        * Added getting started information about working with the {{site.data.keyword.codeengineshort}} CLI

    * [19 September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1923)

        * Updated versions for buildpacks

    * [12 September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1223)

        * CLI version 1.45.4 released

        * Updated versions for buildpacks

    * [07 September 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0723)

        * Updated {{site.data.keyword.codeengineshort}} architecture diagram

* [August 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug23)

    * Review the release notes for August 2023.

    * [29 August 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug2923)

        * Updated versions for buildpacks

        * Added getting started information about working with the {{site.data.keyword.codeengineshort}} API

    * [17 August 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1723)

        * Added troubleshooting information about how to verify a container image reference

    * [10 August 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1023)

        * Added troubleshooting information about application restarts

        * Added troubleshooting information about open ports on an endpoint for a {{site.data.keyword.codeengineshort}} component

        * Added troubleshooting information about jobs that run indefinitely, but don't automatically restart

        * Added information about an approach for processing many files by running jobs

* [July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul23)

    * Review the release notes for July 2023.

    * [26 July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2623)

        * Updated versions for buildpacks

        * CLI version 1.45.3 released

    * [20 July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2023)

        * Added support for displaying details of app instances

        * Added troubleshooting information about app instances that do not scale down as expected

    * [19 July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul1923)

        * Updated environment variable information to include functions

        * Terraform support for {{site.data.keyword.codeengineshort}} service bind is generally available

        * CLI version 1.45.2 released

    * [06 July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul0623)

        * Updated {{site.data.keyword.codeengineshort}} getting started information to include functions

        * Added information comparing {{site.data.keyword.codeengineshort}} apps, jobs, and functions

        * Updated versions for buildpacks

        * CLI version 1.45.1 released

    * [05 July 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul0523)

        * Added support for the scale-down delay autoscaling option in the console

        * Added information about details to provide when you report a support case

* [June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun23)

    * Review the release notes for June 2023.

    * [29 June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun2923)

        * New! Support for functions in {{site.data.keyword.codeengineshort}}

        * CLI version 1.45.0 released

    * [23 June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun2323)

        * Added summary information for getting started with apps and batch jobs in {{site.data.keyword.codeengineshort}}

        * Added support for the scale-down delay autoscaling option

        * CLI version 1.44.0 released

        * Added support for service binding operations in the {{site.data.keyword.codeengineshort}} V2 API

        * Updated versions for buildpacks

    * [13 June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1323)

        * Added troubleshooting information about deleting jobs and job runs when the limit is exceeded

        * Updated versions for buildpacks

    * [08 June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0823)

        * CLI version 1.43.7 released

    * [01 June 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0123)

        * Added troubleshooting information about stopping an app from receiving traffic

        * Updated information about working with multi-line log data

* [May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may23)

    * Review the release notes for May 2023.

    * [30 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may3023)

        * Added support to get status details for a project in the {{site.data.keyword.codeengineshort}} V2 API

    * [25 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may2523)

        * Updated versions for buildpacks

        * Updated information about DDoS protection in {{site.data.keyword.codeengineshort}}

        * Added troubleshooting information for app connectivity

        * Updated information about applying filters on {{site.data.keyword.la_short}} data

    * [18 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1823)

        * Added troubleshooting information for job runs not starting

        * Added troubleshooting information for unavailable details of service binding operations

    * [16 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1623)

        * CLI version 1.43.5 released

        * Updated versions for buildpacks

    * [10 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1023)

        * Terraform support for {{site.data.keyword.codeengineshort}} is generally available

    * [05 May 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may0523)

        * Updated versions for buildpacks

* [April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr23)

    * Review the release notes for April 2023.

    * [27 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2723)

        * CLI version 1.43.4 released

        * Updated versions for buildpacks

    * [26 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2623)

        * Added support for {{site.data.keyword.codeengineshort}} project-wide settings

        * Updated support for TLS secrets

        * Added troubleshooting information for creating an allowlist for {{site.data.keyword.codeengineshort}} apps and jobs

        * Added troubleshooting information for deploying a Python app

    * [19 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1923)

        * Configuring a highly available application tutorial

        * Updated versions for buildpacks

    * [14 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1423)

        * CLI version 1.43.3 released

    * [12 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1223)

        * CLI version 1.43.1 released

        * Updated versions for buildpacks

    * [05 April 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr0523)

        * Updated versions for buildpacks

* [March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar23)

    * Review the release notes for March 2023.

    * [30 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar3023)

        * Added information about troubleshooting images

        * Added information about troubleshooting toolchains

        * Updated documentation for API V2.0

    * [27 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2723)

        * Terraform support for {{site.data.keyword.codeengineshort}} beta release

    * [23 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2323)

        * CLI version 1.43.0 released

        * Added support for managing domain mappings with the CLI

        * Updated versions for buildpacks

    * [16 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1623)

        * CLI version 1.42.0 released

        * Updated support for secrets in the CLI

    * [10 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1023)

        * Added troubleshooting information for why apps stop running

        * Updated versions for buildpacks

    * [02 March 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0223)

        * CLI version 1.41.3 released

* [February 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb23)

    * Review the release notes for February 2023.

    * [23 February 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2323)

        * Important: Project limits for resources in a {{site.data.keyword.codeengineshort}} project is increased

        * CLI version 1.41.2 released

        * Updated versions for buildpacks

    * [17 February 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1723)

        * Added FAQ for Migrating your Cloud Foundry app

        * Updated troubleshooting information for apps that don't achieve a ready status

        * Updated versions for buildpacks

        * CLI version 1.41.1 released

    * [09 February 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0923)

        * Added information about troubleshooting job runs

        * CLI version 1.41.0 released

    * [03 February 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0323)

        * Added information about troubleshooting service bindings

        * CLI version 1.40.8 released

        * Updated versions for buildpacks

* [January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan23)

    * Review the release notes for January 2023.

    * [27 January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2723)

        * Updated SDK versions

    * [26 January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2623)

        * {{site.data.keyword.codeengineshort}} supports service endpoints

        * CLI version 1.40.7 released

        * Updated versions for buildpacks

    * [24 January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2423)

        * Added information about using {{site.data.keyword.codeengineshort}} with a toolchain

    * [20 January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2023)

        * CLI version 1.40.6 released

        * Updated support for service bindings from the console, which provides more options for configuring service bindings

    * [12 January 2023](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1223)

        * CLI version 1.40.5 released

        * Updated versions for buildpacks

        * Added information about supported versions of Knative

* [December 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec22)

    * Review the release notes for December 2022.

    * [14 December 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1422)

        * CLI version 1.40.4 released

        * Updated versions for buildpacks

        * Added information about environment variables for jobs

    * [07 December 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0722)

        * Added GitHub tutorial for sending events

        * Added migration tutorial for Heroku apps

        * Added information about supported TLS versions and ciphers

        * CLI version 1.40.3 released

        * Updated versions for buildpacks

    * [01 December 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0122)

        * CLI version 1.40.2 released

        * Updated versions for buildpacks

* [November 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov22)

    * Review the release notes for November 2022.

    * [17 November 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1722)

        * Added more information about certificates and considerations when you use {{site.data.keyword.cis_short}} with custom domain mappings

        * Updated versions for buildpacks

    * [10 November 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1022)

        * CLI version 1.40.1 released

    * [03 November 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov0322)

        * Added support for custom domain mappings

* [October 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct22)

    * Review the release notes for October 2022.

    * [27 October 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct2722)

        * CLI version 1.40.0 released

        * Updated support of ephemeral storage for apps and jobs

        * Updated versions for buildpacks

    * [20 October 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct2022)

        * CLI version 1.39.6 released

        * Revised and improved descriptions of metrics for monitoring {{site.data.keyword.codeengineshort}}

        * Updated versions for buildpacks

    * [17 October 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1722)

        * Updated versions for buildpacks

    * [06 October 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0622)

        * CLI version 1.39.5 released

        * Updated versions for buildpacks

* [September 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep22)

    * Review the release notes for September 2022.

    * [21 September 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2122)

        * New tutorial

        * Updated versions for buildpacks

    * [15 September 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1522)

        * CLI version 1.39.3 released

        * Updated versions for buildpacks

* [August 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug22)

    * Review the release notes for August 2022.

    * [31 August 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug3122)

        * CLI version 1.39.2 released

        * Updated versions for buildpacks

    * [18 August 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1822)

        * CLI version 1.39.1 released

        * Added support for working with service bindings from the console

        * Updated the default maximum execution time for jobs

        * Updated versions for buildpacks

    * [4 August 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug0422)

        * CLI version 1.38.2 released

        * New tutorial

        * Updated versions for buildpacks

* [July 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul22)

    * Review the release notes for July 2022.

    * [29 July 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2922)

        * CLI version 1.38.1 released

        * Updated CPU and memory limits and maximums for jobs and apps

        * Added support for jobs that can run indefinitely

        * Updated versions for buildpacks

    * [21 July 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2122)

        * CLI version 1.38.0 released

    * [15 July 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul1522)

        * CLI version 1.37.0 released

    * [8 July 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul722)

        * New! Context-based restrictions for {{site.data.keyword.codeengineshort}}

        * Updated versions for buildpacks

* [June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun22)

    * Review the release notes for June 2022.

    * [30 June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun3022)

        * New! Tutorial for how to subscribe to Kafka events with {{site.data.keyword.codeengineshort}}

    * [24 June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun2422)

        * CLI version 1.36.0 released

        * Added support for Kafka event subscriptions with the console and CLI

    * [16 June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1622)

        * CLI version 1.35.0 released

        * Updated versions for buildpacks

    * [09 June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0922)

        * CLI version 1.34.0 released

    * [02 June 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0222)

        * CLI version 1.33.1 released

        * Updated available metrics for monitoring {{site.data.keyword.codeengineshort}}

        * Revised and improved topic organization of {{site.data.keyword.codeengineshort}} limits and quotas

* [May 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may22)

    * Review the release notes for May 2022.

    * [26 May 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may2622)

        * CLI version 1.33.0 released

        * Updated versions for buildpacks

    * [19 May 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1922)

        * CLI version 1.32.0 released

        * Added more information about access authorities for image registries

    * [12 May 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1222)

        * CLI version 1.31.1 released

    * [05 May 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may0522)

        * CLI version 1.31.0 released

        * Added new FAQ topics to Migrating Cloud Foundry information

        * Updated versions for buildpacks

* [April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr22)

    * Review the release notes for April 2022.

    * [29 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2922)

        * Updated versions for buildpacks

    * [27 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2722)

        * New! Deploying apps and running jobs with {{site.data.keyword.codeengineshort}} is even easier!

        * CLI version 1.30.0 released

    * [21 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2122)

        * CLI version 1.29.4 released

        * Updated versions for buildpacks

    * [14 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1422)

        * CLI version 1.29.3 released

    * [12 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1222)

        * CLI version 1.29.2 released

        * New! Tutorial for creating a serverless web application with {{site.data.keyword.codeengineshort}}

    * [7 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr0722)

        * CLI version 1.29.1 released

    * [1 April 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr0122)

        * New! Tutorials for migrating Cloud Foundry apps to {{site.data.keyword.codeengineshort}}

        * CLI version 1.29.0 released

* [March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar22)

    * Review the release notes for March 2022.

    * [31 March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar3122)

        * Review the release notes for 31 March 2022.

        * New region!

    * [23 March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2322)

        * Review the release notes for 23 March 2022.

        * CLI version 1.28.1 released

    * [18 March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1822)

        * Review the release notes for 18 March 2022.

        * CLI version 1.28.0 released

        * Added information about registry access secret types

        * Added information about setting max-scale = 0

        * Updated versions for buildpacks

    * [04 March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0422)

        * Review the release notes for 04 March 2022.

        * CLI version 1.27.1 released

    * [02 March 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0222)

        * Review the release notes for 02 March 2022.

        * CLI version 1.27.0 released

        * Improved service binding implementation

* [February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb22)

    * Review the release notes for February 2022.

    * [24 February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2422)

        * Review the release notes for 24 February 2022.

        * CLI version 1.26.1 released

    * [22 February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2222)

        * Review the release notes for 22 February 2022.

        * New region!

    * [17 February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1722)

        * Review the release notes for 17 February 2022.

        * CLI version 1.26.0 released

        * Updated versions for buildpacks

    * [10 February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1022)

        * Review the release notes for 10 February 2022.

        * CLI version 1.25.4 released

    * [03 February 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0322)

        * Review the release notes for 03 February 2022.

        * CLI version 1.25.3 released

* [January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan22)

    * Review the release notes for January 2022.

    * [27 January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2722)

        * Review the release notes for 27 January 2022.

        * CLI version 1.25.2 released

        * Added more information for troubleshooting jobs when job runs do not complete

        * Added information about considerations when you use SSH keys for accessing your source repository

    * [20 January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2022)

        * Review the release notes for 20 January 2022.

        * CLI version 1.25.0 released

        * Added information about considerations for HTTP handling with {{site.data.keyword.codeengineshort}} apps and jobs

    * [14 January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1422)

        * Review the release notes for 14 January 2022

        * Added clarification for use of direct endpoints when you use private networking with services such as {{site.data.keyword.cos_full_notm}}

    * [13 January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1322)

        * Review the release notes for 13 January 2022.

        * CLI version 1.24.0 released

    * [12 January 2022](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1222)

        * Review the release notes for 12 January 2022.

        * Sample images are stored in {{site.data.keyword.registrylong}}

        * Updated versions for buildpacks

* [December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec21)

    * Review the release notes for December 2021.

    * [15 December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1521)

        * Review the release notes for 15 December 2021.

        * CLI version 1.23.3 released

    * [14 December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1421)

        * Review the release notes for 14 December 2021.

        * New region!

    * [08 December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0821)

        * Review the release notes for 08 December 2021.

        * {{site.data.keyword.codeengineshort}} supports monitoring security and compliance with {{site.data.keyword.compliance_long}}.

    * [06 December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0621)

        * Review the release notes for 06 December 2021.

        * {{site.data.keyword.cos_full_notm}} subscriptions

        * Updated versions for buildpacks

    * [01 December 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0121)

        * Review the release notes for 01 December 2021.

        * CLI version 1.23.2 released

* [November 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov21)

    * Review the release notes for November 2021.

    * [19 November 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1921)

        * Review the release notes for 19 November 2021.

        * CLI version 1.23.1 released

    * [16 November 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1621)

        * Review the release notes for 16 November 2021.

        * {{site.data.keyword.codeengineshort}} supports virtual private endpoints

        * CLI version 1.23.0 released

        * Updated versions for buildpacks

    * [04 November 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov0421)

        * Review the release notes for 04 November 2021.

        * CLI version 1.22.0 released

        * {{site.data.keyword.codeengineshort}} is integrated with {{site.data.keyword.compliance_long}}

        * Updated versions for buildpacks

* [October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct21)

    * Review the release notes for October 2021.

    * [28 October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct2821)

        * Review the release notes for 28 October 2021.

        * CLI version 1.21.1 released

        * {{site.data.keyword.cos_full_notm}} subscriptions

        * Added Python as a supported language for builds that use the Cloud Native Buildpacks strategy

        * Updated versions for buildpacks

    * [21 October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct2121)

        * Review the release notes for 21 October 2021.

        * CLI version 1.21.0 released

    * [15 October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1521)

        * Review the release notes for 15 October 2021.

        * Added support for deploying apps with project-only endpoints

        * Added information about creating custom dashboards to monitor {{site.data.keyword.codeengineshort}} workloads

    * [07 October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0721)

        * Review the release notes for 07 October 2021.

        * Creating builds no longer requires a value for the source branch

        * CLI version 1.20.1 released

    * [04 October 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0421)

        * Review the release notes for 04 October 2021.

        * Revised and improved the application configuration pages in the console

        * CLI version 1.20.0 released

* [September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep21)

    * Review the release notes for September 2021.

    * [23 September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2321)

        * Review the release notes for 23 September 2021.

        * CLI version 1.19.1 released

    * [16 September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1621)

        * Review the release notes for 16 September 2021.

        * CLI version 1.19.0 released

        * Updated the Dockerfile build strategy to use the BuildKit tool

    * [9 September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0921)

        * Review the release notes for 9 September 2021.

        * CLI version 1.18.0 released

        * Updated versions for buildpacks

        * Updated information about the roles that are required for using Kubernetes and Knative with {{site.data.keyword.codeengineshort}}

    * [2 September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0221)

        * Review the release notes for 2 September 2021.

        * Added support for build logs in the {{site.data.keyword.codeengineshort}} console

        * Updated information about `reclamation` commands

    * [1 September 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0121)

        * Review the release notes for 1 September 2021.

        * CLI version 1.17.0 released

        * Added support for Periodic timer (cron) event producers in the {{site.data.keyword.codeengineshort}} console

        * Updated versions for buildpacks

* [August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug21)

    * Review the release notes for August 2021.

    * [24 August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug2421)

        * Review the release notes for 24 August 2021.

        * CLI version 1.16.1 released

    * [19 August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1921)

        * Review the release notes for 19 August 2021.

        * CLI version 1.16.0 released

        * Secrets

        * Updated information about headers and environment variables when you use subscriptions

        * Updated versions for buildpacks

    * [16 August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1621)

        * Review the release notes for 16 August 2021.

        * CLI version 1.15.0 released

        * Troubleshooting subscriptions

        * Subscriptions for {{site.data.keyword.cos_full_notm}} event producers are not available in the Canada Toronto (`ca-tor`) region

        * Updated versions for buildpacks

    * [6 August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug0621)

        * Review the release notes for 6 August 2021.

        * CLI version 1.14.0 released

        * Private repositories

    * [5 August 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug0521)

        * Review the release notes for 5 August 2021.

        * Updated versions for buildpacks

* [July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul21)

    * Review the release notes for July 2021.

    * [30 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul3021)

        * Review the release notes for 30 July 2021.

        * CLI version 1.13.0 released

    * [29 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2921)

        * Review the release notes for 29 July 2021.

        * Deleting projects

        * Updated versions for buildpacks

    * [27 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2721)

        * Review the release notes for 27 July 2021.

        * CLI version 1.12.0 released

        * Added overview topics for deploying apps and running jobs

        * Updated versions for buildpacks

    * [20 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2021)

        * Review the release notes for 20 July 2021.

        * New region!

    * [15 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul1521)

        * Review the release notes for 15 July 2021.

        * CLI version 1.11.0 released

        * Subscription ping limits

        * Applications that use WebSockets

        * Updated versions for buildpacks

    * [7 July 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul0721)

        * Review the release notes for 7 July 2021.

        * Environment variables

        * Troubleshooting overview topics

        * {{site.data.keyword.cos_short}} buckets

* [June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun21)

    * Review the release notes for June 2021.

    * [30 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun3021)

        * Review the release notes for 30 June 2021.

        * Iter8 tutorial

        * Updated versions for buildpacks

    * [29 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun2921)

        * Review the release notes for 29 June 2021.

        * Application revisions

        * Job runs that are created by subscriptions

    * [23 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun2321)

        * Review the release notes for 23 June 2021.

        * CLI version 1.10.0 released

        * Updated app and app revision quotas for projects

        * Added basic troubleshooting information

        * {{site.data.keyword.cloud_notm}} and third-party integrations

        * Added information about security and {{site.data.keyword.codeengineshort}}

        * Updated versions for buildpacks

    * [16 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1621)

        * Review the release notes for 16 June 2021.

        * CLI version 1.9.0 released

        * Build size

        * Configmaps and secrets

        * Added information about updating jobs

    * [10 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1021)

        * Review the release notes for 10 June 2021.

        * Important: Introduced a breaking change with {{site.data.keyword.codeengineshort}} memory and CPU combinations

        * CLI version 1.8.0 released

        * Running job without job configuration

        * Added support for private repositories from the console

        * Updated versions for buildpacks

        * Subscription support for jobs is generally available

    * [8 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0821)

        * Review the release notes for 8 June 2021.

        * New region!

    * [3 June 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun0321)

        * Review the release notes for 3 June 2021.

        * Updated versions for buildpacks

        * Deleting data

* [May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may21)

    * Review the release notes for May 2021.

    * [27 May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may2721)

        * Review the release notes for 27 May 2021.

        * CLI version 1.7.0 released

        * Updated versions for buildpacks

        * Updated information about supported {{site.data.keyword.cos_full_notm}} buckets for subscriptions

        * Added information about specifying the `--path` option when you create a subscription to an application.

        * Updated information about accessing container registries

        * Added information about working with Kubernetes and {{site.data.keyword.codeengineshort}}

    * [18 May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1821)

        * Review the release notes for 18 May 2021.

        * Added information about working with environment variables in {{site.data.keyword.codeengineshort}}

        * Working with secrets and configmaps

        * CLI version 1.6.0 released

    * [10 May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1021)

        * Review the release notes for 10 May 2021.

        * CLI version 1.5.0 released

    * [7 May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may0721)

        * Review the release notes for 7 May 2021.

        * Updated versions for buildpacks

    * [4 May 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may0421)

        * Review the release notes for 4 May 2021.

        * New region!

* [April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr21)

    * Review the release notes for April 2021.

    * [29 April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2921)

        * Review the release notes for 29 April 2021.

        * Added metrics for `jobruns` to information about monitoring in {{site.data.keyword.codeengineshort}}.

        * CLI version 1.4.0 released

    * [21 April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr2121)

        * Review the release notes for 21 April 2021.

        * `CloudEvents` specification

        * CLI version 1.3.0 released

    * [14 April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr1421)

        * Review the release notes for 14 April 2021.

        * New! Subscription support for jobs as a beta function.

        * Project limits

        * Project deletions

        * CLI version 1.2.0 released

    * [8 April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr0821)

        * Review the release notes for 8 April 2021.

        * Learning paths

        * Pending reclamation

        * Environment variables

        * CLI version 1.1.0 released

    * [1 April 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-apr0121)

        * Review the release notes for 1 April 2021.

        * Added information about deploying apps across multiple regions that use a custom domain name.

        * CLI version 1.0.1 released

* [March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar21)

    * Review the release notes for March 2021.

    * [31 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar3121)

        * Review the release notes for 31 March 2021.

        * New! General availability of {{site.data.keyword.codeenginefull_notm}}

        * CLI version 1.0.0 released

    * [30 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar3021)

        * Review the release notes for 30 March 2021.

        * Updated information about setting the `port` value when you deploy apps

        * Updated information about application scaling when apps connect to event producers

    * [26 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2621)

        * Review the release notes for 26 March 2021.

        * CLI versions 0.6.2 and CLI 0.6.3 released

        * Added {{site.data.keyword.codeengineshort}} billing.

        * Updated CPU and memory limits for jobs and apps

    * [25 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2521)

        * Review the release notes for 25 March 2021.

        * Added {{site.data.keyword.codeengineshort}} monitoring information

        * Added information for determining CPU and memory combinations

        * {{site.data.keyword.codeengineshort}} Tutorial

    * [23 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2321)

        * Review the release notes for 23 March 2021.

        * {{site.data.keyword.codeengineshort}} is supported in a new region: Asia Pacific (`jp-tok`)

        * Added {{site.data.keyword.codeengineshort}} high availability and disaster recovery documentation

    * [22 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar2221)

        * Review the release notes for 22 March 2021.

        * CLI version 0.6.1 releases

    * [18 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar1821)

        * Review the release notes for 18 March 2021.

        * CLI versions 0.6.0 and 0.5.25 released

        * Automatically create registry access

        * Added logging information for apps and jobs from the console

        * Updated versions for buildpacks

        * Updated limits for {{site.data.keyword.codeengineshort}}

        * Updated API CRD information for subscriptions and jobs

        * [Using Kubernetes with {{site.data.keyword.codeengineshort}} - Serving CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-serving).

        * Updated information for troubleshooting your builds

        * Updated service bind information

    * [9 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0921)

        * Review the release notes for 9 March 2021.

        * CLI version 0.5.21 released

        * Project reclamation

    * [4 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0421)

        * Review the release notes for 4 March 2021.

        * Added {{site.data.keyword.codeengineshort}} architecture and workload isolation documentation

        * Added HTTP headers and body information for subscriptions

        * System events

        * Updated versions for buildpacks

    * [2 March 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-mar0221)

        * Review the release notes for 2 March 2021.

        * CLI version 0.5.20 released

        * New responsibilities for {{site.data.keyword.codeengineshort}} topic.

* [February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb21)

    * Review the release notes for February 2021.

    * [26 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2621)

        * Review the release notes for 26 February 2021.

        * Commands and arguments

        * Updated versions for buildpacks

        * CLI version 0.5.19 released

        * Added notices file

    * [23 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb2321)

        * Review the release notes for 23 February 2021.

        * CLI version 0.5.18 released

    * [16 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1621)

        * Review the release notes for 16 February 2021.

        * CLI version 0.5.17 released

    * [12 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb1221)

        * Review the release notes for 12 February 2021.

        * Added an {{site.data.keyword.cos_short}} subscription tutorial.

        * Added troubleshooting information for subscriptions.

        * Added an FAQ for WebSocket support.

        * Updated application limits.

    * [9 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0921)

        * Review the release notes for 9 February 2021.

        * CLI version 0.5.16 released

        * Added information about potentially reaching Docker rate limits.

    * [3 February 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-feb0321)

        * Review the release notes for 3 February 2021.

        * Added planning for {{site.data.keyword.codeengineshort}} information

        * Added information about working with configmaps and secrets as mounted files

        * Updated FAQ to add information about differences between {{site.data.keyword.codeengineshort}} builds and Docker builds

        * Added a tip for when you copy an entire Git repository and note about best practices for naming application directories

* [January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan21)

    * Review the release notes for January 2021.

    * [29 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2921)

        * Review the release notes for 29 January 2021.

        * CLI version 0.5.15 released

        * Environment variables

        * Revised subscription topic

        * Ping subscription tutorial

        * Getting support

    * [21 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2121)

        * Review the release notes for 21 January 2021.

        * CLI version 0.5.14 released

    * [20 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan2021)

        * Review the release notes for 20 January 2021.

        * New region!

        * Removed some beta limitations for Code Engine

    * [15 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1521)

        * Review the release notes for 15 January 2021.

        * Added a build tutorial

        * Take a terminology quiz

        * Added a sitemap of {{site.data.keyword.codeengineshort}} topics

        * CLI version 0.5.13 released

    * [12 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan1221)

        * Review the release notes for 12 January 2021.

        * Updated information for troubleshooting your builds

        * New Activity tracker information

        * Updated build information

        * Added API CRD information for subscriptions

        * Updated task information for jobs

        * CLI version 0.5.11 and 0.5.12 released

    * [7 January 2021](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jan0721)

        * Review the release notes for 7 January 2021.

        * Updated task information for applications

* [December 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec20)

    * Review the release notes for December 2020.

    * [17 December 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1720)

        * Review the release notes for 17 December 2020.

        * Updated information for troubleshooting your builds

        * Updated versions for buildpacks

        * Updated sizes for builds

        * CLI versions 0.5.8 and 0.5.9 released

    * [14 December 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec1420)

        * Review the release notes for 14 December 2020.

        * Learn more about scaling your applications

        * CLI version 0.5.7 released

    * [9 December 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0920)

        * Review the release notes for 9 December 2020.

        * Find Dockerfile build tips

        * See [Writing a Dockerfile for Code Engine](/docs/codeengine?topic=codeengine-dockerfile).

        * Updated troubleshooting tips for builds

        * Updated versions for buildpacks

        * CLI version 0.5.6 released

    * [2 December 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-dec0220)

        * Review the release notes for 2 December 2020.

        * CLI version 0.5.5 released

* [November 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov20)

    * Review the release notes for November 2020.

    * [30 November 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov3020)

        * Review the release notes for 30 November 2020.

        * Updated user access information

    * [20 November 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov2020)

        * Review the release notes for 20 November 2020.

        * CLI version 0.5.3 released

        * New logging topic

        * Tips for troubleshooting applications

    * [12 November 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1220)

        * Review the release notes for 12 November 2020.

        * CLI version 0.4.2592 released

    * [11 November 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-nov1120)

        * Review the release notes for 11 November 2020.

        * CLI version 0.4.2577 released

        * SDK documentation published

* [October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct20)

    * Review the release notes for October 2020.

    * [30 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct3020)

        * Review the release notes for 30 October 2020.

        * CLI version 0.4.2493 released

        * Lithops

    * [23 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct2320)

        * Review the release notes for 23 October 2020.

        * CLI version 0.4.2439 released

        * Project selected for current context

        * Updated runtimes for buildpacks

    * [19 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1920)

        * Review the release notes for 19 October 2020.

        * Troubleshooting build information

    * [15 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1520)

        * Review the release notes for 15 October 2020.

        * CLI version 0.4.2397 released

    * [14 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct1420)

        * Review the release notes for 14 October 2020.

        * New troubleshooting information

    * [6 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0620)

        * Review the release notes for 6 October 2020

        * CLI version 0.4.2365 released

    * [5 October 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-oct0520)

        * Review the release notes for 5 October 2020.

        * CLI version 0.4.2335 released

* [September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep20)

    * Review the release notes for September 2020.

    * [28 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2820)

        * Review the release notes for 28 September 2020.

        * CLI version 0.4.2276 released

    * [24 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2420)

        * Review the release notes for 24 September 2020.

        * New tutorial

    * [21 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep2120)

        * Review the release notes for 21 September 2020.

        * CLI version 0.4.2227 released

        * Updated runtimes for buildpacks

    * [18 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1820)

        * Review the release notes for 18 September 2020.

        * CLI version 0.4.2217 released

    * [16 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep1620)

        * Review the release notes for 16 September 2020.

        * New! [{{site.data.keyword.codeenginefull_notm}} beta release](https://cloud.ibm.com/codeengine/overview)

        * CLI version 0.4.2192 released

    * [4 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0420)

        * Review the release notes for 4 September 2020.

        * Application logs

    * [2 September 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-sep0220)

        * Review the release notes for 2 September 2020.

        * CLI version 0.3.1973 released

        * {{site.data.keyword.codeengineshort}} batch CRDs updated to `v1beta1`

* [August 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug20)

    * Review the release notes for August 2020.

    * [21 August 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug2120)

        * Review the release notes for 21 August 2020.

        * CLI version 0.3.1802 released

        * Updated example

        * Project quotas

    * [17 August 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1720)

        * Review the release notes for 17 August 2020.

        * CLI version 0.3.1712 released

        * Ephemeral storage limit

    * [14 August 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug1420)

        * Review the release notes for 14 August 2020.

        * CLI version 0.3.1675 released

    * [4 August 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-aug0420)

        * Review the release notes for 4 August 2020.

        * `array indices`

        * CLI version 0.3.1535 released

* [July 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul20)

    * Review the release notes for July 2020.

    * [30 July 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul3020)

        * Review the release notes for 30 July 2020.

        * `array spec`

        * Example application

    * [22 July 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul2220)

        * Review the release notes for 22 July 2020.

        * Updates to application docs

        * CLI version 0.3.1415 released

    * [17 July 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul1720)

        * Review the release notes for 17 July 2020.

        * CLI version 0.3.1363 released

    * [10 July 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jul1020)

        * Review the release notes for 10 July 2020.

        * CLI version 0.2.1250 released

* [June 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun20)

    * Review the release notes for June 2020.

    * [19 June 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1920)

        * Review the release notes for 19 June 2020.

        * CLI version 0.2.1093 released

    * [11 June 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-jun1120)

        * Review the release notes for 11 June 2020.

        * Updates to service bind

        * CLI version 0.2.966 released

* [May 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may20)

    * Review the release notes for May 2020.

    * [19 May 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1920)

        * Review the release notes for 19 May 2020.

        * Service bind

    * [18 May 2020](/docs/codeengine?topic=codeengine-codeengine-relnotes#codeengine-may1820)

        * Review the release notes for 18 May 2020.

        * New! [{{site.data.keyword.codeenginefull_notm}} experimental release](https://cloud.ibm.com/codeengine/overview){: external}


## Tutorials library for Code Engine
{: #sitemap_tutorials-library-for-code-engine}

[Tutorials library for Code Engine](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}


## App and job tutorials
{: #sitemap_app_and_job_tutorials}


[Deploying and scaling applications](/docs/codeengine?topic=codeengine-deploy-app-tutorial#deploy-app-tutorial)

* [Select an image file](/docs/codeengine?topic=codeengine-deploy-app-tutorial#deploy-app-image-file)

* [Creating and deploying an application](/docs/codeengine?topic=codeengine-deploy-app-tutorial#app-creating-deploying)

* [Updating your application](/docs/codeengine?topic=codeengine-deploy-app-tutorial#app-updating)

* [Scaling your application (scale-to-zero and scale-from-zero)](/docs/codeengine?topic=codeengine-deploy-app-tutorial#app-scaling)

* [Next steps](/docs/codeengine?topic=codeengine-deploy-app-tutorial#nextsteps-deployapptut)

[Running and updating jobs](/docs/codeengine?topic=codeengine-run-job-tutorial#run-job-tutorial)

* [Creating a job](/docs/codeengine?topic=codeengine-run-job-tutorial#batch-jobcreate)

* [Running a job](/docs/codeengine?topic=codeengine-run-job-tutorial#batch-jobrun-ui)

* [Accessing job details](/docs/codeengine?topic=codeengine-run-job-tutorial#batch-accessjobdetails-ui)

* [Updating a job](/docs/codeengine?topic=codeengine-run-job-tutorial#batch-updatejob-ui)

* [Next steps](/docs/codeengine?topic=codeengine-run-job-tutorial#nextsteps-deployjobtut)

[Getting started with your migration from Heroku to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-migrate)

* [Objectives](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-objectives)

* [Prerequisites](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-prereqs)

* [Comparing Heroku and {{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-migrate-terms)

* [Log in to {{site.data.keyword.cloud_notm}}](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-log-cloud)

* [Creating a project](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-create-project)

* [Deploying your application](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-build2-application)

* [Clean up](/docs/codeengine?topic=codeengine-heroku-migrate#heroku-clean-up)

[Configuring a highly available application](/docs/codeengine?topic=codeengine-deploy-multiple-regions#deploy-multiple-regions)

* [Prerequisites](/docs/codeengine?topic=codeengine-deploy-multiple-regions#deploy-setup-cis-prereq)

* [Create projects in different regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions#deploy-project-regions)

* [Deploy your apps in multiple regions](/docs/codeengine?topic=codeengine-deploy-multiple-regions#deploy-app-regions)

* [Generate a certificate for your custom domain](/docs/codeengine?topic=codeengine-deploy-multiple-regions#custom-domain-cert)

* [Create a TLS secret](/docs/codeengine?topic=codeengine-deploy-multiple-regions#create-tls-secret)

* [Configure the custom domain mappings](/docs/codeengine?topic=codeengine-deploy-multiple-regions#config-app-domain)

* [Configure a health check](/docs/codeengine?topic=codeengine-deploy-multiple-regions#config-health-check)

* [Configure the {{site.data.keyword.cis_short}} load-balancer](/docs/codeengine?topic=codeengine-deploy-multiple-regions#=config-load-balancer)

* [Verify that your app is available](/docs/codeengine?topic=codeengine-deploy-multiple-regions#verify-app-domain)

* [Cleaning up your tutorial](/docs/codeengine?topic=codeengine-deploy-multiple-regions#clean-up)

[Building applications that store information in {{site.data.keyword.cloudant}}](/docs/codeengine?topic=codeengine-tutorial-cloudant-local#tutorial-cloudant-local)

* [Create an {{site.data.keyword.cloudant}} service instance and database](/docs/codeengine?topic=codeengine-tutorial-cloudant-local#create-cloudant)

* [Test your application locally](/docs/codeengine?topic=codeengine-tutorial-cloudant-local#test-cloudant-local)

* [Deploying your application to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-tutorial-cloudant-local#deploy-cloudant-ce)

[Building applications by using buildpacks](/docs/codeengine?topic=codeengine-build-app-tutorial#build-app-tutorial)

* [Set up registry access](/docs/codeengine?topic=codeengine-build-app-tutorial#setup-registry-access)

* [Create a build](/docs/codeengine?topic=codeengine-build-app-tutorial#create-a-build)

* [Submit a build run](/docs/codeengine?topic=codeengine-build-app-tutorial#submit-buildrun)

* [Work with the container image](/docs/codeengine?topic=codeengine-build-app-tutorial#use-container-image)

* [Next steps for buildpacks](/docs/codeengine?topic=codeengine-build-app-tutorial#nextsteps-buildapptut)

[Serverless web application and API with Code Engine](https://cloud.ibm.com/docs/solution-tutorials?topic=solution-tutorials-serverless-webapp){: external}

[Text analysis with Code Engine](https://cloud.ibm.com/docs/solution-tutorials?topic=solution-tutorials-text-analysis-code-engine){: external}

[Serverless web app and eventing for data retrieval and analytics](https://cloud.ibm.com/docs/solution-tutorials?topic=solution-tutorials-serverless-github-traffic-analytics){: external}


## Subscription tutorials
{: #sitemap_subscription_tutorials}


[Subscribing to cron events](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#subscribe-cron-tutorial)

* [Determine your cron interval](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#determine-cron-interval)

* [Create your app (or job)](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#create-app)

* [Create a subscription](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#create-subscription)

* [Testing your subscription](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#test-subscription)

* [Update your subscription](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#update-subscription)

* [Clean up for cron subscription tutorial](/docs/codeengine?topic=codeengine-subscribe-cron-tutorial#clean-subscription)

[Subscribing to {{site.data.keyword.cos_short}} events](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#subscribe-cos-tutorial)

* [Determine your {{site.data.keyword.cos_short}} bucket and region](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#determine-cos-bucket-and-region)

* [Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#notify_mgr)

* [Create your app (or job)](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#create-app-cos)

* [Create a subscription](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#create-subscription-cos)

* [Testing your subscription](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#test-subscription-cos)

* [Update your {{site.data.keyword.cos_short}} subscription](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#update-subscription-cos)

* [Clean up for {{site.data.keyword.cos_short}} tutorial](/docs/codeengine?topic=codeengine-subscribe-cos-tutorial#clean-subscription-cos)

[Subscribing to Kafka events](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#subscribe-kafka-tutorial)

* [Setting up the Kafka event producer](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-setup-sender)

* [Setting up a {{site.data.keyword.codeengineshort}} sample app to produce Kafka messages](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-sender-app)

* [Setting up a {{site.data.keyword.codeengineshort}} Kafka subscription](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-subscribe-setup)

* [Testing your subscription](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-test-subscription)

* [Updating your subscription](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-update-subscription)

* [Clean up for Kafka subscription tutorial](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#tutkafka-delete-subscription)

* [Next steps](/docs/codeengine?topic=codeengine-subscribe-kafka-tutorial#nextsteps-kafkatut)

[Sending GitHub events to an application](/docs/codeengine?topic=codeengine-github-event-webhooks#github-event-webhooks)

* [Prerequisites](/docs/codeengine?topic=codeengine-github-event-webhooks#gew-prerequisites)

* [Create an application](/docs/codeengine?topic=codeengine-github-event-webhooks#gew-create-app)

* [Create a webhook](/docs/codeengine?topic=codeengine-github-event-webhooks#gew-create-webhook)

* [Test your GitHub event](/docs/codeengine?topic=codeengine-github-event-webhooks#gew-test-webhook)

* [Clean up](/docs/codeengine?topic=codeengine-github-event-webhooks#github-clean-up)


## Deploying Cloud Foundry applications in {{site.data.keyword.codeengineshort}}: Getting started
{: #sitemap_deploying_cloud_foundry_applications_in_getting_started}


[Deploying Cloud Foundry applications in {{site.data.keyword.codeengineshort}}: Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#migrate-cf-ce-tutorial)

* [Objectives](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-objectives)

* [Prerequisites](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-prereqs)

* [Log in to {{site.data.keyword.cloud_notm}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-log-cloud)

* [Creating a project](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-create-project)

* [Creating a directory and source code](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-create-dir)

* [Deploying your application](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-build2-application)

* [Clean up](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-clean-up)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial#cftut-migrate-next)


## Running a function from local source
{: #sitemap_running_a_function_from_local_source}


[Running a function from local source](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial)

* [Set up your environment](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-envirn)

* [Create the source code](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-sourcecode)

* [Create your function](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-create)

* [Invoke your function](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-invoke)

* [Provide parameters for your function](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-parameters)

* [Clean up](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-clean-up)

* [Next steps](/docs/codeengine?topic=codeengine-fun-tutorial#fun-tutorial-nextsteps)


## Setting up the CLI
{: #sitemap_setting_up_the_cli}


[Setting up the CLI](/docs/codeengine?topic=codeengine-install-cli#install-cli)

* [Supported environments for {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli#cli-env)

* [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/codeengine?topic=codeengine-install-cli#cli-setup)

* [Installing the {{site.data.keyword.codeengineshort}} CLI plug-in](/docs/codeengine?topic=codeengine-install-cli#install-cli-plugin)

* [Updating the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli#update-cli)

* [Uninstalling the CLI](/docs/codeengine?topic=codeengine-install-cli#uninstall-cli)

* [Accessing the {{site.data.keyword.cloud-shell_notm}} in your web browser](/docs/codeengine?topic=codeengine-install-cli#cloud-shell)


## Planning for {{site.data.keyword.codeengineshort}}
{: #sitemap_planning_for_}


[Planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine#plan-codeengine)

* [{{site.data.keyword.codeengineshort}} use cases](/docs/codeengine?topic=codeengine-plan-codeengine#ce-use-cases)

* [When to use an app, job, or function](/docs/codeengine?topic=codeengine-plan-codeengine#when-app-job)

* [Common scenarios for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine#common-scenarios)


## Working with projects
{: #sitemap_working_with_projects}


[Managing projects](/docs/codeengine?topic=codeengine-manage-project#manage-project)

* [What is a project?](/docs/codeengine?topic=codeengine-manage-project#project-def)

    * [How can I see what projects I can access?](/docs/codeengine?topic=codeengine-manage-project#project-access)

    * [How can I see details about a project?](/docs/codeengine?topic=codeengine-manage-project#project-details)

    * [How can I set policies so others can work with my project?](/docs/codeengine?topic=codeengine-manage-project#project-policies)

    * [Are there project limits to consider?](/docs/codeengine?topic=codeengine-manage-project#project-limits)

* [Create a project](/docs/codeengine?topic=codeengine-manage-project#create-a-project)

    * [Creating a project from the console](/docs/codeengine?topic=codeengine-manage-project#create-project-console)

    * [Creating a project with the CLI](/docs/codeengine?topic=codeengine-manage-project#create-project-cli)

* [Work with a project](/docs/codeengine?topic=codeengine-manage-project#target-a-project)

    * [Working with a project from the console](/docs/codeengine?topic=codeengine-manage-project#target-project-console)

    * [Working with a project with the CLI](/docs/codeengine?topic=codeengine-manage-project#target-project-cli)

    * [Determining which project is selected as the current context](/docs/codeengine?topic=codeengine-manage-project#current-project-cli)

* [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project)

    * [Deleting a project from the console](/docs/codeengine?topic=codeengine-manage-project#delete-project-console)

    * [Deleting a project with the CLI](/docs/codeengine?topic=codeengine-manage-project#delete-project-cli)

* [Restoring deleted projects](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project)

    * [Restoring deleted projects from the console](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project-ui)

    * [Restoring deleted projects with the CLI](/docs/codeengine?topic=codeengine-manage-project#restore-softdelete-project-cli)

* [Permanently deleting projects](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project)

    * [Permanently deleting projects from the console](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project-ui)

    * [Permanently deleting projects with the CLI](/docs/codeengine?topic=codeengine-manage-project#perm-delete-project-cli)

[Configuring project-wide settings](/docs/codeengine?topic=codeengine-project-integrations#project-integrations)

* [What are project-wide integrations and why use them?](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-why)

* [Configuring project-wide service binding operations](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb)

    * [What access permissions are required to configure service binding operations?](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb-access)

    * [What's the relationship between the service ID and the operator secret?](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb-relation)

    * [Configuring service bindings operations with a {{site.data.keyword.codeengineshort}} autogenerated service ID](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb-auto)

    * [Configuring service binding operations with a custom service ID](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb-customserviceid)

    * [Removing configured service binding operations](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-sb-remove)

* [Configuring project-wide access to {{site.data.keyword.registryshort_notm}}](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-cr)

    * [What access permissions are required for {{site.data.keyword.codeengineshort}} managed access to {{site.data.keyword.registrylong_notm}}?](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-cr-access)

    * [What's the relationship between the service ID and the registry secret?](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-cr-relation)

    * [Configuring {{site.data.keyword.registryshort_notm}} access](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-cr-config)

    * [Removing {{site.data.keyword.codeengineshort}} managed access to {{site.data.keyword.registryshort_notm}}](/docs/codeengine?topic=codeengine-project-integrations#projectintegration-cr-remove)


## Deploying applications
{: #sitemap_deploying_applications}


[Working with apps in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-application-workloads#application-workloads)

* [How do I make my code run as a {{site.data.keyword.codeengineshort}} application component?](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-containerimage)

* [What do I need to know about ports for apps in {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-ports)

* [Considerations for HTTP handling](/docs/codeengine?topic=codeengine-application-workloads#considerationshttphandlingapp)

* [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility)

    * [Deploying your app with a public endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-public)

    * [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-private)

    * [Deploying your app with a project endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly)

* [Options for deploying a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsdeploy)

    * [Memory and CPU](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-combo)

    * [Deploying your app with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args)

    * [Creating and running your app with environment variables](/docs/codeengine?topic=codeengine-application-workloads#app-option-envvar)

    * [Creating and running your app when using secrets and configmaps](/docs/codeengine?topic=codeengine-application-workloads#app-option-secconfigmap)

* [Considerations for application quotas](/docs/codeengine?topic=codeengine-application-workloads#app-quotas)

* [Next steps](/docs/codeengine?topic=codeengine-application-workloads#app-nextsteps)

[Deploying app workloads from images in a public registry](/docs/codeengine?topic=codeengine-deploy-app#deploy-app)

* [Deploying an app from the console](/docs/codeengine?topic=codeengine-deploy-app&interface=ui#deploy-app-console)

* [Deploying an app with the CLI](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#deploy-app-cli)

* [Next steps](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#nextsteps-appdeploypub)

[Deploying app workloads from images in {{site.data.keyword.registrylong_notm}}](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage)

* [Deploying an app that references an image in {{site.data.keyword.registryshort}} with the console](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-console)

* [Deploying an app with an image in {{site.data.keyword.registryshort}} with the CLI](/docs/codeengine?topic=codeengine-deploy-app-crimage#deploy-app-crimage-cli)

* [Next steps](/docs/codeengine?topic=codeengine-deploy-app-crimage#nextsteps-appdeploycr)

[Deploying app workloads from images in a private registry](/docs/codeengine?topic=codeengine-deploy-app-private#deploy-app-private)

* [Deploying an app that references an image in a private registry with the console](/docs/codeengine?topic=codeengine-deploy-app-private#deploy-app-private-console)

* [Deploying an app with an image from a private registry with CLI](/docs/codeengine?topic=codeengine-deploy-app-private#deploy-app-private-cli)

* [Next steps](/docs/codeengine?topic=codeengine-deploy-app-private#nextsteps-appdeploypriv)

[Deploying your app from repository source code](/docs/codeengine?topic=codeengine-app-source-code#app-source-code)

* [Deploying your app from repository source code from the console](/docs/codeengine?topic=codeengine-app-source-code#deploy-app-source-code)

* [Deploying your app from repository source code with the CLI](/docs/codeengine?topic=codeengine-app-source-code#deploy-app-source-code-cli)

* [Next steps](/docs/codeengine?topic=codeengine-app-source-code#nextsteps-appdeploysource)

[Deploying your app from local source code with the CLI](/docs/codeengine?topic=codeengine-app-local-source-code#app-local-source-code)

* [Next steps](/docs/codeengine?topic=codeengine-app-local-source-code#nextsteps-app-localdeploysource)

[Accessing your app](/docs/codeengine?topic=codeengine-access-service#access-service)

* [Access details about your app](/docs/codeengine?topic=codeengine-access-service#access-app-details)

    * [Accessing app details from the console](/docs/codeengine?topic=codeengine-access-service#access-appdetails-ui)

    * [Accessing app details with the CLI](/docs/codeengine?topic=codeengine-access-service#access-appdetails-cli)

* [Application status](/docs/codeengine?topic=codeengine-access-service#app-status)

[Updating your app](/docs/codeengine?topic=codeengine-update-app#update-app)

* [What if I want to redeploy my application without changing configuration settings?](/docs/codeengine?topic=codeengine-update-app#update-app-nochange)

* [Updating your app from the console](/docs/codeengine?topic=codeengine-update-app#update-app-console)

* [Updating your app to use project-only endpoints from the console](/docs/codeengine?topic=codeengine-update-app#update-app-console-projendpt)

* [Updating your app to use private endpoints from the console](/docs/codeengine?topic=codeengine-update-app#update-app-console-privateendpt)

* [Updating your app with the CLI](/docs/codeengine?topic=codeengine-update-app#update-app-cli)

* [Updating your app to use project-only endpoints with the CLI](/docs/codeengine?topic=codeengine-update-app#update-app-cli-projectonly)

* [Updating your app to use private endpoints with the CLI](/docs/codeengine?topic=codeengine-update-app#update-app-cli-privateendpt)

* [Updating an app to reference a different image](/docs/codeengine?topic=codeengine-update-app#update-app-diff-image)

    * [Updating an app to reference a different image in {{site.data.keyword.registryshort}} from the console](/docs/codeengine?topic=codeengine-update-app#update-app-crimage-console)

    * [Updating an app to reference a different image in {{site.data.keyword.registryshort}} with the CLI](/docs/codeengine?topic=codeengine-update-app#update-app-crimage-cli)

    * [Updating an app to reference an image that is built from source code from the console](/docs/codeengine?topic=codeengine-update-app#update-app-source-console)

    * [Updating an app to reference an image that is built from source code with the CLI](/docs/codeengine?topic=codeengine-update-app#update-app-source-cli)

[Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale#app-scale)

* [How scaling works](/docs/codeengine?topic=codeengine-app-scale#app-how-scale)

    * [Scaling boundaries](/docs/codeengine?topic=codeengine-app-scale#app-scale-boundaries)

    * [Autoscaling settings for concurrency and timing](/docs/codeengine?topic=codeengine-app-scale#app-scale-timeconcurrency)

    * [Example scenario for autoscaling](/docs/codeengine?topic=codeengine-app-scale#app-scale-example)

* [Optimize latency and throughput](/docs/codeengine?topic=codeengine-app-scale#app-optimize-latency)

    * [Determining concurrency of your application container](/docs/codeengine?topic=codeengine-app-scale#app-determine-concurrency)

* [Observing how your app scales with the CLI](/docs/codeengine?topic=codeengine-app-scale#scale-app-cli)

* [Setting the number of minimum and maximum instances for your app](/docs/codeengine?topic=codeengine-app-scale#scale-app-min-max)

    * [Changing the autoscaling range from the console](/docs/codeengine?topic=codeengine-app-scale#set-app-instances-ui)

    * [Changing the autoscaling range with the CLI](/docs/codeengine?topic=codeengine-app-scale#set-app-instances-cli)

[Configuring custom domain mappings for your app](/docs/codeengine?topic=codeengine-app-domainmapping#app-domainmapping)

* [Configuring custom domain mappings from the console](/docs/codeengine?topic=codeengine-app-domainmapping#custom-domain-ui)

* [Configuring custom domain mappings with the CLI](/docs/codeengine?topic=codeengine-app-domainmapping#custom-domain-cli)

* [Completing the custom domain configuration with your domain registrar](/docs/codeengine?topic=codeengine-app-domainmapping#app-completing-custom-domain)

* [Testing your custom domain](/docs/codeengine?topic=codeengine-app-domainmapping#testapp-custom-domain)

[Working with liveness and readiness probes for your app](/docs/codeengine?topic=codeengine-app-probes#app-probes)

* [What are liveness and readiness probes?](/docs/codeengine?topic=codeengine-app-probes#app-probes-terms)

* [Why use liveness and readiness probes with my apps?](/docs/codeengine?topic=codeengine-app-probes#app-probes-why)

* [Implementing a readiness or liveness probe in your code](/docs/codeengine?topic=codeengine-app-probes#app-probes-implement)

* [Configuring liveness and readiness probes in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-app-probes#app-probes-config)

    * [Properties for liveness and readiness probes](/docs/codeengine?topic=codeengine-app-probes#app-probes-properties)

    * [Configuring probes from the console](/docs/codeengine?topic=codeengine-app-probes#app-probes-config-ui)

    * [Configuring probes with the CLI](/docs/codeengine?topic=codeengine-app-probes#app-probes-config-cli)

* [Viewing probe settings in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-app-probes#app-probes-view)

    * [Viewing probe settings from the console](/docs/codeengine?topic=codeengine-app-probes#app-probes-view-ui)

    * [Viewing probe settings with the CLI](/docs/codeengine?topic=codeengine-app-probes#app-probes-view-cli)

* [Updating probes](/docs/codeengine?topic=codeengine-app-probes#app-probes-update)

    * [Updating probes from the console](/docs/codeengine?topic=codeengine-app-probes#app-probes-update-ui)

    * [Updating probes with the CLI](/docs/codeengine?topic=codeengine-app-probes#app-probes-update-cli)

* [Deleting probes](/docs/codeengine?topic=codeengine-app-probes#delete-probes)

    * [Deleting probes from the console](/docs/codeengine?topic=codeengine-app-probes#app-probes-delete-ui)

    * [Deleting probes with the CLI](/docs/codeengine?topic=codeengine-app-probes#app-probes-delete-cli)

[Implementing applications with gRPC](/docs/codeengine?topic=codeengine-app-grpc#app-grpc)

* [Benefits of using gRPC](/docs/codeengine?topic=codeengine-app-grpc#app-grpc-benefits)

* [Configuring {{site.data.keyword.codeengineshort}} applications to use gRPC](/docs/codeengine?topic=codeengine-app-grpc#app-grpc-config-cli)


## Running jobs
{: #sitemap_running_jobs}


[Working with jobs and job runs](/docs/codeengine?topic=codeengine-job-plan#job-plan)

* [How do I make my code run as a {{site.data.keyword.codeengineshort}} job component?](/docs/codeengine?topic=codeengine-job-plan#job-containerimage)

* [Considerations for HTTP handling](/docs/codeengine?topic=codeengine-job-plan#considerationshttphandlingjob)

* [Options for creating and running a job](/docs/codeengine?topic=codeengine-job-plan#job-options)

    * [Memory and CPU for jobs](/docs/codeengine?topic=codeengine-job-plan#job-options-combo)

    * [Creating and running a job with commands and arguments](/docs/codeengine?topic=codeengine-job-plan#job-cmd-args)

    * [Creating and running a job with environment variables](/docs/codeengine?topic=codeengine-job-plan#job-option-envvar)

    * [Creating and running a job with secrets and configmaps](/docs/codeengine?topic=codeengine-job-plan#job-option-secconfigmap)

* [What if I want my job to run indefinitely?](/docs/codeengine?topic=codeengine-job-plan#job-indefinite)

* [Considerations for job quotas](/docs/codeengine?topic=codeengine-job-plan#job-quotas)

* [Next steps](/docs/codeengine?topic=codeengine-job-plan#job-nextsteps)

[Creating a job from images in a public registry](/docs/codeengine?topic=codeengine-create-job#create-job)

* [Creating a job with the console](/docs/codeengine?topic=codeengine-create-job#create-job-ui)

* [Creating a job with the CLI](/docs/codeengine?topic=codeengine-create-job#create-job-cli)

* [Next steps](/docs/codeengine?topic=codeengine-create-job#nextsteps-jobcreatepub)

[Creating a job from images in {{site.data.keyword.registrylong_notm}}](/docs/codeengine?topic=codeengine-create-job-crimage#create-job-crimage)

* [Creating a job that references an image in {{site.data.keyword.registryshort}} with the console](/docs/codeengine?topic=codeengine-create-job-crimage#create-job-crimage-console)

* [Creating a job with an image in {{site.data.keyword.registryshort}} with the CLI](/docs/codeengine?topic=codeengine-create-job-crimage#create-job-crimage-cli)

* [Next steps](/docs/codeengine?topic=codeengine-create-job-crimage#nextsteps-jobcreatecr)

[Creating a job from images in a private registry](/docs/codeengine?topic=codeengine-create-job-private#create-job-private)

* [Creating a job that references an image in a private registry with the console](/docs/codeengine?topic=codeengine-create-job-private#create-job-private-console)

* [Creating a job with an image from a private registry with CLI](/docs/codeengine?topic=codeengine-create-job-private#create-job-private-cli)

* [Next steps](/docs/codeengine?topic=codeengine-create-job-private#nextsteps-jobcreatepriv)

[Creating a job from repository source code](/docs/codeengine?topic=codeengine-run-job-source-code#run-job-source-code)

* [Creating your job from repository source code from the console](/docs/codeengine?topic=codeengine-run-job-source-code#run-job-source-code-ui)

* [Creating your job from repository source code with the CLI](/docs/codeengine?topic=codeengine-run-job-source-code#run-job-source-code-cli)

* [Next steps](/docs/codeengine?topic=codeengine-run-job-source-code#nextsteps-jobcreatesource)

[Creating your job from local source code with the CLI](/docs/codeengine?topic=codeengine-job-local-source-code#job-local-source-code)

* [Next steps](/docs/codeengine?topic=codeengine-job-local-source-code#nextsteps-job-localdeploysource)

[Running a job](/docs/codeengine?topic=codeengine-run-job#run-job)

* [Running a job from the console](/docs/codeengine?topic=codeengine-run-job#run-job-ui)

* [Running a job with the CLI](/docs/codeengine?topic=codeengine-run-job#run-job-cli)

    * [Running a job with the CLI based on a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withjobconfig)

    * [Running a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withoutjobconfig)

* [Resubmitting your job with the CLI](/docs/codeengine?topic=codeengine-run-job#resubmit-job-cli)

* [Next steps](/docs/codeengine?topic=codeengine-run-job#nextsteps-run-job)

[Accessing job details](/docs/codeengine?topic=codeengine-access-job-details#access-job-details)

* [Accessing job details from the console](/docs/codeengine?topic=codeengine-access-job-details#access-jobdetails-ui)

* [Accessing job details with the CLI](/docs/codeengine?topic=codeengine-access-job-details#access-jobdetails-cli)

* [Accessing job details for a specific run of your job with the CLI](/docs/codeengine?topic=codeengine-access-job-details#access-specific-jobdetails-cli)

* [Job status](/docs/codeengine?topic=codeengine-access-job-details#job-status)

[Updating a job](/docs/codeengine?topic=codeengine-update-job#update-job)

* [Updating a job from the console](/docs/codeengine?topic=codeengine-update-job#update-job-ui)

* [Updating a job with the CLI](/docs/codeengine?topic=codeengine-update-job#update-job-cli)

    * [Updating a job configuration with the CLI](/docs/codeengine?topic=codeengine-update-job#update-jobconfig-cli)

    * [Updating a job run with the CLI](/docs/codeengine?topic=codeengine-update-job#update-jobrun-cli)

[Creating and running a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon#job-daemon)

* [Creating and running a job that runs indefinitely from the console](/docs/codeengine?topic=codeengine-job-daemon#job-daemon-ui)

* [Creating and running a job that runs indefinitely with the CLI](/docs/codeengine?topic=codeengine-job-daemon#job-daemon-cli)

* [Stopping a job that runs indefinitely](/docs/codeengine?topic=codeengine-job-daemon#job-daemon-stop)

    * [Stopping a job that runs indefinitely from the console](/docs/codeengine?topic=codeengine-job-daemon#job-daemon-stop-ui)

    * [Stopping a job that runs indefinitely with the CLI](/docs/codeengine?topic=codeengine-job-daemon#job-daemon-stop-cli)

[Running jobs in parallel](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel)

* [Efficiently process many files by using job processing](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel-how)

* [Process a subset of data and dynamically assign work to parallel job run instances](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel-dynamic)

* [Benefits of running parallel batch jobs](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel-benefit)

* [Considerations when planning parallel batch jobs](/docs/codeengine?topic=codeengine-job-run-parallel#job-run-parallel-consider)


## Running functions
{: #sitemap_running_functions}


[Working with functions](/docs/codeengine?topic=codeengine-fun-work#fun-work)

* [Function limitations](/docs/codeengine?topic=codeengine-fun-work#fun-limitations)

* [How do I make my code run as a {{site.data.keyword.codeengineshort}} function component?](/docs/codeengine?topic=codeengine-fun-work#fun-codebundle)

* [What happens when I invoke my function?](/docs/codeengine?topic=codeengine-fun-work#functions-invoke)

* [Can I keep my function instance alive longer?](/docs/codeengine?topic=codeengine-fun-work#functions-scale)

* [Requests and responses](/docs/codeengine?topic=codeengine-fun-work#functions-request)

    * [Example 1: Generating an HTML response from a function](/docs/codeengine?topic=codeengine-fun-work#functions-response1)

    * [Example 2: Setting a response code and response header](/docs/codeengine?topic=codeengine-fun-work#functions-response2)

    * [Example 3: Generating a plain text response from a function](/docs/codeengine?topic=codeengine-fun-work#functions-response3)

* [Error handling and debugging](/docs/codeengine?topic=codeengine-fun-work#functions-error)

* [Function data input/output characteristics](/docs/codeengine?topic=codeengine-fun-work#functions-data)

* [Options for visibility for a {{site.data.keyword.codeengineshort}} function](/docs/codeengine?topic=codeengine-fun-work#optionsvisibilityfun)

    * [Deploying your function with an internal endpoint](/docs/codeengine?topic=codeengine-fun-work#fun-endpoint-projectonly)

    * [Deploying your function with a public endpoint](/docs/codeengine?topic=codeengine-fun-work#fun-endpoint-public)

    * [Deploying your function with a private endpoint](/docs/codeengine?topic=codeengine-fun-work#fun-endpoint-private)

* [Options for creating functions](/docs/codeengine?topic=codeengine-fun-work#functions-options)

    * [Memory and CPU](/docs/codeengine?topic=codeengine-fun-work#functions-combo)

    * [Creating and running your function with environment variables](/docs/codeengine?topic=codeengine-fun-work#functions-envvar)

    * [Creating and running your function when using secrets and configmaps](/docs/codeengine?topic=codeengine-fun-work#functions-secconfigmap)

* [Considerations for functions quotas](/docs/codeengine?topic=codeengine-fun-work#functions-quotas)

* [Next steps](/docs/codeengine?topic=codeengine-fun-work#function-nextsteps)

[Exchanging data with functions](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-exchanging-data)

* [External request data interface](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-request)

    * [MIME types](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-MIME-types)

    * [Request data](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-request-data)

    * [Providing request data as query parameters](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-providing-request-data=as=query)

    * [Providing request data in the request body](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-providing-request-data-in-body)

    * [Providing request header data](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-providing-request-header)

    * [Providing request mixed data](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-providing-request-mixed-data)

* [Internal request data interface](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-internal-data-interface-requests)

    * [Text encoding](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-internal-data-interface-requests-text)

    * [The `args` parameter](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-args)

    * [{{site.data.keyword.codeengineshort}} function environment variables](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-env-vars)

* [Internal response data interface](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-internal-response-data-interface)

    * [`headers` element](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-headers-element)

    * [`statusCode` element](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-statusCode-element)

    * [`body` element](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-body-element)

* [External response data interface](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-response)

    * [MIME types](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-response-mime)

    * [Response data](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-external-data-interface-response-response-data)

* [{{site.data.keyword.codeengineshort}} function invocation examples](/docs/codeengine?topic=codeengine-fun-exchanging-data#fun-invocation-examples)

[Creating function workloads with inline code](/docs/codeengine?topic=codeengine-fun-create-inlinecode#fun-create-inlinecode)

* [Creating a function with inline with the console](/docs/codeengine?topic=codeengine-fun-create-inlinecode#fun-create-inline-console)

* [Creating a function with inline code with the CLI](/docs/codeengine?topic=codeengine-fun-create-inlinecode#fun-create-inline-cli)

* [Next steps](/docs/codeengine?topic=codeengine-fun-create-inlinecode#nextsteps-funinline)

[Creating function workloads with repository source code](/docs/codeengine?topic=codeengine-fun-create-repo#fun-create-repo)

* [Creating function workloads with repository source code from the console](/docs/codeengine?topic=codeengine-fun-create-repo#fun-create-repo-console)

* [Creating function workloads with repository source code with the CLI](/docs/codeengine?topic=codeengine-fun-create-repo#fun-create-repo-cli)

* [Including dependencies for your function](/docs/codeengine?topic=codeengine-fun-create-repo#fun-package-repo)

    * [Including modules for a Node.js function](/docs/codeengine?topic=codeengine-fun-create-repo#function-nodejs-dep-repo)

    * [Including modules for a Python function](/docs/codeengine?topic=codeengine-fun-create-repo#function-python-dep-repo)

* [Next steps](/docs/codeengine?topic=codeengine-fun-create-repo#nextsteps-funsource)

[Creating function workloads from local source code](/docs/codeengine?topic=codeengine-fun-create-local#fun-create-local)

* [Creating a function from local source code with the CLI](/docs/codeengine?topic=codeengine-fun-create-local#fun-create-local-cli)

* [Including dependencies for your function](/docs/codeengine?topic=codeengine-fun-create-local#fun-package-local)

    * [Including modules for a Node.js function](/docs/codeengine?topic=codeengine-fun-create-local#function-nodejs-dep-local)

    * [Including modules for a Python function](/docs/codeengine?topic=codeengine-fun-create-local#function-python-dep-local)

* [Next steps](/docs/codeengine?topic=codeengine-fun-create-local#nextsteps-funruncr)

[Creating function workloads from existing code bundles](/docs/codeengine?topic=codeengine-fun-create-existing#fun-create-existing)

* [Creating a function that references a code bundle in {{site.data.keyword.registryshort}} with the console](/docs/codeengine?topic=codeengine-fun-create-existing#create-fun-cr-console)

* [Deploying a function with an existing code bundle with the CLI](/docs/codeengine?topic=codeengine-fun-create-existing#fun-cr-cli)

    * [Deploying a function from a public registry with the CLI](/docs/codeengine?topic=codeengine-fun-create-existing#fun-cr-cli-public)

    * [Deploying a function from a private registry with the CLI](/docs/codeengine?topic=codeengine-fun-create-existing#fun-cr-cli-private)

* [Next steps](/docs/codeengine?topic=codeengine-fun-create-existing#nextsteps-funrunexisting)

[Configuring custom domain mappings for your function](/docs/codeengine?topic=codeengine-fun-domainmapping#fun-domainmapping)

* [Configuring custom domain mappings from the console](/docs/codeengine?topic=codeengine-fun-domainmapping#fun-custom-domain-ui)

* [Configuring custom domain mappings with the CLI](/docs/codeengine?topic=codeengine-fun-domainmapping#fun-custom-domain-cli)

* [Completing the custom domain configuration with your domain registrar](/docs/codeengine?topic=codeengine-fun-domainmapping#fun-completing-custom-domain)

* [Testing your custom domain](/docs/codeengine?topic=codeengine-fun-domainmapping#testfun-custom-domain)

[Function runtimes](/docs/codeengine?topic=codeengine-fun-runtime#fun-runtime)

* [Supported managed runtimes for functions on {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-managed)

* [Supported CPU and memory combinations for functions](/docs/codeengine?topic=codeengine-fun-runtime#fun-supported-combo)

* [Runtime support lifecycle](/docs/codeengine?topic=codeengine-fun-runtime#fun-runtimes-support-lifecycle)

* [Upgrading a function to a new runtime release](/docs/codeengine?topic=codeengine-fun-runtime#fun-upgrade-to-new-runtime-release)

[Testing {{site.data.keyword.codeengineshort}} functions locally](/docs/codeengine?topic=codeengine-fun-test-local#fun-test-local)

* [Python wrapper](/docs/codeengine?topic=codeengine-fun-test-local#fun-test-python)

* [Node.js wrapper](/docs/codeengine?topic=codeengine-fun-test-local#fun-test-nodejs)

[Migrating IBM Cloud Functions to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate)

* [Comparing Code Engine to Cloud Functions](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-compare)

* [Key capabilities](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-key)

* [What {{site.data.keyword.codeengineshort}} entity is best for my workload?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-compare-app-job)

* [Migrating IBM Cloud Functions Actions to {{site.data.keyword.codeengineshort}} Functions FAQ](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faqs)

    * [How can I process a bulk-load of computations?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq1)

    * [I used Cloud Function to include dynamic elements for my web application. Can I move to {{site.data.keyword.codeengineshort}} Functions?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq2)

    * [Can I trigger my function code?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq3)

    * [Can my function be accessed through a public URL?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq4)

    * [How can I secure my functions?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq5)

    * [Can I include dynamic elements?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq6)

    * [Can I use sequences to chain my functions together?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq7)

    * [Can I use `whisk.system` actions?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq8)

    * [Can I bind my function to service credentials?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq9)

    * [Where can I find information about my in progress and finished {{site.data.keyword.codeengineshort}} Function runs?](/docs/codeengine?topic=codeengine-fun-migrate#fun-migrate-faq10)

    * [Does {{site.data.keyword.codeengineshort}} provide an OpenAPI specification for the deployed function?](/docs/codeengine?topic=codeengine-fun-migrate#openapi-spec-fun-migrate)


## Building source code
{: #sitemap_building_source_code}


[Planning your build](/docs/codeengine?topic=codeengine-plan-build#plan-build)

* [Prepare your source location](/docs/codeengine?topic=codeengine-plan-build#build-plan-repo)

* [Choose a build strategy](/docs/codeengine?topic=codeengine-plan-build#build-strategy)

    * [Dockerfile](/docs/codeengine?topic=codeengine-plan-build#build-dockerfile-strat)

    * [Cloud Native Buildpacks](/docs/codeengine?topic=codeengine-plan-build#build-buildpack-strat)

* [Determine the size of the build](/docs/codeengine?topic=codeengine-plan-build#build-size)

* [Choose your container image registry](/docs/codeengine?topic=codeengine-plan-build#build-registry)

* [Choose your build method](/docs/codeengine?topic=codeengine-plan-build#build-method)

    * [Create build configurations](/docs/codeengine?topic=codeengine-plan-build#build-create-config)

    * [Create container image with stand-alone build commands](/docs/codeengine?topic=codeengine-plan-build#build-create-image-standalone)

    * [Build your code and create your workload](/docs/codeengine?topic=codeengine-plan-build#build-code-create-workload)

* [Next steps for builds](/docs/codeengine?topic=codeengine-plan-build#nextsteps-buildimage)

[Create a build configuration that pulls source from public repository](/docs/codeengine?topic=codeengine-build-create-config1#build-create-config1)

* [Creating a build configuration from the console (public repo)](/docs/codeengine?topic=codeengine-build-create-config1#build-create-console)

* [Creating a build configuration with the CLI (public repo)](/docs/codeengine?topic=codeengine-build-create-config1#build-create-cli)

    * [Creating a build configuration with the CLI (with public repo source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-create-config1#build-create-cli-a)

    * [Creating a build configuration with the CLI (with public repo source and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-create-config1#build-create-cli-b)

[Create a build configuration that pulls source from private repository](/docs/codeengine?topic=codeengine-build-config-gitrepo#build-config-gitrepo)

* [Creating a build configuration from the console (private repo)](/docs/codeengine?topic=codeengine-build-config-gitrepo#build-config-gitrepo-ui)

* [Creating a build configuration with the CLI (private repo)](/docs/codeengine?topic=codeengine-build-config-gitrepo#build-config-gitrepo-cli)

    * [Creating a build configuration with the CLI (with private repo source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-config-gitrepo#build-config-gitrepo-cli-a)

    * [Creating a build configuration with the CLI (with private repo source and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-config-gitrepo#build-config-gitrepo-cli-b)

[Create a build configuration that pulls source from a local directory](/docs/codeengine?topic=codeengine-build-config-local#build-config-local)

* [Creating a build configuration with the CLI (with local source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-config-local#build-config-local-cli-a)

* [Creating a build configuration with the CLI (with local source and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-config-local#build-config-local-cli-b)

[Running a build configuration](/docs/codeengine?topic=codeengine-build-run#build-run)

* [Running a build from the console](/docs/codeengine?topic=codeengine-build-run#build-run-console)

* [Running a build with the CLI for source from a repository (non-local)](/docs/codeengine?topic=codeengine-build-run#build-run-cli)

* [Running a build with the CLI for source from a local directory (local)](/docs/codeengine?topic=codeengine-build-run#build-run-cli-local)

[Building a container image with stand-alone build commands (CLI)](/docs/codeengine?topic=codeengine-build-standalone#build-standalone)

* [Running a single build that pulls source from public repository with the CLI](/docs/codeengine?topic=codeengine-build-standalone#buildsa-public)

    * [Running a single build with the CLI (with public repo source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-public-cli-a)

    * [Running a single build with the CLI (with public repo source and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-public-cli-b)

* [Running a single build that pulls source from private repository with the CLI](/docs/codeengine?topic=codeengine-build-standalone#buildsa-private)

    * [Running a single build with the CLI (with private repo source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-private-cli-a)

    * [Running a single build with the CLI (with private repo source and and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-private-cli-b)

* [Running a single build that pulls source from a local directory](/docs/codeengine?topic=codeengine-build-standalone#buildsa-local)

    * [Running a single build with the CLI (with local source and automatic access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-local-cli-a)

    * [Running a single build with the CLI (with local source and user-provided access to registry)](/docs/codeengine?topic=codeengine-build-standalone#buildsa-local-cli-b)

* [Next steps for builds](/docs/codeengine?topic=codeengine-build-standalone#nextsteps-buildimage-stand)


## Migrating Cloud Foundry apps to Code Engine
{: #sitemap_migrating_cloud_foundry_apps_to_code_engine}


[Getting started with your migration from Cloud Foundry to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart#migrate-cf-ce-getstart)

* [Migration considerations](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart#migrate-cf-ce-considerations)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart#migrate-cf-ce-next)

[Comparing Cloud Foundry and {{site.data.keyword.codeengineshort}} terms](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms#migrate-cf-ce-terms)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms#migrate-cf-ce-next-terms)

[Deploying your application code from a local source](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#migrate-cf-ce-local)

* [Objectives](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#cf-objectives)

* [Prerequisites](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#cf-prereqs)

* [Log in to {{site.data.keyword.cloud_notm}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#local-log-cloud)

* [Creating a project](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#local-create-project)

* [Creating a directory and source code](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#local-create-dir)

* [Deploying your application](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#build2-application)

* [Clean up](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#local-clean-up)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-local#migrate-cf-ce-next-local)

[Migrating your service binding](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#migrate-cf-ce-bind)

* [Creating the service bind](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#migrate-cf-ce-servicebind)

* [Migrating the code](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#migrate-cf-ce-code)

* [Staging your application migration](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#migrate-cf-ce-staging)

* [Building your code and running your app](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#build-cf-ce-staging)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-bind#migrate-cf-ce-next-sb)

[Scaling, high availability, and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale#migrate-cf-ce-scale)

* [Scaling your app](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale#migrate-scale-app)

* [High availability](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale#migrate-ha)

* [Traffic management and rolling updates](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale#migrate-traffic-mgmt)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale#migrate-cf-ce-next-scale)

[{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#migrate-cf-ce-cmd)

* [Connect to the deployment API region commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#deployment-api)

* [Create a deployment location for your workload commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#deployment-place)

* [List your apps and jobs commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#list-workload)

* [Deploy an image as an app or job commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#deploy-commands)

* [Bind a Service to a workload](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#binding-commands)

* [Update applications or jobs commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#update-commands)

* [Control applications and jobs commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#control-commands)

* [Get information about apps commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#get-info-commands)

* [Specifying a buildpack version](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#specify-buildpack)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd#migrate-cf-ce-next-cmd)

[Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#migrate-cf-ce-faq)

* [Can I use a custom URL with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#customurl)

* [My app contains a specific route, Can I use the same route?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#sameroute)

* [Can I stop my app?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_stop)

* [Why do I have so many app instances?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_more)

* [Why are my apps slow to respond?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_response)

* [Can I route requests to a specific application instance?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#specific-app-instance)

* [I use a global load balancer with my Cloud Foundry app. Can I migrate it to {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#app_glb)

* [Does my app need to follow any specifications?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#12factor)

* [What types of workloads are available with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#workloads)

    * [Determining the type of workloads that you want](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#determine-type)

* [I use manifest files. Are there similar options available with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#manifest)

* [I know how to deploy an app with Cloud Foundry. What do I need to know to deploy an app in {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#deployment)

    * [Push code](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#push)

    * [Deployment context](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#deploy-context)

    * [Logs](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#logs)

    * [Creating a service](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#create-service)

    * [Service binding](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#service-binding-cfce)

    * [Updating an app or job](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#update-app-job)

    * [Runtime support](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#runtime)

* [Next steps](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq#migrate-cf-ce-next-faq)


## Binding Code Engine resources to IBM Cloud services
{: #sitemap_binding_code_engine_resources_to_ibm_cloud_services}


[Working with service bindings to integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-service-binding#service-binding)

* [What is {{site.data.keyword.codeenginefull_notm}} service binding?](/docs/codeengine?topic=codeengine-service-binding#about-service-binding)

* [Accessing a bound service instance from a {{site.data.keyword.codeengineshort}} workload](/docs/codeengine?topic=codeengine-service-binding#access-bound-service)

    * [`CE_SERVICES` environment variable](/docs/codeengine?topic=codeengine-service-binding#ce-services)

    * [Prefix method](/docs/codeengine?topic=codeengine-service-binding#prefix-method)

* [What should I consider if I have service bindings that use the previous implementation?](/docs/codeengine?topic=codeengine-service-binding#considerations-previmpl-binding)

    * [How can I replace a service binding that uses the previous implementation?](/docs/codeengine?topic=codeengine-service-binding#replaceprevimpl-binding)

* [Next steps](/docs/codeengine?topic=codeengine-service-binding#service-binding-nextsteps)

[Configuring access for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess#configure-bindaccess)

* [Using the default service binding access policies](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-auto-servid)

    * [Configuring access for {{site.data.keyword.codeengineshort}} to automatically create and manage the service ID for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-auto-servid-access)

    * [Configuring a project to bind services in a different resource group](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-config-proj)

* [Using a custom service ID for service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-custom-servid)

    * [Creating a custom service ID with access permissions for {{site.data.keyword.codeengineshort}} service bindings](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-auto-servid-access-custom)

    * [Configuring a project to use a custom service ID](/docs/codeengine?topic=codeengine-configure-bindaccess#bind-custom-servid-project)

* [Next steps](/docs/codeengine?topic=codeengine-configure-bindaccess#service-bindings-access-nextsteps)

[Binding a service instance to an app, job, or function workload](/docs/codeengine?topic=codeengine-bind-services#bind-services)

* [Binding a service instance to a {{site.data.keyword.codeengineshort}} app or job from the console](/docs/codeengine?topic=codeengine-bind-services#bind-ui)

    * [Binding a service instance with a new service access secret (with a {{site.data.keyword.codeengineshort}} autogenerated credential)](/docs/codeengine?topic=codeengine-bind-services#bind-credential-ui-newsecret-autocred)

    * [Binding a service instance with a new service access secret (with an existing credential)](/docs/codeengine?topic=codeengine-bind-services#bind-credential-ui-newsecret-existingcred)

    * [Binding a service instance with an existing service access secret](/docs/codeengine?topic=codeengine-bind-services#bind-credential-ui-existingsecret)

* [Binding a service instance to a {{site.data.keyword.codeengineshort}} app, job, or function with the CLI](/docs/codeengine?topic=codeengine-bind-services#bind-cli)

    * [Binding a service instance with a new credential](/docs/codeengine?topic=codeengine-bind-services#bind-credentials)

    * [Binding a service instance with a specific role](/docs/codeengine?topic=codeengine-bind-services#bind-credentials-role)

    * [Binding a service instance with existing credentials](/docs/codeengine?topic=codeengine-bind-services#bind-existing-credentials)

* [Unbinding service instances](/docs/codeengine?topic=codeengine-bind-services#unbind)

    * [Unbinding a service instance from the console](/docs/codeengine?topic=codeengine-bind-services#unbind-ui)

    * [Unbinding a service instance with the CLI](/docs/codeengine?topic=codeengine-bind-services#unbind-cli)


## Accessing container registries
{: #sitemap_accessing_container_registries}


[Accessing container registries](/docs/codeengine?topic=codeengine-add-registry#add-registry)

* [Types of image registries](/docs/codeengine?topic=codeengine-add-registry#types-registries)

* [Types of registry secrets](/docs/codeengine?topic=codeengine-add-registry#types-registryaccesssecrets)

* [Setting up authorities for image registries](/docs/codeengine?topic=codeengine-add-registry#authorities-registry)

    * [What authorities do I need?](/docs/codeengine?topic=codeengine-add-registry#authorities-registry-what-auth)

    * [Can I use a service ID?](/docs/codeengine?topic=codeengine-add-registry#authorities-registry-service-id)

    * [Can I access images in a different registry?](/docs/codeengine?topic=codeengine-add-registry#authorities-registry-access-images)

    * [Can I restrict pull access to a certain regional registry or even a single namespace?](/docs/codeengine?topic=codeengine-add-registry#authorities-registry-pull-access)

* [Accessing images from a public account](/docs/codeengine?topic=codeengine-add-registry#images-public-account)

* [Accessing images in your own account from console](/docs/codeengine?topic=codeengine-add-registry#images-your-account)

* [Accessing images from your account with an API key](/docs/codeengine?topic=codeengine-add-registry#images-your-account-api-key)

    * [Creating an API key from the console](/docs/codeengine?topic=codeengine-add-registry#access-registry-account-console)

    * [Creating an API key with the CLI](/docs/codeengine?topic=codeengine-add-registry#access-registry-account-cli)

* [Accessing images in a shared account](/docs/codeengine?topic=codeengine-add-registry#images-shared-account)

* [Accessing images in a different account](/docs/codeengine?topic=codeengine-add-registry#images-different-account)

* [Accessing images in a private Docker Hub account](/docs/codeengine?topic=codeengine-add-registry#access-private-docker-hub)

* [Add registry access to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce)

    * [Adding registry access from the console](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce-console)

    * [Adding registry access with the CLI](/docs/codeengine?topic=codeengine-add-registry#add-registry-access-ce-cli)

* [Authorizing access to {{site.data.keyword.registryshort}} with service ID](/docs/codeengine?topic=codeengine-add-registry#authorize-cr-service-id)

    * [Authorizing access to {{site.data.keyword.registryshort}} with service ID from the console](/docs/codeengine?topic=codeengine-add-registry#authorize-console-service-id)

    * [Authorizing access to {{site.data.keyword.registryshort}} with the CLI](/docs/codeengine?topic=codeengine-add-registry#authorize-cr-cli)

* [Controlling access to {{site.data.keyword.registryshort}} for {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-add-registry#control-cr-access)

* [Considerations for images in your registry](/docs/codeengine?topic=codeengine-add-registry#considerations-registry)


## Accessing private code repositories
{: #sitemap_accessing_private_code_repositories}


[Accessing private code repositories](/docs/codeengine?topic=codeengine-code-repositories#code-repositories)

* [Create code repository access](/docs/codeengine?topic=codeengine-code-repositories#create-code-repo)

    * [Choosing an SSH key for code repository](/docs/codeengine?topic=codeengine-code-repositories#choose-ssh-key)

    * [Adding private repository access from the console](/docs/codeengine?topic=codeengine-code-repositories#add-repo-access-ce-console)

    * [Adding private repository access with the CLI](/docs/codeengine?topic=codeengine-code-repositories#create-code-repo-console)

* [Referencing a private Git repository in a build](/docs/codeengine?topic=codeengine-code-repositories#referencing-coderepo-build)

    * [Referencing a private Git repository in a build from the console](/docs/codeengine?topic=codeengine-code-repositories#referencing-coderepo-build-ui)

    * [Referencing an SSH secret in a build with the CLI](/docs/codeengine?topic=codeengine-code-repositories#referencing-coderepo)

* [Next steps for Git repository access](/docs/codeengine?topic=codeengine-code-repositories#nextsteps-coderepo)


## Writing a Dockerfile for {{site.data.keyword.codeengineshort}}
{: #sitemap_writing_a_dockerfile_for_}


[Writing a Dockerfile for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-dockerfile#dockerfile)

* [Dockerfile basics](/docs/codeengine?topic=codeengine-dockerfile#dockerfile-basics)

* [Reducing the size of a container image](/docs/codeengine?topic=codeengine-dockerfile#reduce-container)

    * [Combine several commands in a single `RUN` statement to reduce image size](/docs/codeengine?topic=codeengine-dockerfile#combine-commands)

    * [Use a tiny base image](/docs/codeengine?topic=codeengine-dockerfile#small-base-image)

    * [Do not include sources and build tools to reduce image size](/docs/codeengine?topic=codeengine-dockerfile#dont-include-source)

    * [Keep your image clean](/docs/codeengine?topic=codeengine-dockerfile#clean-basics)

* [Improving the start time of your image](/docs/codeengine?topic=codeengine-dockerfile#image-startup)

* [Running a container as non-root](/docs/codeengine?topic=codeengine-dockerfile#container-non-root)


## Integrating {{site.data.keyword.codeengineshort}} workloads with {{site.data.keyword.contdelivery_short}}
{: #sitemap_integrating_workloads_with_}


[Integrating {{site.data.keyword.codeengineshort}} workloads with {{site.data.keyword.contdelivery_short}}](/docs/codeengine?topic=codeengine-toolchain-ce#toolchain-ce)

* [Before you begin](/docs/codeengine?topic=codeengine-toolchain-ce#toolchain-begin)

* [Configuring access for your toolchain](/docs/codeengine?topic=codeengine-toolchain-ce#permissions-toolchain)

* [Creating a toolchain](/docs/codeengine?topic=codeengine-toolchain-ce#create-toolchain)

* [{{site.data.keyword.codeengineshort}} options in your toolchain](/docs/codeengine?topic=codeengine-toolchain-ce#toolchain-options)

* [Troubleshooting toolchain issues](/docs/codeengine?topic=codeengine-toolchain-ce#ts-toolchain)


## Setting up Terraform for {{site.data.keyword.codeengineshort}}
{: #sitemap_setting_up_terraform_for_}


[Setting up Terraform for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce#terraform-setup-ce)

* [Installing Terraform and configuring resources for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-terraform-setup-ce#install-terraform)

* [What's next?](/docs/codeengine?topic=codeengine-terraform-setup-ce#terraform-setup-next)

    * [Resources](/docs/codeengine?topic=codeengine-terraform-setup-ce#terraform-supported-resources)

    * [Data Sources](/docs/codeengine?topic=codeengine-terraform-setup-ce#terraform-supported-data-sources)


## Working with custom domain mappings
{: #sitemap_working_with_custom_domain_mappings}


[Working with custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings#domain-mappings)

* [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-domain-mappings#considerations-custom-domain)

* [Obtaining a custom domain and its TLS certificate and private key](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain)

    * [How can I obtain a certificate for my custom domain?](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain-cert)

    * [Can I use {{site.data.keyword.cis_short}} for domain management when I am using custom domain mapping with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-domain-mappings#prepare-use-cis)

    * [How can I use {{site.data.keyword.cis_short}} with custom domain mapping?](/docs/codeengine?topic=codeengine-domain-mappings#completing-custom-domain-cis)

    * [How do I obtain the CNAME record for a custom domain mapping?](/docs/codeengine?topic=codeengine-domain-mappings#completing-custom-domain-cname)

* [Configuring custom domain mappings in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-domain-mappings#configure-domainmapping)

* [Viewing domain mappings](/docs/codeengine?topic=codeengine-domain-mappings#view-domain-mapping)

    * [Viewing domain mappings from the console](/docs/codeengine?topic=codeengine-domain-mappings#view-domain-mapping-ui)

    * [Viewing domain mappings with the CLI](/docs/codeengine?topic=codeengine-domain-mappings#view-domain-mapping-cli)

* [Updating domain mappings](/docs/codeengine?topic=codeengine-domain-mappings#update-custom-domain)

    * [Updating a domain mapping from the console](/docs/codeengine?topic=codeengine-domain-mappings#update-custom-domain-ui)

    * [Updating a domain mapping with the CLI](/docs/codeengine?topic=codeengine-domain-mappings#update-custom-domain-cli)

* [Deleting domain mappings](/docs/codeengine?topic=codeengine-domain-mappings#delete-custom-domain)

    * [Deleting domain mappings from the console](/docs/codeengine?topic=codeengine-domain-mappings#delete-custom-domain-ui)

    * [Deleting domain mappings with the CLI](/docs/codeengine?topic=codeengine-domain-mappings#delete-custom-domain-cli)

* [Next steps](/docs/codeengine?topic=codeengine-domain-mappings#domain-mappings-next)


## Subscribing to event producers
{: #sitemap_subscribing_to_event_producers}


[Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events)

* [Subscriptions for apps and app scaling](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-app-scaling)

* [Subscriptions for jobs and job run limitations](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-jobrun-limits)

* [Eventing metadata](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)

    * [Example HTTP headers for an {{site.data.keyword.cos_full_notm}} event that is sent to an application](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-httpheaders-app)

    * [Example environment variables for an {{site.data.keyword.cos_full_notm}} event that is sent to a job](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-envvars-job)

* [What happens when I create a subscription?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-what-happens)

[Working with the Periodic timer (cron) event producer](/docs/codeengine?topic=codeengine-subscribe-cron#subscribe-cron)

* [Subscribing to Periodic timer (cron) events for an application](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app)

    * [Subscribing to Periodic timer (cron) events for an application from the console](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app-ui)

    * [Subscribing to Periodic timer (cron) events for an application with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-app-cli)

    * [Updating your cron subscription with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#update-cron-sub-cli)

    * [Viewing event information for an application from the console](/docs/codeengine?topic=codeengine-subscribe-cron#view-eventing-cron-app-ui)

    * [Viewing event information for an application with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#view-eventing-cron-app-cli)

    * [Cron header and body information for events delivered to applications](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron)

* [Subscribing to Periodic timer (cron) events for a function](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-fun-existing)

    * [Subscribing to Periodic timer (cron) events for a function from the console](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-fun-ui)

    * [Subscribing to Periodic timer (cron) events for a function with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-existing-fun-cli)

    * [Updating your cron subscription with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#update-cron-sub-fun-cli)

    * [Viewing event information for a function from the console](/docs/codeengine?topic=codeengine-subscribe-cron#view-eventing-cron-fun-ui)

    * [Cron header and body information for events delivered to functions](/docs/codeengine?topic=codeengine-subscribe-cron#sub-header-body-cron-fun)

* [Subscribing to Periodic timer (cron) events for a job](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job)

    * [Subscribing to Periodic timer (cron) events for a job from the console](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job-ui)

    * [Subscribing to Periodic timer (cron) events for a job with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#eventing-cron-job-cli)

    * [Viewing event information for a job from the console](/docs/codeengine?topic=codeengine-subscribe-cron#view-eventing-cron-job-ui)

    * [Viewing event information for a job with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#view-eventing-cron-job-cli)

    * [Environment variables for events that are delivered to jobs](/docs/codeengine?topic=codeengine-subscribe-cron#sub-envir-variables-cron)

* [Defining additional event attributes](/docs/codeengine?topic=codeengine-subscribe-cron#additional-attributes-cron)

* [Deleting a subscription](/docs/codeengine?topic=codeengine-subscribe-cron#subscription-delete-cron)

    * [Deleting a subscription from the console](/docs/codeengine?topic=codeengine-subscribe-cron#subscription-delete-cron-ui)

    * [Deleting a subscription with the CLI](/docs/codeengine?topic=codeengine-subscribe-cron#subscription-delete-cron-cli)

[Working with the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#eventing-cosevent-producer)

* [Setting up the {{site.data.keyword.cos_full_notm}} event producer](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#setup-cosevent-producer)

* [Assigning the Notifications Manager role to {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#notify-mgr-cos)

* [Subscribing to {{site.data.keyword.cos_full_notm}} events for an application](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_app)

    * [Subscribing to {{site.data.keyword.cos_full_notm}} events for an application from the console](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#eventing-cos-app-ui)

    * [Subscribing to {{site.data.keyword.cos_full_notm}} events for an application with the CLI](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#eventing-cos-app-cli)

    * [Viewing event information for an application from the console](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#view-eventing-cos-app-ui)

    * [Viewing event information for an application with the CLI](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#view-eventing-cos-app-cli)

    * [{{site.data.keyword.cos_full_notm}} header and body information for events delivered to applications](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-header-body-cos)

* [Subscribing to {{site.data.keyword.cos_full_notm}} events for a job](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#obstorage_ev_job)

    * [Subscribing to {{site.data.keyword.cos_full_notm}} events for a job from the console](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#eventing-cos-job-ui)

    * [Subscribing to {{site.data.keyword.cos_full_notm}} events for a job with the CLI](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#eventing-cos-job-cli)

    * [Viewing event information for a job from the console](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#view-eventing-cos-job-ui)

    * [Viewing event information for a job with the CLI](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#view-eventing-cos-job-cli)

    * [Environment variables for events delivered to jobs](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#sub-envir-variables-cos)

* [Defining additional event attributes](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#additional-attributes-cos)

* [Deleting a subscription](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#subscription-delete-cos)

    * [Deleting a subscription from the console](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#subscription-delete-cos-ui)

    * [Deleting a subscription with the CLI](/docs/codeengine?topic=codeengine-eventing-cosevent-producer#subscription-delete-cos-cli)

[Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#working-kafkaevent-producer)

* [Setting up the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subkafka-setup-sender)

    * [Setting up the {{site.data.keyword.messagehub}} CLI environment](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#setup-kafka-es-cli)

    * [Setting up your Kafka instance](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#setup-kafka-es-instance)

    * [Setting up a {{site.data.keyword.codeengineshort}} sample app to produce Kafka messages](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#setup-kafka-sender-app)

* [Setting up {{site.data.keyword.codeengineshort}} to receive Kafka events for an app](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#setup-kafka-receiverapp)

    * [Subscribing to Kafka events for an app from the console](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-app-ui)

    * [Subscribing to Kafka events for an app with the CLI](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-app-cli)

    * [Header and body information for Kafka events that are delivered to apps](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subkafka-headerbody-app)

* [Setting up {{site.data.keyword.codeengineshort}} to receive Kafka events for a job](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-job)

    * [Subscribing to Kafka events for a job from the console](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-job-ui)

    * [Subscribing to Kafka events for a job with the CLI](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subscribe-kafka-job-cli)

    * [Environment variables for Kafka events that are delivered to jobs](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subkafka-envvar-job)

* [Viewing and updating Kafka event subscriptions](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-view-update)

    * [Viewing and updating Kafka event subscriptions from the console](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-view-update-ui)

    * [Viewing and updating Kafka event subscriptions with the CLI](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-view-update-cli)

* [Deleting a Kafka event subscription](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-delete)

    * [Deleting a Kafka subscription from the console](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-delete-ui)

    * [Deleting a Kafka subscription with the CLI](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#sub-kafka-delete-cli)

* [Defining additional event attributes](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#additional-attributes-kafka)


## Working with environment variables, secrets, and configmaps
{: #sitemap_working_with_environment_variables_secrets_and_configmaps}


[Working with environment variables](/docs/codeengine?topic=codeengine-envvar#envvar)

* [Creating and updating environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-create)

    * [Creating environment variables from the console](/docs/codeengine?topic=codeengine-envvar#envvar-create-ui)

    * [Updating environment variables from the console](/docs/codeengine?topic=codeengine-envvar#envvar-update-ui)

    * [Creating and updating environment variables with the CLI](/docs/codeengine?topic=codeengine-envvar#envvar-create-cli)

* [Considerations for updating workloads with environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-upd-consider)

* [Deleting environment variables](/docs/codeengine?topic=codeengine-envvar#envvar-delete)

    * [Deleting environment variables from the console](/docs/codeengine?topic=codeengine-envvar#envvar-delete-ui)

    * [Deleting environment variables with the CLI](/docs/codeengine?topic=codeengine-envvar#envvar-delete-cli)

[Working with secrets](/docs/codeengine?topic=codeengine-secret#secret)

* [What are secrets and why would I use them?](/docs/codeengine?topic=codeengine-secret#secret-whatwhy)

    * [What kind of secrets can I create in {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-secret#secret-categories)

* [Creating secrets](/docs/codeengine?topic=codeengine-secret#secret-create)

    * [Creating a secret from the console](/docs/codeengine?topic=codeengine-secret#secret-create-ui)

    * [Creating secrets with the CLI](/docs/codeengine?topic=codeengine-secret#secret-create-cli)

* [Updating secrets](/docs/codeengine?topic=codeengine-secret#secret-update)

    * [Updating secrets from the console](/docs/codeengine?topic=codeengine-secret#secret-update-ui)

    * [Updating secrets with the CLI](/docs/codeengine?topic=codeengine-secret#secret-update-cli)

* [Referencing secrets](/docs/codeengine?topic=codeengine-secret#secret-ref)

    * [Referencing secrets from the console](/docs/codeengine?topic=codeengine-secret#secret-ref-ui)

    * [Referencing secrets with the CLI](/docs/codeengine?topic=codeengine-secret#secret-ref-cli)

* [Deleting secrets](/docs/codeengine?topic=codeengine-secret#secret-delete)

    * [Deleting secrets from the console](/docs/codeengine?topic=codeengine-secret#secret-delete-ui)

    * [Deleting secrets with the CLI](/docs/codeengine?topic=codeengine-secret#secret-delete-cli)

[Working with configmaps](/docs/codeengine?topic=codeengine-configmap#configmap)

* [What are configmaps and why would I use them?](/docs/codeengine?topic=codeengine-configmap#configmap-whatwhy)

* [I see configmaps that I didn't create. Can I delete them?](/docs/codeengine?topic=codeengine-configmap#inside-configmaps)

* [Creating configmaps](/docs/codeengine?topic=codeengine-configmap#configmap-create)

    * [Creating a configmap from the console](/docs/codeengine?topic=codeengine-configmap#configmap-create-ui)

    * [Create a configmap with the CLI](/docs/codeengine?topic=codeengine-configmap#configmap-create-cli)

* [Updating configmaps](/docs/codeengine?topic=codeengine-configmap#configmap-update)

    * [Updating configmaps from the console](/docs/codeengine?topic=codeengine-configmap#configmap-update-ui)

    * [Updating configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap#configmap-update-cli)

* [Referencing configmaps](/docs/codeengine?topic=codeengine-configmap#configmap-ref)

    * [Referencing configmaps from the console](/docs/codeengine?topic=codeengine-configmap#configmap-ref-ui)

    * [Referencing configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap#configmap-ref-cli)

* [Deleting configmaps](/docs/codeengine?topic=codeengine-configmap#configmap-delete)

    * [Deleting configmaps from the console](/docs/codeengine?topic=codeengine-configmap#configmaps-delete-ui)

    * [Deleting configmaps with the CLI](/docs/codeengine?topic=codeengine-configmap#configmap-delete-cli)

[Referencing secrets and configmaps with environment variables (CLI)](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference)

* [Referencing a full secret with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-fullref-cli)

* [Referencing individual keys of a configmap with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-keyref-cli)

* [Overriding references with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-overfull-cli)

    * [Scenario A.  Override a fully referenced secret with another fully referenced secret](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-overfull-withfull-cli)

    * [Scenario B.  Override a fully referenced secret with a key reference](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-overfull-withkey-cli)

    * [Scenario C.  Override key references with new keys](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-overkey-withkey-cli)

* [Removing fully referenced secrets or configmaps with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-fullremove-cli)

* [Removing key references with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference#secretcm-reference-keyremove-cli)

[Referencing secrets and configmaps as mounted files (CLI)](/docs/codeengine?topic=codeengine-secretcm-reference-mountedfiles#secretcm-reference-mountedfiles)

* [Referencing a secret as a mounted file with the CLI](/docs/codeengine?topic=codeengine-secretcm-reference-mountedfiles#secret-reference-mount-file-cli)


## Observability
{: #sitemap_observability}


[Viewing logs](/docs/codeengine?topic=codeengine-logging#logging)

* [Viewing logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-logs-ui)

    * [Considerations for viewing logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-logs-considerations)

    * [Viewing app, job, or function logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-appjobfunctionlogs-ui)

    * [Viewing build logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-build-ui)

* [Viewing logs with the CLI](/docs/codeengine?topic=codeengine-logging&interface=cli#view-logs-cli)

    * [Viewing application logs with the CLI](/docs/codeengine?topic=codeengine-logging&interface=cli#view-applog-cli)

    * [Viewing job logs with the CLI](/docs/codeengine?topic=codeengine-logging&interface=cli#view-joblog-cli)

    * [Viewing build logs with the CLI](/docs/codeengine?topic=codeengine-logging&interface=cli#view-build-cli)

[Auditing events for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-at_events#at_events)

* [List of events from {{site.data.keyword.cloud_notm}} console and CLI actions](/docs/codeengine?topic=codeengine-at_events#list-events-cli-console)

    * [Project events](/docs/codeengine?topic=codeengine-at_events#project-events)

    * [Application events](/docs/codeengine?topic=codeengine-at_events#app-events)

    * [Configmap events](/docs/codeengine?topic=codeengine-at_events#configmap-events)

    * [Secret events](/docs/codeengine?topic=codeengine-at_events#secret-events)

    * [Build and build run events](/docs/codeengine?topic=codeengine-at_events#build-events)

    * [Job and job run events](/docs/codeengine?topic=codeengine-at_events#job-events)

    * [Subscription events](/docs/codeengine?topic=codeengine-at_events#subscription-events)

* [List of events from **`kubectl`** and **`kn`** commands](/docs/codeengine?topic=codeengine-at_events#kubect1-events)

    * [Pod events](/docs/codeengine?topic=codeengine-at_events#kubect1-pod-events)

    * [Service account events](/docs/codeengine?topic=codeengine-at_events#kubect1-serviceaccount-events)

    * [Event events](/docs/codeengine?topic=codeengine-at_events#kubect1-event-events)

    * [Resource quota events](/docs/codeengine?topic=codeengine-at_events#kubect1-resourcequote-events)

    * [Limit range events](/docs/codeengine?topic=codeengine-at_events#kubect1-limitrange-events)

    * [Deployment events](/docs/codeengine?topic=codeengine-at_events#kubect1-deployment-events)

    * [Service binding events](/docs/codeengine?topic=codeengine-at_events#kubect1-servicebinding-events)

* [Viewing events](/docs/codeengine?topic=codeengine-at_events#view)

* [Analyzing events](/docs/codeengine?topic=codeengine-at_events#at_events_analyze)

[Monitoring for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor#monitor)

* [Set up your {{site.data.keyword.mon_full_notm}} service instance](/docs/codeengine?topic=codeengine-monitor#setup-monitor)

* [Accessing your {{site.data.keyword.mon_full_notm}} metrics](/docs/codeengine?topic=codeengine-monitor#access-monitor)

* [Metrics available for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor#metrics-by-plan)

    * [`ibm_codeengine_application_actual_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_actual_instances)

    * [`ibm_codeengine_application_requested_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_requested_instances)

    * [`ibm_codeengine_application_not_ready_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_not_ready_instances)

    * [`ibm_codeengine_application_pending_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_pending_instances)

    * [`ibm_codeengine_application_desired_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_desired_instances)

    * [`ibm_codeengine_application_terminating_instances`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_terminating_instances)

    * [`ibm_codeengine_application_requests_total`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_requests_total)

    * [`ibm_codeengine_application_revision_count`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_revision_count)

    * [`ibm_codeengine_application_service_count`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_service_count)

    * [`ibm_codeengine_application_route_count`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_route_count)

    * [`ibm_codeengine_application_target_concurrency_per_pod`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_target_concurrency_per_pod)

    * [`ibm_codeengine_application_panic_request_concurrency`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_panic_request_concurrency)

    * [`ibm_codeengine_application_stable_request_concurrency`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_stable_request_concurrency)

    * [`ibm_codeengine_application_panic_mode`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_application_panic_mode)

    * [`ibm_codeengine_functions_activations`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_activations)

    * [`ibm_codeengine_functions_exceeded_limit`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_exceeded_limit)

    * [`ibm_codeengine_functions_execution_time_count`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_execution_time_count)

    * [`ibm_codeengine_functions_execution_time_sum`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_execution_time_sum)

    * [`ibm_codeengine_functions_init_time_count`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_init_time_count)

    * [`ibm_codeengine_functions_init_time_sum`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_init_time_sum)

    * [`ibm_codeengine_functions_status_success`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_status_success)

    * [`ibm_codeengine_functions_status_error_application`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_status_error_application)

    * [`ibm_codeengine_functions_status_error_developer`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_functions_status_error_developer)

    * [`ibm_codeengine_jobruns`](/docs/codeengine?topic=codeengine-monitor#ibm_codeengine_jobruns)

* [Attributes for segmentation](/docs/codeengine?topic=codeengine-monitor#attributes)

    * [Global Attributes](/docs/codeengine?topic=codeengine-monitor#global-attributes)

    * [More attributes](/docs/codeengine?topic=codeengine-monitor#additional-attributes)

[Creating custom dashboards to monitor {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor-custom#monitor-custom)

* [Create custom dashboards to monitor {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-monitor-custom#create-custom-monitor)

    * [Scenario 1: Focusing on {{site.data.keyword.codeengineshort}} application instances and job runs](/docs/codeengine?topic=codeengine-monitor-custom#custom-monitor-scenario1)

    * [Scenario 2: Using PromQL queries with {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-monitor-custom#custom-monitor-scenario2)


## Connecting over private networks
{: #sitemap_connecting_over_private_networks}


[Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-vpe#vpe)

* [Using your VPE to manage project resources securely](/docs/codeengine?topic=codeengine-vpe#using-vpes-project)

* [Using your VPE to access an app securely](/docs/codeengine?topic=codeengine-vpe#using-vpes-app)

* [Using your VPE to access a function securely](/docs/codeengine?topic=codeengine-vpe#using-vpes-fun)

[Using service endpoints with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt)

* [Public endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-public-endpoints)

* [Private endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-private-endpoints)

* [Enabling service endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-enabling-service-endpoints)

* [Managing {{site.data.keyword.codeengineshort}} resources securely by using service endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-ce-manageresources)

* [Accessing your app securely with service endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-ce-access-app)

* [Accessing your function securely with service endpoints](/docs/codeengine?topic=codeengine-serviceendpt#serviceendpt-ce-access-fun)


## Enhancing security for Code Engine
{: #sitemap_enhancing_security_for_code_engine}


[Learning about {{site.data.keyword.codeengineshort}} architecture and workload isolation](/docs/codeengine?topic=codeengine-architecture#architecture)

* [{{site.data.keyword.codeengineshort}} workload isolation](/docs/codeengine?topic=codeengine-architecture#workload-isolation)

[Managing user access](/docs/codeengine?topic=codeengine-iam#iam)

* [How do I know which access policies are set for me?](/docs/codeengine?topic=codeengine-iam#iam-accesspolicy)

* [Managing access by using access groups](/docs/codeengine?topic=codeengine-iam#groups)

* [Managing access by assigning policies directly to users](/docs/codeengine?topic=codeengine-iam#users)

* [{{site.data.keyword.cloud_notm}} platform roles](/docs/codeengine?topic=codeengine-iam#platform)

* [{{site.data.keyword.cloud_notm}} service roles](/docs/codeengine?topic=codeengine-iam#service)

* [{{site.data.keyword.codeengineshort}} CLI access requirements](/docs/codeengine?topic=codeengine-iam#cli-access-req)

* [{{site.data.keyword.codeengineshort}} container registry requirements](/docs/codeengine?topic=codeengine-iam#container-registry-access-req)

* [{{site.data.keyword.codeengineshort}} service binding access requirements](/docs/codeengine?topic=codeengine-iam#service-binding-access-req)

* [{{site.data.keyword.codeengineshort}} access requirements for your toolchain](/docs/codeengine?topic=codeengine-iam#toolchain-access-req)

[Securing your data in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-mng-data#mng-data)

* [How your data is stored and encrypted in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-mng-data#data-storage)

* [Deleting your data in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-mng-data#data-delete)

[{{site.data.keyword.codeengineshort}} and security](/docs/codeengine?topic=codeengine-secure#secure)

* [Supported TLS versions and cipher suites](/docs/codeengine?topic=codeengine-secure#secure-tls)

    * [TLS cipher suites](/docs/codeengine?topic=codeengine-secure#secure-cipher-suites)

* [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos)

[Protecting {{site.data.keyword.codeengineshort}} resources with context-based restrictions](/docs/codeengine?topic=codeengine-cbr#cbr)

[{{site.data.keyword.codeengineshort}} public and private IP addresses](/docs/codeengine?topic=codeengine-network-addresses#network-addresses)


## CLI reference
{: #sitemap_cli_reference}


[{{site.data.keyword.codeenginefull_notm}} CLI](/docs/codeengine?topic=codeengine-cli#cli)

* [Prerequisites](/docs/codeengine?topic=codeengine-cli#codeengine-cli-prereq)

* [Application commands](/docs/codeengine?topic=codeengine-cli#cli-application)

    * [`ibmcloud ce application bind`](/docs/codeengine?topic=codeengine-cli#cli-application-bind)

    * [`ibmcloud ce application create`](/docs/codeengine?topic=codeengine-cli#cli-application-create)

    * [`ibmcloud ce application delete`](/docs/codeengine?topic=codeengine-cli#cli-application-delete)

    * [`ibmcloud ce application events`](/docs/codeengine?topic=codeengine-cli#cli-application-events)

    * [`ibmcloud ce application get`](/docs/codeengine?topic=codeengine-cli#cli-application-get)

    * [`ibmcloud ce application list`](/docs/codeengine?topic=codeengine-cli#cli-application-list)

    * [`ibmcloud ce application logs`](/docs/codeengine?topic=codeengine-cli#cli-application-logs)

    * [`ibmcloud ce application restart`](/docs/codeengine?topic=codeengine-cli#cli-application-restart)

    * [`ibmcloud ce application unbind`](/docs/codeengine?topic=codeengine-cli#cli-application-unbind)

    * [`ibmcloud ce application update`](/docs/codeengine?topic=codeengine-cli#cli-application-update)

* [Build commands](/docs/codeengine?topic=codeengine-cli#cli-build)

    * [`ibmcloud ce build create`](/docs/codeengine?topic=codeengine-cli#cli-build-create)

    * [`ibmcloud ce build delete`](/docs/codeengine?topic=codeengine-cli#cli-build-delete)

    * [`ibmcloud ce build get`](/docs/codeengine?topic=codeengine-cli#cli-build-get)

    * [`ibmcloud ce build list`](/docs/codeengine?topic=codeengine-cli#cli-build-list)

    * [`ibmcloud ce build update`](/docs/codeengine?topic=codeengine-cli#cli-build-update)

* [Buildrun commands](/docs/codeengine?topic=codeengine-cli#cli-buildrun)

    * [`ibmcloud ce buildrun cancel`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-cancel)

    * [`ibmcloud ce buildrun delete`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-delete)

    * [`ibmcloud ce buildrun events`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-events)

    * [`ibmcloud ce buildrun get`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-get)

    * [`ibmcloud ce buildrun list`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-list)

    * [`ibmcloud ce buildrun logs`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-logs)

    * [`ibmcloud ce buildrun submit`](/docs/codeengine?topic=codeengine-cli#cli-buildrun-submit)

* [Configmap commands](/docs/codeengine?topic=codeengine-cli#cli-configmap)

    * [`ibmcloud ce configmap create`](/docs/codeengine?topic=codeengine-cli#cli-configmap-create)

    * [`ibmcloud ce configmap delete`](/docs/codeengine?topic=codeengine-cli#cli-configmap-delete)

    * [`ibmcloud ce configmap get`](/docs/codeengine?topic=codeengine-cli#cli-configmap-get)

    * [`ibmcloud ce configmap list`](/docs/codeengine?topic=codeengine-cli#cli-configmap-list)

    * [`ibmcloud ce configmap update`](/docs/codeengine?topic=codeengine-cli#cli-configmap-update)

* [Domainmapping commands](/docs/codeengine?topic=codeengine-cli#cli-domainmapping)

    * [`ibmcloud ce domainmapping create`](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-create)

    * [`ibmcloud ce domainmapping delete`](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-delete)

    * [`ibmcloud ce domainmapping get`](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-get)

    * [`ibmcloud ce domainmapping list`](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-list)

    * [`ibmcloud ce domainmapping update`](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-update)

* [Function commands](/docs/codeengine?topic=codeengine-cli#cli-function)

    * [`ibmcloud ce function bind`](/docs/codeengine?topic=codeengine-cli#cli-function-bind)

    * [`ibmcloud ce function create`](/docs/codeengine?topic=codeengine-cli#cli-function-create)

    * [`ibmcloud ce function delete`](/docs/codeengine?topic=codeengine-cli#cli-function-delete)

    * [`ibmcloud ce function get`](/docs/codeengine?topic=codeengine-cli#cli-function-get)

    * [`ibmcloud ce function list`](/docs/codeengine?topic=codeengine-cli#cli-function-list)

    * [`ibmcloud ce function runtimes`](/docs/codeengine?topic=codeengine-cli#cli-function-runtimes)

    * [`ibmcloud ce function unbind`](/docs/codeengine?topic=codeengine-cli#cli-function-unbind)

    * [`ibmcloud ce function update`](/docs/codeengine?topic=codeengine-cli#cli-function-update)

* [Help command](/docs/codeengine?topic=codeengine-cli#cli-help)

    * [`ibmcloud ce help`](/docs/codeengine?topic=codeengine-cli#cli-helpcmd)

* [Job commands](/docs/codeengine?topic=codeengine-cli#cli-job)

    * [`ibmcloud ce job bind`](/docs/codeengine?topic=codeengine-cli#cli-job-bind)

    * [`ibmcloud ce job create`](/docs/codeengine?topic=codeengine-cli#cli-job-create)

    * [`ibmcloud ce job delete`](/docs/codeengine?topic=codeengine-cli#cli-job-delete)

    * [`ibmcloud ce job get`](/docs/codeengine?topic=codeengine-cli#cli-job-get)

    * [`ibmcloud ce job list`](/docs/codeengine?topic=codeengine-cli#cli-job-list)

    * [`ibmcloud ce job unbind`](/docs/codeengine?topic=codeengine-cli#cli-job-unbind)

    * [`ibmcloud ce job update`](/docs/codeengine?topic=codeengine-cli#cli-job-update)

* [Jobrun commands](/docs/codeengine?topic=codeengine-cli#cli-jobrun)

    * [`ibmcloud ce jobrun delete`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-delete)

    * [`ibmcloud ce jobrun events`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-events)

    * [`ibmcloud ce jobrun get`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-get)

    * [`ibmcloud ce jobrun list`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-list)

    * [`ibmcloud ce jobrun logs`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs)

    * [`ibmcloud ce jobrun restart`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-restart)

    * [`ibmcloud ce jobrun resubmit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-resubmit)

    * [`ibmcloud ce jobrun submit`](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit)

* [Project commands](/docs/codeengine?topic=codeengine-cli#cli-project)

    * [`ibmcloud ce project create`](/docs/codeengine?topic=codeengine-cli#cli-project-create)

    * [`ibmcloud ce project current`](/docs/codeengine?topic=codeengine-cli#cli-project-current)

    * [`ibmcloud ce project delete`](/docs/codeengine?topic=codeengine-cli#cli-project-delete)

    * [`ibmcloud ce project get`](/docs/codeengine?topic=codeengine-cli#cli-project-get)

    * [`ibmcloud ce project list`](/docs/codeengine?topic=codeengine-cli#cli-project-list)

    * [`ibmcloud ce project restore`](/docs/codeengine?topic=codeengine-cli#cli-project-restore)

    * [`ibmcloud ce project select`](/docs/codeengine?topic=codeengine-cli#cli-project-select)

    * [`ibmcloud ce project tag`](/docs/codeengine?topic=codeengine-cli#cli-project-tag)

    * [`ibmcloud ce project update`](/docs/codeengine?topic=codeengine-cli#cli-project-update)

* [Reclamation commands](/docs/codeengine?topic=codeengine-cli#cli-reclamation)

    * [`ibmcloud ce reclamation delete`](/docs/codeengine?topic=codeengine-cli#cli-reclamation-delete)

    * [`ibmcloud ce reclamation get`](/docs/codeengine?topic=codeengine-cli#cli-reclamation-get)

    * [`ibmcloud ce reclamation list`](/docs/codeengine?topic=codeengine-cli#cli-reclamation-list)

    * [`ibmcloud ce reclamation restore`](/docs/codeengine?topic=codeengine-cli#cli-reclamation-restore)

* [Registry commands](/docs/codeengine?topic=codeengine-cli#cli-registry)

    * [`ibmcloud ce registry create`](/docs/codeengine?topic=codeengine-cli#cli-registry-create)

    * [`ibmcloud ce registry delete`](/docs/codeengine?topic=codeengine-cli#cli-registry-delete)

    * [`ibmcloud ce registry get`](/docs/codeengine?topic=codeengine-cli#cli-registry-get)

    * [`ibmcloud ce registry list`](/docs/codeengine?topic=codeengine-cli#cli-registry-list)

    * [`ibmcloud ce registry update`](/docs/codeengine?topic=codeengine-cli#cli-registry-update)

* [Repo commands](/docs/codeengine?topic=codeengine-cli#cli-repo)

    * [`ibmcloud ce repo create`](/docs/codeengine?topic=codeengine-cli#cli-repo-create)

    * [`ibmcloud ce repo delete`](/docs/codeengine?topic=codeengine-cli#cli-repo-delete)

    * [`ibmcloud ce repo get`](/docs/codeengine?topic=codeengine-cli#cli-repo-get)

    * [`ibmcloud ce repo list`](/docs/codeengine?topic=codeengine-cli#cli-repo-list)

    * [`ibmcloud ce repo update`](/docs/codeengine?topic=codeengine-cli#cli-repo-update)

* [Revision commands](/docs/codeengine?topic=codeengine-cli#cli-revision)

    * [`ibmcloud ce revision delete`](/docs/codeengine?topic=codeengine-cli#cli-revision-delete)

    * [`ibmcloud ce revision events`](/docs/codeengine?topic=codeengine-cli#cli-revision-events)

    * [`ibmcloud ce revision get`](/docs/codeengine?topic=codeengine-cli#cli-revision-get)

    * [`ibmcloud ce revision list`](/docs/codeengine?topic=codeengine-cli#cli-revision-list)

    * [`ibmcloud ce revision logs`](/docs/codeengine?topic=codeengine-cli#cli-revision-logs)

* [Secret commands](/docs/codeengine?topic=codeengine-cli#cli-secret)

    * [`ibmcloud ce secret create`](/docs/codeengine?topic=codeengine-cli#cli-secret-create)

    * [`ibmcloud ce secret delete`](/docs/codeengine?topic=codeengine-cli#cli-secret-delete)

    * [`ibmcloud ce secret get`](/docs/codeengine?topic=codeengine-cli#cli-secret-get)

    * [`ibmcloud ce secret list`](/docs/codeengine?topic=codeengine-cli#cli-secret-list)

    * [`ibmcloud ce secret update`](/docs/codeengine?topic=codeengine-cli#cli-secret-update)

* [Subscription cos commands](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos)

    * [`ibmcloud ce subscription cos create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-create)

    * [`ibmcloud ce subscription cos delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-delete)

    * [`ibmcloud ce subscription cos get`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-get)

    * [`ibmcloud ce subscription cos list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-list)

    * [`ibmcloud ce subscription cos update`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cos-update)

* [Subscription cron commands](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron)

    * [`ibmcloud ce subscription cron create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-create)

    * [`ibmcloud ce subscription cron delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-delete)

    * [`ibmcloud ce subscription cron get`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-get)

    * [`ibmcloud ce subscription cron list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-list)

    * [`ibmcloud ce subscription cron update`](/docs/codeengine?topic=codeengine-cli#cli-subscription-cron-update)

* [Subscription `kafka` commands](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka)

    * [`ibmcloud ce subscription kafka create`](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create)

    * [`ibmcloud ce subscription kafka delete`](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-delete)

    * [`ibmcloud ce subscription kafka get`](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-get)

    * [`ibmcloud ce subscription kafka list`](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-list)

    * [`ibmcloud ce subscription kafka update`](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-update)

* [Version command](/docs/codeengine?topic=codeengine-cli#cli-version)

    * [`ibmcloud ce version`](/docs/codeengine?topic=codeengine-cli#cli-versioncmd)

[CLI version history](/docs/codeengine?topic=codeengine-cli_versions#cli_versions)

[Getting started with the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-cecli-getstart#cecli-getstart)

* [Setting up your CLI environment](/docs/codeengine?topic=codeengine-cecli-getstart#cecli-getstart-setup)

* [Working with the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-cecli-getstart#cecli-getstart-workcecli)

* [Next steps](/docs/codeengine?topic=codeengine-cecli-getstart#cecli-getstart-next)


## API reference
{: #sitemap_api_reference}


[Code Engine API](https://cloud.ibm.com/apidocs/codeengine){: external}

[API change log](/docs/codeengine?topic=codeengine-api-changelog#api-changelog)

* [API versioning](/docs/codeengine?topic=codeengine-api-changelog#api-versioning)

    * [Active version dates](/docs/codeengine?topic=codeengine-api-changelog#active-version-dates)

* [21 November 2024](/docs/codeengine?topic=codeengine-api-changelog#21-november-2024)

* [17 May 2024](/docs/codeengine?topic=codeengine-api-changelog#17-may-2024)

* [30 January 2024](/docs/codeengine?topic=codeengine-api-changelog#30-jan-2024)

* [04 January 2024](/docs/codeengine?topic=codeengine-api-changelog#04-jan-2024)

* [03 November 2023](/docs/codeengine?topic=codeengine-api-changelog#03-nov-2023)

* [27 September 2023](/docs/codeengine?topic=codeengine-api-changelog#27-sep-2023)

* [22 June 2023](/docs/codeengine?topic=codeengine-api-changelog#22-june-2023)

* [30 May 2023](/docs/codeengine?topic=codeengine-api-changelog#30-may-2023)

* [27 March 2023](/docs/codeengine?topic=codeengine-api-changelog#27-mar-2023)

* [9 December 2022](/docs/codeengine?topic=codeengine-api-changelog#9-dec-2022)

[Getting started with the {{site.data.keyword.codeengineshort}} REST API](/docs/codeengine?topic=codeengine-ceapi-getstart#ceapi-getstart)

* [Setting up your API environment](/docs/codeengine?topic=codeengine-ceapi-getstart#ceapi-getstart-setup)

* [Working with a {{site.data.keyword.codeengineshort}} application in the API](/docs/codeengine?topic=codeengine-ceapi-getstart#ceapi-getstart-workapps)

* [Next steps](/docs/codeengine?topic=codeengine-ceapi-getstart#ceapi-getstart-next)


## Automatically injected environment variables
{: #sitemap_automatically_injected_environment_variables}


[Automatically injected environment variables](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars)

* [Automatically injected environment variables for applications](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-app)

* [Automatically injected environment variables for functions](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-fun)

* [Automatically injected environment variables for jobs](/docs/codeengine?topic=codeengine-inside-env-vars#inside-env-vars-jobs)


## Defining commands and arguments for your workloads
{: #sitemap_defining_commands_and_arguments_for_your_workloads}


[Defining commands and arguments for your workloads](/docs/codeengine?topic=codeengine-cmd-args#cmd-args)


## Limits and quotas for {{site.data.keyword.codeengineshort}}
{: #sitemap_limits_and_quotas_for_}


[Limits and quotas for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-limits#limits)

* [Application defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_application)

* [Job defaults and limits](/docs/codeengine?topic=codeengine-limits#limits_job)

    * [Job size limit](/docs/codeengine?topic=codeengine-limits#job_size_limit)

* [Function limits](/docs/codeengine?topic=codeengine-limits#limits_functions)

* [Periodic timer (cron) subscription limits](/docs/codeengine?topic=codeengine-limits#subscription-cron-limit)

* [Project limits](/docs/codeengine?topic=codeengine-limits#limits_projects)

* [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas)

* [Increasing limits](/docs/codeengine?topic=codeengine-limits#increase-limits)


## Supported memory and CPU combinations
{: #sitemap_supported_memory_and_cpu_combinations}


[Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo#mem-cpu-combo)

* [Supported combinations for apps and jobs](/docs/codeengine?topic=codeengine-mem-cpu-combo#supported-combo)

* [Supported combinations for functions](/docs/codeengine?topic=codeengine-mem-cpu-combo#supported-combo-fun)

* [Units of measurement](/docs/codeengine?topic=codeengine-mem-cpu-combo#unit-measurements)


## Regions
{: #sitemap_regions}


[Regions](/docs/codeengine?topic=codeengine-regions#regions)

* [{{site.data.keyword.codeengineshort}} endpoints for managing project resources](/docs/codeengine?topic=codeengine-regions#endpoints-project)

* [{{site.data.keyword.codeengineshort}} endpoints for accessing applications](/docs/codeengine?topic=codeengine-regions#endpoints-app)


## Provided TLS certificates for {{site.data.keyword.codeengineshort}} projects
{: #sitemap_provided_tls_certificates_for_projects}


[Provided TLS certificates for {{site.data.keyword.codeengineshort}} projects](/docs/codeengine?topic=codeengine-tls-certificate#tls-certificate)

* [About certificates](/docs/codeengine?topic=codeengine-tls-certificate#certificates-about)

* [{{site.data.keyword.codeengineshort}} certificates and their certificate authority](/docs/codeengine?topic=codeengine-tls-certificate#ce-certificates-about)

    * [Let's Encrypt as the certificate authority](/docs/codeengine?topic=codeengine-tls-certificate#ce-certificates-lets-encrypt)

    * [Need more control?](/docs/codeengine?topic=codeengine-tls-certificate#ce-certificates-lets-encrypt-more-control)


## Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}
{: #sitemap_understanding_your_responsibilities_when_using_}


[Understanding your responsibilities when using {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-responsibilities-ce#responsibilities-ce)

* [Tasks for shared responsibilities by area](/docs/codeengine?topic=codeengine-responsibilities-ce#task-responsibilities)

    * [Incident and operations management](/docs/codeengine?topic=codeengine-responsibilities-ce#incident-and-ops)

    * [Change management](/docs/codeengine?topic=codeengine-responsibilities-ce#change-management)

    * [Identity and access management](/docs/codeengine?topic=codeengine-responsibilities-ce#iam-responsibilities)

    * [Security and regulation compliance](/docs/codeengine?topic=codeengine-responsibilities-ce#security-compliance)

    * [Disaster recovery](/docs/codeengine?topic=codeengine-responsibilities-ce#disaster-recovery)


## Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}
{: #sitemap_understanding_high_availability_and_disaster_recovery_for_}


[Understanding high availability and disaster recovery for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-ha-dr#ha-dr)

* [{{site.data.keyword.codeengineshort}} regions](/docs/codeengine?topic=codeengine-ha-dr#ha-dr-regions)

* [Availability of {{site.data.keyword.codeengineshort}} instances](/docs/codeengine?topic=codeengine-ha-dr#ha-dr-availability)

* [Disaster Recovery for {{site.data.keyword.codeengineshort}} instances](/docs/codeengine?topic=codeengine-ha-dr#ha-dr-disaster)

* [Backing up your {{site.data.keyword.codeengineshort}} instances](/docs/codeengine?topic=codeengine-ha-dr#ha-dr-backup)


## Understanding data portability for {{site.data.keyword.codeengineshort}}
{: #sitemap_understanding_data_portability_for_}


[Understanding data portability for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-data-portability#data-portability)

* [Responsibilities](/docs/codeengine?topic=codeengine-data-portability#data-portability-responsibilities)

* [Data export procedures](/docs/codeengine?topic=codeengine-data-portability#data-portability-procedures)

    * [Tools required for exporting data](/docs/codeengine?topic=codeengine-data-portability#tools-required-for-exporting-data)

    * [Exporting `project` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-project-configuration)

    * [Exporting a `KUBECONFIG` to export project entities](/docs/codeengine?topic=codeengine-data-portability#exporting-a-kubeconfig-to-export-project-entities)

    * [Exporting `application` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-application-configuration)

    * [Exporting `application revision` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-application-revision-configuration)

    * [Exporting `build` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-build-configuration)

    * [Exporting `build run` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-build-run-configuration)

    * [Exporting `configmap` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-configmap-configuration)

    * [Exporting `secret` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-secret-configuration)

    * [Exporting `domain mapping` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-domain-mapping-configuration)

    * [Exporting `{{site.data.keyword.cos_full_notm}} event subscription` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting--event-subscription-configuration)

    * [Exporting `cron event subscription` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-cron-event-subscription-configuration)

    * [Exporting `Kafka event subscription` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-kafka-event-subscription-configuration)

    * [Exporting `function` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-function-configuration)

    * [Exporting `job` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-job-configuration)

    * [Exporting `job run` configuration](/docs/codeengine?topic=codeengine-data-portability#exporting-job-run-configuration)

* [Exported data formats](/docs/codeengine?topic=codeengine-data-portability#data-portability-data-formats)

* [Data ownership](/docs/codeengine?topic=codeengine-data-portability#data-portability-ownership)


## Supported IBM Cloud and third-party integrations
{: #sitemap_supported_ibm_cloud_and_third-party_integrations}


[Supported integrations for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-supported-integrations#supported-integrations)

* [{{site.data.keyword.cloud_notm}} integrations](/docs/codeengine?topic=codeengine-supported-integrations#supported-cloud-integrations)

* [Third-party integrations](/docs/codeengine?topic=codeengine-supported-integrations#supported-third-integrations)

[Running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops#lithops)

* [Running your first flow by using the Lithops framework](/docs/codeengine?topic=codeengine-lithops#first-lithops)

    * [Installing Lithops](/docs/codeengine?topic=codeengine-lithops#install-lithops)

    * [Setting up a storage backend for Lithops](/docs/codeengine?topic=codeengine-lithops#storage-lithops)

    * [Deploy your first {{site.data.keyword.codeengineshort}} job by using Lithops](/docs/codeengine?topic=codeengine-lithops#running-first)

    * [Next steps for Lithops](/docs/codeengine?topic=codeengine-lithops#nextsteps-lithops)

[Validating your application code and latency with Iter8](/docs/codeengine?topic=codeengine-slovalidationtut#slovalidationtut)

* [Finding the URL of your {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-slovalidationtut#geturl-slovalidationtut)

* [Running the Iter8 Docker container](/docs/codeengine?topic=codeengine-slovalidationtut#running-slovalidationtut)

* [Initializing the Iter8 Docker container](/docs/codeengine?topic=codeengine-slovalidationtut#initialize-slovalidationtut)

* [Validating service-level objectives (SLOs)](/docs/codeengine?topic=codeengine-slovalidationtut#experiment-slovalidationtut)

* [Getting the results of the SLO validation](/docs/codeengine?topic=codeengine-slovalidationtut#results-slovalidationtut)

* [Rolling back a revision](/docs/codeengine?topic=codeengine-slovalidationtut#rollout-slovalidationtut)

* [Removing the Iter8 container](/docs/codeengine?topic=codeengine-slovalidationtut#cleanup-slovalidationtut)

* [Next steps for Iter8](/docs/codeengine?topic=codeengine-slovalidationtut#nextsteps-slovalidationtut)

[Securing your application with Guard](/docs/codeengine?topic=codeengine-getting-started-with-guard#getting-started-with-guard)

* [Deploy a guard-learner application as a per-project service](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-learner)

* [Creating and deploying a protected Hello World application](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-deploy-app)

* [Finding the namespace and service URLs](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-get-parameters)

* [Exposing the Hello World application to the internet through Guard](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-expose-app)

* [Managing the security of the Hello World application and gaining situational awareness](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-situational-awareness)

* [Clean up the tutorial applications](/docs/codeengine?topic=codeengine-getting-started-with-guard#guard-cleanup)


## Pricing for {{site.data.keyword.codeengineshort}}
{: #sitemap_pricing_for_}


[Pricing for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-pricing#pricing)

* [Application pricing](/docs/codeengine?topic=codeengine-pricing#app-pricing)

* [Job pricing](/docs/codeengine?topic=codeengine-pricing#job-pricing)

* [Function pricing](/docs/codeengine?topic=codeengine-pricing#functions-pricing)

* [Build pricing](/docs/codeengine?topic=codeengine-pricing#build-pricing)


## {{site.data.keyword.codeengineshort}} notices
{: #sitemap__notices}


[{{site.data.keyword.codeengineshort}} notices](/docs/codeengine?topic=codeengine-notices#notices)

* [CREATIVE COMMONS ATTRIBUTION 2.0 GENERIC](/docs/codeengine?topic=codeengine-notices#cca2gen)

* [CREATIVE COMMONS ATTRIBUTION 2.5 GENERIC](/docs/codeengine?topic=codeengine-notices#cca25gen)

* [CREATIVE COMMONS ATTRIBUTION 3.0 GENERIC](/docs/codeengine?topic=codeengine-notices#cca3gen)

* [CREATIVE COMMONS ATTRIBUTION 4.0 GENERIC](/docs/codeengine?topic=codeengine-notices#cca4gen)


## Using Kubernetes with {{site.data.keyword.codeengineshort}}
{: #sitemap_using_kubernetes_with_}


[Using Kubernetes with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-kubernetes#kubernetes)

* [Installing the Kubernetes command-line interface](/docs/codeengine?topic=codeengine-kubernetes#kubernetes-kubectl)

* [Interacting with Kubernetes API](/docs/codeengine?topic=codeengine-kubernetes#kubectl-kubeconfig)

* [Required access authorities to work with Kubernetes API](/docs/codeengine?topic=codeengine-kubernetes#kubectl-api)

* [Retrieving your Kubernetes configuration](/docs/codeengine?topic=codeengine-kubernetes#kubernetes-getconfig)

    * [Retrieve your Kubernetes configuration with REST API](/docs/codeengine?topic=codeengine-kubernetes#api-rest)

    * [Retrieve your Kubernetes configuration with the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-kubernetes#api-cli)

* [Custom resource definition (CRD)](/docs/codeengine?topic=codeengine-kubernetes#kubernetes-api-crd)

    * [Batch CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-batch)

    * [Function CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-function)

    * [Serving CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-serving)

    * [Source-to-image CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-s2i)

    * [Subscription CRD methods](/docs/codeengine?topic=codeengine-kubernetes#api-crd-subscription)


## Using Knative with Code Engine
{: #sitemap_using_knative_with_code_engine}


[Using Knative with Code Engine](/docs/codeengine?topic=codeengine-knative#knative)

* [What is the supported version of Knative?](/docs/codeengine?topic=codeengine-knative#knative-version)

* [Installing the Knative command-line interface](/docs/codeengine?topic=codeengine-knative#knative-kubectl)

* [Interacting with Kubernetes API](/docs/codeengine?topic=codeengine-knative#kubectl-kubeconfig-knative)

* [Required access authorities to work with Knative API](/docs/codeengine?topic=codeengine-knative#knative-api)


## FAQs
{: #sitemap_faqs}


[FAQs](/docs/codeengine?topic=codeengine-faqs#faqs)

* [What is {{site.data.keyword.codeenginefull_notm}}?](/docs/codeengine?topic=codeengine-faqs#what-is-codeengine)

* [What is a project?](/docs/codeengine?topic=codeengine-faqs#what-is-project)

* [Where can I find code samples?](/docs/codeengine?topic=codeengine-faqs#find-code-samples)

* [I need more memory! Can I increase my limits?](/docs/codeengine?topic=codeengine-faqs#increase-ce-limits)

* [Do I need a Docker Hub account to use {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-faqs#dockerhub-options)

* [What is the difference between a Docker build on my system and a build in {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild)

* [Why do images that are built with non-Intel processors not work with {{site.data.keyword.codeengineshort}}?](/docs/codeengine?topic=codeengine-faqs#buildimage-nonintel)

* [Do {{site.data.keyword.codeengineshort}} apps support WebSockets?](/docs/codeengine?topic=codeengine-faqs#app-websockets)

* [Do {{site.data.keyword.codeengineshort}} apps support gRPC?](/docs/codeengine?topic=codeengine-faqs#app-grpc-supported)

* [Does {{site.data.keyword.codeengineshort}} provide a way to limit access to a particular entity within a {{site.data.keyword.codeengineshort}} project?](/docs/codeengine?topic=codeengine-faqs#limit-access-fun)

* [Does {{site.data.keyword.codeengineshort}} provide an OpenAPI specification for the deployed function?](/docs/codeengine?topic=codeengine-faqs#openapi-spec-fun)

* [How can I review the {{site.data.keyword.codeengineshort}} service terms?](/docs/codeengine?topic=codeengine-faqs#review-service-terms)

* [How can I give feedback?](/docs/codeengine?topic=codeengine-faqs#give-feedback)


## Learning paths for {{site.data.keyword.codeengineshort}}
{: #sitemap_learning_paths_for_}


[Learning paths for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-learning-paths#learning-paths)

* [Plan your deployments](/docs/codeengine?topic=codeengine-learning-paths#lp-plan-deployments)

* [Install the tools](/docs/codeengine?topic=codeengine-learning-paths#lp-install-tools)

* [Create your first project](/docs/codeengine?topic=codeengine-learning-paths#lp-set-environment)

* [Develop your application, job, or function](/docs/codeengine?topic=codeengine-learning-paths#lp-develop-app-job)

    * [Do you have source code or a container image for your application or job?](/docs/codeengine?topic=codeengine-learning-paths#lp-develop-app-job-source-code-image)

* [Deploy your application](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app)

    * [How does your application scale?](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app-how-app-scale)

    * [Do yo want to customize your application?](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app-customize-app)

    * [Are you ready to deploy?](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app-ready-to-deploy)

    * [Do you want to add more customizations?](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app-add-customizations)

    * [Are you ready to access your application?](/docs/codeengine?topic=codeengine-learning-paths#lp-deploy-app-ready-to-access-app)

* [Run your job](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job)

    * [Do you want to create a job definition?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job-create-job-definition)

    * [Do you want to run a job without first creating a definition?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job_run-job-without-definition)

    * [Do you want to customize your job?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job-customize-job)

    * [Are you ready to create and run your job?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job_ready-to-create-run-job)

    * [Do you want to add more customizations?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-job-add-customizations)

* [Run your Function](/docs/codeengine?topic=codeengine-learning-paths#lp-run-fun)

    * [Do you want to customize your function?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-fun-customize)

    * [Areyou ready to deploy?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-fun-ready-to-deploy)

    * [Do you want to add more customizations?](/docs/codeengine?topic=codeengine-learning-paths#lp-run-fun-add-customizations)

* [Log and monitor your workloads](/docs/codeengine?topic=codeengine-learning-paths#lp-log-mon)

* [Migrate your workloads](/docs/codeengine?topic=codeengine-learning-paths#lp-migrate)


## Troubleshooting
{: #sitemap_troubleshooting}


[Troubleshooting overview](/docs/codeengine?topic=codeengine-troubleshooting_over#troubleshooting_over)

* [General ways to resolve issues](/docs/codeengine?topic=codeengine-troubleshooting_over#help-general)

* [Reviewing Cloud issues and status](/docs/codeengine?topic=codeengine-troubleshooting_over#help-cloud-status)

* [Getting help](/docs/codeengine?topic=codeengine-troubleshooting_over#help-functions)


### Troubleshooting apps
{: #sitemap_troubleshooting_apps}


[Debugging apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#troubleshoot-apps)

* [App limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-limits)

* [Confirm port value](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-port)

* [Getting logs for my apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettinglogs)

* [Getting details about app instances](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-instancedetails)

* [Getting system event information for my apps](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-gettingevent)

* [Verifying the container image reference for my app](/docs/codeengine?topic=codeengine-troubleshoot-apps#ts-app-verifyimage)

[Why is my app create failing?](/docs/codeengine?topic=codeengine-ts-app-create-fails#ts-app-create-fails)

[Why doesn't my app ever become ready?](/docs/codeengine?topic=codeengine-ts-app-neverready#ts-app-neverready)

[Why did my app stop running?](/docs/codeengine?topic=codeengine-ts-app-end#ts-app-end)

[Why did my app restart?](/docs/codeengine?topic=codeengine-ts-app-restart#ts-app-restart)

[How can I add my {{site.data.keyword.codeengineshort}} app to an allowlist?](/docs/codeengine?topic=codeengine-ts-allowlist-app#ts-allowlist-app)

[Why does my app connection fail?](/docs/codeengine?topic=codeengine-ts-app-connection-fail#ts-app-connection-fail)

* [Updating your app timeout value from the console](/docs/codeengine?topic=codeengine-ts-app-connection-fail#ts-app-timeout-console)

* [Updating your app timeout value with the CLI](/docs/codeengine?topic=codeengine-ts-app-connection-fail#ts-app-timeout-cli)

[Why does my app connection fail when using a proxy?](/docs/codeengine?topic=codeengine-ts-app-connection-failwithproxy#ts-app-connection-failwithproxy)

[Can I stop my app?](/docs/codeengine?topic=codeengine-ts-app-stop-traffic#ts-app-stop-traffic)

[Why aren't my app instances scaling down as expected?](/docs/codeengine?topic=codeengine-ts-app-domain-notscaledown#ts-app-domain-notscaledown)

[Why does my port scan show more open ports than expected?](/docs/codeengine?topic=codeengine-ts-app-toomanyports#ts-app-toomanyports)


### Troubleshooting builds
{: #sitemap_troubleshooting_builds}


[Debugging builds](/docs/codeengine?topic=codeengine-troubleshoot-build#troubleshoot-build)

* [Build limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-limits)

* [Getting logs for my builds](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettinglogs)

    * [Getting logs for my builds from the console](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettinglogs-ui)

    * [Getting logs for my builds with the CLI](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettinglogs-cli)

* [Getting system event information for my builds](/docs/codeengine?topic=codeengine-troubleshoot-build#ts-build-gettingevent)

[How can I verify my image reference?](/docs/codeengine?topic=codeengine-ts-build-verify-image#ts-build-verify-image)

[Build fails when the build did not register correctly and a secret does not exist](/docs/codeengine?topic=codeengine-ts-build-notreg-nosecret#ts-build-notreg-nosecret)

[Build fails in the source step](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-gitsource-stepfail)

* [Resolution for a non-existent repository during build](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-noexistrepo)

* [Resolution for a wrong protocol or missing secret during build](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-wrongprotocol)

    * [For public repositories](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-wrongprotocol-public)

    * [For private repositories](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-wrongprotocol-private)

* [Resolution for a wrong revision during build](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-wrongrevision)

* [Resolution for an expired SSH key during build](/docs/codeengine?topic=codeengine-ts-build-gitsource-stepfail#ts-build-expiredsshkey)

[Build fails when the ephemeral storage limit is exceeded](/docs/codeengine?topic=codeengine-ts-build-ephemeral-limit#ts-build-ephemeral-limit)

[Build fails when the memory limit is exceeded](/docs/codeengine?topic=codeengine-ts-build-memory-limit#ts-build-memory-limit)

[Build fails in the build and push step](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-bldpush-stepfail)

* [Resolution for memory limit during build](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-memorylimit)

* [Resolution for a container registry problem during build](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-containerregistryprob)

* [Resolution for Dockerfile not found during build](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-dockerfile-notfound)

* [Resolution for {{site.data.keyword.registryfull_notm}} quota limit is reached during build](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-icrquota)

* [Resolution for build source not specified correctly](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-buildsource-notcorrect)

* [Resolution for a problem due to Docker Hub rate limits](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-dockerbuild-ratelimits)

* [Resolution for build source not supported by buildpacks](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-buildpack-notsupported)

* [Resolution for a problem with the Docker build](/docs/codeengine?topic=codeengine-ts-build-bldpush-stepfail#ts-build-dockerbuild)

[Why does my Python app fail to deploy?](/docs/codeengine?topic=codeengine-ts-build-python#ts-build-python)

[Why is my build from a Dockerfile failing with a `no command specified` error?](/docs/codeengine?topic=codeengine-ts-build-nocmdspecified#ts-build-nocmdspecified)


### Troubleshooting functions
{: #sitemap_troubleshooting_functions}


[Debugging functions](/docs/codeengine?topic=codeengine-troubleshoot-function#troubleshoot-function)

* [Function return codes](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-return-codes)

* [Function limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-limits)

* [Getting logs for my function](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-funcrtion-gettinglogs)

* [Keeping your runtime and CLI versions up to date](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-uptodate)

* [Verifying the code bundle reference for my function](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-verifyimage)

* [Additional topics](/docs/codeengine?topic=codeengine-troubleshoot-function#ts-function-topics)

[How can I add my {{site.data.keyword.codeengineshort}} function to an allowlist?](/docs/codeengine?topic=codeengine-ts-allowlist-function#ts-allowlist-function)


### Troubleshooting images
{: #sitemap_troubleshooting_images}


[Debugging images](/docs/codeengine?topic=codeengine-troubleshoot-images#troubleshoot-images)

* [Working with images](/docs/codeengine?topic=codeengine-troubleshoot-images#ts-image-workwith)

* [Getting logs for my images](/docs/codeengine?topic=codeengine-troubleshoot-images#ts-images-logs)

* [Getting system event information for my images](/docs/codeengine?topic=codeengine-troubleshoot-images#ts-images-systemevents)

[Why can't {{site.data.keyword.codeengineshort}} pull an image?](/docs/codeengine?topic=codeengine-image-cannot-pull#image-cannot-pull)

* [Next steps](/docs/codeengine?topic=codeengine-image-cannot-pull#image-cannot-pull-next)


### Troubleshooting jobs
{: #sitemap_troubleshooting_jobs}


[Debugging jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#troubleshoot-job)

* [Job limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-limits)

* [Getting logs for my jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-gettinglogs)

* [Getting system event information for my jobs](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-job-gettingevent)

* [Verifying the container image reference for my job](/docs/codeengine?topic=codeengine-troubleshoot-job#ts-jobrun-verifyimage)

[Why can't I submit a job run with the CLI?](/docs/codeengine?topic=codeengine-ts-jobrun-submit-fails-cli#ts-jobrun-submit-fails-cli)

[Why is my job run not starting?](/docs/codeengine?topic=codeengine-ts-jobrun-notstart#ts-jobrun-notstart)

[Why is my job run not completing?](/docs/codeengine?topic=codeengine-ts-jobrun-doesnotcomplete#ts-jobrun-doesnotcomplete)

[I'm over my limit for jobs or job runs. How can I delete them?](/docs/codeengine?topic=codeengine-ts-jobrun-deleteforquota#ts-jobrun-deleteforquota)

[Where is my job run?](/docs/codeengine?topic=codeengine-ts-jobrun-deleted#ts-jobrun-deleted)

[How can I find information about my job run?](/docs/codeengine?topic=codeengine-ts-jobrun-learnmore#ts-jobrun-learnmore)

[How can I add my {{site.data.keyword.codeengineshort}} job to an allowlist?](/docs/codeengine?topic=codeengine-ts-allowlist-job#ts-allowlist-job)

[Why does my daemon job not automatically restart?](/docs/codeengine?topic=codeengine-ts-jobrun-daemon#ts-jobrun-daemon)


### Troubleshooting projects
{: #sitemap_troubleshooting_projects}


[Debugging projects](/docs/codeengine?topic=codeengine-troubleshoot-project#troubleshoot-project)

* [Project limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-project#ts-project-limits)

[Why can't I access a project?](/docs/codeengine?topic=codeengine-ts-access-project#ts-access-project)

[Why can't I create a project?](/docs/codeengine?topic=codeengine-ts-create-project#ts-create-project)


### Troubleshooting service bindings
{: #sitemap_troubleshooting_service_bindings}


[Debugging service bindings](/docs/codeengine?topic=codeengine-troubleshoot-servicebindings#troubleshoot-servicebindings)

* [Limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-servicebindings#ts-sb-limits)

* [Configuring service binding operations](/docs/codeengine?topic=codeengine-troubleshoot-servicebindings#ts-sb-operations)

* [Listing service bindings](/docs/codeengine?topic=codeengine-troubleshoot-servicebindings#ts-sb-listing)

[Why do the service credentials in my service binding to {{site.data.keyword.cos_full_notm}} show as `REDACTED`?](/docs/codeengine?topic=codeengine-ts-sb-cosredacted#ts-sb-cosredacted)

[Why does my service binding to a Db2 Enterprise instance fail?](/docs/codeengine?topic=codeengine-ts-sb-db2createfails#ts-sb-db2createfails)

[Why can't I display details of my configured service binding operations?](/docs/codeengine?topic=codeengine-ts-sb-projsettings-nodetails#ts-sb-projsettings-nodetails)


### Troubleshooting subscriptions
{: #sitemap_troubleshooting_subscriptions}


[Debugging subscriptions](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions#troubleshoot-subscriptions)

* [Subscription limits to consider](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions#ts-subscription-limits)

* [Subscription logs](/docs/codeengine?topic=codeengine-troubleshoot-subscriptions#ts-subscription-cos-logs)

[Why does my subscription show errors when it delivers events?](/docs/codeengine?topic=codeengine-ts-subscription-deliveryerrors#ts-subscription-deliveryerrors)

[Why is my `subscription cos create` command failing?](/docs/codeengine?topic=codeengine-ts-cossub-create#ts-cossub-create)

[Why does my {{site.data.keyword.cos_short}} subscription never become ready?](/docs/codeengine?topic=codeengine-ts-cossub-notready#ts-cossub-notready)

[When I create a single file in my {{site.data.keyword.cos_short}} bucket, why do I get multiple events?](/docs/codeengine?topic=codeengine-ts-cossub-multipleevents#ts-cossub-multipleevents)

[Why is my `subscription cron create` command failing?](/docs/codeengine?topic=codeengine-ts-cronsub-create#ts-cronsub-create)

[Why does my cron subscription never become ready?](/docs/codeengine?topic=codeengine-ts-cronsub-notready#ts-cronsub-notready)


### Troubleshooting toolchain
{: #sitemap_troubleshooting_toolchain}


[Debugging your {{site.data.keyword.codeengineshort}} toolchain](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce#troubleshoot-toolchain-ce)

* [Creating a debug log file for your pipeline](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce#troubleshoot-toolchain-ce-log)

* [More information](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce#troubleshoot-toolchain-ce-info)

[Why does my build run in my toolchain time out?](/docs/codeengine?topic=codeengine-ts-buildrun-timeout-toolchain#ts-buildrun-timeout-toolchain)

[Why is my toolchain package too large?](/docs/codeengine?topic=codeengine-ts-toolchain-size#ts-toolchain-size)


### Troubleshooting Terraform
{: #sitemap_troubleshooting_terraform}


[Debugging Terraform](/docs/codeengine?topic=codeengine-troubleshoot-terraform#troubleshoot-terraform)

* [More topics](/docs/codeengine?topic=codeengine-troubleshoot-terraform#ts-terraform-topics)

[Why does Terraform show environment variables discrepancies during app or job creation?](/docs/codeengine?topic=codeengine-ts-terraform-environment-variables#ts-terraform-environment-variables)


### Troubleshooting - other
{: #sitemap_troubleshooting_other}


[Why am I getting ECONNRESET errors when connecting to an endpoint?](/docs/codeengine?topic=codeengine-ts-other-econnreset#ts-other-econnreset)


## Getting help and support for {{site.data.keyword.codeengineshort}}
{: #sitemap_getting_help_and_support_for_}


[Getting help and support for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-get-support#get-support)

* [Providing support case details](/docs/codeengine?topic=codeengine-get-support#support-case-details)
