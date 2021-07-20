---

copyright:
  years: 2021
lastupdated: "2021-07-20"

keywords: learning paths, code engine, deployments, tools, applications, jobs, project, log, monitor

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



<style>
    <!--
        #tutorials { /* hide the page header */
            display: none !important;
        }
        .allCategories {
            display: flex !important;
            flex-direction: row !important;
            flex-wrap: wrap !important;
        }
        .categoryBox {
            flex-grow: 1 !important;
            width: calc(33% - 20px) !important;
            text-decoration: none !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            border: 1px #dfe6eb solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
            text-align: center !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
        }
        .solutionBoxContainer {}
        .solutionBoxContainer a {
            text-decoration: none !important;
            border: none !important;
        }
        .solutionBox {
            display: inline-block !important;
            width: 100% !important;
            margin: 0 10px 20px 0 !important;
            padding: 16px !important;
            background-color: #f4f4f4 !important;
        }
        @media screen and (min-width: 960px) {
            .solutionBox {
            width: calc(50% - 3%) !important;
            }
            .solutionBox.solutionBoxFeatured {
            width: calc(50% - 3%) !important;
            }
            .solutionBoxContent {
            height: 350px !important;
            }
        }
        @media screen and (min-width: 1298px) {
            .solutionBox {
            width: calc(33% - 2%) !important;
            }
            .solutionBoxContent {
            min-height: 350px !important;
            }
        }
        .solutionBox:hover {
            border: 1px rgb(136, 151, 162)solid !important;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.2) !important;
        }
        .solutionBoxContent {
            display: flex !important;
            flex-direction: column !important;
        }
        .solutionBoxTitle {
            margin: 0rem !important;
            margin-bottom: 5px !important;
            font-size: 14px !important;
            font-weight: 900 !important;
            line-height: 16px !important;
            height: 37px !important;
            text-overflow: ellipsis !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 2 !important;
            -webkit-box-orient: vertical !important;
            -webkit-box-align: inherit !important;
        }
        .solutionBoxDescription {
            flex-grow: 1 !important;
            display: flex !important;
            flex-direction: column !important;
        }
        .descriptionContainer {
        }
        .descriptionContainer p {
            margin: 0 !important;
            overflow: hidden !important;
            display: -webkit-box !important;
            -webkit-line-clamp: 4 !important;
            -webkit-box-orient: vertical !important;
            font-size: 14px !important;
            font-weight: 400 !important;
            line-height: 1.5 !important;
            letter-spacing: 0 !important;
            max-height: 70px !important;
        }
        .architectureDiagramContainer {
            flex-grow: 1 !important;
            min-width: calc(33% - 2%) !important;
            padding: 0 16px !important;
            text-align: center !important;
            display: flex !important;
            flex-direction: column !important;
            justify-content: center !important;
            background-color: #f4f4f4;
        }
        .architectureDiagram {
            max-height: 175px !important;
            padding: 5px !important;
            margin: 0 auto !important;
        }
    -->
    </style>

