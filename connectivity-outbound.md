---

copyright:
  years: 2025
lastupdated: "2025-08-11"

keywords: connectivity, outbound connections, outbound connectivity

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with outbound connectivity in {{site.data.keyword.codeengineshort}}
{: #connectivity-outbound}

The {{site.data.keyword.codeenginefull}} outbound connections feature supports defining reachable endpoints for your {{site.data.keyword.codeengineshort}} projects by using allowed destination IP address ranges for outbound connections in CIDR notation. The allowed destinations ensure that outbound traffic is restricted to addresses you define as safe. Therefore, you prevent unwanted access to the internet, and enhance compliance and security.
{: shortdesc}

CIDR range specifications do not affect project-internal communication, private path connections, or private service connections, all of which are always allowed destinations. In consequence, restricting outbound traffic based on CIDR ranges does not prevent applications within your Code Engine project from communicating with each other, or communicating with a connected private path service, or with a private endpoint of an IBM Cloud Service API.
{: note}

Your use case can determine your outbound connection specifications. Typical use cases are as follows:
* Specifying no rules (that is, no allowed IP addresses), if {{site.data.keyword.codeengineshort}} applications within a project are not supposed to reach any external endpoints.

* Specifying a single allowed destination IP address range (`0.0.0.0/0`) to allow all possible endpoints. By default, there is a rule, named **allow-all**, set with an IP range of 0.0.0.0/0.

* Specifying a rule with an allowed destination IP address range that allows the workload within your {{site.data.keyword.codeengineshort}} project to reach only your specified range of endpoints (for example, to your on-premises data center).

You can create outbound connections by using the console or the CLI.

## Private Service Connections
{: #private-service-connections}

Connecting to private endpoints of a set of common IBM Cloud platform services is enabled as part the allowed outbound destinations of all {{site.data.keyword.codeengineshort}} projects. The set of enabled platform services varies by region as detailed in the following table.

| Platform service | Private endpoint available in regions |
| --- | --- |
| Global Search ([Endpoint URL](https://cloud.ibm.com/apidocs/search#endpoint-url)) and Global Tagging ([Endpoint URL](https://cloud.ibm.com/apidocs/tagging#endpoint-url)) | `au-syd`, `br-sao`, `ca-tor`, `eu-de`, `eu-es`, `eu-gb`, `jp-osa`, `jp-tok`, `us-east`, `us-south` |
| Global Catalog ([Endpoint URL](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#endpoint-url)) | `au-syd`, `br-sao`, `eu-de`, `jp-osa`, `us-east`, `us-south` |
| Account Management  ([Endpoint URL](https://private.accounts.cloud.ibm.com)) | `eu-de`, `us-east`, `us-south` |
| Usage Metering ([Endpoint URL](https://cloud.ibm.com/apidocs/usage-metering#endpoint)) | `eu-de`, `us-east`, `us-south` |
| Enterprise Management ([Endpoint URL](https://cloud.ibm.com/apidocs/enterprise-apis/enterprise#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
| Resource Controller ([Endpoint URL](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
| User Management ([Endpoint URL](https://cloud.ibm.com/apidocs/user-management#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
{: caption="Platform services with enabled private endpoints per region" caption-side="bottom"}

## Managing allowed destination IP address ranges by using the console
{: #working-with-allowed-destination-ui}
{: ui}

### Adding an allowed destination IP address range for outbound connectivity
{: #add-allowed-destination-ui}
{: ui}

You can create allowed destination IP address ranges to limit where your workload can connect to over an external network.

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** to see a list of existing allowed destination IP address ranges.
2. Click **Add** to create an allowed destination IP address range.
3. Provide a name.
4. Provide an IP address range in CIDR notation.
5. Confirm your configuration.

### Updating an allowed destination IP address range for outbound connectivity
{: #update-allowed-destination-ui}
{: ui}

You can change allowed destination IP address ranges to disallow your workload to connect to unintended endpoints (for example, to connect to public internet).

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** to see a list of existing allowed destination IP address ranges.
2. Click the row with the allowed destination IP address range that you want to edit.
3. Provide the updated IP address range and save your changes.

When you update the outbound connectivity rules, note:
* Allowed destination IP address ranges do not conflict; they are additive. When you define multiple ranges, the allowed destinations create a union of all specified ranges so that the order of adding ranges does not affect the resulting allowed destinations. If you add a second range that is already covered by an existing range, the system rejects the creation as it is redundant.

* Specifying the IP address range `0.0.0.0/0` removes all existing rules and opens up full connectivity.

* After you restrict outbound connectivity rules, it can take some time for your workload to pick up the rules. For example, if the HTTP client that is used in your code establishes a connection before you update the outbound connectivity rule, it can open a connection to that endpoint. To make sure that your outbound connectivity rules are applied immediately, reset all connections. You can reset by redeploying your workloads or by handling such situations in your code.

* After you restrict outbound connections from your {{site.data.keyword.codeengineshort}} project, you can see unintended side effects such as failing build runs because no external requests can be made.

### Deleting an allowed destination IP address range for outbound connectivity
{: #delete-allowed-destination-ui}
{: ui}

You can delete previously defined allowed destination IP address ranges, if you no longer want them defined for outbound connectivity.

Deleting allowed destination IP address ranges blocks outbound traffic for {{site.data.keyword.codeengineshort}} applications, function, and jobs within a project.
{: remember}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** to see a list of existing allowed destination IP address ranges.
2. Go to the row with the allowed destination IP address range that you want to remove and click the delete (trash can) icon.
3. Confirm the deletion when prompted.

## Managing allowed destination IP address ranges by using the CLI
{: #working-with-allowed-destination-cli}
{: cli}

To work with allowed destination IP address ranges by using CLI commands, log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external} and [select the {{site.data.keyword.codeengineshort}} account and resource group](/docs/codeengine?topic=codeengine-install-cli).

For {{site.data.keyword.codeengineshort}} connectivity CLI commands, you can specify
the `--cidr-name` and `--cidr` values. Follow these CIDR guidelines:
* Do not use an IP range from the [reserved IP ranges](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#vrf-overview).
* Do not use duplicate `--cidr-name` and `--cidr` values.
* Do not use an unsupported CIDR name.
* Do not use an unsupported IP address range. Follow CIDR notation.

### Adding an allowed destination IP address range for outbound connectivity
{: #add-allowed-destination-cli}
{: cli}

You can create allowed destination IP address ranges to limit where your workload can connect to over an external network.

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Create an allowed destination IP address range by specifying the `--cidr-name` and `--cidr` options. Provide a valid name and IP address. Refer to these examples:

    ```txt
    ibmcloud ce connectivity outbound create --cidr-name mycidr1 --cidr 192.68.5.0/24

    ibmcloud ce connectivity outbound create --cidr-name mycidr2-allow-all --cidr 0.0.0.0/0

    ibmcloud ce connectivity outbound create --cidr-name mycidr2-allow-all --cidr 0.0.0.0/0 --force
    ```
    {: pre}

### Showing existing allowed destination IP address ranges for outbound connectivity
{: #show-allowed-destination-cli}
{: cli}

To show a specific allowed destination IP address range, specify the CIDR name. For example:

 ```txt
ibmcloud ce connectivity outbound get --cidr-name mycidr
```
{: pre}

To show all allowed destination IP address ranges, run:

```txt
ibmcloud ce connectivity outbound list
```
{: pre}

### Updating an allowed destination IP address range for outbound connectivity
{: #update-allowed-destination-cli}
{: cli}

You can change allowed destination IP address ranges to disallow your workload to connect to unintended endpoints (for example, to connect to the public internet).

Update an allowed destination IP address range by specifying the `--cidr-name` and `--cidr` options. Provide a valid name and IP address. Refer to these examples:

```txt
ibmcloud ce connectivity outbound update --cidr-name mycidr1 --cidr 192.68.5.0/24

ibmcloud ce connectivity outbound update --cidr-name mycidr2-allow-all --cidr 0.0.0.0/0
Are you sure you want to update an allowed destination IP address range with '0.0.0.0/0'?, It will remove all other entries [y/N]>

ibmcloud ce connectivity outbound update --cidr-name mycidr2-allow-all --cidr 0.0.0.0/0 --force
```
{: pre}

When you update the outbound connectivity rules, note:
* Allowed destination IP address ranges do not conflict; they are additive. When you define multiple ranges, the allowed destinations create a union of all specified ranges so that the order of adding ranges does not affect the resulting allowed destinations. If you add a second range that is already covered by an existing range, the system rejects the creation as it is redundant.

* Specifying the IP address range `0.0.0.0/0` removes all existing rules and opens up full connectivity.

* Even after you restrict outbound connectivity rules, it can take some time for your workload to pick up the rules. For example, if the HTTP client that is used in your code establishes a connection before you update the outbound connectivity rule, it can open a connection to that endpoint. To make sure that your outbound connectivity rules are applied immediately, reset all connections. You can reset by redeploying your workloads or by handling such situations in your code.

* After you restrict outbound connections from your {{site.data.keyword.codeengineshort}} project, you can see unintended side effects such as failing build runs because no external requests can be made.

### Deleting an allowed destination IP address range for outbound connectivity
{: #delete-allowed-destination-cli}
{: cli}

You can delete previously defined allowed destination IP address ranges, if you no longer want them defined for outbound connectivity.

Deleting allowed destination IP address ranges blocks outbound traffic for {{site.data.keyword.codeengineshort}} applications, function, and jobs within a project.
{: remember}

To delete an allowed destination IP address range with confirmation, specify the CIDR name. For example:

```txt
ibmcloud ce connectivity outbound delete --cidr-name mycidr
```
{: pre}

To delete an allowed destination IP address range forcefully (that is, without confirmation), run:

```txt
ibmcloud ce connectivity outbound delete --cidr-name mycidr --force
```
{: pre}
