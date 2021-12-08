---

copyright:
  years: 2021
lastupdated: "2021-12-08"

keywords: monitoring for code engine, performance metrics, monitor, metrics, requests, pods, application, attributes, jobrun, panic mode

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with {{site.data.keyword.codeengineshort}}
{: #manage-security-compliance}

{{site.data.keyword.codeenginefull_notm}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}


With the {{site.data.keyword.compliance_short}}, you can define rules for {{site.data.keyword.codeengineshort}} that can help to standardize resource configuration.

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.codeengineshort}}.
* Define rules for {{site.data.keyword.codeengineshort}} that can help to standardize resource configuration.

## Monitoring security and compliance posture with {{site.data.keyword.codeengineshort}}
{: #monitor-security-compliance}

As a security or compliance focal, you can use the {{site.data.keyword.codeengineshort}} [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identify potential issues as they arise.

All of the goals for {{site.data.keyword.codeengineshort}} are added to the `{{site.data.keyword.cloud_notm}} Best Practices Controls 1.0` profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, see [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started)

### Available goals for {{site.data.keyword.codeengineshort}}
{: #ce-available-goals}

- Check whether {{site.data.keyword.codeenginefull_notm}} projects are located in the regions. 

To review the pre-defined goal parameters for {{site.data.keyword.codeengineshort}}, access the {{site.data.keyword.compliance_full}}. In the {{site.data.keyword.cloud_notm}} console, click the menu icon and select **Security and compliance > Configure > Goals** and navigate to the **Goal parameters** table. Expand the `{{site.data.keyword.cloud_notm}} Services Goals Input Parameters` to review the values for `{{site.data.keyword.codeengineshort}} region`. If needed, you can [customize your region goal](/docs/security-compliance?topic=security-compliance-custom-goals). 
{: important}

## Governing {{site.data.keyword.codeengineshort}} resource configuration
{: #govern-service_name}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.codeengineshort}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.codeengineshort}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| project | location | [Operators]}](/docs/security-compliance?topic=security-compliance-formatting-rules-templates #operators)  | [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions) | *Indicates whether the location to the {{site.data.keyword.codeengineshort}} project is allowed. |
{: caption="Table 1. Rule properties for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

To learn more about config rules, check out [What is a config rule](/docs/security-compliance?topic=security-compliance-what-is-governance).

The following example illustrates a rule that allows {{site.data.keyword.codeengineshort}} projects to be created only in the `us-south` and `eu-de` regions. 

#### Example output

```sh
{
	"target": {
		"service_name": "codeengine",
		"resource_kind": "project",
		"additional_target_attributes": []
	},
	"required_config": {
		"description": "Code Engine Project",
		"or": [
			{
				"property": "location",
				"operator": "string_equals",
				"value": "us-south"
			},
			{
				"property": "location",
				"operator": "string_equals",
				"value": "eu-de"
			}
		]
	}
}
```
{: screen}



