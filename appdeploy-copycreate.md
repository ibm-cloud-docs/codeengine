---

copyright:
  years: 2026
lastupdated: "2026-10-06"

keywords: applications in code engine, apps in code engine, copy create app in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, app, copy, duplicate, clone

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Copying an {{site.data.keyword.codeengineshort}} application to create a new application
{: #appdeploy-copycreate}

With {{site.data.keyword.codeenginefull}}, you can create a new application by copying the configuration of an existing app. The *copy create* feature duplicates all configuration settings of a source application — including the container image reference, resource allocation, environment variables, scaling settings, and endpoint visibility — into a new application that you can then customize independently.
{: shortdesc}

The new application is created as a separate, independent workload. Changes to the original application after copying do not affect the new application, and vice versa.

Before you begin, make sure that an existing app is already deployed in your project.

## What is copied when you use copy create?
{: #copycreate-what-is-copied}

When you copy an app to create a new app, the following configuration is copied from the source application to the new application.

| Configuration | Description |
| --- | --- |
| Container image | The image reference, including the registry, namespace, repository, and tag. |
| Registry secret | The registry secret that is used to pull the container image, if specified. |
| Resource allocation | The CPU and memory that are assigned to the application. See [Supported memory and CPU combinations](/docs/codeengine?topic=codeengine-mem-cpu-combo). |
| Environment variables | All literal environment variables and references to secrets and configmaps. See [Working with environment variables](/docs/codeengine?topic=codeengine-envvar). |
| Scaling settings | The minimum and maximum number of instances, concurrency, concurrency target, request timeout, and scale-down delay. See [Configuring application scaling](/docs/codeengine?topic=codeengine-app-scale). |
| Endpoint visibility | The visibility setting (public, private, or project) for the application endpoint. See [Options for visibility for a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility). |
| Port | The listening port configuration for the application, including any gRPC (`h2c`) settings. |
| Commands and arguments | Any commands and arguments that override the container image entrypoint. See [Defining commands and arguments for your {{site.data.keyword.codeengineshort}} workloads](/docs/codeengine?topic=codeengine-cmd-args). |
| Liveness and readiness probes | The probe configuration for the application, if set. See [Working with liveness and readiness probes for your app](/docs/codeengine?topic=codeengine-app-probes). |
{: caption="Configuration that is copied when you use copy create" caption-side="bottom"}

The new application is assigned the name that you specify and starts with no traffic until the app is fully deployed and its status changes to **Ready**.

Build source configuration (repository or local source builds) and custom domain mappings (mappings of your own domain names to the application) are **not** copied to the new application. The endpoint visibility setting (public, private, or project-only) is copied as part of the application configuration.
{: note}

## Copying an app from the console
{: #copycreate-console}

You can create a new application by copying the configuration of an existing application with the {{site.data.keyword.codeengineshort}} console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. Click **Applications** to open a list of your applications.
3. Select one of the following ways to click **Create copy**:
    * Click the name of the application that you want to copy to open its application page. Then click the **dropdown chevron** in the upper right corner of the page and select **Create copy**.
    * In the applications list, click the row actions icon (⋮) of the application that you want to copy and select **Create copy**.
4. On the Create application page, the configuration of the source application is pre-populated. Enter a unique name for the new application. Use a name that is unique within the project.
5. Review and optionally modify any configuration settings for the new application, such as the container image, resource allocation, environment variables, or scaling settings.
6. Click **Create** to create and deploy the new application.
7. After the application status changes to **Ready**, you can test the new application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**.

Now that you have deployed your application, you can view information about application revisions and any running instances, and configuration details.  



## Updating a copied app
{: #copycreate-update}

After the new application is created, it behaves as an independent application. You can update it in the same ways as any other {{site.data.keyword.codeengineshort}} application. The source application is not affected.

For more information about updating an application, see [Updating your app](/docs/codeengine?topic=codeengine-update-app).
