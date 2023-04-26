---

copyright:
  years: 2023, 2023
lastupdated: "2023-04-24"

keywords: troubleshooting for code engine, troubleshooting builds in code engine, tips for builds in code engine, resolution of builds in code engine, builds, python build

subcollection: codeengine

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does my Python app fail to deploy?
{: #ts-build-python}
{: troubleshoot}

When you build a Python app from source, the image builds and is visible in Container Registry. However, the app fails to deploy.  
{: tsSymptoms}

When you build Python from a buildpack, the buildpack does not provide a way to define a start process. By default, it sets the start process to `python`, which starts the correct version's REPL. To run a Python program, the `Procfile` mechanism can be used to override the default start process: `web`.
{: tsCauses}


The following `Procfile` sets the `entrypoint` of the resulting image to `main.py` and must be present in the root of the context directory.
{: tsResolve}


```python
web: python main.py
```
{: codeblock}




