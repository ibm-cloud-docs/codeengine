---

copyright:
  years: 2022
lastupdated: "2022-08-22"

keywords: application, deploy app, deploy app multiple regions, multiple regions, custom domain name, domain name, TLS, load-balancer, Cloud Internet Services

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Deploying an app across multiple regions with a custom domain name
{: #deploy-multiple-regions}

Deploying your {{site.data.keyword.codeenginefull}} application across multiple regions can make it resilient to regional failures. Note that this example uses [{{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-getting-started), but you can use alternate providers.
{: shortdesc}

For more information about deploying an app with a custom domain through Cloudflare, see the [Configuring a Custom Domain for Your IBM Cloud Code Engine Application](https://www.ibm.com/cloud/blog/configuring-a-custom-domain-for-your-ibm-cloud-code-engine-application){: external}  blog.
{: tip} 

Before you begin, you must have a custom domain name for your application, such as `example.com`. When you register your domain name with {{site.data.keyword.cis_short}}, you are delegating control of your domain name to {{site.data.keyword.cis_short}}. This domain name is used by your {{site.data.keyword.codeengineshort}} application.

## Step 1: Set up {{site.data.keyword.cis_short}}
{: #deploy-setup-cis}

If you do not have a {{site.data.keyword.cis_short}} instance set up, [provision an instance](https://cloud.ibm.com/catalog/services/internet-services){: external}.

## Step 2: Add your domain name to {{site.data.keyword.cis_short}}
{: #deploy-domain-name}

From the {{site.data.keyword.cis_short}} overview page,

1. Click **Add Domain**. 

2. Connect to your domain by entering your custom domain name.

3. Set up your DNS records by uploading them in BIND format. 

4. Delegate your domain management. 

For more information about adding a domain, see [Getting started with {{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-getting-started).

## Step 3: Deploy your apps in multiple regions
{: #deploy-app-regions}

Deploy your application in multiple regions. You must deploy it in each region that you want to use. For more information about deploying your application, see [Deploying applications](/docs/codeengine?topic=codeengine-application-workloads). Record the URL endpoints for each deployment. To find your endpoint for an app, run 

```txt
ibmcloud ce app get --name NAME
```
{: pre}

## Step 4: Configure the {{site.data.keyword.cis_short}} load-balancer
{: #deploy-config-load-balancer}

After your applications successfully deploy in multiple regions and are in a ready state, configure the {{site.data.keyword.cis_short}} load-balancer for your application global endpoint.

1. Go to the Reliability page in the {{site.data.keyword.cis_short}} console.

2. Select **Origin pools** and click **Create**.

    Name your pool and then add each {{site.data.keyword.codeengineshort}} application endpoint. For example, if your application endpoint for your app that you created in `eu-de` is `custom-app.1a2b3c4d.eu-de.codeengine.appdomain.cloud`, then enter `eude` as your origin name, `custom-app.1a2b3c4d.eu-de.codeengine.appdomain.cloud` as your origin address, and set the weight to `1`. Ensure that this origin is enabled. Click **Add +** to enter additional application endpoints until all the endpoints of the applications that you deployed in Step 3 are added. 
    Click **Save**.

3. Select **Load balancers** and click **Create**.

    Name your load balancer and turn **Enable** and **Proxy** on. Under **Geo Routes**, click **Add route** and add the pool that you created in the previous step. 
    Click **Add**.

4. From **Create a load balancer**, click **Create**.

For more information, see [Configuring a global load balancer](/docs/cis?topic=cis-configure-glb).

## Step 5: Configure the {{site.data.keyword.cis_short}} instance to provide TLS certificate
{: #deploy-cis-tls}

Transport Layer Security (TLS) certificates are used to encrypt traffic between CIS edge servers and your users. You must provide a TLS certificate for the appropriate hostnames for your application. You can choose a {{site.data.keyword.cis_short}}-provided TLS certificate or you can provide your own.

To provide your own TLS certificate,

1. Go to the Security page in the {{site.data.keyword.cis_short}} console.

2. Select **TLS**.

3. Under **Mode**, select **End to End CA Signed**.

4. From **Edge certificates**, click **Upload**.  You can then upload your own certificate or create a certificate with {{site.data.keyword.cis_short}}. Note that your certificate might not be ready for up to 24 hours.

To order a free certificate from {{site.data.keyword.cis_short}},

1. Go to the Security page in the {{site.data.keyword.cis_short}} console.

2. Select **Origin**.

3. Click **Order +**.

4. Provide a Certificate Signing Request (CSR) or select a private key type for {{site.data.keyword.cis_short}} to generate a key and CSR.

5. Specify your certificate hostnames and an expiration date.

6. Click **Order**.

For more information about generating an origin certificate or about installing other types of certificates, see [Ordering an origin certificate](/docs/cis?topic=cis-cis-origin-certificates#cis-origin-certificates-ordering).

## Step 6: Configure and deploy a {{site.data.keyword.cis_short}} Edge Function
{: #deploy-edge-function}

Configure and deploy a {{site.data.keyword.cis_short}} Edge Function to act as a load-balancer for your application instances.

1. Go to the **Edge Function** page in the {{site.data.keyword.cis_short}} console.

2. Select **Action->Create**. 

3. Copy in your JavaScript code that manages the load-balancing logic that you want to implement. Click **Save**.

4. Select **Trigger->Create**. 

5. Create a trigger that maps your application hostname with an action. The value that you specify must match any URL that is used when you access the application. If you include a path component in the URL, such as `users` in `example.com/users`, then you must include `/*` at the end of the value. For example, specify `example.com/*` as your trigger URL. Select the action that you created in the previous step. Click **Save**.

For more information, see [Working with Edge functions](/docs/cis?topic=cis-working-with-edge-functions).

For example, the following action code can be used to fail over across the HTTP endpoints of the applications that you deployed in Step 3.

```javascript
addEventListener('fetch', (event) => {
    const mutable_request = new Request(event.request);
    event.respondWith(redirectAndLog(mutable_request));
});

async function redirectAndLog(request) {
    const response = await redirectOrPass(request);
    return response;
}

async function getSite(request, site) {
    const url = new URL(request.url);
    // let our servers know what origin the request came from
    // https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-Host
    request.headers.set('X-Forwarded-Host', url.hostname);
    request.headers.set('host', site);
    url.hostname = site;
    url.protocol = "https:";
    response = fetch(url.toString(), request);
    console.log('Got getSite Request to ' + site, response);
    return response;
}

async function redirectOrPass(request) {
    const urlObject = new URL(request.url);

    let response = null;

    try {
        console.log('Got MAIN request', request);

    response = await getSite(request, 'custom-app.1a2b3c4d.us-south.codeengine.appdomain.cloud');
    console.log('Got MAIN response', response.status);
    if (!response.ok && !response.redirected) {
        console.log('Got FALLBACK request', response);
        response = await getSite(request, 'custom-app.1a2b3c4d.eu-de.codeengine.appdomain.cloud');
        console.log('Got Inside ', response);
    }
    return response;

    } catch (error) {
        // if no action found, play the regular request
    console.log('Got Error', error);
    return await fetch(request);

    }

}
```
{: codeblock}

Now your applications are highly available and deployed with a custom domain name.


