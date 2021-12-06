---

copyright:
  years: 2021
lastupdated: "2021-12-06"

keywords: monitoring for code engine, performance metrics, monitor, metrics, requests, pods, application, attributes, jobrun, panic mode

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with {{site.data.keyword.codeengineshort}}
{: #manage-security-compliance}

{{site.data.keyword.codeenginefull_notm}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}


With the {{site.data.keyword.compliance_short}}, you can define rules for {{site.data.keyword.codeengineshort}} that can help to standardize resource configuration.



## Governing {{site.data.keyword.codeengineshort}} resource configuration
{: #govern-service_name}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.codeengineshort}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the about the data that you can use to create a rule for {{site.data.keyword.codeengineshort}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| project | location | string_equals  | [Regions for {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-regions) | *Indicates whether the location to the {{site.data.keyword.codeengineshort}} project is allowed. |
{: caption="Table 1. Rule properties for {{site.data.keyword.codeengineshort}}" caption-side="bottom"}

To learn more about config rules, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-governance).

The following example illustrates a rule that only allows {{site.data.keyword.codeengineshort}} projects to be created in the `us-south` and `eu-de` regions. 

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
				"operator": "string_match",
				"value": "us-south"
			},
			{
				"property": "location",
				"operator": "string_match",
				"value": "eu-de"
			}
		]
	}
}
```
{: screen}



