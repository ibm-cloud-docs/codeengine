---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-03"

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

To create and setup custom domain mappings, you complete these steps:
1. Review the [Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}}](#considerations-custom-domain).
2. [Prepare to add a custom domain mapping](#prepare-custom-domain) (outside of {{site.data.keyword.codeengineshort}}).
3. [Configure custom domain mappings](#custom-domain-ui) (from the {{site.data.keyword.codeengineshort}} console).
4. [Complete the custom domain configuration with your domain registrar](#completing-custom-domain-registrar) (outside of {{site.data.keyword.codeengineshort}}).

After the custom domain mapping is created, you can [test](#test-custom-domain), [update](#update-custom-domain-ui), [view](#view-domain-mapping-ui), or [delete](#delete-custom-domain) your custom domain mappings. 

## Considerations before you use custom domain mappings in {{site.data.keyword.codeengineshort}} 
{: #considerations-custom-domain}

Before you implement custom domain mappings in {{site.data.keyword.codeengineshort}}, be aware of the following considerations:

* {{site.data.keyword.codeengineshort}} supports custom domain mappings for domains that are protected with a SSL/TLS certificate, which is signed by a public, trusted certificate authority (CA).
* You can define custom domain mappings that point to public domain names.
* If your domain name can be resolved only by a nonpublic domain name system (DNS), you must provide a certificate that lists the domain name and is signed by a public, trusted CA. 
* You cannot use self-signed certificates. 
* You cannot use certificates that are signed by an untrusted or a nonpublic enterprise CA. 

## Preparing to add a custom domain mapping
{: #prepare-custom-domain}

When you want to use a custom domain mapping with {{site.data.keyword.codeengineshort}} application, you must take the following actions outside of {{site.data.keyword.codeengineshort}} before you can create the custom domain mapping.

1. From a domain registrar, obtain your custom domain; for example, `www.example.com`.
2. From your certificate authority (CA), you must obtain a signed SSL/TLS *certificate* for your custom domain from your certificate authority (CA). This certificate is a type of digital certificate that is used to establish communication privacy between a server and a client. Certificates are issued by certificate authorities and contain information that is used to create trusted and secure connections between endpoints. You must also obtain a matching *private key* for the TLS certificate.

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
4. From the Create a domain mapping page, specify the TLS secret to use with this domain mapping. 

    To create a new TLS secret,
      1. Click **Create**.
      2. Add the TLS certificate, including all intermediate certificates, which are associated with your domain.
      3. Add the private key that corresponds to your certificate.

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
3. From the Domain mappings page, view a listing of the defined domain mappings for your existing applications. The `Type` indicates whether the mapping is automatically generated or if it is a custom domain mapping. Notice that the visibility of the endpoint URL is provided. Information about the application endpoints is also available from the **Domain mappings** tab on the specific application page.

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

You can delete only domain mappings of type `Custom`. Domain mappings that are auto-generated by {{site.data.keyword.codeengineshort}} cannot be deleted from the **Domain mappings** page.

If you delete an application that is referenced in a domain mapping, this action also deletes any custom domain mapping that is associated with the application.

When you delete a custom domain mapping, if the DNS settings of your domain are still configured, such that the CNAME points to the {{site.data.keyword.codeengineshort}} project, your traffic still is routed to the {{site.data.keyword.codeengineshort}} project. However, the request is answered with a 404 (not found) error message. Ensure that the associated CNAME record for the fully qualified domain name is updated in the DNS settings by the domain registrar.
{: note}

To delete a custom domain mapping, use the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Domain mappings** to view a listing of defined domain mappings.
3. (optional) Click **Type** to filter the domain mappings by type.
4. From the Domain mappings page, delete the custom domain mapping that you want to remove from your application. Click the **Actions** icon ![**Actions** icon](../icons/action-menu-icon.svg "Actions") > **Delete** to delete the mapping. 







