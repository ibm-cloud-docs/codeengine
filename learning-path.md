---

copyright:
  years: 2023
lastupdated: "2023-03-17"

keywords: learning paths, code engine, deployments, tools, applications, jobs, project, log, monitor

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}



# Learning paths for {{site.data.keyword.codeengineshort}}
{: #learning-paths}

Find your path to accomplish what you want with {{site.data.keyword.codeenginefull}}.
{: shortdesc}



## Plan your deployments
{: #lp-plan-deployments}

Before you start, [learn about {{site.data.keyword.codeengineshort}} and some common terms](/docs/codeengine?topic=codeengine-about).

Then, decide whether you want to deploy an application or create a job by reading [planning for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-plan-codeengine).

You can even try out our [application tutorial](/docs/codeengine?topic=codeengine-deploy-app-tutorial) or our [job tutorial](/docs/codeengine?topic=codeengine-run-job-tutorial).

## Install the tools
{: #lp-install-tools}

If you plan to use the CLI, you must [install it](/docs/codeengine?topic=codeengine-install-cli). As you work with your {{site.data.keyword.codeengineshort}} workloads, refer to the [CLI command reference](/docs/codeengine?topic=codeengine-cli) and track CLI version updates with the [CLI change log](/docs/codeengine?topic=codeengine-cli_versions). You can also [access the {{site.data.keyword.cloud-shell_notm}}](/docs/codeengine?topic=codeengine-install-cli#cloud-shell) in your web browser.

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
- If your image is in a private registry, either in a different {{site.data.keyword.registryshort}} account or in private registry such as Docker Hub, you must [set up access](/docs/codeengine?topic=codeengine-add-registry).

Then, you are ready to [deploy your application](#lp-deploy-app) or [run your job](#lp-run-job).

I have source code. **How do I get started?**

- Find out what advantages are available when you [build your image with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-faqs#dockerbld-cebuild).
- [Plan for your build](/docs/codeengine?topic=codeengine-plan-build). 
- You can also find [tips for creating a Dockerfile](/docs/codeengine?topic=codeengine-dockerfile).
- If your source code is in a private repository, [set up access](/docs/codeengine?topic=codeengine-code-repositories).
- Optionally, set up an {{site.data.keyword.registrylong_notm}} namespace to hold your built image. If the {{site.data.keyword.registryshort}} namespace is in a different account, [set up access](/docs/codeengine?topic=codeengine-add-registry). If you do not set up access to your {{site.data.keyword.registrylong_notm}} namespace, access is created automatically for you.
- [Build your source code](/docs/codeengine?topic=codeengine-build-image).

Need help? Check out [troubleshooting tips for builds](/docs/codeengine?topic=codeengine-troubleshoot-build). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Deploy your application
{: #lp-deploy-app}

To get started, read [plan a container image for {{site.data.keyword.codeengineshort}} applications](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-containerimage).

**How does your application scale?** See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale).

**Want to customize your application?**

- Does your application require a project endpoint? See [Deploying your app with a project endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-projectonly).
- Does your application require a private endpoint? See [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-private).
- How much CPU and memory does your application need? See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
- Do you have commands and arguments to add to your application? See [Deploying your app with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args).
- Want to define environment variables for your application? Find out how with [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).
- Does your application take advantage of configmaps or secrets? Take a look at [Working with secrets](/docs/codeengine?topic=codeengine-secret) or [Working with configmaps](/docs/codeengine?topic=codeengine-configmap).

**Ready to deploy?**

- [Deploy application workloads from a public repository](/docs/codeengine?topic=codeengine-deploy-app).
- [Deploy application workloads from images in {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-deploy-app-crimage).
- [Deploy application workloads from images in a private repository](/docs/codeengine?topic=codeengine-deploy-app-private).

To make your application **highly available** or to use a custom domain name, see [Deploying an application across multiple regions with a custom domain name](/docs/codeengine?topic=codeengine-deploy-multiple-regions).

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

To get started, read [plan a container image for {{site.data.keyword.codeengineshort}} jobs](/docs/codeengine?topic=codeengine-job-plan#job-containerimage).

**Do you want to create a job definition?**

By creating a job definition, you can more easily run your job multiple times based on your configuration.

- [Create a job from a public repository](/docs/codeengine?topic=codeengine-create-job).
- [Create a job from images in {{site.data.keyword.registryshort}}](/docs/codeengine?topic=codeengine-create-job-crimage).
- [Create a job from images in a private repository](/docs/codeengine?topic=codeengine-create-job-private).

**Do you want to run a job without first creating a definition?**

With the CLI, you can submit a job run without first creating a job configuration. You can specify the same configuration options on the `jobrun submit` and `jobrun resubmit` commands that are available with the `job create` command.

- [Run a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withoutjobconfig). 

**Want to customize your job?**

- How much CPU and memory does your job need? See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo).
- Do you have commands and arguments to add to your job? See [Deploying your application with commands and arguments](/docs/codeengine?topic=codeengine-application-workloads#deploy-app-cmd-args).
- Want to define environment variables for your job? Find out how with [Working with environment variables](/docs/codeengine?topic=codeengine-envvar).
- Does your job take advantage of configmaps or secrets? Take a look at [Working with secrets](/docs/codeengine?topic=codeengine-secret) or [Working with configmaps](/docs/codeengine?topic=codeengine-configmap).

{{site.data.keyword.codeengineshort}} supports **Lithops** for running jobs. See [running jobs with Lithops framework](/docs/codeengine?topic=codeengine-lithops).

**Ready to create and run your job?**

You can run your job directly or create a job definition and run your job based on that configuration. 

- To run a job directly, see [Run a job with the CLI without first creating a job configuration](/docs/codeengine?topic=codeengine-run-job#run-job-cli-withoutjobconfig).
- To run a job from a job definition, see [run a job](/docs/codeengine?topic=codeengine-run-job).

**Want to add more customizations?**

- Want to integrate with other {{site.data.keyword.cloud_notm}} services? See [Integrating {{site.data.keyword.cloud_notm}} services with service binding](/docs/codeengine?topic=codeengine-service-binding).
- Want to connect an event producer to your job? See [Subscribing to event producers](/docs/codeengine?topic=codeengine-subscribing-events).

Need help? Check out [troubleshooting tips for jobs](/docs/codeengine?topic=codeengine-troubleshoot-job). If you need more help, try [getting support](/docs/codeengine?topic=codeengine-get-support).

## Log and monitor your workloads
{: #lp-log-mon}

Logging can help you troubleshoot your applications and jobs. See [Viewing logs](/docs/codeengine?topic=codeengine-view-logs). 

You can also [view, manage, and audit](/docs/codeengine?topic=codeengine-at_events) user-initiated activities that occur in your {{site.data.keyword.codeengineshort}} project.

Finally, analyze performance metrics by collecting information with [{{site.data.keyword.mon_full_notm}}](/docs/codeengine?topic=codeengine-monitor). You can create [custom dashboards to monitor {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-monitor-custom).


