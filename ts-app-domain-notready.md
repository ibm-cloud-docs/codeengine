---

copyright:
  years: 2023, 2023
lastupdated: "2023-04-11"

keywords: troubleshooting for code engine, troubleshooting domain mapping in code engine, tips for custom domain mapping in code engine, debugging custom domain mapping in code engine, custom domain mapping and code engine

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why isn't my custom domain mapping ready?
{: #ts-app-domain-notready}
{: troubleshoot}

You created a custom domain mapping for your application, but it never shows a `Ready` state.
{: tsSymptoms}

This state can have multiple reasons.
{: tsCauses}

- When you create a custom domain mapping in {{site.data.keyword.codeengineshort}}, the domain name that you use in the mapping must be unique in the region.
- If you use a wildcard certificate, you can use it only one time per region.
- If your certificate lists multiple domain names, you can use it only one time per region.

To resolve this issue, verify that your custom domain mapping is unique in the region. 
{: tsResolve}

If you use a wildcard certificate or your certificate lists multiple domain names, create a single TLS secret and then reuse this secret when you create your domain mappings. Note that the applications that use this TLS secret must be in the same project. To use your domain mappings across projects that are in the same region, create separate certificates.
  


  
