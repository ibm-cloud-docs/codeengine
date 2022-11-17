---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-17"

keywords: code engine, getting started, migrating, cloud foundry

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Migrating your service binding
{: #migrate-cf-ce-bind}

Let's take a common cloud-native app that follows the 12-factor app principles, simplify and update the code, and create both a Cloud Foundry and a {{site.data.keyword.codeengineshort}} version. These versions serve as an example for the discussion of migration steps and deployment aspects.
{: shortdesc}

The sample app is a typical web app that is written in Node.js (JavaScript) and uses the Express web framework. An IBM Cloudant NoSQL database serves as the backing service to store data displayed by the app. As typical for cloud-native, 12-factor apps, the sample app is based on discrete, reusable components that act as microservices to make up the overall app. Both the deployed Node.js program and the database can be scaled, improved, or even replaced independently. The components work together because of how they are configured and by using well-defined APIs.

![Simple cloud-native app with backend database service.](images/getting-started-CF2CE.png){: caption="Figure 1. Simple cloud-native app with backend database service." caption-side="bottom"}

The IBM Cloudant database can be configured to work as an attached resource with the app versions that are deployed to Cloud Foundry and {{site.data.keyword.codeengineshort}}. For simplicity, the solution is kept to these two components.


## Creating the service bind
{: #migrate-cf-ce-servicebind}
{: step}

This sample application requires a Cloudant database to store content. You can configure access to Cloudant by manually injecting environment variables, but the typical process is through [service binding](/docs/codeengine?topic=codeengine-service-binding). The relationship between the app and its backing services is explicitly stated, so credentials are created and automatically injected into the runtime environment. Cloud Foundry provides the credentials as part of the `VCAP_SERVICES` object. {{site.data.keyword.codeengineshort}} mimics this object through its [`CE_SERVICES`](/docs/codeengine?topic=codeengine-service-binding#ce-services) environment variable.

Both the Cloud Foundry and the {{site.data.keyword.codeengineshort}} applications attach to the database service. The code deployed to {{site.data.keyword.codeengineshort}} can be considered a different, newer version of the Cloud Foundry app. It continues to be bound to the same database service, but through other means.

To bind the {{site.data.keyword.codeengineshort}} version of the app to a service,

1. Access your [Cloudant database instance](https://cloud.ibm.com/catalog/services/cloudant){: external}. If you do not have one, create one.
2. Create service credentials (IAM service key) for your Cloudant instance with a descriptive name. Specify the IAM role (`Manager`, `Writer`, or `Reader`) for your app. Pick a role with the least level of privilege required for your application. 
3. Bind the service to the app by using the existing credential. {{site.data.keyword.codeengineshort}} can create credentials for you when you bind a service. However, by creating your own credential, you can track and even change the privilege independently of {{site.data.keyword.codeengineshort}}. 

For this sample app with Cloudant as the database service, run the following commands to create the service key `Cloudant-CF2CE-Manager` with the `Manager` role and then use it to bind the service.

```txt
ibmcloud resource service-key-create Cloudant-CF2CE-Manager Manager --instance-name Cloudant-CF2CE
```
{: pre}

```txt
ibmcloud ce app bind --name cf2ce-app --service-instance Cloudant-CF2CE --service-credential Cloudant-CF2CE-Manager
```
{: pre}

If your Cloud Foundry app connects to a service through a [user-provided service](https://docs.cloudfoundry.org/devguide/services/user-provided.html){: external}, create an app that uses [secrets and ConfigMaps](/docs/codeengine?topic=codeengine-configmap-secret) for {{site.data.keyword.codeengineshort}}. By using ConfigMaps and secrets, you can inject the service credentials into the runtime environment and manage them as a named object within the {{site.data.keyword.codeengineshort}} project.

## Migrating the code
{: #migrate-cf-ce-code}

Usually, code migration is straight-forward. For example, instead of reading from an environment variable that is called `VCAP_SERVICES` for Cloud Foundry, your code must read from `CE_SERVICES` for {{site.data.keyword.codeengineshort}}. In addition, be aware of subtle differences in how services are named due to the method that services are made available through brokers for Cloud Foundry and through IAM-based resource management for {{site.data.keyword.codeengineshort}}.

Depending on the programming language, your code might use a code library or module to access the Cloud Foundry runtime environment, locally injected configuration (`"dotenv"`), and more. Those sections must be adapted. 

Compare the code in the `server.js` file in these two application examples.

- [1cloudfoundry_base](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/1cloudfoundry_base){: external}
- [3codeengine_target](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/3codeengine_target){: external}


## Staging your application migration
{: #migrate-cf-ce-staging}

If your application cannot be down while you move it from Cloud Foundry to {{site.data.keyword.codeengineshort}}, consider performing the code migration with an intermediate step.

- [1cloudfoundry_base](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/1cloudfoundry_base){: external}: The Cloud Foundry code base as the initial source. This app runs only in Cloud Foundry.
- [2cf_ce_intermediate_hybrid](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/2cf_ce_intermediate_hybrid){: external}: Add code to also support a {{site.data.keyword.codeengineshort}} deployment. This application runs in both Cloud Foundry and {{site.data.keyword.codeengineshort}}.
- [3codeengine_target](https://github.com/IBM-Cloud/CloudFoundry-to-CodeEngine/tree/3codeengine_target){: external}: Finally, move to a {{site.data.keyword.codeengineshort}}-only code base after the actual project migration is completed. This application runs only in {{site.data.keyword.codeengineshort}}.

This approach is beneficial because you can continue to maintain or enhance the code base during the migration process, independently of the deployment environment. 

## Building your code and running your app
{: #build-cf-ce-staging}

When you are finished setting up your service bind, migrating your code, and preparing to stage your migration, it is time to build your code. Follow the steps in the [first migration tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-tutorial) to build your code from a local source. If you want to use the console to build your code, your code must be in Git-hub. For more information, see [Deploying your app from source code](/docs/codeengine?topic=codeengine-app-source-code).

## Next steps
{: #migrate-cf-ce-next-sb}

1. Just starting your migration? Check out [Getting started](/docs/codeengine?topic=codeengine-migrate-cf-ce-getstart).
2. [Compare Cloud Foundry terminology with {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-migrate-cf-ce-terms).
3. [Try out {{site.data.keyword.codeengineshort}} with a local build tutorial](/docs/codeengine?topic=codeengine-migrate-cf-ce-local).
4. **Migrating your service binding (current page)**
5. Learn about [scaling and traffic management](/docs/codeengine?topic=codeengine-migrate-cf-ce-scale).
6. Find [{{site.data.keyword.codeengineshort}} equivalents to Cloud Foundry commands](/docs/codeengine?topic=codeengine-migrate-cf-ce-cmd).
7. Still have questions? Try the [Migrating Cloud Foundry applications to {{site.data.keyword.codeengineshort}} FAQ](/docs/codeengine?topic=codeengine-migrate-cf-ce-faq).

Other information

- Find out about [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
- Try other [{{site.data.keyword.codeengineshort}} tutorials](https://cloud.ibm.com/docs?tab=tutorials&tags=codeengine&page=1&pageSize=20){: external}.
- Explore other [{{site.data.keyword.codeengineshort}} topics](/docs/codeengine?topic=codeengine-learning-paths).

