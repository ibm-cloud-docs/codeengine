---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-17"

keywords: applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, application workloads in code engine, deploying workloads in code engine, application, app, memory, cpu, environment variables

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Automatically injected environment variables
{: #inside-env-vars}

When you deploy an application or a function, or when you run a job, {{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the application, function, or job.
{: shortdesc}

## Automatically injected environment variables for applications
{: #inside-env-vars-app}

When you deploy an application, {{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the application. The following table lists automatically injected environment variables into each instance of your deployed application. The following examples of automatically injected environment variables are based on an application that is named `myapp`, which references the {{site.data.keyword.codeengineshort}} sample image, `icr.io/codeengine/codeengine`.

The environment variables, `CE_APP`, `CE_DOMAIN`, and `CE_SUBDOMAIN` are used to construct the URL of an application, `https://CE_APP.CE_SUBDOMAIN.CE_DOMAIN`. For example, if `CE_APP=myapp`, `CE_SUBDOMAIN=01234567-abcd` and `CE_DOMAIN=us-south.codeengine.dev.appdomain.cloud`, your application external URL is `https://myapp.01234567-abcd.us-south.codeengine.dev.appdomain.cloud`. The private URL of your application is `appName.CE_SUBDOMAIN`, or `myapp.01234567-abcd`.

| Environment variable | Description | Example |
|--------------------|-------------------------------------------------------|--------------|
| `CE_API_BASE_URL`  | The {{site.data.keyword.codeengineshort}} API URL that is based on the region of the project. Use this URL for API endpoint calls to the endpoint for all components (including applications) that are located in the same region of your {{site.data.keyword.codeengineshort}} project.  | `CE_API_BASE_URL=https://api.us-south.codeengine.cloud.ibm.com` |
| `CE_APP`           | The name of the application.                                          | `CE_APP=myapp` |
| `CE_DOMAIN`        | The domain name portion of the URL of the application (and project).  | `CE_DOMAIN=us-south.codeengine.dev.appdomain.cloud` |
| `CE_REGION`        | The region where the application resides. | `CE_REGION=us-south` |
| `CE_PROJECT_ID`     | The project ID of your project. | `CE_PROJECT_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f` |
| `CE_SUBDOMAIN`     | The subdomain portion of the URL associated with the application (and project). If you are familiar with Kubernetes, CE_SUBDOMAIN maps to the Kubernetes namespace associated with your project. | `CE_SUBDOMAIN=01234567-abcd` |
| `HOME`             | Your home directory that is running the application.                          | `HOME=/root` |
| `HOSTNAME`         | The name of instance that your application is deployed to.                    | `HOSTNAME=myapp-00001-deployment-65684cffd-xng7z` |
| `K_CONFIGURATION`  | The name of your application.                                                 | `K_CONFIGURATION=myapp` |
| `K_REVISION`       | The name of the current revision of your deployed application.                | `K_REVISION=myapp-00001` |
| `K_SERVICE`        | The name of your application.                                                 | `K_SERVICE=myapp` |
| `PATH`             | The list of directories in which the system looks for executables.    | `PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` |
| `PORT`             | The port that your application listens to, to receive HTTP requests.              | `PORT=8080` |
| `PWD`              | The current working directory.                                        | `PWD=/` |
{: caption="Automatically injected environment variables when deploying {{site.data.keyword.codeengineshort}} apps"}

Note that you can override the `PORT` variable by deploying your application from the console and specifying the **Listening port** value or by using the CLI and setting the `--port` option.

## Automatically injected environment variables for functions
{: #inside-env-vars-fun}

When you deploy an function, {{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the function.  The following table lists automatically injected environment variables into each instance of your deployed function.

The environment variables, `CE_FUNCTION`, `CE_DOMAIN`, and `CE_SUBDOMAIN` are used to construct the URL of a function, `https://CE_FUNCTION.CE_SUBDOMAIN.CE_DOMAIN`. For example, if `CE_FUNCTION=myfunc`, `CE_SUBDOMAIN=01234567-abcd` and `CE_DOMAIN=us-south.codeengine.dev.appdomain.cloud`, your function external URL is `https://myfunc.01234567-abcd.us-south.codeengine.dev.appdomain.cloud`. The private URL of your application is `CE_FUNCTION.CE_SUBDOMAIN.private.CE_DOMAIN`, or `myfunc.01234567-abcd.private.us-south.codeengine.appdomain.cloud`.

| Environment variable | Description | Example |
|--------------------|-------------------------------------------------------|--------------|
| `CE_API_BASE_URL`  | The private {{site.data.keyword.codeengineshort}} API URL that is based on the region of the project. Use this URL for API endpoint calls to the endpoint for all components (including functions) that are located in the same region of your {{site.data.keyword.codeengineshort}} project.  | `CE_API_BASE_URL=https://api.private.us-south.codeengine.cloud.ibm.com` |
| `CE_ALLOW_CONCURRENT`| This internal boolean setting is used by the {{site.data.keyword.codeengineshort}} function controller to indicate if the runtime supports concurrent invocations of the same function instance, and can be ignored. | `CE_ALLOW_CONCURRENT=true` |
| `CE_DOMAIN`          | The domain name portion of the URL of the function (and project).  | `CE_DOMAIN=us-south.codeengine.dev.appdomain.cloud` |
| `CE_REGION`    | The region where the function resides. | `CE_REGION=us-south` |
| `CE_PROJECT_ID` | The project ID of your project. | `CE_PROJECT_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f` |
| `CE_EXECUTION_ENV`   | The managed runtime type and its release version.                     | `CE_EXECUTION_ENV=ibm/action-python-v3.11` This example specifies to use Python v3.11.  |
| `CE_FUNCTION`        | The name of the function.                                             | `CE_FUNCTION=myfunc` |
| `CE_SUBDOMAIN`       | The subdomain portion of the URL associated with the function (and project). If you are familiar with Kubernetes, `CE_SUBDOMAIN` maps to the Kubernetes namespace associated with your project. | `CE_SUBDOMAIN=01234567-abcd` |
| `HOME`               | The home directory of the runtime container for the function.         | `HOME=/root` |
| `LC_CTYPE`           | The locale that is used by the `ctype` and `multibyte` operating system API. Available only with Python runtimes.     | `LC_CTYPE=C.UTF-8` |
| `PATH`               | The current setting of the PATH variable, which lists the directories in which the system looks for executables. | `PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` |
| `PYTHONIOENCODING`   | The standard encoding that is used by standard input, standard output, and standard error streams. This variable only applies to a Python runtime. | `PYTHONIOENCODING=UTF-8` |
| `PWD`                | The current working directory.                                        | `PWD=/` |
{: caption="Automatically injected environment variables when deploying {{site.data.keyword.codeengineshort}} functions"}

## Automatically injected environment variables for jobs
{: #inside-env-vars-jobs}

When you run a job, {{site.data.keyword.codeengineshort}} automatically injects certain environment variables into the job run instance.

The following table lists automatically injected environment variables into each instance of your running job. The following examples of automatically injected environment variables are based on a job that is named `myjob`, which references the {{site.data.keyword.codeengineshort}} sample image, `icr.io/codeengine/codeengine`.

| Environment variable | Description | Example |
|----------------|---------------------|---------|
| `CE_API_BASE_URL`  | The {{site.data.keyword.codeengineshort}} API URL that is based on the region of the project. Use this URL for API endpoint calls to the endpoint for all components (including jobs) that are located in the same region of your {{site.data.keyword.codeengineshort}} project.   | `CE_API_BASE_URL=https://api.us-south.codeengine.cloud.ibm.com` |
| `CE_DOMAIN`    | The domain name of the project.                                           | `CE_DOMAIN=us-south.codeengine.appdomain.cloud` |
| `CE_REGION`    | The region where the job run resides. | `CE_REGION=us-south` |
| `CE_PROJECT_ID` | The project ID of your project. | `CE_PROJECT_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f` |
| `CE_JOB`       | The name of the defined job configuration that was used for the job run.  | `CE_JOB=myjobdef` |
| `CE_JOBRUN`    | The name of the job run.                                                  | `CE_JOBRUN=myjob-jobrun-f5kxz` |
| `CE_SUBDOMAIN` | The subdomain associated with the project in which your job is running. If you are familiar with Kubernetes, `CE_SUBDOMAIN` maps to the Kubernetes namespace that is associated with your project.                       | `CE_SUBDOMAIN=01234567-abcd` |
| `HOME`         | Your home directory that is running the job.                              | `HOME=/root` |
| `HOSTNAME`     | The name of instance that your application is deployed to.                        | `HOSTNAME=myjob-jobrun-6bgmg-0-0` |
| `JOB_ARRAY_SIZE` | The number of job instances to run in parallel. The value is specified directly as the job run array size, or computed by counting the specified indices.  | `JOB_ARRAY_SIZE=10` |
| `JOB_INDEX`    | The index of a specific job run instance.                                 | `JOB_INDEX=1` |
| `JOB_INDEX_RETRY_COUNT` |  The current retry count of the job instance.                    | `JOB_INDEX_RETRY_COUNT=0` |
| `JOB_MODE`    | The mode for runs of a job. In `task` mode, jobs run for a maximum time and failed instances are retried per the job retries limit. In `daemon` mode, jobs run without a maximum time and failed instances are restarted indefinitely.  | `JOB_MODE=task` |
| `JOB_RETRY_LIMIT` | The configured retry limit of the jobrun.                              | `JOB_RETRY_LIMIT=3`
| `PATH`         | The list of directories in which the system looks for executables.        | `PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin` |
| `PWD`          | The current working directory.                                            | `PWD=/` |
{: caption="Automatically injected environment variables when deploying {{site.data.keyword.codeengineshort}} jobs"}

Note that each job run instance gets its own index from the array of indices that were specified when the job was created. {{site.data.keyword.codeengineshort}} automatically assigns indices starting from 0 to (array size - 1). The `JOB_INDEX` environment variable contains the index value.

While the job itself doesn't have a URL associated with it, the `CE_DOMAIN` and `CE_SUBDOMAIN` values might be useful if you need to reference an application that is running in the same project. The full external URL of this application is `appName.CE_SUBDOMAIN.CE_DOMAIN`. To reference the private URL of an application, use `appName.CE_SUBDOMAIN`.
