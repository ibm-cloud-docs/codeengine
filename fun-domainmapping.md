---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-09"

keywords: domain mapping, custom domain, functions in code engine, http requests in code engine, function workloads in code engine, deploying workloads in code engine, Function, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring custom domain mappings for your function
{: #fun-domainmapping}

Domain mappings provide the URL route to your {{site.data.keyword.codeengineshort}} function within a project. With {{site.data.keyword.codeengineshort}}, these mappings are automatically created, by default, whenever you deploy your function. However, you can map your own custom domain to a {{site.data.keyword.codeengineshort}} function to route requests from your custom URL to your function from the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc}

If you want to target your function with a domain that you own, you can use a custom domain mapping. When you set a custom domain mapping in {{site.data.keyword.codeengineshort}}, you define a 1-to-1 mapping between your fully qualified domain name (FQDN) and a {{site.data.keyword.codeengineshort}} function in your project.

A custom domain mapping must point to only one mapping. However, you can configure multiple domain mappings to a single function.

You can create at most 80 custom domain mappings per project. See [Project quotas](/docs/codeengine?topic=codeengine-limits#project_quotas).

When you create a custom domain mapping in {{site.data.keyword.codeengineshort}}, the domain name that you use in the mapping must be unique in the region.
{: important}

To create and set up custom domain mappings, complete these steps:
1. Review the [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-domain-mappings#considerations-custom-domain).
2. [Obtain your custom domain from a domain registrar](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*). 
3. Configure a custom domain mapping in {{site.data.keyword.codeengineshort}} for your [function](/docs/codeengine?topic=codeengine-fun-domainmapping) (*from the {{site.data.keyword.codeengineshort}} console or CLI*). 
4. Complete the custom domain configuration with your domain registrar. (*outside of {{site.data.keyword.codeengineshort}}*).


Suppose that you want to create a custom domain mapping for `www.example.com` and `shop.example.com`. In this case, you must create a custom domain mapping for each unique domain or subdomain. However, you can reuse the same TLS secret for multiple custom domain mappings if the certificates of the TLS secret includes the domain that is specified in the custom domain mapping. This means that you can map a TLS secret to multiple domains, such as `www.example.com` and `shop.example.com`, or to a wildcard domain such as `*.example.com`.
{: note}
 


## Configuring custom domain mappings from the console
{: #fun-custom-domain-ui}

You can create a custom domain mapping with your {{site.data.keyword.codeengineshort}} function to your registered domain name with the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

Before you begin

* [Obtain a custom domain from a domain registrar and its signed TLS certificate and private key](/docs/codeengine?topic=codeengine-domain-mappings#prepare-custom-domain).
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create a function](/docs/codeengine?topic=codeengine-fun-create-existing).

In this scenario, create a custom domain mapping to a function with a TLS secret. For example, create a custom domain mapping to map the `www.example.com` domain to the `myfunction` function.
  
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
    * Select an existing target function; for example, `myfunction`. For this example, the `myfunction` function uses the `icr.io/codeengine/helloworld` sample image. For more information about the code that is used for this example, see [`helloworld`](https://github.com/IBM/CodeEngine/tree/main/helloworld){: external}.
    * Notice the **CNAME target** field. This value is the CNAME entry that is required when you [complete the custom domain configuration with your domain registrar](#fun-completing-custom-domain) so that traffic that targets your custom domain is routed to the specified function.

6. Click **Create** to create the custom domain mapping.

Now you have a domain mapping that is created in {{site.data.keyword.codeengineshort}}. However, requests that are sent to your function are not (yet) routed to your custom domain. Next, [complete the custom domain configuration with your domain registrar](#fun-completing-custom-domain).

Suppose that you want to create a custom domain mapping for `www.example.com` and `shop.example.com`. In this case, you must create a custom domain mapping for each unique domain or subdomain. However, you can reuse the same TLS secret for multiple custom domain mappings if the TLS secret includes certification for the domain that is specified in the custom domain mapping. The TLS secret can contain certificates that map to specific multiple domains, such as `www.example.com` and `shop.example.com`, or a wildcard domain such as `*.example.com`. Note that you cannot use the wildcard domain more than one time within a region.
{: note}

## Configuring custom domain mappings with the CLI
{: #fun-custom-domain-cli}

To create a custom domain mapping with the CLI, use the **`domainmapping create`** command. This command requires a fully qualified domain name (FQDN), such as `www.example.com`, a target function, and a TLS secret.  For a complete listing of options, see the [**`ibmcloud ce domainmapping create`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-create) command.
{: shortdesc}


Before you begin

* Obtain the registered domain name.
* Obtain the signed TLS certificate and the private key for your custom domain.
* Set up your [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli) environment.
* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create a function](/docs/codeengine?topic=codeengine-fun-create-repo).

When your domain name is registered, you have a signed TLS certificate and its matching private key for this domain, and you have an existing {{site.data.keyword.codeengineshort}} function, you are ready to add a custom domain mapping . You can use the **`domainmapping create`** command in the CLI to create a custom domain mapping with your {{site.data.keyword.codeengineshort}} function.


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


2. Create the custom domain mapping between the {{site.data.keyword.codeengineshort}} `myfunction` function and the custom domain, `www.example.com`. Use the TLS secret that you created in the previous step. 



    ```txt
    ibmcloud ce domainmapping create --domain-name www.example.com --target myhellofun --tls-secret mytlssecret
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
| `--target` | The name of the target {{site.data.keyword.codeengineshort}} function. This value is required.  |
| `--tls-secret` | The TLS secret for the domain mapping. This value is required.  |
{: caption="Command description" caption-side="bottom"}


Now your custom domain mapping is created in {{site.data.keyword.codeengineshort}}. However, requests that are sent to your function are not (yet) routed to your custom domain. Next, you must [complete the custom domain configuration with your domain registrar](#fun-completing-custom-domain).



## Completing the custom domain configuration with your domain registrar
{: #fun-completing-custom-domain}

After the {{site.data.keyword.codeengineshort}} custom domain mapping is created, a CNAME record that matches the fully qualified domain name must be added to the DNS settings of the custom domain. You can find the DNS settings in the configuration settings of the corresponding domain registrar. Complete this step so that traffic that targets your custom domain is routed to the {{site.data.keyword.codeengineshort}} function as defined in your {{site.data.keyword.codeengineshort}} custom domain mapping.


## Testing your custom domain
{: #testfun-custom-domain}

After you complete the custom domain configuration with your domain registrar and the CNAME record updates are published, you can test the function with the custom domain mapping.

With a browser, call the function by targeting the custom domain with the `curl` command. 

```txt
curl -v -X GET https://www.example.com
```
{: pre}


The output of the call to the custom domain is mapped to the `myhellofun` function, which uses the `icr.io/codeengine/helloworld` sample image.
{: note}
