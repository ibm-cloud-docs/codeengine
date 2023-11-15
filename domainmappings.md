---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-15"

keywords: domain mapping, custom domain, applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, functions in code engine, function workloads in code engine, Function, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with custom domain mappings
{: #domain-mappings}

Domain mappings provide the URL route to your {{site.data.keyword.codeengineshort}} application or function within a project. With {{site.data.keyword.codeengineshort}}, these mappings are automatically created, by default, whenever you deploy an application or create a function. However, you can map your own custom domain to a {{site.data.keyword.codeengineshort}} application or function to route requests from your custom URL to your application or function from the {{site.data.keyword.codeengineshort}} console or CLI.
{: shortdesc}

If you want to target your {{site.data.keyword.codeengineshort}} application or function with a domain that you own, you can use a custom domain mapping. When you set a custom domain mapping in {{site.data.keyword.codeengineshort}}, you define a 1-to-1 mapping between your fully qualified domain name (FQDN) and a {{site.data.keyword.codeengineshort}} application or function in your project.

A custom domain mapping must point to only one {{site.data.keyword.codeengineshort}} application or function. However, you can configure multiple domain mappings to a single application or function.


To work with custom domain mappings in {{site.data.keyword.codeengineshort}}, complete the following steps. Notice that some steps are completed outside of {{site.data.keyword.codeengineshort}}.

1. Review the [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](#considerations-custom-domain). 
2. [Obtain your custom domain from a domain registrar](#prepare-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*).
3. Configure a custom domain mapping in {{site.data.keyword.codeengineshort}} for your [application](/docs/codeengine?topic=codeengine-app-domainmapping) or [function](/docs/codeengine?topic=codeengine-fun-domainmapping).    (*from the {{site.data.keyword.codeengineshort}} console or CLI*). 
4. Complete the custom domain configuration with your domain registrar. (*outside of {{site.data.keyword.codeengineshort}}*)


After you have completed the setup and configuration of your custom domain with your domain registrar, and you have completed the configuration of a domain mapping for your application or function in {{site.data.keyword.codeengineshort}}, test the domain mapping. 

In {{site.data.keyword.codeengineshort}}, you can [view](#view-domain-mapping), [update](#update-custom-domain), or [delete](#delete-custom-domain) domain mappings to your applications or functions. 

## Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}} 
{: #considerations-custom-domain}

Before you implement custom domain mappings in {{site.data.keyword.codeengineshort}}, be aware of the following considerations:

* {{site.data.keyword.codeengineshort}} supports custom domain mappings for domains that are protected with a SSL/TLS certificate, which is signed by a public, trusted certificate authority (CA).
* You can define custom domain mappings that point to public domain names.
* If your domain name can be resolved only by a nonpublic domain name system (DNS), you must provide a certificate that lists the domain name and is signed by a public, trusted CA.
* You must provide the *entire* certificate chain, starting with the certificate that corresponds to the custom domain, followed by all intermediate certificates up to the root certificate.
* You cannot use self-signed certificates.
* You cannot use certificates that are signed by an untrusted or a nonpublic enterprise CA. 
* Your certificate must have an expiry date that is set. 

## Obtaining a custom domain and its TLS certificate and private key
{: #prepare-custom-domain}

Before you configure custom domain mappings in {{site.data.keyword.codeengineshort}}, you must first obtain your custom domain from a domain registrar (*outside of {{site.data.keyword.codeengineshort}}*). 

1. From a domain registrar, obtain your custom domain; for example, `www.example.com`.
2. From your certificate authority (CA), you must obtain a signed SSL/TLS *certificate* for your custom domain. This certificate is a type of digital certificate that is used to establish communication privacy between a server and a client. Certificates contain information that is used to create trusted and secure connections between endpoints. You must also obtain a matching *private key* for the TLS certificate. For security reasons, {{site.data.keyword.codeengineshort}} supports only custom domain mappings that are configured with a TLS/SSL certificate that is signed by a public, trusted CA.

### How can I obtain a certificate for my custom domain?
{: #prepare-custom-domain-cert}

In an enterprise environment, work with your corporate domain administrator to obtain the necessary certificates. However, if the custom domain is within your control and you want quickly create a certificate that is not self-certified, then you can optionally use the [Let's Encrypt](https://letsencrypt.org/){: external} service and [Certbot](https://certbot.eff.org/){: external} to obtain a certificate. 

1. Install [Certbot](https://certbot.eff.org/){: external}. Certbot is a client for the [Automatic Certificate Management Environment (ACME)](https://letsencrypt.org/2019/03/11/acme-protocol-ietf-standard.html#/){: external} protocol for automating interactions between a CA and a server. The Let's Encrypt service uses this client to verify domain ownership and issue certificates. From the [Certbot Instructions page](https://certbot.eff.org/instructions){: external}, select `Other` as the software and select the operating system for your workstation to obtain the applicable information to install the Certbot command line.
2. Run the following command to create your certificate. This example command creates a certificate for the `example.com` and `www.example.com` custom domains. Be sure to update the command for your own custom domain.

    ```txt
    certbot certonly --manual --preferred-challenges dns --email webmaster@example.com --server https://acme-v02.api.letsencrypt.org/directory --agree-tos --domain example.com --domain www.example.com
    ```
    {: pre}

3. To verify that you own the domain, set a `TXT` record with your domain registrar for the domains that you requested in the previous step with values that were provided with the Certbot tool output; for example, `_acme_challenge.example.com` and `_acme_challenge.ww.example.com`. After you set the `TXT` record, continue with the Certbot command.
4. Certbot retrieves the certificate that is signed by Let's Encrypt. The location where the certificate is stored is provided by the Certbot output. Find the `fullchain.pem` and `privkey.pem` files.

Example command to run Certbot on an Ubuntu system

```txt
sudo certbot certonly --manual --preferred-challenges dns --email webmaster@example.com --server https://acme-v02.api.letsencrypt.org/directory --agree-tos --domain example.com --domain www.example.com
```
{: pre}

Example output for the certificate request for `example.com` and `www.example.com`


```txt
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:
_acme-challenge.example.com.
with the following value:
<MASKED>
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:
_acme-challenge.www.example.com
with the following value:
<MASKED>
(This must be set up in addition to the previous challenges; do not remove,
replace, or undo the previous challenge tasks yet. Note that you might be
asked to create multiple distinct TXT records with the same name. This is
permitted by DNS standards.)
Before continuing, verify the TXT record has been deployed. Depending on the DNS
provider, this may take some time, from a few seconds to multiple minutes. You can
check if it has finished deploying with aid of online tools, such as the Google
Admin Toolbox: https://toolbox.googleapps.com/apps/dig/#TXT/_acme-challenge.www.example.com.
Look for one or more bolded line(s) below the line ';ANSWER'. It should show the
value(s) you've just added.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/example.com/fullchain.pem
Key is saved at: /etc/letsencrypt/live/example.com/privkey.pem
This certificate expires on 2023-02-01.
These files will be updated when the certificate renews.
NEXT STEPS:
- This certificate will not be renewed automatically. Autorenewal of --manual certificates requires the use of an authentication hook script (--manual-auth-hook) but one was not provided. To renew this certificate, repeat this same certbot command before the certificate's expiry date.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt: https://letsencrypt.org/donate
 * Donating to EFF: https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```
{: screen}

Your certificate is ready.

### Can I use {{site.data.keyword.cis_short}} for domain management when I am using custom domain mapping with {{site.data.keyword.codeengineshort}}?
{: #prepare-use-cis}

Yes, you can use {{site.data.keyword.cis_full_notm}} for domain management with custom domain mapping with {{site.data.keyword.codeengineshort}}. 

To enable a domain that is managed by {{site.data.keyword.cis_short_notm}} to point to a {{site.data.keyword.codeengineshort}} application or function, set the TLS encryption mode to [End-to-End CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed) within CIS. This mode requires that you obtain a certificate that is generated and signed by a public and trusted CA, outside of {{site.data.keyword.cis_short_notm}}.

Because origin certificates ordered in CIS are not signed by a public and trusted CA, those certificates cannot be used for a domain mapping in {{site.data.keyword.codeengineshort}}. You must obtain a CA signed certificated, outside of CIS.

### How can I use {{site.data.keyword.cis_short}} with custom domain mapping?
{: #completing-custom-domain-cis}

You cannot use the CIS TLS encryption mode of End-to-End flexible with {{site.data.keyword.codeengineshort}} custom domain mappings because this mode uses self-signed certificates that are not allowed. Instead, you can use the default TLS encryption mode of [End-to-End CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed). If you use the CIS TLS mode of End-to-End-flexible, you can switch to use the CIS TLS End-to-End CA signed mode, and obtain a CA signed certificate that is created outside of {{site.data.keyword.cis_short}}.

1. Create the TLS/SSL certificate outside of CIS. See [How can I obtain a certificate for my custom domain?](#prepare-custom-domain-cert)
2. Create a custom domain mapping in {{site.data.keyword.codeengineshort}} for your [application](/docs/codeengine?topic=codeengine-app-domainmapping) or [function](/docs/codeengine?topic=codeengine-fun-domainmapping) with the certificate chain and the private key. 
3. [Obtain the CNAME record for the custom domain mapping](#completing-custom-domain-cname).
4. In CIS, update the DNS records to point to your {{site.data.keyword.codeengineshort}} project. In CIS, go to the DNS records page (**Reliability>DNS**) and **Add** the CNAME record. 
5. Change the CIS mode. Go to the TLS security page (**Security>TLS**). Select **End-to-end CA signed** as the TLS mode. 

If you need to register multiple domains and subdomains, such as `example.com` and `www.example.com`, you must repeat the previous steps 2 and 3 for each subdomain. You can consider creating a single certificate that covers more than one domain. However, you can use that single certificate only one time in a region. If you plan to use your custom domains in more than one project in a single region, keep them separate.
{: note}


### How do I obtain the CNAME record for a custom domain mapping?
{: #completing-custom-domain-cname}

{{site.data.keyword.codeengineshort}} provides the CNAME target for your defined custom domain mapping. 

To obtain the CNAME record from the {{site.data.keyword.codeengineshort}} console, open your defined custom domain mapping and view the Update domain mapping page. Open the Update domain mapping page in one of the following ways:
* From the Domain mappings table, click in the row of your defined custom domain.
* Click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **Edit** to edit the mapping.

From the **Update domain mappings** page, you can obtain the `CNAME target` value. For example, the `www.example.com` mapping has the `custom.abcdabcdabc.us-east.codeengine.appdomain.cloud` CNAME value, where `abcdabcdabc` is an automatically generated unique identifier and `us-east` is the region of your project.

To obtain the CNAME record with the CLI, use the [**`ibmcloud ce domainmapping get`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-get) command. For example,


```txt
ibmcloud ce domainmapping get --domain-name www.example.com
```
{: pre}

Example output

```txt
Getting domain mapping 'www.example.com'...
OK

Domain Name:  www.example.com  
CNAME:        custom.abcdabcdabc.us-south.codeengine.appdomain.cloud  
Target Name:  myapp  
Target Type:  app  
TLS Secret:   mytlssecret  
Status:       ready  
```
{: screen}


After you have the CNAME target, you are ready to add the CNAME record entry to the DNS settings of your custom domain. Note that publishing of the CNAME record with the domain registrar can take some time to populate the DNS changes in the internet.




## Configuring custom domain mappings in {{site.data.keyword.codeengineshort}}
{: #configure-domainmapping}

Now that you are familiar with the concepts of working with custom domain mappings and you have obtained your custom domain from a domain registrar, you can configure your {{site.data.keyword.codeengineshort}} applications or functions to use custom domain mappings. See

* [Configuring custom domain mappings for your application](/docs/codeengine?topic=codeengine-app-domainmapping).
* [Configuring custom domain mappings for your function](/docs/codeengine?topic=codeengine-fun-domainmapping). 


## Viewing domain mappings 
{: #view-domain-mapping}

### Viewing domain mappings from the console
{: #view-domain-mapping-ui}

You can view a listing of all automatically generated and custom domain mappings for your application or function from the console. By default, the contents of the table are scoped to custom domain mappings. Use the **Type** filter to modify the view.

This view displays information about the expiration of the certificate that is associated with your mapping. When the certificate expires, the application or function is no longer reachable with the domain mapping, and this condition yields an SSL error. If you have a certificate that is about to expire, [update the custom domain mapping](#update-custom-domain) to use an updated certificate.

This view also displays information about the specific application or function that is associated with the domain mapping, and the type of the domain mapping. For mappings that are generated by {{site.data.keyword.codeengineshort}}, the type can be `System-public`, `System-private`, or `System-internal`. For custom domain mappings that you create, the type is `Custom`.

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, view a listing of the defined domain mappings for your existing applications or functions. The `Type` indicates whether the mapping is automatically generated or if it is a custom domain mapping.

### Viewing domain mappings with the CLI
{: #view-domain-mapping-cli}

To view a listing of all custom domain mappings for your applications or functions with the CLI, use the [**`ibmcloud ce domainmapping list`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-list) command. For example, 

```txt
ibmcloud ce domainmapping list
```
{: pre}

Example output

```txt
Listing domain mappings...
OK

Name              CNAME                                                        Target  Target-Type  Status  Secret Name  Age
www.example.com   custom.abcdabcdabc.us-south.codeengine.appdomain.cloud       myapp   app          ready   mytlssecret  36m
```
{: screen}

To view a listing of all domain mappings for your applications or functions, including both custom domain mappings that you create and automatically generated domain mappings that {{site.data.keyword.codeengineshort}} creates, specify the `--all` option with the [**`ibmcloud ce domainmapping list`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-list) command. Custom domain mappings display a value for `CNAME`.


## Updating domain mappings
{: #update-custom-domain}

When you create a custom domain mapping, the TLS secret is valid until the certificate expires. From the domain mapping page, you can view information about the remaining days until the certificate expires.



### Updating a domain mapping from the console
{: #update-custom-domain-ui}

Suppose the custom domain mapping for `www.example.com` has a certificate that expires soon. You can update the domain mapping from the console to use an updated certificate or even replace the TLS secret for the mapping. You can also update your domain mapping to point to a different application or function in your project.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **Edit** to edit the mapping. Or, you can click in the row of your defined custom domain to update the mapping.
4. From the Update a domain mapping page, you can change the application or function that is associated with this domain mapping, or you can replace or update the TLS secret for this mapping.
5. Click **Update** to save your changes.

After you update the mapping, you can view the list of domain mappings for the latest changes.


### Updating a domain mapping with the CLI
{: #update-custom-domain-cli}

To update a custom domain mapping, use the [**`ibmcloud ce domainmapping update`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-list) command.

Suppose the custom domain mapping for `www.example.com` has a certificate that expires soon. You can update the domain mapping to use an updated certificate or even replace the TLS secret for the mapping with the `--tls-secret` option. You can also update your domain mapping to point to a different application or function in your project with the `--target` option. 

The following example updates the `www.example.com` custom domain mapping to use an updated TLS secret, `mytlssecret`.

1. Update the TLS secret `mytlssecret` with updated certificate and private key information, which are contained in the `mycertchain2.txt` and `myprivatekey2` files that reside on a local workstation. 

    ```txt
    ibmcloud ce secret update --name mytlssecret --cert-chain-file  mycertchain2.txt --private-key-file myprivatekey2.txt
    ```
    {: pre}

    Example output

    ```txt
    Updating secret mytlssecret..
    OK

    ```
    {: screen}

2. Update the domain mapping to use the updated TLS secret. 

    ```txt
    ibmcloud ce domainmapping update --domain-name www.example.com --tls-secret mytlssecret2
    ```
    {: pre}

    Example output

    ```txt
    Getting domain mapping 'www.example.com.org'...
    Updating domain mapping 'www.example.com.org'...

    ```
    {: screen}

## Deleting domain mappings
{: #delete-custom-domain}

When you delete a domain mapping, you are removing the association of your {{site.data.keyword.codeengineshort}} application or function with your custom domain mapping within {{site.data.keyword.codeengineshort}}. This action does not delete the associated application, function, or TLS secret.

If you delete an application or function that is referenced in a domain mapping, this action also deletes any custom domain mapping that is associated with the application or function. 

When you delete a custom domain mapping, if the DNS settings of your domain are still configured, such that the CNAME points to the {{site.data.keyword.codeengineshort}} project, your traffic still is routed to the {{site.data.keyword.codeengineshort}} project. However, the request is answered with a 404 (not found) error message. Ensure that the associated CNAME record for the fully qualified domain name is updated in the DNS settings by the domain registrar.
{: note}

### Deleting domain mappings from the console
{: #delete-custom-domain-ui}

From the console, you can delete only domain mappings of type `Custom`. Domain mappings that are automatically generated by {{site.data.keyword.codeengineshort}} cannot be deleted.

To delete a custom domain mapping from the console, 

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings** to view a listing of defined domain mappings.
3. (Optional) Click **Type** to filter the domain mappings by type.
4. From the Domain mappings page, delete the custom domain mapping that you want to remove from your application or function. Click the **Actions** icon ![Actions](../icons/action-menu-icon.svg "Actions") > **Delete** to delete the mapping. 

### Deleting domain mappings with the CLI
{: #delete-custom-domain-cli}

To delete a custom domain mapping with the CLI, use the [**`ibmcloud ce domainmapping delete`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-delete) command.

You can delete only custom domain mappings, and not domain mappings that are generated by {{site.data.keyword.codeengineshort}}. Run the [**`ibmcloud ce domainmapping list`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-get) command to display a list of custom domain mappings with the CLI. A custom domain mapping has a generated `CNAME` record. In the CLI, you can obtain the generated `CNAME` value for a specified custom domain mapping by using the [**`ibmcloud ce domainmapping get`**](/docs/codeengine?topic=codeengine-cli#cli-domainmapping-get) command. 


```txt
ibmcloud ce domainmapping delete --domain-name www.example.com -f
```
{: pre}

Example output

```txt
Deleting domain mapping 'www.example.com'...
OK

```
{: screen}



## Next steps 
{: #domain-mappings-next}

Now that you are familiar with working with custom domain mappings and you have obtained your a custom domain with its TLS certificate and private key, you are ready to configure a custom domain mapping in {{site.data.keyword.codeengineshort}} for your [application](/docs/codeengine?topic=codeengine-app-domainmapping) or [function](/docs/codeengine?topic=codeengine-fun-domainmapping).
