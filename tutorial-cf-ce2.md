---

copyright:
  years: 2022, 2022
lastupdated: "2022-04-01"

keywords: code engine, getting started, migrating, cloud foundry

subcollection: codeengine

content-type: tutorial
completion-time: 30m 

---

{{site.data.keyword.attribute-definition-list}}

# Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}}: Service binding
{: #migrate-cf-ce-tutorial2}
{: toc-content-type="tutorial"}
{: toc-completion-time="30m"}

In the first of the [Migrating Cloud Foundry applications to {{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial), you learned some basics about {{site.data.keyword.codeengineshort}}, including terminology, how to deploy a basic app, and some comparisons between Cloud Foundry and {{site.data.keyword.codeengineshort}}. Now, let's take a common cloud-native app that follows the 12-factor app principles, simplify and update the code, and create both a Cloud Foundry and a {{site.data.keyword.codeengineshort}} version. These versions serve as an example for the discussion of migration steps and deployment aspects.
{: shortdesc}

The sample app is a typical web app, written in Node.js (JavaScript) and uses the Express web framework. An IBM Cloudant NoSQL database serves as the backing service to store data displayed by the app. As typical for cloud-native, 12-factor apps, the sample app is based on discrete, reusable components that act as microservices to make up the overall app. Both the deployed Node.js program and the database can be scaled, improved, or even replaced independently. The components work together because of how they are configured and by using well-defined APIs.

![Simple cloud-native app with backend database service.](images/getting-started-CF2CE.png){: caption="Figure 1. Simple cloud-native app with backend database service." caption-side="bottom"}

The IBM Cloudant database can be configured to work as an attached resource with the app versions deployed to Cloud Foundry and {{site.data.keyword.codeengineshort}}. For simplicity, the solution is kept to these two components.

Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage.
{: note}

## Objectives
{: #migrate-cf-ce-objectives}

Migrate a Cloud Foundry application to {{site.data.keyword.codeengineshort}}.

## Prerequisites
{: #migrate-cf-ce-prereqs}

Before you can get started with {{site.data.keyword.codeengineshort}}, you need to set up your account and install the CLI.

- All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account.

- While you can use {{site.data.keyword.codeengineshort}} through the console, the examples in this documentation focus on the command line. Therefore, you must install the {{site.data.keyword.codeengineshort}} CLI.

    ```txt
    ibmcloud plugin install code-engine
    ```
    {: pre}

    For more information, see [setting up the {{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli). For more information about the CLI, see [{{site.data.keyword.codeengineshort}} CLI reference](/docs/codeengine?topic=codeengine-cli).

## Migration considerations
{: #migrate-cf-ce-considerations}

To migrate an existing solution from Cloud Foundry to {{site.data.keyword.codeengineshort}}, consider the following aspects of your code.

- Code migration
- Service binding
- Build and deployment process (for example, commands, toolchain integration, DevOps)
- Scaling and resource management, including high availability
- Routing
- Security and compliance

All of these aspects depend on the complexity of your solution, its performance and availability requirements, organizational characteristics, and more. Because this code migration depends on the strategy for service binding, we will discuss service binding first.

## Creating the new service bind
{: #migrate-cf-ce-servicebind}
{: step}

This sample application requires a Cloudant database to store content. You can configure access to Cloudant by manually injecting environment variables, but the typical process is through [service binding](/docs/codeengine?topic=codeengine-service-binding). The relationship between the app and its backing services is explicitly stated, so credentials are created and automatically injected into the runtime environment. Cloud Foundry provides the credentials as part of the VCAP_SERVICES object. {{site.data.keyword.codeengineshort}} mimics this object through its [CE_SERVICES](/docs/codeengine?topic=codeengine-service-binding#ce-services) environment variable.

As previously discussed, both the Cloud Foundry and the {{site.data.keyword.codeengineshort}} applications attach to the database service. The code deployed to {{site.data.keyword.codeengineshort}} can be considered a different, newer version of the Cloud Foundry app. It continues to be bound to the same database service, but through other means.

To bind the {{site.data.keyword.codeengineshort}} version of the app to a service

1. Access your [Cloudant database instance](https://cloud.ibm.com/catalog/services/cloudant){: external}. If you do not have one, create one.
2. Create service credentials (IAM service key) for your Cloudant instance with a descriptive name. Specify the IAM role (Manager, Writer, or Reader) for your app. Pick a role with the least level of privilege required for your application. 
3. Bind the service to the app by using the existing credential. {{site.data.keyword.codeengineshort}} can create credentials for you when you bind a service, however, creating your own credential allows you to track and even change the privilege independently of {{site.data.keyword.codeengineshort}}. 

For this sample app with Cloudant as the database service, run the following commands to create the service key `Cloudant-CF2CE-Manager` with the `Manager` role and then use it to bind the service.

```txt
ibmcloud resource service-key-create Cloudant-CF2CE-Manager Manager --instance-name Cloudant-CF2CE
```
{: pre}

```txt
ibmcloud ce app bind --name cf2ce-app --service-credential Cloudant-CF2CE-Manager
```
{: pre}

If your Cloud Foundry app connects to a service through a [user-provided service](https://docs.cloudfoundry.org/devguide/services/user-provided.html){: external}, consider using [secrets and configmaps](/docs/codeengine?topic=codeengine-configmap-secret) for {{site.data.keyword.codeengineshort}}. By using configmaps and secrets, you can inject the service credentials into the runtime environment and manage them as a named object within the {{site.data.keyword.codeengineshort}} project.

## Migrating the code
{: #migrate-cf-ce-code}
{: step}

In most cases, code migration is straight-forward. For example, instead of reading from an environment variable called `VCAP_SERVICES` for Cloud Foundry, your code must read from `CE_SERVICES` for {{site.data.keyword.codeengineshort}}. In addition, there might be subtle differences in how services are named due to the method that services are made available through brokers for Cloud Foundry and through IAM-based resource management for {{site.data.keyword.codeengineshort}}.

Depending on the programming language, your code might use a code library or module to access the Cloud Foundry runtime environment, locally injected configuration (`"dotenv"`), and more. Those sections must be adapted. 

Compare the code in the `server.js` file in these two application examples.

- [1cloudfoundry_base](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/1cloudfoundry_base){: external}
- [3codeengine_target](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/3codeengine_target){: external}


## Staging your application migration
{: #migrate-cf-ce-staging}
{: step}

If your application cannot be down while you move it from Cloud Foundry to {{site.data.keyword.codeengineshort}}, consider performing the code migration with an intermediate step.

- [1cloudfoundry_base](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/1cloudfoundry_base){: external}: The Cloud Foundry code base as the initial source. This app runs only in Cloud Foundry.
- [2cf_ce_intermediate_hybrid](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/2cf_ce_intermediate_hybrid){: external}: Add code to also support a {{site.data.keyword.codeengineshort}} deployment. This application runs in both Cloud Foundry and {{site.data.keyword.codeengineshort}}.
- [3codeengine_target](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/3codeengine_target){: external}: Finally, move to a {{site.data.keyword.codeengineshort}}-only code base after the actual project migration is completed. This application runs only in {{site.data.keyword.codeengineshort}}.

This approach is beneficial because you can continue to maintain or enhance the code base during the migration process, independently of the deployment environment. 

## Building your code and running your app
{: #build-cf-ce-staging}
{: step}

When you are finished setting up your service bind, migrating your code, and preparing to stage your migration, it is time to build your code. Follow the steps in the [first migration tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial) to build your code from a local source. If you want to use the console to build your code, your code must be in Github. For more information, see [Deploying your app from source code](/docs/codeengine?topic=codeengine-app-source-code).


