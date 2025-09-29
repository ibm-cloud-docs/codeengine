---

copyright:
  years: 2025, 2025
lastupdated: "2025-09-29"

keywords: fleets, fleets in code engine, fleets in code engine, large volumes in code engine, deploy fleets in code engine,  running fleets in code engine, deploying fleets in code engine, fleet, instance, task, large volume

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Preparing to run a fleet
{: #fleet-prep}

Before you can use Code Engine fleets, you must prepare a secret with required values for network placement. These values are required as they determine which VPC subnets your fleet workers are deployed on. Then, you must create a required persistent data store. You only have to complete these steps once for each project that you want to run fleets in. 
{: shortdesc}

Want to configure logging and monitoring for fleets? After you complete the steps on this page, see [Setting up observability for fleets]().
{: tip}

## 1. Gather the required networking values for the secret
{: #fleet-prep-gather}

Follow the steps to gather the networking values for the secret. For a complete list of secret values, see [this table](#fleet-prep-secret).

1. Run the commands to get the CRN of up to three subnets that you want your fleet workers to attach to. In the output, find the  **CRN**, which has a format similar to the following: `crn:v1:bluemix:public:is:us-east-2:a/1af204bc1def56171eed1a8100b1cc121::subnet:1345-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`.

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

3. For each subnet in the previous step, run the commands to get the CRN of up to three security groups you want to apply to the fleet workers attached to the subnet. In the output, find the **CRN**, which has the following format: `crn:v1:bluemix:public:is:us-east-2:a/1af204bc1def56171eed1a8100b1cc121::subnet:1345-16e10cc-ba18-19ee-de1b0-1213aa1a41a0156`.

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

## 2. (Optional) Add a public gateway to your subnets
{: #fleet-prep-pubgateway}

If you want to run images from a public container registry, you must attach a public gateway to the subnets you specify in the default secret.

1. Navigate to the [Subnets for VPC list](https://cloud.ibm.com/infrastructure/network/subnets){: external} in the console.
2. Click the subnet you want to add to the secret.
3. In the **Public gateway** section of the subnet details page, click the option to attach a public gateway to the subnet.
4. Repeat this step for each subnet you want to specify in the default secret.


## 3. Configure the secret
{: #fleet-prep-secret}

Configure the required secret. 

1. In the UI, go to the [Code Engine console](https://cloud.ibm.com/codeengine/overview).
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


## 4. Create a persistent data store
{: #fleet-prep-pds}

A persistent data store is required to run fleets. Follow the steps in [Working with persistent data stores](/docs/codeengine?topic=codeengine-persistent-data-store).
