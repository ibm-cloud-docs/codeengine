---

copyright:
  years: 2023, 2023
lastupdated: "2023-06-30"

keywords: code engine, function, create function, code engine function, create code engine function

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Functions
{: #functions}

A Function is a stateless code snippet that performs tasks in response to an HTTP request. With IBM Code Engine Functions, you can run your business logic in a scalable and serverless way. IBM Code Engine Functions provide an optimized runtime environment to support low latency and rapid scale-out scenarios. Your Function code can be written in in Node.js or Python, which are optimized to run in IBM Code Engine Functions. In addition, your Function code can be written for any OpenWhisk compatible runtime environment or a custom runtime image. 
{: shortdesc}

Before you begin

- If you want to use the {{site.data.keyword.codeengineshort}} console, go to [{{site.data.keyword.codeengineshort}} overview](https://cloud.ibm.com/codeengine/overview){: external}. 
- If you want to use the CLI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- Plan and choose your approach for making your code run as a {{site.data.keyword.codeengineshort}} Function component.

## Function limitations
{: #fun-limitations1}

- Supported in Washington, D.C. (`us-east`), Frankfurt (`eu-de`), and Sydney (`au-syd`) regions only.
- No support for subscribing to event producers.
- No support for custom domains.
- No support for limiting the visibility of your function.
- No support for Terraform.

You can find more information about working with Functions in the following topics.

- [Get an overview of Functions](/docs/codeengine?topic=codeengine-cefunctions).
- [Take a tutorial](/docs/codeengine?topic=codeengine-fun-tutorial).
- [Dive deeper into Functions](/docs/codeengine?topic=codeengine-fun-work).
- [Learn about migrating your functions from Cloud Functions to Code Engine Functions](/docs/codeengine?topic=codeengine-fun-migrate).



