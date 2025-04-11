---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-11"

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

The following table shows the service behavior changes for each version date. Switching to a later version date activates all changes that are introduced in earlier versions.

| Version date | Version number | Summary of changes                                                                                                                                                                        |
|---|---|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`2024-05-13`| Version 2.1.0 | Environment variables defined and set by Code Engine are now split out from user-defined environment variables and are exposed as part of the `computed_env_variables` field in the API.  |
|`2022-12-09`| Version 2.0.0 |                                                                                                                                                                                           |
|`2021-03-31`| Version 1.0.0 |                                                                                                                                                                                           |
{: caption="Changes in the IBM Cloud Code Engine API" caption-side="bottom"}

## 03 April 2025
{: #03-april-2025}

Added support for HMAC auth secrets. Specify to create HMAC auth secrets with the `format` field and specify the details of HMAC auth secrets with the `hmac_auth` field.
:   - See [Create a secret API](https://cloud.ibm.com/apidocs/codeengine/v2#create-secret){: external}.

Added the `run_compute_resource_token_enabled` property for app create, app update, job create, job update, function create, and function update. Use this property to enable or disable Trusted Profiles support for the selected resource.
:   - See [Create an app API](https://cloud.ibm.com/apidocs/codeengine/v2#create-app){: external}.
:   - See [Update an app API](https://cloud.ibm.com/apidocs/codeengine/v2#update-app){: external}.
:   - See [Create a job API](https://cloud.ibm.com/apidocs/codeengine/v2#create-job){: external}.
:   - See [Update a job API](https://cloud.ibm.com/apidocs/codeengine/v2#update-job){: external}.
:   - See [Create a function API](https://cloud.ibm.com/apidocs/codeengine/v2#create-function){: external}.
:   - See [Update a function API](https://cloud.ibm.com/apidocs/codeengine/v2#update-function){: external}.

Replaced nodejs-18 support with nodejs-20
:   - See [List the function runtimes API](https://cloud.ibm.com/apidocs/codeengine/v2#list-function-runtimes){: external}.
:   - See [Create a function API](https://cloud.ibm.com/apidocs/codeengine/v2#create-function){: external}.
:   - See [Update a function API](https://cloud.ibm.com/apidocs/codeengine/v2#update-function){: external}.

## 21 February 2025
{: #21-february-2025}

Added support for `run_build_params` property for build and buildrun.
:   - See [Create a build API](https://cloud.ibm.com/apidocs/codeengine/v2#create-build){: external}.
:   - See [Get a build API](https://cloud.ibm.com/apidocs/codeengine/v2#get-build){: external}.
:   - See [Update a build API](https://cloud.ibm.com/apidocs/codeengine/v2#update-build){: external}.
:   - See [Create a build run API](https://cloud.ibm.com/apidocs/codeengine/v2#create-build-run){: external}.
:   - See [Get a build run API](https://cloud.ibm.com/apidocs/codeengine/v2#get-build-run){: external}.

## 16 January 2025
{: #16-january-2025}

Added jobrun `indices_details` property to the existing jobrun `status_details` property.
:   - See [Get a job run API](https://cloud.ibm.com/apidocs/codeengine/v2#get-job-run){: external}.

## 21 November 2024
{: #21-november-2024}

Added support for allowed outbound destinations in the API.
:   - See [List allowed outbound destinations API](https://cloud.ibm.com/apidocs/codeengine/v2#list-allowed-outbound-destination){: external}.
:   - See [Create an allowed outbound destination API](https://cloud.ibm.com/apidocs/codeengine/v2#create-allowed-outbound-destination){: external}.
:   - See [Get an allowed outbound destination API](https://cloud.ibm.com/apidocs/codeengine/v2#get-allowed-outbound-destination){: external}.
:   - See [Delete an allowed outbound destination API](https://cloud.ibm.com/apidocs/codeengine/v2#delete-allowed-outbound-destination){: external}.
:   - See [Update an allowed outbound destination API](https://cloud.ibm.com/apidocs/codeengine/v2#update-allowed-outbound-destination){: external}.

## 17 May 2024
{: #17-may-2024}

Added support for functions in the API.
:   - See [List function runtimes API](https://cloud.ibm.com/apidocs/codeengine/v2#list-function-runtimes){: external}.
:   - See [List functions API](https://cloud.ibm.com/apidocs/codeengine/v2#list-functions){: external}.
:   - See [Create a function API](https://cloud.ibm.com/apidocs/codeengine/v2#create-function){: external}.
:   - See [Get a function API](https://cloud.ibm.com/apidocs/codeengine/v2#get-function){: external}.
:   - See [Delete a function API](https://cloud.ibm.com/apidocs/codeengine/v2#delete-function){: external}.
:   - See [Update a function API](https://cloud.ibm.com/apidocs/codeengine/v2#update-function){: external}.

## 30 January 2024
{: #30-jan-2024}

Added support for the `build` and `buildrun` properties for jobs.
:   - See [Create a job API](https://cloud.ibm.com/apidocs/codeengine/v2#create-job){: external}.
:   - See [Get a job API](https://cloud.ibm.com/apidocs/codeengine/v2#get-job){: external}.
:   - See [Update a job API](https://cloud.ibm.com/apidocs/codeengine/v2#update-job){: external}.


## 04 January 2024
{: #04-jan-2024}

Added support for the `scale_array_size_variable_override` property for job runs.
:   - See [Create a job run API](https://cloud.ibm.com/apidocs/codeengine/v2#create-job-run){: external}.


## 03 November 2023
{: #03-nov-2023}

Added support for domain mappings in the API. 
:   - See [List domain mappings API](https://cloud.ibm.com/apidocs/codeengine/v2#list-domain-mappings){: external}.
:   - See [Create a domain mapping API](https://cloud.ibm.com/apidocs/codeengine/v2#create-domain-mapping){: external}.
:   - See [Get a domain mapping API](https://cloud.ibm.com/apidocs/codeengine/v2#get-domain-mapping){: external}.
:   - See [Delete a domain mapping API](https://cloud.ibm.com/apidocs/codeengine/v2#delete-domain-mapping){: external}.
:   - See [Update a domain mapping API](https://cloud.ibm.com/apidocs/codeengine/v2#update-domain-mapping){: external}.


## 27 September 2023
{: #27-sep-2023}

Added support for liveness and readiness probes for applications in the API. Set the probes and their properties when you create or update an application with the API.
:   - See [Create an application API](https://cloud.ibm.com/apidocs/codeengine/v2#create-app){: external}.
:   - See [Update an application API](https://cloud.ibm.com/apidocs/codeengine/v2#update-app){: external}.


## 22 June 2023
{: #22-june-2023}

Added support for service binding operations in the API.
:   - See [List bindings API](https://cloud.ibm.com/apidocs/codeengine/v2#list-bindings){: external}.
:   - See [Create a binding API](https://cloud.ibm.com/apidocs/codeengine/v2#create-binding){: external}.
:   - See [Get a binding API](https://cloud.ibm.com/apidocs/codeengine/v2#get-binding){: external}.
:   - See [Delete a binding API](https://cloud.ibm.com/apidocs/codeengine/v2#delete-binding){: external}.

Added support for service access secrets, which are required for service binding operations. Specify to create service access secrets with the `format` field and specify the details of service access secrets with the `service_access` field.
:   - See [Create a secret API](https://cloud.ibm.com/apidocs/codeengine/v2#create-secret){: external}.



## 30 May 2023
{: #30-may-2023}

Added support to get status details for a project.
:   - See [Get the status details for a project API](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-status-details){: external}.

## 27 March 2023
{: #27-mar-2023}

Added support to provide private and public egress IP addresses for a project.
:   - See [List egress IP addresses for projects API](https://cloud.ibm.com/apidocs/codeengine/v2#get-project-egress-ips){: external}.
:   - See [{{site.data.keyword.codeengineshort}} public and private IP addresses](/docs/codeengine?topic=codeengine-network-addresses).


Improved documentation for create and update of secrets to include the `One of` fields for specific secret formats as part of the `data` field. 
:   - See [Create a secret API](https://cloud.ibm.com/apidocs/codeengine/v2#create-secret){: external}.
:   - See [Update secret API](https://cloud.ibm.com/apidocs/codeengine/v2#replace-secret){: external}.


## 9 December 2022
{: #9-dec-2022}

{{site.data.keyword.codeenginefull}} API Version 2.0.0  

API Version 2.0.0 released
:   This version of the API is enhanced to support more {{site.data.keyword.codeengineshort}} resources, and more regions.
    - The API supports the following {{site.data.keyword.codeengineshort}} resources: `projects`, `reclamations`, `apps`, `revisions`, `job`, `job runs`, `builds`, `build runs`, `config maps`, and `secrets`. See [{{site.data.keyword.codeengineshort}} API](https://cloud.ibm.com/apidocs/codeengine){: external}.
    - The API supports more regional endpoints. See [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions).
