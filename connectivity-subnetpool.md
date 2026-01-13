---

copyright:
  years: 2026
lastupdated: "2026-01-09"

keywords: connectivity, subnet pool, fleet

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with subnet pool connectivity in {{site.data.keyword.codeengineshort}}
{: #connectivity-subnetpool}

The {{site.data.keyword.codeenginefull}} subnet pool connections feature supports to manage VPC subnet pool references, including security groups. 
You create a subnet pool to specify the VPC subnets and availability zones where your workload will be processed.
For example, you can create a subnet pool with a single subnet in zone `eu-de-1` or a subnet pool with multiple subnets to span all 3 zones in `eu-de`.
In addition, you can specify the security group that your workload should be attached to.
A subnet pool can be referenced when creating a fleet to specify into which network zone the {{site.data.keyword.codeengineshort}} fleet workers get deployed.
{: shortdesc}

{{site.data.keyword.vpc_full}} (VPC) is a virtual network that is linked to your customer account. It gives you cloud security, with the ability to scale dynamically, by providing fine-grained control over your virtual infrastructure and your network traffic segmentation.
Subnets in your VPC offer private connectivity.
Subnets in your VPC can connect to the public internet through an optional public gateway.
You can keep your VPC and workloads secure by controlling network traffic using security groups.
See [About networking](/docs/vpc?topic=vpc-about-networking-for-vpc) and [Security in your VPC](/docs/vpc?topic=vpc-security-in-your-vpc) for further reading.

You can manage subnet pools by using the console or the CLI.

## Managing subnet pools by using the console
{: #working-with-subnetpools-ui}
{: ui}

### Adding a subnet pool
{: #add-subnetpool-ui}
{: ui}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** and navigate to the **Subnet pools for network placement** section to see a list of existing subnet pools.
2. Click **Create** to create a subnet pool.
3. Provide a name.
4. Select **Specify by name**.
    1. Select the VPC.
    2. Select the VPC subnet you want to specify for network placement
    3. Optional: Select one or more VPC security group to attach to the subnet. If you do not specify any security group, the default security group of the VPC is used.
    4. Click **Add to subnet pool** to add the subnet CRN and optionally its security group CRN to the subnet pool. Repeat this step if the subnet pool should allow network placement to multiple subnets.
5. Confirm your configuration by clicking **Create**.

### Adding a subnet pool by CRN
{: #add-subnetpool-crn-ui}
{: ui}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** and navigate to the **Subnet pools for network placement** section to see a list of existing subnet pools.
2. Click **Create subnet pool** to create a subnet pool.
3. Provide a name.
4. Select **Specify by CRN** and provide a VPC subnet CRN. Optionally, provide a VPC security group CRN. Click **Add security group** if you want to attach more than one security group to the subnet. If you do not specify any security group, the default security group of the VPC is used. Click **Add to subnet pool** to add the subnet CRN and optionally its security group CRN to the subnet pool. Repeat this step if the subnet pool should allow network placement to multiple subnets.
5. Confirm your configuration by clicking **Create**.

### Deleting a subnet pool
{: #delete-subnetpool-ui}
{: ui}

You can delete previously defined subnet pools if you no longer use them.

To run a fleet, you need at least one subnet pool configured within a project.
{: remember}

1. Go to the Connectivity page:
    1. Select your project from the [Projects page in the {{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/projects){: external}.
    2. Click **Project settings** > **Connectivity** and navigate to the **Subnet pools** section to see a list of existing subnet pools.
2. Go to the row with the subnet pool that you want to remove and click the three dots row actions icon. Click **Delete**.
3. Confirm the deletion when prompted.

## Managing subnet pools by using the CLI
{: #working-with-subnetpools-cli}
{: cli}

To work with subnet pools by using CLI commands, log in to your [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/){: external} and [select the {{site.data.keyword.codeengineshort}} account and resource group](/docs/codeengine?topic=codeengine-install-cli).

### Adding a subnet pool
{: #add-subnetpool-cli}
{: cli}

For {{site.data.keyword.codeengineshort}} `connectivity subnetpool` CLI commands, you can specify
the `--name`, `--subnet-crn`, and optionally `--security-group-crn` options to configure subnet pools.
Follow these guidelines:

* Do not use duplicate `--name` values within a project.
* Do not use duplicate `--subnet-crn` values within one subnet pool.

1. Select your {{site.data.keyword.codeengineshort}} project. For example:

    ```txt
    ibmcloud ce project select --name myproject
    ```
    {: pre}

2. Create a subnet pool by specifying the `--name`, `--subnet-crn`, and optionally `--security-group-crn` options. The `--subnet-crn` and `--security-group-crn` options can be specified multiple times. To correlate `--security-group-crn` values with their `--subnet-crn` value, use an arbitrary identifier as key. Refer to this example, which uses keys `S1` and `IDx`:

    ```txt
    ibmcloud ce connectivity outbound subnetpool create --name my-other-pool \
        --subnet-crn S1=crn:v1:bluemix:public:is:eu-de-3:a/abcdefabcdefabcdefabcd1234567890::subnet:1a1a-2b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f21 \
        --security-group-crn S1=crn:v1:bluemix:public:is:eu-de:a/abcdefabcdefabcdefabcd1234567890::security-group:2b2b-3c3c3c3c-4d4d-5e5e-6f6f-7g7g7g7g7g7g \
        --subnet-crn IDx=crn:v1:bluemix:public:is:eu-de-3:a/abcdefabcdefabcdefabcd1234567890::subnet:1a1a-2b2b2b2b-3c3c-4d4d-5e5e-6f6f6f6f6f22 \
        --security-group-crn IDx=crn:v1:bluemix:public:is:eu-de:a/abcdefabcdefabcdefabcd1234567890::security-group:2b2b-3c3c3c3c-4d4d-5e5e-6f6f-7g7g7g7g7g7g \
        --security-group-crn IDx=crn:v1:bluemix:public:is:eu-de:a/abcdefabcdefabcdefabcd1234567890::security-group:2b2b-3c3c3c3c-4d4d-5e5e-6f6f-7g7g7g7g7g8h
    ```
    {: pre}

### Showing existing subnet pools
{: #show-subnetpools-cli}
{: cli}

To show a specific subnet pool, specify the name or ID. For example:

```txt
ibmcloud ce connectivity subnetpool get --name my-other-pool
```
{: pre}

To show all subnet pools, run:

```txt
ibmcloud ce connectivity subnetpool list
```
{: pre}

### Deleting a subnet pool
{: #delete-subnetpool-cli}
{: cli}

You can delete previously defined subnet pools if you no longer use them.

To run a fleet, you need at least one subnet pool configured within a project.
{: remember}

To delete a subnet pool with confirmation, specify the name or ID. For example:

```txt
ibmcloud ce connectivity subnetpool delete --name my-other-pool
```
{: pre}

To delete a subnet pool forcefully (that is, without confirmation), run:

```txt
ibmcloud ce connectivity subnetpool delete --name my-other-pool --force
```
{: pre}
