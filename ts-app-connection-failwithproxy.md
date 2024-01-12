---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-02"

keywords: troubleshooting for code engine, troubleshooting connections in code engine, tips for app connections in code engine, debugging connections in code engine, app connectivity and code engine, app connection fails with proxy

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my app connection fail when using a proxy?
{: #ts-app-connection-failwithproxy}
{: troubleshoot}

Your application connects to another service with a proxy such as [{{site.data.keyword.cis_full_notm}} (CIS)](/docs/cis?topic=cis-getting-started), which is based on CloudFlare. When your app runs, you notice that the connection ends unexpectedly, and you receive an `ERROR_CONNECTION_CLOSED` message. 
{: tsSymptoms}



If you use {{site.data.keyword.cis_short}} or Cloudflare as a proxy for your {{site.data.keyword.codeengineshort}} application, after 100 seconds, if Cloudflare does not detect an HTTP response, the connection is closed and a 524 error is given by the proxy.
{: tsCauses}


To resolve this situation, make sure that your code responds to the proxy within 100 seconds, or increase the timeout value.
{: tsResolve}

For more information about addressing timeout errors in {{site.data.keyword.cis_short}}, see [Troubleshooting 500 class errors](/docs/cis?topic=cis-html-5xx-errors). 

For more information about the Cloudflare timeout error, see [Timeout error 524 for Cloudflare](https://developers.cloudflare.com/support/troubleshooting/cloudflare-errors/troubleshooting-cloudflare-5xx-errors/#error-524-a-timeout-occurred){: external}. 


For more information about troubleshooting other app connection failures, see [Why does my app connection fail](/docs/codeengine?topic=codeengine-ts-app-connection-fail)?




