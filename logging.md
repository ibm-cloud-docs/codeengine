---

copyright:
  years: 2020, 2024
lastupdated: "2024-06-04"

keywords: logging for code engine, logs for code engine, job logs for code engine, app logs for code engine, build logs for code engine, logs

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

{:ui: .ph data-hd-interface='ui'}
{:cli: .ph data-hd-interface='cli'}

# Viewing logs
{: #view-logs}

Logging can help you troubleshoot issues in {{site.data.keyword.codeenginefull}}. You can view logs by using the console or by using the CLI.
{: shortdesc}

## Viewing logs from the console
{: #view-logs-ui}
{: ui}

When you work with {{site.data.keyword.codeengineshort}} apps, jobs, functions, or builds in the console with logging enabled, logs are forwarded to an {{site.data.keyword.la_full_notm}} service where they are indexed, enabling full-text search through all generated messages and convenient querying based on specific fields.
{: shortdesc}

To view logs for your app, job or build in the {{site.data.keyword.codeengineshort}} console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} component. From your {{site.data.keyword.codeengineshort}} app, job, function, or build page in the console, you can add logging capabilities.

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: note}

### Considerations for viewing logs from the console
{: #view-logs-considerations}
{: ui}

When you want to use logging from the console, you must first configure {{site.data.keyword.la_full_notm}} platform logs to receive {{site.data.keyword.codeengineshort}} logging data. To check for active {{site.data.keyword.la_short}} instances, see the [Observability dashboard](https://cloud.ibm.com/observe/logging).

Review the {{site.data.keyword.la_short}} [service plan](/docs/log-analysis?topic=log-analysis-service_plans) information as you consider retention, search, and log analysis needs.

When you use the {{site.data.keyword.la_short}} *free* tier and you want to view log data, configure and start logging before you start your application, or run your job or build. Also, be sure to keep your platform logs window open to receive your {{site.data.keyword.codeengineshort}} logging data. Take these actions because log data is not retained when you use the Lite service plan and is lost when you close the window.

When you use a {{site.data.keyword.la_short}} *paid* tier, you do not need to leave your logging window open. Log data is preserved for a configurable amount of time, depending on your plan. You can adjust log filters and apply searches for past log entries.

When you view log data for {{site.data.keyword.codeengineshort}} applications, runs of your job, or runs of your build, delays can occur before the data is available in {{site.data.keyword.la_short}}. For example, it might take around 5 minutes for your log data to show in {{site.data.keyword.la_short}}, especially if you are using the Lite service plan.
{: important}

When you use logging with the CLI, you do not need to configure {{site.data.keyword.la_short}} platform logs, as the {{site.data.keyword.codeengineshort}} CLI logging fetches its data differently.

#### Can I apply filters on {{site.data.keyword.la_short}} data?
{: #view-logs-filters}
{: ui}

Yes! When you configure and start logging in the {{site.data.keyword.codeengineshort}} console for a specific component, {{site.data.keyword.codeengineshort}} automatically sets log filters in {{site.data.keyword.la_short}} that are scoped to the context of your application, job, or build. However, you can modify and scope the preset filter to display log data at a specific level or a more granular level to a specific application revision, job run, or build run from the {{site.data.keyword.la_full_notm}} page, based on your needs.

* If `_platform` is set to `'Code Engine'`, then only {{site.data.keyword.codeengineshort}} logs are displayed.
* If `label.Project:'<project_name>'` is set, then only logs from a specific project are displayed.
* If `app:'<your_component_name>'` is set, then only logs from the specified component (application, job, or build) are displayed. If your {{site.data.keyword.codeengineshort}} components share the same name, the filter includes logs from these components. For example,

    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myapp` scopes the logs to the `myapp` application level.
    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myapp-00002` scopes the logs to the `myapp-0002` application revision level.
    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myjob` scopes the logs to the specific `myjob` job level.
    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myjob-jobrun-t6m7l` scopes the logs to the specific `myjob-jobrun-t6m7l` job run level.
    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:mybuild` scopes the logs to the specific `mybuild` build level.
    * The filter `_platform:'{{site.data.keyword.codeengineshort}}' app:mybuild-run-121212` scopes the logs to the specific `mybuild-run-121212` build run level.

For more information about configuring and starting logging in the console, see [Viewing logs for apps](/docs/codeengine?topic=codeengine-view-logs#view-applogs-ui), [Viewing logs for jobs](/docs/codeengine?topic=codeengine-view-logs#view-joblogs-ui), and [Viewing logs for functions](/docs/codeengine?topic=codeengine-view-logs#view-funlogs-ui).

#### What if my log data is multi-line?
{: #view-logs-multiline}
{: ui}

Every log line must contain log level and timestamp information to appear correctly in {{site.data.keyword.la_full_notm}}. If your log lines span multiple lines, change how you format and output your logs so that they are in a single line. Use the JSONL format for your logs with {{site.data.keyword.la_full_notm}}. Your logs must also
conform to [limits for {{site.data.keyword.la_full_notm}} logs](/docs/log-analysis?topic=log-analysis-ingest_limits). After you make log formatting changes, you can take advantage of {{site.data.keyword.la_full_notm}} search and formatting features.

### Viewing app, job, or function logs from the console
{: #view-appjobfunctionlogs-ui}
{: ui}

You can view logs for apps, jobs, or functions. The steps to view any of these from the console are very similar.

After you select the project that you want to work with, you can add logging capabilities from the {{site.data.keyword.codeengineshort}} Overview page or one of its child pages such as the **Applications**, **Jobs**, or **Functions** page; or from the page that is specific to your application, job, or function. The following steps assume that you are working from a specific {{site.data.keyword.codeengineshort}} page.
{: note}

1. Go to an app, job, or function that you created and deployed. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, select your project and then select **Applications**, **Jobs**, or **Functions** as appropriate. Select the app, job, or function with which you want to work.
2. Add logging capabilities. If you have previously created a {{site.data.keyword.la_short}} instance, click **Logging**, and this action opens the {{site.data.keyword.la_short}} service. Orherwise, complete the following steps to configure logging capabilities:
    1. From the **Test application**, **Submit job**, or **Test function** options menu, click **Add logging** to create the {{site.data.keyword.la_full_notm}} instance. This action opens the {{site.data.keyword.la_short}} service.
    2. From the {{site.data.keyword.la_short}} service, create your logging instance. To confirm that your logging instance is created, check the [Observability dashboard](https://cloud.ibm.com/observe/logging).
    3. From your {{site.data.keyword.codeengineshort}} app, job, or funcion page, click **Add logging** from the **Test application**, **Submit job**, or **Test function** options menu. This time, select a {{site.data.keyword.la_short}} instance to receive platform logs. Choose the logging instance that you created in the prior step. Click **Select**. {{site.data.keyword.codeengineshort}} requires enabled platform logs to receive {{site.data.keyword.codeengineshort}} logging data. When you complete this action, {{site.data.keyword.codeengineshort}} enables platform logging for you.
3. Now that platform logs are configured, from your {{site.data.keyword.codeengineshort}} app, job, or function page, click **Logging** from the **Test application**, **Submit job**, or **Test function** options menu to open your platform logs window. Be sure to keep this platform logs window open to receive your logging data if you are using the {{site.data.keyword.la_short}} free tier. You don't need to keep this window open if you are using a {{site.data.keyword.la_short}} paid tier as log data is preserved for a configurable amount of time, depending on your plan. To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging).
4. (optional) Refine the [filter for your search](#view-logs-filters), if needed.
5. Verify your configuration by doing one of the following steps:
    * For an application or a function, test it: click **Test application** or **Test function** as apprioriate, and then click **Send request**. To open the application or function in a web page, click **Application URL** or **Function URL**. You can view platform logs from the test in the platform logs window.
    * For a job, run it: from the **Job runs** area, click **Submit job** to run your job. Provide the job run configuration values or you can take the default values. Click **Submit job** to run your job. You can view platform logs from the job run in the platform logs window.

Your {{site.data.keyword.la_short}} instance is now configured such that it can receive platform logging for your {{site.data.keyword.codeengineshort}} app, job, or function.

Alternatively, you can configure a {{site.data.keyword.la_short}} instance by using the [Observability dashboard](https://cloud.ibm.com/observe/logging) to create the instance, and then by [configuring platform logs](/docs/log-analysis?topic=log-analysis-config_svc_logs&interface=ui#config_svc_logs_ui). After you create your instance, click **Configure platform logs**. Select the {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. You can also apply [filters for your search](#view-logs-filters) in {{site.data.keyword.la_short}} for your {{site.data.keyword.codeengineshort}} log data.

### Viewing build logs from the console
{: #view-build-ui}
{: ui}

You can display logs for specific build run instances from the console.
{: shortdesc}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Image builds**.
4. From the **Image build** tab, click the name of your image build to open the build page for a defined build, or [create a build](/docs/codeengine?topic=codeengine-build-create-config1#build-create-console).
5. From the build page for your defined build, click the name of the instance of your build run in the **Build runs** section. You might need to click **Submit build** to create a build run. You can view platform logs from the build run in the platform logs window. Alternatively, you can also view build log information for the build step details from the build run instance page. Expand the build steps for specific build step log data. You can optionally refine the [filter for your search](#view-logs-filters), if needed.

## Viewing logs with the CLI
{: #view-logs-cli}
{: cli}

To view logging output with the CLI, you must have a running instance of your app or job. If an [app is scaled to zero](/docs/codeengine?topic=codeengine-app-scale) or a job run instance is completed, the output for the [**`ibmcloud ce app logs`**](/docs/codeengine?topic=codeengine-cli#cli-application-logs) and [**`ibmcloud ce jobrun logs`**](/docs/codeengine?topic=codeengine-cli#cli-jobrun-logs) commands does not have log data. Alternatively, you can use the {{site.data.keyword.la_full_notm}} service to view log data.
{: important}

### Viewing application logs with the CLI
{: #view-applog-cli}
{: cli}

To view app logs for a specific app with the CLI, use the `application logs` command. You can display logs of all the instances of an app or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

* To view the logs for all instances of the `myapp` app, specify the name of the app with the `--app` option; for example,

    ```txt
    ibmcloud ce app logs --app myapp
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-ii18y-2-deployment-7657c5f4f9-dgk5f:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

* To view the logs for a specific instance of the app, specify the name of the specific instance of the app with the `--instance` option; for example,

    ```txt
    ibmcloud ce app logs --instance myapp-ii18y-2-deployment-7657c5f4f9-dgk5f
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for application instance 'myapp-a5yp2-2-deployment-65766594d4-hj6c5'...
    OK

    myapp-a5yp2-2-deployment-65766594d4-hj6c5:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

### Viewing job logs with the CLI
{: #view-joblog-cli}
{: cli}

To view logs for a specific job run with the CLI, use the `jobrun logs` command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. The `jobrun get` command displays details about your job run, including the instances of the job run.

* To view the logs for all instances of the `testjobrun` job run, specify the name of the job run with the `--jobrun` option; for example,

    ```txt
    ibmcloud ce jobrun logs --jobrun testjobrun
    ```
    {: pre}

    Example output

    ```txt
    Getting jobrun 'testjobrun'...
    Getting instances of jobrun 'testjobrun'...
    Getting logs for all instances of job run 'testjobrun'...
    OK

    testjobrun-1-0:
    Hello World!

    testjobrun-2-0:
    Hello World!

    testjobrun-3-0:
    Hello World!

    testjobrun-4-0:
    Hello World!

    testjobrun-5-0:
    Hello World!
    ```
    {: screen}

* To view the logs for the `testjobrun-1-0` job run instance, specify the name of a specific instance of the job run with the `--instance` option; for example,

    ```txt
    ibmcloud ce jobrun logs --instance testjobrun-1-0
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for job run instance 'testjobrun-1-0'...
    OK

    testjobrun-1-0:
    Hello World!
    ```
    {: screen}

### Viewing build logs with the CLI
{: #view-build-cli}
{: cli}

To view build logs for a specific build run with the CLI, use the `buildrun logs` command. You can display logs of all the instances of a build run based on the name of the build run.

To view the logs for all instances of the `mybuildrun` build run, specify the name of the build run with the `--name` option; for example,

```txt
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

Example output

```txt
Getting build run 'mybuildrun'...
Getting instances of build run 'mybuildrun'...
Getting logs for build run 'mybuildrun'...
OK

mybuildrun-zg5rj-pod-z5gzb/step-git-source-source-r9fcf:
{"level":"info","ts":1614363665.8331757,"caller":"git/git.go:169","msg":"Successfully cloned https://github.com/IBM/CodeEngine @ 8b514ce871e50d67cfea3e344b90cade4bd26e90 (grafted, HEAD, origin/main) in path /workspace/source"}
{"level":"info","ts":1614363666.82988,"caller":"git/git.go:207","msg":"Successfully initialized and updated submodules in path /workspace/source"}

mybuildrun-zg5rj-pod-z5gzb/step-build-and-push:
INFO[0002] Retrieving image manifest node:12-alpine
INFO[0002] Retrieving image node:12-alpine
INFO[0003] Retrieving image manifest node:12-alpine
INFO[0003] Retrieving image node:12-alpine
INFO[0003] Built cross stage deps: map[]
INFO[0003] Retrieving image manifest node:12-alpine
INFO[0003] Retrieving image node:12-alpine
INFO[0004] Retrieving image manifest node:12-alpine
INFO[0004] Retrieving image node:12-alpine
INFO[0004] Executing 0 build triggers
INFO[0004] Unpacking rootfs as cmd RUN npm install requires it.
INFO[0008] RUN npm install
INFO[0008] Taking snapshot of full filesystem...
INFO[0010] cmd: /bin/sh
INFO[0010] args: [-c npm install]
INFO[0010] Running: [/bin/sh -c npm install]
npm WARN saveError ENOENT: no such file or directory, open '/package.json'
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN enoent ENOENT: no such file or directory, open '/package.json'
npm WARN !invalid#2 No description
npm WARN !invalid#2 No repository field.
npm WARN !invalid#2 No README data
npm WARN !invalid#2 No license field.

up to date in 0.267s
found 0 vulnerabilities

INFO[0011] Taking snapshot of full filesystem...
INFO[0011] COPY server.js .
INFO[0011] Taking snapshot of files...
INFO[0011] EXPOSE 8080
INFO[0011] cmd: EXPOSE
INFO[0011] Adding exposed port: 8080/tcp
INFO[0011] CMD [ "node", "server.js" ]

mybuildrun-zg5rj-pod-z5gzb/step-image-digest-exporter-ngl6j:
2021/02/26 18:21:02 warning: unsuccessful cred copy: ".docker" from "/tekton/creds" to "/tekton/home": unable to open destination: open /tekton/home/.docker/config.json: permission denied
{"severity":"INFO","timestamp":"2021-02-26T18:21:26.372494581Z","caller":"logging/config.go:116","message":"Successfully created the logger."}
{"severity":"INFO","timestamp":"2021-02-26T18:21:26.372621756Z","caller":"logging/config.go:117","message":"Logging level set to: info"}
```
{: screen}
