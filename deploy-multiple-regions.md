---

copyright:
  years: 2023
lastupdated: "2023-04-19"

keywords: application, deploy app, deploy app multiple regions, multiple regions, custom domain name, domain name, TLS, load-balancer, Cloud Internet Services

subcollection: codeengine

content-type: tutorial
services: codeengine, cis
account-plan: pay-as-you-go
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}

# Configuring a highly available application
{: #deploy-multiple-regions}
{: toc-content-type="tutorial"}
{: toc-services="codeengine, cis"}
{: toc-completion-time="30m"}

You can deploy your {{site.data.keyword.codeenginefull}} application across multiple regions to make it resilient to regional failures. Note that this example uses [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-getting-started), but you can use alternate providers. This example also uses a custom domain.
{: shortdesc}

## Prerequisites
{: #deploy-setup-cis-prereq}

- You must have a custom domain name for your application, such as `example.com`. This domain name is used by your {{site.data.keyword.codeengineshort}} application.
- Set up an instance of [{{site.data.keyword.cis_short}}](https://cloud.ibm.com/catalog/services/internet-services){: external}.
- [Add your domain name to {{site.data.keyword.cis_short}}](/docs/cis?topic=cis-getting-started#add-configure-your-domain). When you register your domain name with {{site.data.keyword.cis_short}}, you are delegating control of your domain name to {{site.data.keyword.cis_short}}. Note that this step can take a while to complete. 


## Create projects in different regions
{: #deploy-project-regions}
{: step}

Create a {{site.data.keyword.codeengineshort}} project in three different regions. You can use a common naming pattern and a shared tag.

For example, create a project called `global-app-project` in the `au-syd`, `eu-de`, and `br-sao` regions with either the CLI or from the console.

| Name | Status | Tag | Location | Resource group | Created |
| --- | --- | --- | --- | --- | --- |
| `global-app-project` | Ready | `global-app` | Sydney (`au-syd`) | default |  |
| `global-app-project` | Ready | `global-app` | Frankfurt (`eu-de`) | default | 2 min |
| `global-app-project` | Ready | `global-app` | Sao Paulo (`br-sao`) | default | 3 min |
{: caption="Table 1. Projects in multiple regions" caption-side="bottom"}

For more information, see [Managing projects](/docs/codeengine?topic=codeengine-manage-project).

## Deploy your apps in multiple regions
{: #deploy-app-regions}
{: step}

Now that your projects are created in multiple regions, deploy your application in each project. 

For example, deploy the `codeengine/helloworld` app.

1. From the [{{site.data.keyword.codeengineshort}} projects](https://cloud.ibm.com/codeengine/projects){: external} page, click the name of one of the projects that you created.
2. Click **Create application**.    
3. Configure your app with the following settings.
    1. Name your application `global-app`.
    2. Select **Container image** to reference a container image for your app.
    3. Enter `icr.io/codeengine/helloworld` for your image reference.
    4. Under **Runtime settings**, set your minimum number of instances to 1. By setting your minimum number of instances to 1, you can enable health checks from your CIS instance to monitor the availability of pools so that traffic can be routed to the healthy ones.
    5. Leave the rest of the options at the default settings and click **Create**.

4. Repeat these steps to create the application in each project.

For more information about deploying your application, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads).


## Generate a certificate for your custom domain
{: #custom-domain-cert}
{: step}

In an enterprise environment, work with your corporate domain administrator to obtain the necessary certificates. However, if the custom domain is within your control and you want quickly create a certificate that is not self-certified, then you can optionally use the [Let's Encrypt](https://letsencrypt.org/){: external} service and [Certbot](https://certbot.eff.org/){: external} to obtain a certificate. 

1. Install [Certbot](https://certbot.eff.org/){: external}. Certbot is a client for the [Automatic Certificate Management Environment (ACME)](https://letsencrypt.org/2019/03/11/acme-protocol-ietf-standard.html#/){: external} protocol for automating interactions between a CA and a server. The Let's Encrypt service uses this client to verify domain ownership and issue certificates. From the [Certbot Instructions page](https://certbot.eff.org/instructions){: external}, select `Other` as the software and select the operating system for your workstation to obtain the applicable information to install the Certbot command line.
2. Run the following command to create your certificate. This example command creates a certificate for the `example.com` and `www.example.com` custom domains. Be sure to update the command for your own custom domain.

    ```txt
    certbot certonly --manual --preferred-challenges dns --email webmaster@example.com --server https://acme-v02.api.letsencrypt.org/directory --agree-tos --domain example.com --domain www.example.com
    ```
    {: pre}

3. To verify that you own the domain, set a `TXT` record with your domain registrar for the domains that you requested in the previous step with values that were provided with the Certbot tool output; for example, `_acme_challenge.example.com` and `_acme_challenge.ww.example.com`. After you set the `TXT` record, continue with the Certbot command.
4. Certbot retrieves the certificate that is signed by Let's Encrypt. The location where the certificate is stored is provided by the Certbot output. Find the `fullchain.pem` and `privkey.pem` files.

## Create a TLS secret
{: #create-tls-secret}
{: step}

Create a TLS secret to store your certificate in {{site.data.keyword.codeengineshort}}.

1. From the [{{site.data.keyword.codeengineshort}} projects](https://cloud.ibm.com/codeengine/projects){: external} page, click the name of one of the projects that you created.
2. Select **Secrets and configmaps**.
3. Click **Create**.
4. Click **TLS secret**.
5. Enter `global-tls` as the name.
6. Copy the content of the `fullchain.pem` file into the **Certificate chain** field.
7. Copy the content of the `privkey.pem` file into the **Private key** field.
8. Click **Create**.
9. Repeat these steps to create a TLS secret in each project that you created earlier.

For more information, see [Working with secrets](/docs/codeengine?topic=codeengine-secret).

## Configure the custom domain mappings
{: #config-app-domain}
{: step}

After your apps are deployed, configure a custom domain mapping for them.

1. From the [{{site.data.keyword.codeengineshort}} projects](https://cloud.ibm.com/codeengine/projects){: external} page, click the name of one of the projects that you created.
2. Select **Applications**.
3. Select your `global-app` application.
4. Select **Domain mappings**.
5. Select **Public** for your visibility.
6. Click **Create** to create a custom domain mapping.
7. Click **Select** to choose an existing TLS secret and select `global-tls`.
8. Enter your fully qualified domain name; for example, `www.example.com`.
9. Note the `CNAME` target value. You need this value to set up routing for your domain in CIS.
10. Verify that the app name is `global-app`.
11. Click **Create**.
12. Repeat these steps to create a custom domain mapping for each application that you created. 

## Configure a health check
{: #config-health-check}
{: step}

When you created your applications, you set the **Minimum number of instances** to 1. Because there is always an instance of your app running in each region, you can set up a health check from your CIS instance to monitor the availability of pools. By setting up a health check, traffic is always routed to a running instance, making your app highly available. 

1. From your CIS instance, navigate to **Reliability > Global load balancers > Health checks**.
2. Click **Create**.
3. Name your health check the same as your application name: `global-app`.
4. Set the **Monitor type** to `HTTPS` and the **Port** to `443`.
5. Accept the defaults for the rest of the options. Note that if you are using an app other than `codeengine/helloworld` app, adjust any options that your app requires.
6. Click **Create**. 

For more information, see [Setting up health checks](/docs/cis?topic=cis-glb-features-healthchecks).

## Configure the {{site.data.keyword.cis_short}} load-balancer
{: #=config-load-balancer}
{: step}

After your custom domain mappings are in a `Ready` state, configure the {{site.data.keyword.cis_short}} load-balancer for your application global endpoint. For more information, see [Configuring a global load balancer](/docs/cis?topic=cis-configure-glb).

1. Go to the Reliability page in the {{site.data.keyword.cis_short}} console.

2. Select **Origin pools** and click **Create**.

    1. Name your pool `global-app-au-syd`.
    2. Set the **Origin address** to the CNAME target of your domain name mapping.
    3. Set the Host header to your domain name.
    4. From the **Health check**, select **Existing health check** and then select `global-app`.
    5. Click **Save**.
    6. Repeat these steps for each region that contains your deployed app. Change the name to reflect the region that you are targeting. For example, `global-app-de-eu` and `global-app-br-sao`.

3. Select **Load balancers** and click **Create**.

    1. Name your load balancer. Note that this name appears in your custom domain URL. For example, if your custom domain is `global-app.example.com` and you name your load balancer `global-app`, your URL is `global-app.example.com`. 
    2. Set **Traffic steering** to `Geo`.
    3. Add your geo routes. You can choose to create a route for all CIS regions or only some of the regions.
        - If you create a route for all CIS regions, then in each route that you create, add all the origin pools that you created earlier. Sort them so that a region that contains your running app and is closest to the region route that you are configuring. For example, if you created apps in `au-syd`, `eu-de`, and `br-sao`, then for `Oceana`, put `au-syd` first. For Eastern and Western Europe, put `de-eu` first. And for North and South America, put `br-sao` first.
        - If you create a route for only some CIS regions, add a route for the **Default** region. This route is the fallback to use when a specified region is not available.
    4.  Click **Create** to create the load balancer.

## Verify that your app is available
{: #verify-app-domain}
{: step}

Open a browser and enter your load balancer name plus your custom domain name; for example, `www.global-app.example.com`

Now your applications are highly available.


## Cleaning up your tutorial
{: #clean-up}
{: step}

1. Delete the global load balancers and origin pools from CIS.
2. Delete your DNS records from CIS. For more information, see [Deleting DNS records](/docs/cis?topic=cis-set-up-your-dns-for-cis#deleting-dns-records).
3. Delete each project that you created. When you delete a project, all the components contained in that project are also deleted. For more information, see [Delete a project](/docs/codeengine?topic=codeengine-manage-project#delete-project).

Note that your custom domain is not deleted, but is no longer associated with the application that you created. 
