---

copyright:
  years: 2025
lastupdated: "2025-12-12"

keywords: connectivity, outbound connections, outbound connectivity, private path

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with outbound connectivity in {{site.data.keyword.codeengineshort}}
{: #connectivity-outbound}

The {{site.data.keyword.codeenginefull}} outbound connections feature supports defining reachable endpoints for your {{site.data.keyword.codeengineshort}} projects.
* Use allowed destination IP address ranges for outbound connections in CIDR notation. The allowed destinations ensure that outbound traffic is restricted to addresses you define as safe. Therefore, you prevent unwanted access to the internet, and enhance compliance and security.
* Connect your {{site.data.keyword.codeengineshort}} project with {{site.data.keyword.cloud_notm}} VPC [Private Path services](/docs/vpc?topic=vpc-private-path-service-about) by using the {{site.data.keyword.codeengineshort}} console or CLI. Private Path allows connections between an IBM Cloud service like {{site.data.keyword.codeengineshort}} and your VPC without compromising security or putting your VPC at risk. See [Enabling an IBM Cloud service to connect to a provider's VPC](/docs/vpc?topic=vpc-private-path-service-intro#pps-use-case-4).
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

Connecting to private endpoints of a set of common IBM Cloud platform services is enabled as part of the allowed outbound destinations of all {{site.data.keyword.codeengineshort}} projects. The set of enabled platform services varies by region as detailed in the following table.

| Platform service | Private endpoint available in regions |
| --- | --- |
| Global Search ([Endpoint URL](https://cloud.ibm.com/apidocs/search#endpoint-url)) and Global Tagging ([Endpoint URL](https://cloud.ibm.com/apidocs/tagging#endpoint-url)) | `au-syd`, `br-sao`, `ca-tor`, `eu-de`, `eu-es`, `eu-gb`, `jp-osa`, `jp-tok`, `us-east`, `us-south` |
| Global Catalog ([Endpoint URL](https://cloud.ibm.com/apidocs/resource-catalog/global-catalog#endpoint-url)) | `au-syd`, `br-sao`, `eu-de`, `jp-osa`, `us-east`, `us-south` |
| Account Management  (Endpoint URL `(https://private.accounts.cloud.ibm.com)`) | `eu-de`, `us-east`, `us-south` |
| Usage Metering ([Endpoint URL](https://cloud.ibm.com/apidocs/usage-metering#endpoint)) | `eu-de`, `us-east`, `us-south` |
| Enterprise Management ([Endpoint URL](https://cloud.ibm.com/apidocs/enterprise-apis/enterprise#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
| Resource Controller ([Endpoint URL](https://cloud.ibm.com/apidocs/resource-controller/resource-controller#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
| User Management ([Endpoint URL](https://cloud.ibm.com/apidocs/user-management#endpoint-url)) | `eu-de`, `us-east`, `us-south` |
{: caption="Platform services with enabled private endpoints per region" caption-side="bottom"}

## Managing allowed outbound destinations by using the console
{: #working-with-allowed-destination-ui}
{: ui}

### Adding an allowed destination IP address range for outbound connectivity
{: #add-allowed-destination-ui}
{: ui}

You can create allowed destination IP address ranges to limit where your workload can connect to over an external network.

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** > **CIDR ranges** tab to see a list of existing allowed destination IP address ranges.
2. Click **Add** to create an allowed destination IP address range.
3. Provide a name.
4. Provide an IP address range in CIDR notation.
5. Confirm your configuration.

### Adding a private path connection for outbound connectivity
{: #add-allowed-destination-pps-ui}
{: ui}

You can establish a Private Path connection between your {{site.data.keyword.codeengineshort}} project and your VPC.

This diagram illustrates how to establish a Private Path service with connections to the VPE gateway of a {{site.data.keyword.codeengineshort}} application and your VPC. First, the {{site.data.keyword.codeengineshort}} application connects to the VPE gateway within the {{site.data.keyword.codeengineshort}}'s VPC. Then, the VPE gateway connects to the Private Path NLB in the provider's VPC. In turn, the Private Path NLB connects to the provider's application. The provider's application then responds to the request. This Private Path service activity is completely contained in a single region (e.g. `us-south`) in an {{site.data.keyword.cloud_notm}} private network.

![Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network.](images/private_path_detailed_4.svg "Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network."){: caption="Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network." caption-side="bottom"}

Once the connection to VPC is created, the Private Path service owner will receive a connection request. The owner can review, permit or deny this connection request. Use the consumer `Code Engine account ID` and `VPE gateway creation timestamp` displayed in the private path connection details view to identify the respective connection request within the Private Path service.
{: note}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** > **Private Path connections** tab to see a list of existing private path connections.
2. Click **Add** to create a private path connection.
3. Provide a name.
4. You specify the Private Path service instance to connect to by name or by CRN.
   1. By **Name**, select the Private Path service instance from the drop-down list.
   2. By **CRN**, provide the Private Path service instance CRN.
5. Confirm your configuration.

### Updating an allowed destination IP address range for outbound connectivity
{: #update-allowed-destination-ui}
{: ui}

You can change allowed destination IP address ranges to disallow your workload to connect to unintended endpoints (for example, to connect to public internet).

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** > **CIDR ranges** tab to see a list of existing allowed destination IP address ranges.
2. Click the row with the allowed destination IP address range that you want to edit.
3. Provide the updated IP address range and save your changes.

When you update the outbound connectivity rules, note:
* Allowed destination IP address ranges do not conflict; they are additive. When you define multiple ranges, the allowed destinations create a union of all specified ranges so that the order of adding ranges does not affect the resulting allowed destinations. If you add a second range that is already covered by an existing range, the system rejects the creation as it is redundant.

* Specifying the IP address range `0.0.0.0/0` removes all existing rules and opens up full connectivity.

* After you restrict outbound connectivity rules, it can take some time for your workload to pick up the rules. For example, if the HTTP client that is used in your code establishes a connection before you update the outbound connectivity rule, it can open a connection to that endpoint. To make sure that your outbound connectivity rules are applied immediately, reset all connections. You can reset by redeploying your workloads or by handling such situations in your code.

* After you restrict outbound connections from your {{site.data.keyword.codeengineshort}} project, you can see unintended side effects such as failing build runs because no external requests can be made.

### Deleting an allowed outbound destination for outbound connectivity
{: #delete-allowed-destination-ui}
{: ui}

You can delete previously defined allowed outbound destinations, if you no longer want them defined for outbound connectivity.

Deleting allowed destination IP address ranges blocks outbound traffic for {{site.data.keyword.codeengineshort}} applications, function, and jobs within a project.
{: remember}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** > **CIDR ranges** tab to see a list of existing allowed destination IP address ranges, or **Private Path connections** tab to see a list of existing private path connections.
2. Go to the row with the allowed outbound destination that you want to remove and click the delete (trash can) icon.
3. Confirm the deletion when prompted.

## Managing allowed outbound destinations by using the CLI
{: #working-with-allowed-destination-cli}
{: cli}

To work with allowed outbound destinations by using CLI commands, log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external} and [select the {{site.data.keyword.codeengineshort}} account and resource group](/docs/codeengine?topic=codeengine-install-cli).

### Adding an allowed destination IP address range for outbound connectivity
{: #add-allowed-destination-cli}
{: cli}

For {{site.data.keyword.codeengineshort}} connectivity outbound CLI commands, you can specify
the `--name` and `--cidr` values to configure allowed destination IP address ranges. 
Follow these CIDR guidelines:
* Do not use an IP range from the [reserved IP ranges](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#vrf-overview).
* Do not use duplicate `--name` and `--cidr` values.
* Do not use an unsupported CIDR name.
* Do not use an unsupported IP address range. Follow CIDR notation.

You can create allowed destination IP address ranges to limit where your workload can connect to over an external network.

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Create an allowed destination IP address range by specifying the `--name` and `--cidr` options. Provide a valid name and IP address. Refer to these examples:

    ```txt
    ibmcloud ce connectivity outbound create --name mycidr1 --cidr 192.68.5.0/24

    ibmcloud ce connectivity outbound create --name mycidr2-allow-all --cidr 0.0.0.0/0

    ibmcloud ce connectivity outbound create --name mycidr2-allow-all --cidr 0.0.0.0/0 --force
    ```
    {: pre}

### Adding a private path connection for outbound connectivity
{: #add-allowed-destination-pps-cli}
{: cli}

For {{site.data.keyword.codeengineshort}} connectivity outbound CLI commands, you can specify
the `--name`, `--format`, and `--pps-crn` values to establish a Private Path connections between your {{site.data.keyword.codeengineshort}} project and your VPC.

This diagram illustrates how to establish a Private Path service with connections to the VPE gateway of a {{site.data.keyword.codeengineshort}} application and your VPC. First, the {{site.data.keyword.codeengineshort}} application connects to the VPE gateway within the {{site.data.keyword.codeengineshort}}'s VPC. Then, the VPE gateway connects to the Private Path NLB in the provider's VPC. In turn, the Private Path NLB connects to the provider's application. The provider's application then responds to the request. This Private Path service activity is completely contained in a single region (e.g. `us-south`) in an {{site.data.keyword.cloud_notm}} private network.

![Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network.](images/private_path_detailed_4.svg "Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network."){: caption="Use Private Path to connect your {{site.data.keyword.codeengineshort}} project to your VPC over private network." caption-side="bottom"}

Once the connection to VPC is created, the Private Path service owner will receive a connection request. The owner can review, permit or deny this connection request. Use the consumer `Code Engine account ID` and `VPE gateway creation timestamp` details displayed in `ibmcloud ce connectivity outbound get --name OUTBOUND_DESTINATION_NAME` command to identify the respective connection request within the Private Path service.
{: note}

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Create a private path connection for outbound connectivity by specifying the `--name`, `--format`, and `--pps-crn` options. Provide a valid name, format and CRN. Refer to this example:

    ```txt
    ibmcloud ce connectivity outbound create --name my-pps-connection --format pps --pps-crn crn:v1:bluemix:public:is:eu-de:a/abcdefabcdefabcdefabcd1234567890::private-path-service-gateway:r010-2b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f6f
    ```
    {: pre}

### Showing existing allowed destinations for outbound connectivity
{: #show-allowed-destination-cli}
{: cli}

To show a specific allowed outbound destination, specify the name. For example:

```txt
ibmcloud ce connectivity outbound get --name my-allowed-destination
```
{: pre}

To show all allowed outbound destinations, run:

```txt
ibmcloud ce connectivity outbound list
```
{: pre}

To show selected formats of allowed outbound destinations, run for example:

```txt
ibmcloud ce connectivity outbound list --format cidr,pps

ibmcloud ce connectivity outbound list --format cidr

ibmcloud ce connectivity outbound list --format pps
```
{: pre}

### Updating an allowed destination IP address range for outbound connectivity
{: #update-allowed-destination-cli}
{: cli}

You can change allowed destination IP address ranges to disallow your workload to connect to unintended endpoints (for example, to connect to the public internet).

Update an allowed destination IP address range by specifying the `--name` and `--cidr` options. Provide a valid name and IP address. Refer to these examples:

```txt
ibmcloud ce connectivity outbound update --name mycidr1 --cidr 192.68.5.0/24

ibmcloud ce connectivity outbound update --name mycidr2-allow-all --cidr 0.0.0.0/0
Are you sure you want to update an allowed destination IP address range with '0.0.0.0/0'?, It will remove all other entries [y/N]>

ibmcloud ce connectivity outbound update --name mycidr2-allow-all --cidr 0.0.0.0/0 --force
```
{: pre}

When you update the outbound connectivity rules, note:
* Allowed destination IP address ranges do not conflict; they are additive. When you define multiple ranges, the allowed destinations create a union of all specified ranges so that the order of adding ranges does not affect the resulting allowed destinations. If you add a second range that is already covered by an existing range, the system rejects the creation as it is redundant.

* Specifying the IP address range `0.0.0.0/0` removes all existing rules and opens up full connectivity.

* Even after you restrict outbound connectivity rules, it can take some time for your workload to pick up the rules. For example, if the HTTP client that is used in your code establishes a connection before you update the outbound connectivity rule, it can open a connection to that endpoint. To make sure that your outbound connectivity rules are applied immediately, reset all connections. You can reset by redeploying your workloads or by handling such situations in your code.

* After you restrict outbound connections from your {{site.data.keyword.codeengineshort}} project, you can see unintended side effects such as failing build runs because no external requests can be made.

### Deleting an allowed outbound destination for outbound connectivity
{: #delete-allowed-destination-cli}
{: cli}

You can delete previously defined allowed outbound destinations, if you no longer want them defined for outbound connectivity.

Deleting allowed destination IP address ranges blocks outbound traffic for {{site.data.keyword.codeengineshort}} applications, function, and jobs within a project.
{: remember}

To delete an allowed outbound destination with confirmation, specify the name. For example:

```txt
ibmcloud ce connectivity outbound delete --name my-allowed-destination
```
{: pre}

To delete an allowed outbound destination forcefully (that is, without confirmation), run:

```txt
ibmcloud ce connectivity outbound delete --name my-allowed-destination --force
```
{: pre}
