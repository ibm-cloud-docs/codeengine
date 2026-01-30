---

copyright:
  years: 2023, 2026
lastupdated: "2026-01-27"

keywords: troubleshooting for code engine, troubleshooting domain mapping in code engine, tips for custom domain mapping in code engine, debugging custom domain mapping in code engine, custom domain mapping and code engine, application scaling in code engine, scaling http requests in code engine, open ports, Cloudflare, ports, scan, scanning tool

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my port scan show more open ports than expected?
{: #ts-app-toomanyports}
{: troubleshoot}


If you perform a port scan on an endpoint for a {{site.data.keyword.codeengineshort}} component, the result includes more open network ports than expected. 
{: tsSymptoms}

For incoming connections that use HTTP, the transport layer security (TLS) aspects are managed automatically by {{site.data.keyword.codeengineshort}} outside of the application code. In particular, {{site.data.keyword.codeengineshort}} uses {{site.data.keyword.cis_short}} in {{site.data.keyword.cloud_notm}}, which is based on CloudFlare, as the intrusion prevention system (IPS) for DNS and DDOS protection on Layer 4. The TCP/IP connection that is established on the IPS is owned and managed by Cloudflare. 
{: tsCauses}

{{site.data.keyword.codeengineshort}} exposes only ports `443` (HTTPS) and `80` (HTTP) for application endpoints on Layer 3, Layer 4, and Layer 7. As a result, any other ports, which are opened by Cloudflare, are not being used or routed to the application. If your scanning tool reports open ports, other than `443` and `80`, then the scanning tool is scanning the Cloudflare IP and not the {{site.data.keyword.codeengineshort}} application endpoint. 

To resolve this issue, consider blocking your network traffic on ports other than `80` and `443`. For more information, see [Cloudflare documentation](https://developers.cloudflare.com/fundamentals/reference/network-ports/#how-to-block-traffic-on-additional-ports){: external} 
{: tsResolve}

Cloudflare has a large infrastructure and resolves IP addresses depending on the client location to serve traffic worldwide. To learn about IP ranges for Cloudflare, see [Cloudflare documentation - IP ranges](https://www.cloudflare.com/ips/){: external}. 

To learn about immediate DDOS protection for {{site.data.keyword.codeengineshort}} applications, see [DDoS protection](/docs/codeengine?topic=codeengine-secure#secure-ddos). 
