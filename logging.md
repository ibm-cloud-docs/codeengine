---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-06"

keywords: logging for code engine, logs for code engine, job logs for code engine, app logs for code engine, build logs for code engine, logs

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Viewing logs
{: #view-logs}

Logging can help you troubleshoot issues in {{site.data.keyword.codeenginefull}}. 
{: shortdesc}

## Viewing logs from the console 
{: #view-logs-ui}

When you work with {{site.data.keyword.codeengineshort}} apps and jobs in the console with logging enabled, logs are forwarded to an {{site.data.keyword.la_full_notm}} service where they are indexed, enabling full-text search through all generated messages and convenient querying based on specific fields.
{: shortdesc}

To view logs for an app or a job in the {{site.data.keyword.codeengineshort}} console, you must create an {{site.data.keyword.la_full_notm}} instance in the same region as your {{site.data.keyword.codeengineshort}} project. You are not required to create this instance before you work with your {{site.data.keyword.codeengineshort}} app or job. {{site.data.keyword.codeengineshort}} makes it easy to enable logging for your apps and jobs. 

You need to enable logging for {{site.data.keyword.codeengineshort}} only one time per region, per account.
{: note}

{{site.data.keyword.codeengineshort}} requires {{site.data.keyword.la_short}} platform logs be configured to receive {{site.data.keyword.codeengineshort}} logging data.

To check for active {{site.data.keyword.la_short}} instances, see the [Observability dashboard](https://cloud.ibm.com/observe/logging). 

{{site.data.keyword.codeengineshort}} automatically sets log filters. From the {{site.data.keyword.la_full_notm}} page, you can modify and scope the preset filter to display log data at a specific level or a more granular level of a specific app, job, or build run. For example, the filter `_platform:'{{site.data.keyword.codeengineshort}}' app:myjob-jobrun-t6m7l` filters log data to the specific `myjob-jobrun-t6m7l` job run level; whereas, `_platform:'Code Engine' app:myjob` scopes the log data to the job level. 

When you use the {{site.data.keyword.la_full_notm}} free tier, be sure to keep your platform logs window open to receive your {{site.data.keyword.codeengineshort}} logging data. Log data is not retained when you use the Lite service plan and is lost when you close the window.

When you use a {{site.data.keyword.la_short}} paid tier, you do not need to leave your logging window open. Log data is preserved for a configurable amount of time, depending on your plan. You can adjust log filters and apply searches for past log entries. 

Review the [service plan](/docs/log-analysis?topic=log-analysis-service_plans) information as you consider retention, search, and log analysis needs.
{: tip}

### Viewing app logs from the console
{: #view-applogs-ui}

1. Go to an app that you created and deployed. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, select your project and then select **Applications**. Select the app that you want to work with. 
2. From your {{site.data.keyword.codeengineshort}} app page, you can add logging capabilities. If you have not previously created a {{site.data.keyword.la_short}} instance, click **Add logging**. If you have previously created a {{site.data.keyword.la_short}} instance, **Launch logging** displays and you do not need to complete this step. 
    1. Click **Add logging** to create the {{site.data.keyword.la_full_notm}} instance. This action opens the {{site.data.keyword.la_short}} service.  
    2. From the {{site.data.keyword.la_short}} service, create your logging instance. To confirm that your logging instance is created, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 
    3. From your {{site.data.keyword.codeengineshort}} app page, click **Configure logging**. This time, select a {{site.data.keyword.la_short}} instance to receive platform logs. {{site.data.keyword.codeengineshort}} requires platform logs be configured to receive {{site.data.keyword.codeengineshort}} logging data. Choose the logging instance that was created in the prior step. Click **Select**. 
3. Now that platform logging is configured, from your {{site.data.keyword.codeengineshort}} app page, click **Launch logging** to open your platform logs window. Be sure to keep this platform logs window open to receive your logging data if you are using the {{site.data.keyword.la_short}} free tier. You don't need to keep this window open if you are using a {{site.data.keyword.la_short}} paid tier as log data is preserved for a configurable amount of time, depending on your plan. To confirm that platform logs are set for your region, check the [Observability dashboard](https://cloud.ibm.com/observe/logging).
4. Test your application. Click **Test application** and then click **Send request** in the Test application pane. To open the application in a web page, click **Application URL**. 

You have completed the steps to configure your {{site.data.keyword.la_short}} instance such that it can receive platform logging for your {{site.data.keyword.codeengineshort}} app.

Alternatively, you can also configure a {{site.data.keyword.la_short}} instance by using the [Observability dashboard](https://cloud.ibm.com/observe/logging) to create the instance, and then by [configuring platform logs](/docs/log-analysis?topic=log-analysis-config_svc_logs#config_svc_logs_ui). After you create your instance, click **Configure platform logs**. Select the {{site.data.keyword.loganalysisshort}} instance to receive the platform log data by specifying a region and your log instance. 

### Viewing job logs from the console
{: #view-joblogs-ui}

1. Navigate to a job that you created and deployed. From the [Projects page on the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}, select your project and then select **Jobs**. Select the job that you want to work with.
2. From your {{site.data.keyword.codeengineshort}} job page, you can add logging capabilities. If you have not previously created a {{site.data.keyword.la_short}} instance, from the **Actions** menu, click **Add logging**. If you have previously created a {{site.data.keyword.la_short}} instance, the **Actions** menu displays **Launch logging** displays and you do not need to complete this step. 
    1. From the **Actions** menu, click **Add logging** to create the {{site.data.keyword.la_short}} instance. This action opens the {{site.data.keyword.la_short}} service.
    2. From the {{site.data.keyword.la_short}} service, create your logging instance. To confirm that your logging instance is created, check the [Observability dashboard](https://cloud.ibm.com/observe/logging). 
    3. From your {{site.data.keyword.codeengineshort}} job page, in the **Actions** menu, click **Add logging** again. This time, select a {{site.data.keyword.la_short}} instance to receive platform logs. {{site.data.keyword.codeengineshort}} requires platform logs be configured to receive {{site.data.keyword.codeengineshort}} logging data. Choose the logging instance that was created in the prior step. Click **Select**. 
3. Now that platform logging is configured, from your {{site.data.keyword.codeengineshort}} job page, from the **Actions** menu, click **Logging** to open your platform logs window. Be sure to keep this platform logs window open to receive your logging data if you are using the {{site.data.keyword.la_short}} free tier. Don't keep this window open if you are using a {{site.data.keyword.la_short}} paid tier. 
4. Run your job. From the **Job runs** area, click **Submit job** to run your job. Provide the job run configuration values or you can take the default values. Click **Submit job** to run your job. You can view platform logs from the test of your application in the platform logs window. 

You have completed the steps to configure your {{site.data.keyword.la_short}} instance such that it can receive platform logging for your {{site.data.keyword.codeengineshort}} job.

Alternatively, you can also configure a {{site.data.keyword.la_short}} instance by using the [Observability dashboard](https://cloud.ibm.com/observe/logging) to create the instance, and then by [configuring platform logs](/docs/log-analysis?topic=log-analysis-config_svc_logs#config_svc_logs_ui). After you create your instance, click **Configure platform logs**. Select the {{site.data.keyword.la_short}} instance to receive the platform log data by specifying a region and your log instance. 

### Viewing build logs from the console
{: #view-build-ui}

You can display logs for specific build run instances from the console. 
{: shortdesc}

1. Go to the [{{site.data.keyword.codeengineshort}} dashboard](https://cloud.ibm.com/codeengine/overview).
2. Select a project (or [create one](/docs/codeengine?topic=codeengine-manage-project#create-a-project)).
3. From the project page, click **Image builds**.
4. Click the name of your build to open the build page for a defined build, or [create a build](/docs/codeengine?topic=codeengine-build-image#build-create-console).
5. From the build page for your defined build, click the name of the instance of your build run in the **Build runs** section. You might need to click **Submit build** to create a build run.  
6. From the build run instance page, you can view the build log information. Expand the specific build steps for detailed logging information.

## Viewing logs with the CLI 
{: #view-logs-clu}

### Viewing application logs with the CLI
{: #view-applog-cli}

To view app logs for a specific app with the CLI, use the `application logs` command. You can display logs of all the instances of an app or display logs of a specific instance of an app. The `app get` command displays details about your app, including the running instances of the app.

* To view the logs for all instances of the `myapp` app, specify the name of the app with the `--app` option; for example,  

    ```sh
    ibmcloud ce app logs --app myapp 
    ```
    {: pre}

    **Example output**

    ```sh
    Getting logs for all instances of application 'myapp'...
    OK

    myapp-ii18y-2-deployment-7657c5f4f9-dgk5f:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

* To view the logs for a specific instance of the app, specify the name of the specific instance of the app with the `--instance` option; for example, 

    ```sh
    ibmcloud ce app logs --instance myapp-ii18y-2-deployment-7657c5f4f9-dgk5f 
    ```
    {: pre}

    **Example output**

    ```sh
    Getting logs for application instance 'myapp-a5yp2-2-deployment-65766594d4-hj6c5'...
    OK

    myapp-a5yp2-2-deployment-65766594d4-hj6c5:
    Server running at http://0.0.0.0:8080/
    ```
    {: screen}

### Viewing job logs with the CLI
{: #view-joblog-cli}

To view logs for a specific job run with the CLI, use the `jobrun logs` command. You can display logs of all the instances of a job run or display logs of a specific instance of a job run. The `jobrun get` command displays details about your job run, including the instances of the job run. 

* To view the logs for all instances of the `testjobrun` job run, specify the name of the job run with the `--jobrun` option; for example, 

    ```sh
    ibmcloud ce jobrun logs --jobrun testjobrun
    ```
    {: pre}

    **Example output**

    ```sh
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

    ```sh
    ibmcloud ce jobrun logs --instance testjobrun-1-0 
    ```
    {: pre}

    **Example output**

    ```sh
    Getting logs for job run instance 'testjobrun-1-0'...
    OK

    testjobrun-1-0:
    Hello World!
    ```
    {: screen}

### Viewing build logs with the CLI
{: #view-build-cli}

To view build logs for a specific build run with the CLI, use the `buildrun logs` command. You can display logs of all the instances of a build run based on the name of the build run.

To view the logs for all instances of the `mybuildrun` build run, specify the name of the build run with the `--name` option; for example,  

```sh
ibmcloud ce buildrun logs --name mybuildrun
```
{: pre}

**Example output**

```sh
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


