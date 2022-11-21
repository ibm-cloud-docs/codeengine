---

copyright:
  years: 2022, 2022
lastupdated: "2022-11-21"

keywords: domain mapping, custom domain, applications in code engine, apps in code engine, http requests in code engine, deploy apps in code engine, app workloads in code engine, deploying workloads in code engine, application, domain mappings, custom domain mappings, CNAME, TLS, TLS secret, private key, certificate

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Configuring custom domain mappings for your app
{: #domain-mappings}

Domain mappings provide the URL route to your {{site.data.keyword.codeengineshort}} applications within a project. With {{site.data.keyword.codeengineshort}}, these mappings are automatically created, by default, whenever you deploy an application. However, you can map your own custom domain to a {{site.data.keyword.codeengineshort}} application to route requests from your custom URL to your application from the {{site.data.keyword.codeengineshort}} console.
{: shortdesc}

If you want to target your application with a domain that you own, you can use a custom domain mapping. When you set a custom domain mapping in {{site.data.keyword.codeengineshort}}, you define a 1-to-1 mapping between your fully qualified domain name (FQDN) and a {{site.data.keyword.codeengineshort}} application in your project.

A custom domain mapping must point to only one application. However, you can configure multiple domain mappings to a single application.

You can create at most 40 custom domain mappings per project.

When you create a custom domain mapping in {{site.data.keyword.codeengineshort}}, the domain name that you use in the mapping must be unique in the region.
{: important}

To create and setup custom domain mappings, complete these steps:
1. Review the [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](#considerations-custom-domain).
2. [Prepare to add a custom domain mapping](#prepare-custom-domain) (*outside of {{site.data.keyword.codeengineshort}}*).
3. [Configure custom domain mappings](#custom-domain-ui) (*from the {{site.data.keyword.codeengineshort}} console*).
4. [Complete the custom domain configuration with your domain registrar](#completing-custom-domain-registrar) (*outside of {{site.data.keyword.codeengineshort}}*).

After the custom domain mapping is created, you can [test](#test-custom-domain), [update](#update-custom-domain-ui), [view](#view-domain-mapping-ui), or [delete](#delete-custom-domain) your custom domain mappings. 

## Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}} 
{: #considerations-custom-domain}

Before you implement custom domain mappings in {{site.data.keyword.codeengineshort}}, be aware of the following considerations:

* {{site.data.keyword.codeengineshort}} supports custom domain mappings for domains that are protected with a SSL/TLS certificate, which is signed by a public, trusted certificate authority (CA).
* You can define custom domain mappings that point to public domain names.
* If your domain name can be resolved only by a nonpublic domain name system (DNS), you must provide a certificate that lists the domain name and is signed by a public, trusted CA.
* You must provide the *entire* certificate chain, starting with the certificate that corresponds to the custom domain, followed by all intermediate certificates up to the root certificate.
* You cannot use self-signed certificates.
* You cannot use certificates that are signed by an untrusted or a nonpublic enterprise CA.

## Preparing to add a custom domain mapping
{: #prepare-custom-domain}

When you want to use a custom domain mapping with {{site.data.keyword.codeengineshort}} application, you must take the following actions outside of {{site.data.keyword.codeengineshort}} before you can create the custom domain mapping.

1. From a domain registrar, obtain your custom domain; for example, `www.example.com`.
2. From your certificate authority (CA), you must obtain a signed SSL/TLS *certificate* for your custom domain from your certificate authority (CA). This certificate is a type of digital certificate that is used to establish communication privacy between a server and a client. Certificates are issued by certificate authorities and contain information that is used to create trusted and secure connections between endpoints. You must also obtain a matching *private key* for the TLS certificate. For security reasons, {{site.data.keyword.codeengineshort}} supports only custom domain mappings that are configured with a TLS/SSL certificate, which is signed by a public, trusted CA.

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

Example command running Certbot on an Ubuntu system

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

Yes! You can use {{site.data.keyword.cis_full_notm}} for domain management with custom domain mapping with {{site.data.keyword.codeengineshort}}. However, the CIS TLS encryption mode of End-to-End flexible uses self-signed certificates, which are not allowed with {{site.data.keyword.codeengineshort}} custom domain mapping. Instead, use the default TLS encryption mode of [End-to-End CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed). If you use the CIS TLS mode of End-to-End flexible, switch to use the CIS TLS End-to-End CA signed mode. With this mode, you must obtain a CA signed certificate that is created outside of CIS. For more information, see [How can I use {{site.data.keyword.cis_short}} with custom domain mapping?](#completing-custom-domain-cname).


## Configuring custom domain mappings from the console
{: #custom-domain-ui}

When your domain name is registered and you have a signed TLS certificate and its matching private key for this domain, and you have an existing {{site.data.keyword.codeengineshort}} application, you are ready to add a custom domain mapping to this application. Use the console to create a custom domain mapping with your {{site.data.keyword.codeengineshort}} application.

The transport layer security (TLS) secret that {{site.data.keyword.codeengineshort}} creates contains the signed TLS certificate and its matching private key. A TLS secret can also contain a signed TLS certificate and its matching private key for specified multiple domains, or it can contain a wildcard domain, such as for `*.example.com`.

In this scenario, let's create a custom domain mapping to an application with a TLS secret. For example, create a custom domain mapping to map the `www.example.com` domain to the `myapp` application.

Before you begin

* [Create a project](/docs/codeengine?topic=codeengine-manage-project).
* [Create an app](/docs/codeengine?topic=codeengine-deploy-app#deploy-app-console).
* Obtain the signed TLS certificate and the private key.


1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, click **Create** to create your mapping.
4. From the Create a domain mapping page, specify the TLS secret to use with this domain mapping. {{site.data.keyword.codeengineshort}} validates whether the certificate is signed by a trusted CA, and whether the certificate matches the provided custom domain name and private key.

    To create a new TLS secret,
      1. Click **Create**.
      2. Add the TLS certificate, including all intermediate certificates, which are associated with your domain. If the certificate is provided to you as separate files, concatenate the content of the files.
      3. Add the private key that corresponds to your certificate.

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
    * Notice the **CNAME target** field. This value is the CNAME entry that is required when you [complete the custom domain configuration with your domain registrar](#completing-custom-domain-registrar) so that traffic that targets your custom domain is routed to the specified application.

6. Click **Create** to create the custom domain mapping.

Now you have a domain mapping that is created in {{site.data.keyword.codeengineshort}}. However, requests that are sent to your application are not (yet) routed to your custom domain. Next, [complete the custom domain configuration with your domain registrar](#completing-custom-domain-registrar).

Suppose that you want to create a custom domain mapping for `www.example.com` and `shop.example.com`. In this case, you must create a custom domain mapping for each unique domain or subdomain. However, you can reuse the same TLS secret for multiple custom domain mappings if the TLS secret includes certification for the domain that is specified in the custom domain mapping. The TLS secret can contain certificates that map to specific multiple domains, such as `www.example.com` and `shop.example.com`, or a wildcard domain such as `*.example.com`.
{: note}

## Completing the custom domain configuration with your domain registrar
{: #completing-custom-domain-registrar}

After the {{site.data.keyword.codeengineshort}} custom domain mapping is created, a CNAME record that matches the fully qualified domain name must be added to the DNS settings of the custom domain. You can find the DNS settings in the configuration settings of the corresponding domain registrar. Complete this step so that traffic that targets your custom domain is routed to the {{site.data.keyword.codeengineshort}} application as defined in your {{site.data.keyword.codeengineshort}} custom domain mapping.

### How do I obtain the CNAME record for the custom domain mapping?
{: #completing-custom-domain-cname}

{{site.data.keyword.codeengineshort}} provides the CNAME target for your custom domain mapping. To obtain the CNAME record, open your defined custom domain mapping and view the Update domain mapping page. Open the Update domain mapping page in one of the following ways:
* From the Domain mappings table, click in the row of your defined custom domain.
* Click the **Actions** icon ![**Actions** icon](../icons/action-menu-icon.svg "Actions") > **Edit** to edit the mapping.

From the Update domain mappings page, you can obtain the `CNAME target` value. For example, the `www.example.com` mapping has the `custom.abcdabcdabc.us-east.codeengine.test.appdomain.cloud` CNAME value, where `abcdabcdabc` is an automatically generated unique identifier and `us-east` is the region of your project.

After you have the CNAME target, you are ready to add the CNAME record entry to the DNS settings of your custom domain. Note that publishing of the CNAME record with the domain registrar can take some time to populate the DNS changes in the internet.

### How can I use {{site.data.keyword.cis_short}} with custom domain mapping?
{: #completing-custom-domain-cis}

You cannot use the CIS TLS encryption mode of End-to-End flexible with {{site.data.keyword.codeengineshort}} custom domain mapping, because this mode uses self-signed certificates that are not allowed. Instead, you can use the default TLS encryption mode of [End-to-End CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed). If you use the CIS TLS mode of End-to-End-flexible, you can switch to use the CIS TLS End-to-End CA signed mode, and obtain a CA signed certificate that is created outside of CIS.

1. Create the TLS/SSL certificate outside of CIS. See [How can I obtain a certificate for my custom domain?](#prepare-custom-domain-cert)
2. [Create the custom domain mapping](#custom-domain-ui) in {{site.data.keyword.codeengineshort}} with the certificate chain and the private key. 
3. [Obtain the CNAME record for the custom domain mapping](#completing-custom-domain-cname).
4. In CIS, update the DNS records to point to your {{site.data.keyword.codeengineshort}} project. In CIS, go to the DNS records page (**Reliability>DNS**) and **Add** the CNAME record. 
5. Change the CIS mode. Go to the TLS security page (**Security>TLS**). Select **End-to-end CA signed** as the TLS mode. 

If you need to register multiple domains and subdomains, such as `example.com` and `www.example.com`, you must repeat the previous steps 2 and 3 for each subdomain. You can consider creating a single certificate that covers more than one domain. 
{: note}

## Testing your custom domain
{: #test-custom-domain}

After the CNAME record updates are published, you can test the application with the custom domain mapping.

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
CE_APP=myapp
CE_DOMAIN=us-east.codeengine.appdomain.cloud
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

## Viewing domain mappings from the console
{: #view-domain-mapping-ui}

You can view a listing of all automatically generated and custom domain mappings for your applications from the console. By default, the table contents are scoped to custom domain mappings. Use the **Type** filter to modify the view.

This view displays information about the expiration of the certificate that is associated with your mapping. When the certificate expires, the application is no longer reachable with the domain mapping, and this condition yields an SSL error. If you have a certificate that is about to expire, [update the custom domain mapping](#update-custom-domain-ui) to use an updated certificate.

This view also displays information about the specific application that is associated with the domain mapping, and the type of the domain mapping. For mappings that are generated by {{site.data.keyword.codeengineshort}}, the type can be `System-public`, `System-private`, or `System-internal`. For custom domain mappings, the type is `Custom`.

1. After your project is in **Active** status, click the name of your project on the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, view a listing of the defined domain mappings for your existing applications. The `Type` indicates whether the mapping is automatically generated or if it is a custom domain mapping.

## Updating a custom domain mapping from the console
{: #update-custom-domain-ui}

When you create a custom domain mapping, the TLS secret is valid until the certificate expires. From the domain mapping page, you can view information about the remaining days until the certificate expires.

Suppose the custom domain mapping for `www.example.com` has a certificate that expires soon. You can update the domain mapping to use an updated certificate or even replace the TLS secret for the mapping. You can also update your domain mapping to point to a different application in your project.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings**.
3. From the Domain mappings page, click the **Actions** icon ![**Actions** icon](../icons/action-menu-icon.svg "Actions") > **Edit** to edit the mapping. Or, you can click in the row of your defined custom domain to update the mapping.
4. From the Update a domain mapping page, you can change the application that is associated with this domain mapping, or you can replace or update the TLS secret for this mapping.
5. Click **Update** to save your changes.

After you update the mapping, you can view the list of domain mappings for the latest changes.

## Deleting domain mappings
{: #delete-custom-domain}

When you delete a domain mapping, you are removing the association of your {{site.data.keyword.codeengineshort}} application with your custom domain mapping within {{site.data.keyword.codeengineshort}}. This action does not delete the associated application or TLS secret.

You can delete only domain mappings of type `Custom`. Domain mappings that are auto generated by {{site.data.keyword.codeengineshort}} cannot be deleted from the **Domain mappings** page.

If you delete an application that is referenced in a domain mapping, this action also deletes any custom domain mapping that is associated with the application.

When you delete a custom domain mapping, if the DNS settings of your domain are still configured, such that the CNAME points to the {{site.data.keyword.codeengineshort}} project, your traffic still is routed to the {{site.data.keyword.codeengineshort}} project. However, the request is answered with a 404 (not found) error message. Ensure that the associated CNAME record for the fully qualified domain name is updated in the DNS settings by the domain registrar.
{: note}

To delete a custom domain mapping, use the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings** to view a listing of defined domain mappings.
3. (optional) Click **Type** to filter the domain mappings by type.
4. From the Domain mappings page, delete the custom domain mapping that you want to remove from your application. Click the **Actions** icon ![**Actions** icon](../icons/action-menu-icon.svg "Actions") > **Delete** to delete the mapping.


