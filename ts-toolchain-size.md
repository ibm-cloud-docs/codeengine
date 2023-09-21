---

copyright:
  years: 2023, 2023
lastupdated: "2023-09-21"

keywords: troubleshooting for code engine, troubleshooting toolchain in code engine, tips for toolchain in code engine, debugging toolchain in code engine, toolchain and code engine

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my toolchain package too large?
{: #ts-toolchain-size}
{: troubleshoot}

When you try to create a toolchain, it fails at the `Containerize` stage.
{: tsSymptoms}

You receive a message that your package is too large. Your message is similar to the following example.

```txt
Unable to upload packaged files. Package is too large. For details on how to ignore certain file patterns from within your source code by using the '.ceignore' file, visit https://cloud.ibm.com/docs/codeengine?topic=codeengine-plan-build#build-plan-repo.
```
{: screen}


When {{site.data.keyword.codeengineshort}} builds source code from a local source, the source is compressed and loaded into {{site.data.keyword.registrylong_notm}}. If the size of the compressed file is more than 100 MB, the package is rejected.
{: tsCauses}

You can resolve this issue by creating a `.ceignore` file for your local directory. To find out what files are being included in your package, enable traces by setting `pipeline-debug` environment property to `1`, run your toolchain again, and then check the log files.
{: tsResolve}
 
 
For more information about setting the `pipeline-debug` environment property, see [Creating a debug log file for your pipeline](/docs/codeengine?topic=codeengine-troubleshoot-toolchain-ce#troubleshoot-toolchain-ce-log).

For more information about creating a `.ceignore` file, see [Prepare your source location](/docs/codeengine?topic=codeengine-plan-build#build-plan-repo).

