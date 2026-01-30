---

copyright:
  years: 2025, 2026
lastupdated: "2026-01-27"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Preparing to run a fleet
{: #fleet-prep}

Before you can use {{site.data.keyword.codeengineshort}} fleets:

* You must define network placement configuration by creating a subnet pool. It is required to determine within which VPC subnets your fleet workers get deployed.
* You must create a persistent data store.
You have to complete these steps only once for each project that you want to run fleets in.
{: shortdesc}

Want to configure logging and monitoring for fleets? After you complete the steps on this page, see [Setting up observability for fleets](/docs/codeengine?topic=codeengine-fleet-observability).
{: tip}

## 1. Gather the required subnet information for network placement
{: #fleet-prep-gather}

This step is required if you want to specify a subnet pool for network placement by providing the **CRN** of one or more VPC subnets.
{: note}

Run the commands to get the CRN of up to three subnets that you want your fleet workers to attach to. These subnets must reside in the same region as the {{site.data.keyword.codeengineshort}} project you want to run your fleets in. In the output, find the  **CRN**, which has a format similar to the following: `crn:v1:bluemix:public:is:us-east-2:a/1af204bc1def56171eed1a8100b1cc121::subnet:1345-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`. These CRNs are referenced later in the subnet pool.

To list all subnets.

```txt
ibmcloud is subnets
```
{: pre}

To get the details of a single subnet.

```txt
ibmcloud is subnet <subnet_id>
```
{: pre}

## 2. (Optional) Gather security group information for each subnet
{: #fleet-prep-gather-sg}

If you want to apply existing custom security groups to the subnets attached to your fleet workers, run the commands to get the CRN of all security groups for each subnet you found in the previous step. In the output for each security group, find the **CRN**, which has the following format: `crn:v1:bluemix:public:is:us-east:a/1af204bc1def56171eed1a8100b1cc121::security-group:6789-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`. These CRNs are referenced later in the subnet pool. If you do not specify a security group, the default security group of the VPC is used.

To list all security groups

```txt
ibmcloud is sgs
```
{: pre}

To get the details of a single security group.

```txt
ibmcloud is sg <securitygroup_id>
```
{: pre}

## 3. Add security groups to VPE gateways
{: #fleet-prep-gather-vpegw}

If the subnets specified for network placement also have attached VPE gateways for {{site.data.keyword.cos_full_notm}} or {{site.data.keyword.registrylong_notm}}, then you must attach the security groups found in the previous step to those VPE gateways. This is required for fleet workers to have access to the VPE gateway.

1. For each subnet found in previous steps, check if the subnet has VPE gateways attached.
   1. Navigate to your [list of subnets](https://cloud.ibm.com/infrastructure/network/subnets){: external} and find the subnets you want to use for network placement.
   2. For each subnet used in network placement, click the subnet name to open the details page. 
   3. Click **Attached resources** and find the **Attached virtual endpoint gateways** section.
2. For each VPE gateway that lists **Cloud Object Storage** or **Container Registry** under **Service details**, add the security groups.
   1. Click the VPE gateway name to open the gateway details page.
   2. Click **Attached resources** and find the **Security groups** section.
   3. Click **Attach** and follow the prompts to attach the security groups used in network placement for fleets. 

## 4. (Optional) Add a public gateway to your subnets
{: #fleet-prep-pubgateway}

If you want to run images from a public container registry, you must attach a public gateway to the subnets you specify in the subnet pool.

1. Navigate to the [Subnets for VPC list](https://cloud.ibm.com/infrastructure/network/subnets){: external} in the console.
2. Click the subnet you want to use for fleet workers network placement.
3. In the **Public gateway** section of the subnet details page, click the option to attach a public gateway to the subnet.
4. Repeat this step for each subnet you want to use for fleet workers network placement.

## 5. Configure a subnet pool
{: #fleet-prep-subnetpool}

Configure at least one subnet pool. You can prepare this following the steps in [Working with subnet pool connectivity in {{site.data.keyword.codeengineshort}}](/docs/codeengine?topic=codeengine-connectivity-subnetpool), or you can configure one or more subnetpools for network placement adhoc when [Running a fleet by using the console](/docs/codeengine?topic=codeengine-fleet-run#fleet-run-ui).

## 6. Create a persistent data store
{: #fleet-prep-pds}

A persistent data store is required to store the state of the tasks of a fleet. Follow the steps in [Working with persistent data stores](/docs/codeengine?topic=codeengine-persistent-data-store).

Make sure to follow all the prerequisite steps for creating an {{site.data.keyword.cos_full_notm}} bucket and service credentials, as well as the step to create an HMAC secret.
{: important}

To load input data from or write output data to COS buckets, it is recommended to create separate persistent data stores and mount these into the task instance containers at fleet creation time. Be mindful of the [Limitations](/docs/codeengine?topic=codeengine-persistent-data-store#pds-limitations) when writing files to persistent data stores:

* Write large files to the mount only once, since COS writes entire objects only.
* If writing to a file repeatedly during task execution, write it to a temporary directory in the task container first, and move it to the mount only when done.
* If writing many small files, write them into a temporary directory in the task container, put them all into a single file (for example a ZIP or tar.gz archive), and move that one to the mount once done.
