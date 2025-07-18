---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-18"

keywords: domain mapping, custom domain, applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring custom domain mappings for your app 
{: #app-domainmapping}

Domain mappings provide the URL route to your {{site.data.keyword.codeengineshort}} applications within a project. With {{site.data.keyword.codeengineshort}}, these mappings are automatically created, by default, whenever you deploy an application. However, you can map your own custom domain to a {{site.data.keyword.codeengineshort}} application to route requests from your custom URL to your application from the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc}

If you want to target your application with a domain that you own, you can use a custom domain mapping. When you set a custom domain mapping in {{site.data.keyword.codeengineshort}}, you define a 1-to-1 mapping between your fully qualified domain name (FQDN) and a {{site.data.keyword.codeengineshort}} application in your project.

A custom domain mapping must point to only one application. However, you can configure multiple domain mappings to a single application.

You can create at most 80 custom domain mappings per project. See [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

When you create a custom domain mapping in {{site.data.keyword.codeengineshort}}, the domain name that you use in the mapping must be unique in the region.
{: important}

To create and set up custom domain mappings, complete these steps:
1. Review the [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-domain-mappings#considerations-custom-domain).
2. [Obtain your custom domain from a domain registrar](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*). 
3. Configure a custom domain mapping in {{site.data.keyword.codeengineshort}} for your [application](/docs/codeengine?topic=codeengine-app-domainmapping) (*from the {{site.data.keyword.codeengineshort}} console or CLI*). 
4. Complete the custom domain configuration with your domain registrar (*outside of {{site.data.keyword.codeengineshort}}*).

Suppose that you want to create a custom domain mapping for `www.example.com` and `shop.example.com`. In this case, you must create a custom domain mapping for each unique domain or subdomain. However, you can reuse the same TLS secret for multiple custom domain mappings if the certificates of the TLS secret includes the domain that is specified in the custom domain mapping. This means that you can map a TLS secret to multiple domains, such as `www.example.com` and `shop.example.com`, or to a wildcard domain such as `*.example.com`.
{: note}
 


## Configuring custom domain mappings from the console
{: #custom-domain-ui}

You can create a custom domain mapping with your {{site.data.keyword.codeengineshort}} application to your registered domain name with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}


In this scenario, let's create a custom domain mapping to an application with a TLS secret. For example, create a custom domain mapping to map the `www.example.com` domain to the `myapp` application.

Before you begin

* [Obtain a custom domain from a domain registrar and its signed TLS certificate and private key](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain).
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an app](/docs/codeengine?topic=codeengine-deploy-app&interface=ui#deploy-app-console).


1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, click **Create** to create your mapping.
4. From the Create a domain mapping page, specify the TLS secret to use with this domain mapping. {{site.data.keyword.codeengineshort}} validates whether the certificate is signed by a trusted CA, and whether the certificate matches the provided custom domain name and private key.

    To create a new TLS secret,
      1. Click **Create**.
      2. Add the TLS certificate, including all intermediate certificates, which are associated with your domain. If the certificate is provided to you as separate files, concatenate the content of the files. You can provide this information in a file. 
      3. Add the private key that corresponds to your certificate. You can provide this information in a file. 

      Example format for a certificate chain

      ```txt 
      -----BEGIN CERTIFICATE-----
      ...certificate...
      -----END CERTIFICATE-----
      -----BEGIN CERTIFICATE-----
      ...intermediate-certificate...
      -----END CERTIFICATE-----
      -----BEGIN CERTIFICATE-----
      ...intermediate-certificate...
      -----END CERTIFICATE-----
      ```
      {: screen}


    Or, to use an existing TLS secret,
      1. Click **Select**.
      2. Select the existing secret from the list that you want to use.

5. Specify the domain name and target component.
    * Specify the fully qualified domain name for your custom domain name; for example, `www.example.com`.
    * Select an existing target application; for example, `myapp`. For this example, the `myapp` application uses the `icr.io/codeengine/helloworld` sample image. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.
    * Notice the **CNAME target** field. This value is the CNAME entry that is required when you [complete the custom domain configuration with your domain registrar](#app-completing-custom-domain) so that traffic that targets your custom domain is routed to the specified application.

6. Click **Create** to create the custom domain mapping.

Now you have a domain mapping that is created in {{site.data.keyword.codeengineshort}}. However, requests that are sent to your application are not (yet) routed to your custom domain. Next, you must [complete the custom domain configuration with your domain registrar](#app-completing-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*).




## Configuring custom domain mappings with the CLI
{: #custom-domain-cli}

To create a custom domain mapping with the CLI, use the **`domainmapping create`** command. This command requires a fully qualified domain name (FQDN), such as `www.example.com`, a target application, and a TLS secret.  For a complete listing of options, see the [**`ibmcloud ce domainmapping create`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-create) command.
{: shortdesc}


Before you begin

* Obtain the registered domain name.
* Obtain the signed TLS certificate and the private key for your custom domain.
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an app](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#deploy-app-cli).

When your domain name is registered, you have a signed TLS certificate and its matching private key for this domain, and you have an existing {{site.data.keyword.codeengineshort}} application, you are ready to add a custom domain mapping to this application. You can use the **`domainmapping create`** command in the CLI to create a custom domain mapping with your {{site.data.keyword.codeengineshort}} application.


1. Create a TLS secret with the signed TLS certificate and the private key. In this example, the `mycert.txt` file contains the TLS certificate, including all intermediate certificates, which are associated with your domain. If the certificate is provided to you as separate files, concatenate the content of the files. The `myprivatekey.txt` file contains the matching private key that corresponds to the certificate chain.  

    ```txt
    ibmcloud ce secret create --name mytlssecret --format tls --cert-chain-file  mycertchain.txt --private-key-file myprivatekey.txt
    ```
    {: pre}

    Example output

    ```txt
    Creating tls secret 'mytlssecret'...
    OK
    ```
    {: screen}


2. Create the custom domain mapping between the {{site.data.keyword.codeengineshort}} `myapp` application and the custom domain, `www.example.com`. Use the TLS secret that you created in the previous step. 



    ```txt
    ibmcloud ce domainmapping create --domain-name www.example.com --target myapp --tls-secret mytlssecret
    ```
    {: pre}

    Example output

    ```txt
    OK
    Domain mapping successfully created.
    ```
    {: screen}

The following table summarizes the options that are used with the **`domainmapping create`** command in this example. For more information about the command and its options, see the [**`ibmcloud ce domainmapping create`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-create) command.

| Option | Description |
| -------------- | -------------- |
| `--domain-name` | The name of the custom domain mapping. Specify the name of your custom domain, such as `www.example.com`.  This value is required. |
| `--target` | The name of the target {{site.data.keyword.codeengineshort}} application. This value is required.  |
| `--tls-secret` | The TLS secret for the domain mapping. This value is required.  |
{: caption="Command description" caption-side="bottom"}


Now you have a custom domain mapping that is created in {{site.data.keyword.codeengineshort}}. However, requests that are sent to your application are not (yet) routed to your custom domain. Next, [complete the custom domain configuration with your domain registrar](#app-completing-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*).


## Completing the custom domain configuration with your domain registrar
{: #app-completing-custom-domain}

After the {{site.data.keyword.codeengineshort}} custom domain mapping is created, a CNAME record that matches the fully qualified domain name must be added to the DNS settings of the custom domain. You can find the DNS settings in the configuration settings of the corresponding domain registrar. Complete this step so that traffic that targets your custom domain is routed to the {{site.data.keyword.codeengineshort}} function as defined in your {{site.data.keyword.codeengineshort}} custom domain mapping.

## Testing your custom domain
{: #testapp-custom-domain}

After you complete the custom domain configuration with your domain registrar and the CNAME record updates are published, you can test the application with the custom domain mapping.

With a browser, call the application by targeting the custom domain by using `curl`. 

```txt
curl -v -X GET https://www.example.com
```
{: pre}

Example output

```txt
Hello World from:
     ___  __  ____  ____
    / __)/  \(    \(  __)
   ( (__(  O )) D ( ) _)
    \___)\__/(____/(____)
 ____  __ _   ___  __  __ _  ____
(  __)(  ( \ / __)(  )(  ( \(  __)
 ) _) /    /( (_ \ )( /    / ) _)
(____)\_)__) \___/(__)\_)__)(____)
Some Env Vars:
--------------
CE_API_BASE_URL=https://api.private.us-south.codeengine.cloud.ibm.com
CE_APP=myapp
CE_DOMAIN=us-south.codeengine.appdomain.cloud
CE_PROJECT_ID=abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
CE_REGION=us-south
CE_SUBDOMAIN=abcdabcdab
HOME=/root
HOSTNAME=myapp-00001-deployment-6db6d89dc7-k6qc7
K_REVISION=myapp-00001
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
PORT=8080
PWD=/
SHLVL=1
```
{: screen}



The output of the call to the custom domain is mapped to the `myapp` application, which uses the `icr.io/codeengine/helloworld` sample image.
{: note}

For more information about domain mappings in {{site.data.keyword.codeengineshort}}, see [Working with custom domain mappings](/docs/codeengine?topic=codeengine-domain-mappings).
