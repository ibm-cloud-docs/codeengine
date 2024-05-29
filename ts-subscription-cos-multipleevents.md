---

copyright:
  years: 2024
lastupdated: "2024-05-29"

keywords: troubleshooting for code engine subscriptions, subscriptions, tips for subscriptions, ping, object storage

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# When I create a single file in my {{site.data.keyword.cos_short}} bucket, why do I get multiple events?
{: #ts-cossub-multipleevents}
{: troubleshoot}

When you create a file as an object in {{site.data.keyword.cos_short}}, it can involve multiple {{site.data.keyword.codeengineshort}} events for this one file, which creates multiple HTTP requests or multiple job invocations for the same file.
{: tsSymptoms}

Depending on your method of uploading files to {{site.data.keyword.cos_short}} (such as using `s3fs` or similar functions), {{site.data.keyword.cos_short}} creates an {{site.data.keyword.cos_short}} object that represents a file using multiple steps. For example, setting a creation date includes one creation step followed by multiple update steps.
{: tsCauses}

Since {{site.data.keyword.cos_short}} notifies {{site.data.keyword.codeengineshort}} for each create and update request, there is no possibility for {{site.data.keyword.codeengineshort}} to filter out the additional events. However, you can use another way to import the files into {{site.data.keyword.cos_short}}; for example, use the {{site.data.keyword.cos_short}} API directly instead of using a file system layer (such as `s3fs`).
{: tsResolve}
