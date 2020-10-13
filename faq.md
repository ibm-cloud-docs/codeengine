---

copyright:
  years: 2020
lastupdated: "2020-10-13"

keywords: code engine, faq

subcollection: codeengine

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}


# FAQs 
{: #faqs}

Answers to common questions about the {{site.data.keyword.codeenginefull_notm}} service. 
{:shortdesc}


## What is {{site.data.keyword.codeenginefull_notm}}? 
{: #what-is-codeengine}
{: faq}
{: support}

{{site.data.keyword.codeengineshort}} is an open source platform that was developed by IBM. The goal is to extend the capabilities of Kubernetes to help you create modern, source-centric containerized, and serverless apps that run on your Kubernetes cluster.. The platform is designed to address the needs of developers who today must decide what type of app they want to run in the cloud: 12-factor apps, containers, or functions. For more information, see [About {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-about).

## What is a Project? 
{: #what-is-project}
{: faq}
{: support}

A project is a grouping of {{site.data.keyword.codeengineshort}} entities, such as applications, jobs, and builds.  Projects are used to manage resources and provide access to its entities. 

For more information, see [{{site.data.keyword.codeengineshort}} terminology](/docs/codeengine?topic=codeengine-about#terminology).

## What is an Application?  
{: #what-is-app}
{: faq}
{: support}

An application, or app, is a {{site.data.keyword.codeengineshort}} entity that runs your code to serve HTTP requests. Applications are organized and run within a defined [Project](#what-is-project).

Build your code in any language, by using your favorite libraries, dependencies, and tools. When you create your Application, you specify where your code resides. The Application has a URL for incoming requests.  

The number of running instances of an Application are automatically scaled up or down (to zero) based on incoming workload. 

An app contains one or more *revisions* (revision entities). A revision represents an immutable version of the configuration properties of the app. Each update of an app configuration property creates a new revision of the app.

## What is a Job?   
{: #what-is-job}
{: faq}
{: support}

A job runs your code in a {{site.data.keyword.codeengineshort}} service to complete a task. Unlike applications,  jobs are meant to be used for running container images that contain an executable that is designed to run one time and then exit. When you create a job, you can specify workload configuration information that is used each time that the job is run. 

A job runs within a defined [Project](#what-is-project). 

A job can run many instances, which enables work on large volumes of input data in parallel.

 ## Where can I find code samples?   
{: #review-service-terms}
{: faq}
{: support}

You can find samples to help you explore the capabilities of {{site.data.keyword.codeengineshort}}. Visit our [{{site.data.keyword.codeengineshort}} samples repository on GitHub](https://github.com/IBM/CodeEngine){: external}. 

 ## How can I review the {{site.data.keyword.codeengineshort}} service terms?  
{: #review-service-terms}
{: faq}
{: support}

For the latest service level agreement terms, see the [terms of service](/docs/overview/terms-of-use?topic=overview-terms).

 ## How can I give feedback? 
{: #review-service-terms}
{: faq}
{: support}

Your feedback on {{site.data.keyword.codeengineshort}} is important to us and helps us improve. You can provide feedback in multiple ways:
  * Click **Feedback** from any page on the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview){: external} or in the product documentation to provide your comments.  
  * Share feedback through Slack. You can [register](https://cloud.ibm.com/kubernetes/slack){: external} and join the discussion in the [#code-engine channel](https://ibm-cloud-success.slack.com){: external}. 


