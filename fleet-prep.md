---

copyright:
  years: 2025, 2025
lastupdated: "2025-11-24"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Preparing to run a fleet
{: #fleet-prep}

Before you can use {{site.data.keyword.codeengineshort}} fleets, you must prepare a secret with required values for network placement. These values are required as they determine which VPC subnets your fleet workers are deployed on. Then, you must create a required persistent data store. You only have to complete these steps once for each project that you want to run fleets in. 
{: shortdesc}

Want to configure logging and monitoring for fleets? After you complete the steps on this page, see [Setting up observability for fleets](/docs/codeengine?topic=codeengine-fleet-observability&interface=ui).
{: tip}

## 1. Gather the required subnet information for network placement
{: #fleet-prep-gather}

Run the commands to get the CRN of up to three subnets that you want your fleet workers to attach to. These subnets must reside in the same region as the {{site.data.keyword.codeengineshort}} project you want to run your fleets in. In the output, find the  **CRN**, which has a format similar to the following: `crn:v1:bluemix:public:is:us-east-2:a/1af204bc1def56171eed1a8100b1cc121::subnet:1345-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`. These CRNs are referenced later in the required secret. 

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

If you want to apply existing custom security groups to the subnets attached to your fleet workers, run the commands to get the CRN of all security groups for each subnet you found in the previous step. In the output for each subnet, find the **CRN**, which has the following format: `crn:v1:bluemix:public:is:us-east-2:a/1af204bc1def56171eed1a8100b1cc121::subnet:1345-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`. These CRNs are referenced later in the secret. If you do not specify a security group, the subnet's default security group is used.

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
    
## 3.  Add security groups to VPE gateways

If the subnets specified for network placement also have attached VPE gateways for {{site.data.keyword.cos_full_notm}} or {{site.data.keyword.registrylong_notm}}, then you must attach the security groups found in the previous step to those VPE gateways. This is required for fleet workers to have access to the VPE gateway. 

1. For each subnet found in previous steps, check if the subnet has VPE gateways attached.
  1. Navigate to your [list of subnets](https://cloud.ibm.com/infrastructure/network/subnets){: external} and find the subnets you want to use for network placement.
  2. For each subnet used in network placement, click on the subnet name to open the details page. 
  3. Click **Attached resources** and find the **Attached virtual endpoint gateways** section.
2. For each VPE gateway that lists **Cloud Object Storage** or **Container Registry** under **Service details**, add the security groups.
   1. Click on the VPE gateway name to open the gateway details page.
   2. Click **Attached resources** and find the **Security groups** section.
   3. Click **Attach** and follow the prompts to attach the security groups used in network placement for fleets. 


## 4. (Optional) Add a public gateway to your subnets
{: #fleet-prep-pubgateway}

If you want to run images from a public container registry, you must attach a public gateway to the subnets you specify in the default secret.

1. Navigate to the [Subnets for VPC list](https://cloud.ibm.com/infrastructure/network/subnets){: external} in the console.
2. Click the subnet you want to add to the secret.
3. In the **Public gateway** section of the subnet details page, click the option to attach a public gateway to the subnet.
4. Repeat this step for each subnet you want to specify in the default secret.


## 5. Configure the secret
{: #fleet-prep-secret}

Configure the required secret. 

1. In the UI, go to the [{{site.data.keyword.codeengineshort}} console](https://cloud.ibm.com/codeengine/overview).
2. Click **Serverless projects** to navigate to your project dashboard. Select the relevant project, or create a new one. 
3. Click **Secrets and configmaps**, then click **Create**.
4. Select **Generic secret**, then click **Next**.
5. Name the secret `codeengine-fleet-defaults`. You must use this exact name and formatting.
6. Create a secret with the values listed in the following tables. For steps on finding the CRN, endpoints, and API key values, see **Gathering values for the secret**. 

|  Key  |  Required?   |  Description |
| ----  | -----------  | ------------ |
| `pool_subnet_crn_1` | Required. | The CRN of the subnet. |
| `pool_security_group_crns_1` | Optional. | The CRNs of the security groups you want to apply to the workers that use the subnet. Include multiple values as a comma-separated list. |
| `pool_subnet_crn_2` | Optional. | The CRN of the subnet. |
| `pool_security_group_crns_2` | Optional. | The CRNs of the security groups you want to apply to the workers that use the subnet. Include multiple values as a comma-separated list. |
| `pool_subnet_crn_3` | Optional. | The CRN of the subnet. |
| `pool_security_group_crns_3` | Optional. | The CRNs of the security groups you want to apply to the workers that use the subnet. Include multiple values as a comma-separated list. |
{: caption="Key value pairs for required secret." caption-side="bottom"}


## 6. Create a persistent data store
{: #fleet-prep-pds}

A persistent data store is required to run fleets. Follow the steps in [Working with persistent data stores](/docs/codeengine?topic=codeengine-persistent-data-store). 

Make sure to follow all of the pre-requisite steps for creating a {{site.data.keyword.cos_full_notm}} bucket and service credentials, as well as the step to create an HMAC secret. 
{: important}
