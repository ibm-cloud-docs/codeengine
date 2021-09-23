---

copyright:
  years: 2021
lastupdated: "2021-09-17"

keywords: regions for code engine, target region for code engine, endpoints for code engine, api endpoints in code engine, regions, endpoints

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Regions 
{: #regions}

{{site.data.keyword.codeenginefull}} is available in the following regions:
{: shortdesc}

- Asia Pacific Osaka (`jp-osa`) region
- Asia Pacific Tokyo (`jp-tok`) region
- Canada Toronto (`ca-tor`) region
- EU Germany (`eu-de`) region
- EU Great Britain (`eu-gb`) region
- US South (`us-south`) region

You can target a specific region whenever you log in to the {{site.data.keyword.cloud_notm}} CLI or change your current region by using the [`target -r`](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) option.


```
ibmcloud target -r <region>
```
{: pre}

For example, to target the US South region:

```
ibmcloud target -r us-south
```
{: pre}

## {{site.data.keyword.codeengineshort}} endpoints
{: #endpoints}

The following endpoints are available for {{site.data.keyword.codeengineshort}} and can be used with [{{site.data.keyword.codeengineshort}} APIs](https://cloud.ibm.com/apidocs/codeengine).

| Region | Endpoint |
| ---- | -------- |
| Asia Pacific Osaka | `https://jp-osa.codeengine.appdomain.cloud` |
| Asia Pacific Tokyo| `https://jp-tok.codeengine.appdomain.cloud` |
| Canada Toronto| `https://ca-tor.codeengine.appdomain.cloud` |
| EU Germany | `https://eu-de.codeengine.appdomain.cloud` |
| EU Great Britain | `https://eu-gb.codeengine.appdomain.cloud` |
| US South | `https://us-south.codeengine.appdomain.cloud` |
{: caption="{{site.data.keyword.codeengineshort}} endpoints" caption-side="top"}


