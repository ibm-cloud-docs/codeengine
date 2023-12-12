---

copyright:
  years: 2023, 2023
lastupdated: "2023-12-11"

keywords: troubleshooting for code engine builds, dockerfile error, no command specified

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my build from a Dockerfile failing with a `no command specified` error?
{: #ts-build-nocmdspecified}
{: troubleshoot}


I'm building code by using a Dockerfile. However, my build is failing and I receive an error that contains the phrase `no command specified`.
{: tsSymptoms}

Your Dockerfile must include an `Entrypoint` field. 
{: tsCauses}

You can resolve this issue by rewriting your Dockerfile to include an `Entrypoint` field. For more information, see [Dockerfile basics](/docs/codeengine?topic=codeengine-dockerfile#dockerfile-basics).
{: tsResolve}