# Learning paths for {{site.data.keyword.codeengineshort}}
{: #learning-paths}

Find your path to accomplish what you want with {{site.data.keyword.codeenginefull}}.
{: shortdesc}

<div class=solutionBoxContainer>
<div class="solutionBox">
<a href = "#lp-plan-deployments">
<div>
<img src="images/progress.svg" alt="Planning your deployment icon." style="height:50px; border-style: none"/>
  <p><strong>Plan your deployments</strong></p>
<p class="bx--type-caption">Learn about {{site.data.keyword.codeengineshort}} applications and jobs.</p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-install-tools">
<div>
<img src="images/tools.svg" alt="Installing the tools icon." style="height:50px; border-style: none"/>
<p><strong>Install the tools</strong></p>
 <p class="bx--type-caption">Install the CLI or find the dashboard for {{site.data.keyword.codeengineshort}}.</br></p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-set-environment">
<div>
<img src="images/cloud-planning.svg" alt="Create a project icon." style="height:50px; border-style: none"/>
<p><strong>Create a project</strong></p>
<p class="bx--type-caption">Create a project and set up your authorizations.</p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-develop-app-job">
<div>
<img src="images/develop.svg" alt="Developing your application icon." style="height:50px; border-style: none"/>
<p><strong>Develop your application or job</strong></p>
<p class="bx--type-caption">Learn about options for deploying applications and running jobs.</p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-deploy-app">
<div>
<img src="images/rocket.svg" alt="Deploying your application icon." style="height:50px; border-style: none"/>
<p><strong>Deploy your applications</strong></p>
<p class="bx--type-caption">Deploy your application from {{site.data.keyword.codeengineshort}}.</br></p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-run-job">
<div>
<img src="images/runjob.svg" alt="Run a job icon." style="height:50px; border-style: none"/>
<p><strong>Run your jobs</strong></p>
<p class="bx--type-caption">Create your job configuration and run your job from {{site.data.keyword.codeengineshort}}.</p>
</div>
</a>
</div>
<div class="solutionBox">
<a href = "#lp-log-mon">
<div>
<img src="images/chartline.svg" alt="Logging and monitoring icon." style="height:50px; border-style: none"/>
<p><strong>Log and monitor your workloads</strong></p>
<p class="bx--type-caption">Improve your workload health and performance with logging and monitoring.</p>
</div>
</a>
</div>
</div>

## Plan your deployments
{: #lp-plan-deployments}

Before you start, [learn about {{site.data.keyword.codeengineshort}} and some common terms](/docs/codeengine?topic=codeengine-about).

Then, decide whether you want to deploy an application or create a job by reading [planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

You can even try out our [application tutorial](/docs/codeengine?topic=codeengine-deploy-app-tutorial) or our [job tutorial](/docs/codeengine?topic=codeengine-deploy-job-tutorial).

## Install the tools
{: #lp-install-tools}

If you plan to use the CLI, you must [install it](/docs/codeengine?topic=codeengine-install-cli). As you work with your {{site.data.keyword.codeengineshort}} workloads, refer to the [CLI command reference](/docs/codeengine?topic=codeengine-cli) and track of CLI version updates with the [CLI change log](/docs/codeengine?topic=codeengine-cli_versions).

If you do not want to use the CLI, you can [work from the console](https://cloud.ibm.com/codeengine/overview){: external}.

## Create your first project
{: #lp-set-environment}

To get started with {{site.data.keyword.codeengineshort}}, [create a project](/docs/codeengine?topic=codeengine-manage-project) to contain your entities. You can also [set access policies](/docs/codeengine?topic=codeengine-iam) for your project.

Need help? Check out [troubleshooting tips for projects](/docs/codeengine?topic=codeengine-troubleshoot-project). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Develop your application or job
{: #lp-develop-app-job}

{{site.data.keyword.codeengineshort}} deploys applications and runs jobs that are bundled into container images. If you do not have a container image, you can build and deploy your code from within {{site.data.keyword.codeengineshort}}.

**Do you have source code or a container image for your application or job?** 

I have a container image. **Where is your image stored?** 

- If your image is stored in a [container registry](/docs/codeengine?topic=codeengine-add-registry) that you have access to, then you are ready to deploy. 
- If your image is in a private registry, either in a different {{site.data.keyword.registryshort}} account or in private registry such as DockerHub, you must [set up access](/docs/codeengine?topic=codeengine-add-registry).

Then, you are ready to [deploy your application](#lp-deploy-app) or [run your job](#lp-run-job).

I have source code. **How do I get started?**

- Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
- [Plan for your build](/docs/codeengine?topic=codeengine-plan-build). 
- You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile).
- If your source code is in a private repository, [set up access](/docs/codeengine?topic=codeengine-code-repositories).
- Set up an {{site.data.keyword.registrylong_notm}} namespace to hold your built image. If the {{site.data.keyword.registryshort}} namespace is in a different account, [set up access](/docs/codeengine?topic=codeengine-add-registry).
- [Build your source code](/docs/codeengine?topic=codeengine-build-image).

Need help? Check out [troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Deploy your application
{: #lp-deploy-app}

To get started, read [plan a container image for {{site.data.keyword.codeengineshort}} applications](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-containerimage).

**How does your application scale?** See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

**Want to customize your application?**

  - Does your application require a private endpoint? See [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-endpoint).
  - How much CPU and memory does your application need? See [Determining memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
  - Do you have commands and arguments to add to your application? See [Deploying your app with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args).
  - Want to define environment variables for your application? Find out how with [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).
  - Does your application take advantage of configmaps or secrets? Take a look at [Setting up and using secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret).

**Ready to deploy?**

   - [Deploy application workloads from a public repository](/docs/codeengine?topic=codeengine-deploy-app).
   - [Deploy application workloads from images in {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-deploy-app-crimage).
   - [Deploy application workloads from images in a private repository](/docs/codeengine?topic=codeengine-deploy-app-private).
   
To make your application **highly available**, see [Deploying an application across multiple regions with a custom domain name](/docs/codeengine?topic=codeengine-deploy-multiple-regions).
   
**Want to add more customizations?**

- Want to integrate with other {{site.data.keyword.cloud_notm}} services? See [Integrating {{site.data.keyword.cloud_notm}} services with service binding](/docs/codeengine?topic=codeengine-service-binding).
- Want to connect an event producer to your application? See [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events).

**Ready to access your application?**

- [Access the application](/docs/codeengine?topic=codeengine-access-service). 
- You can also assign a custom URL. See [Deploying an application across multiple regions with a custom domain name](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

Each **update of an application** configuration property creates a new revision of the application.
- Find information to [update your app](/docs/codeengine?topic=codeengine-update-app).

You can use Iter8 to [validate your application code and latency](/docs/codeengine?topic=codeengine-slovalidationtut) and then determine if your revision is ready to use or if you must roll back to a more stable version.

Need help? Check out [troubleshooting tips for applications](/docs/codeengine?topic=codeengine-troubleshoot-apps). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Run your job
{: #lp-run-job}

To get started, read [plan a container image for {{site.data.keyword.codeengineshort}} jobs](/docs/codeengine?topic=codeengine-job-deploy#deploy-job-containerimage).

**Do you want to create a job definition?**

By creating a job definition, you can more easily run your job multiple times based on your configuration.

- [Create a job from a public repository](/docs/codeengine?topic=codeengine-job-deploy#create-job).
- [Create a job from images in {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-job-deploy#create-job-crimage).
- [Create a job from images in a private repository](/docs/codeengine?topic=codeengine-job-deploy#create-job-private).

**Do you want to run a job without first creating a definition?**

With the CLI, you can submit a job run without first creating a job configuration. You can specify the same configuration options on the `jobrun submit` and `jobrun resubmit` commands that are available with the `job create` command.

- [Run a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-job-deploy#run-job-cli-withoutjobconfig). 

**Want to customize your job?**

  - How much CPU and memory does your job need? See [Determining memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
  - Do you have commands and arguments to add to your job? See [Deploying your application with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args).
  - Want to define environment variables for your job? Find out how with [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).
  - Does your job take advantage of configmaps or secrets? Take a look at [Setting up and using secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret).

{{site.data.keyword.codeengineshort}} supports **Lithops** for running jobs. See [running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops).

**Ready to create and run your job?**

You can run your job directly or create a job definition and run your job based on that configuration. 

- To run a job directly, use the [**`jobrun submit`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-submit) command and specify the `--name` and `--image` options rather than referencing the job definition. 
- To run a job from a job definition, see [run a job](/docs/codeengine?topic=codeengine-job-deploy#run-job).

**Want to add more customizations?**

- Want to integrate with other {{site.data.keyword.cloud_notm}} services? See [Integrating {{site.data.keyword.cloud_notm}} services with service binding](/docs/codeengine?topic=codeengine-service-binding).
- Want to connect an event producer to your job? See [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events).

Need help? Check out [troubleshooting tips for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Log and monitor your workloads
{: #lp-log-mon}

Logging can help you troubleshoot your applications and jobs. See [Viewing logs](/docs/codeengine?topic=codeengine-view-logs). 

You can also [view, manage, and audit](/docs/codeengine?topic=codeengine-at_events) user-initiated activities that occur in your {{site.data.keyword.codeengineshort}} project.

Finally, analyze performance metrics by collecting information with [{{site.data.keyword.mon_full_notm}}](/docs/codeengine?topic=codeengine-monitor).
