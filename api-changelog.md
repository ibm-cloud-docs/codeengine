---

copyright:
  years: 2022, 2023
lastupdated: "2023-05-30"

keywords: api change log for code engine, api version for code engine, change log for api in code engine, api history for code engine, change log, api version history

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# API change log
{: #api-changelog}

Find a summary of the latest changes, improvements, and updates for the {{site.data.keyword.codeenginefull}} API plug-in. Changes to existing API versions are designed to be compatible with existing client applications. 
{: shortdesc}

## API versioning
{: #api-versioning}

API requests require a version parameter that takes the date in the format `version=YYYY-MM-DD`. Send the version parameter with every API request.

When the API is changed in a way that is not compatible with previous versions, a new minor version is released. To take advantage of the changes in a new version, change the value of the version parameter to the new date. If you're not ready to update to that version, don't change your version date.

### Active version dates
{: #active-version-dates}

The following table shows the service behavior changes for each version date. Switching to a later version date will activate all changes introduced in earlier versions.

| Version date | Summary of changes |
|---|---|
|`2022-Dec-09`| Version 2.0.0 |
|`2021-Mar-31`| Version 1.0.0  |
{: caption="Changes in the IBM Cloud Code Engine API" caption-side="bottom"} 



## 30 May 2023
{: #30-may-2023}

Added support to get status details for a project.
:   - See [Get the status details for a project API](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-status-details){: external}.


## 27 Mar 2023
{: #27-mar-2023}

Added support to provide private and public egress IP addresses for a project.
:   - See [List egress IP addresses for projects API](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-egress-ips){: external}.
:   - See [{{site.data.keyword.codeengineshort}} public and private IP addresses](/docs/codeengine?topic=codeengine-network-addresses).


Improved documentation for create and update of secrets to include the `One of` fields for specific secret formats as part of the `data` field. 
:   - See [Create a secret API](https://cloud.ibm.com/apidocs/codeengine/v2#create-secret){: external}.
:   - See [Update secret API](https://cloud.ibm.com/apidocs/codeengine/v2#replace-secret){: external}.



## 9 Dec 2022
{: #9-dec-2022}

{{site.data.keyword.codeenginefull}} API Version 2.0.0  

API Version 2.0.0 released
:   This version of the API is enhanced to support more {{site.data.keyword.codeengineshort}} resources, and more regions.
    - The API supports the following {{site.data.keyword.codeengineshort}} resources: `projects`, `reclamations`, `apps`, `revisions`, `job`, `job runs`, `builds`, `build runs`, `config maps`, and `secrets`. See [{{site.data.keyword.codeengineshort}} API](https://cloud.ibm.com/apidocs/codeengine){: external}.
    - The API supports more regional endpoints. See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).
  

