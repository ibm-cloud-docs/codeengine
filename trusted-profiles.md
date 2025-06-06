---

copyright:
  years: 2025
lastupdated: "2025-04-04"

keywords: service access, trusted profiles, enabling trusted profiles

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with trusted profiles in {{site.data.keyword.codeengineshort}} to access {{site.data.keyword.cloud_notm}} services
{: #trusted-profiles}

You can configure your {{site.data.keyword.codeengineshort}} components (applications, jobs, or functions) to use IAM trusted profiles to authorize {{site.data.keyword.codeengineshort}} components and access {{site.data.keyword.cloud}} services without managing separate credentials. Trusted profiles do not require storing and managing secret credentials. No maintenance or credential rotation are needed.
{: shortdesc}

Before you enable an application, job, or function to access {{site.data.keyword.cloud_notm}} services to use a trusted profile, you require an {{site.data.keyword.iamlong}} (IAM) trusted profile. Create a trusted profile in IAM that trusts your {{site.data.keyword.codeengineshort}} component as a compute resource and grant access to the target service. See [IAM documentation](/docs/account?topic=account-create-trusted-profile&interface=ui) to create your trusted profile.

The {{site.data.keyword.codeengineshort}} application, job, or function then needs access to a compute resource token so that it can identify itself and authenticate as an {{site.data.keyword.codeengineshort}} component for IAM. This token authenticates the services to which the {{site.data.keyword.codeengineshort}} component is allowed to communicate. Trusted profiles control the specific services with which the {{site.data.keyword.codeengineshort}} component can communicate.

You can enable {{site.data.keyword.codeengineshort}} to provide this token to the application, job, or function, to provide full trusted profile support in {{site.data.keyword.codeengineshort}}, by using the {{site.data.keyword.codeengineshort}} console or the CLI.

## Configuring {{site.data.keyword.codeengineshort}} to support trusted profiles by using the console
{: #configuring-trusted-profiles-ui}
{: ui}

The following steps describe locating an existing {{site.data.keyword.codeengineshort}} application, job, or function and then enabling trusted profiles support. When you create a new application, job, or function, you can enable trusted profiles during the creation, by using the **Optional settings** > **Service access** section.
{: tip}

### Configuring a {{site.data.keyword.codeengineshort}} application to use trusted profiles
{: #configuring-trusted-profiles-app-ui}
{: ui}

1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
2. Click the name of your project to open the Overview page.
3. Click **Applications** to open a list of your applications. Click the name of your application to open its application page.
4. Click **Service access** > **Trusted profiles**.
5. Set the **Enable trusted profiles** option to **Enabled**. When you enable this application for trusted profiles, {{site.data.keyword.codeengineshort}} provides a token that the application's code can use to match trusted profiles by project or by application name.
6. [Enable your application code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).

### Configuring a {{site.data.keyword.codeengineshort}} job to use trusted profiles
{: #configuring-trusted-profiles-job-ui}
{: ui}

1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
2. Click the name of your project to open the Overview page.
3. Click **Jobs** to open a list of your jobs. Click the name of your job to open its job page.
4. Click **Service access** > **Trusted profiles**.
5. Set the **Enable trusted profiles** option to **Enabled**. When you enable this job for trusted profiles, {{site.data.keyword.codeengineshort}} provides a token that the job's code can use to match trusted profiles by project or by job name.
6. [Enable your job code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).

### Configuring a {{site.data.keyword.codeengineshort}} function to use trusted profiles
{: #configuring-trusted-profiles-function-ui}
{: ui}

1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
2. Click the name of your project to open the Overview page.
3. Click **Functions** to open a list of your functions. Click the name of your function to open its function page.
4. Click **Service access** > **Trusted profiles**.
5. Set the **Enable trusted profiles** option to **Enabled**. When you enable this function for trusted profiles, {{site.data.keyword.codeengineshort}} provides a token that the function's code can use to match trusted profiles by project or by function name.
6. [Enable your function code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).

## Configuring {{site.data.keyword.codeengineshort}} to support trusted profiles by using the CLI
{: #configuring-trusted-profiles-cli}
{: cli}

### Configuring a {{site.data.keyword.codeengineshort}} application to use trusted profiles
{: #configuring-trusted-profiles-app-cli}
{: cli}

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Enable trusted profile support:
    * By default, when you create a new {{site.data.keyword.codeengineshort}} application, trusted profile support is not enabled. To enable trusted profiles support when you create a new application, use the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce app create --name myapp --image icr.io/codeengine/hello --trusted-profiles-enabled=true
        ```
        {: pre}

    * If you have an existing application and want to enable trusted profile support for it, update it with the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce app update --name myapp --trusted-profiles-enabled=true
        ```
        {: pre}

        If required, you can later disable trusted profiles support by updating the application with the `trusted-profiles-enabled=false` setting.
        {: tip}

3. [Enable your application code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).

### Configuring a {{site.data.keyword.codeengineshort}} job to use trusted profiles
{: #configuring-trusted-profiles-job-cli}
{: cli}

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Enable trusted profile support:
    * By default, when you create a new {{site.data.keyword.codeengineshort}} job, trusted profile support is not enabled. To enable trusted profiles support when you create a new job, use the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce job create --name myjob --image icr.io/codeengine/helloworld --trusted-profiles-enabled=true
        ```
        {: pre}

    * If you have an existing job and want to enable trusted profile support for it, update it with the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce job update --name myjob --trusted-profiles-enabled=true
        ```
        {: pre}

        If required, you can later disable trusted profiles support by updating the job with the `trusted-profiles-enabled=false` setting.
        {: tip}

3. [Enable your job code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).

### Configuring a {{site.data.keyword.codeengineshort}} function to use trusted profiles
{: #configuring-trusted-profiles-function-cli}
{: cli}

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Enable trusted profile support:
    * By default, when you create a new {{site.data.keyword.codeengineshort}} function, trusted profile support is not enabled. To enable trusted profiles support when you create a new function, use the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce fn create --name myhellofun --inline-code main.js --runtime nodejs --trusted-profiles-enabled=true
        ```
        {: pre}

    * If you have an existing function and want to enable trusted profile support for it, update it with the `trusted-profiles-enabled=true` setting. For example:

        ```txt
        ibmcloud ce fn update --name myhellofun --trusted-profiles-enabled=true
        ```
        {: pre}

        If required, you can later disable trusted profiles support by updating the function with the `trusted-profiles-enabled=false` setting.
        {: tip}

3. [Enable your function code to authenticate trusted profiles](/docs/codeengine?topic=codeengine-trusted-profiles-authentication-file).
