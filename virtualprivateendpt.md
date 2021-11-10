---

copyright:
  years: 2020, 2021
lastupdated: "2021-11-10"

keywords: endpoints, virtual private endpoints, public endpoints, private endpoints, service endpoints

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Using Virtual Private Endpoints with {{site.data.keyword.codeengineshort}}
{: #vpe}

All {{site.data.keyword.codeenginefull}} projects offer integration with {{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for Virtual Private Cloud (VPC). This support gives you the ability to connect from your VPC network to {{site.data.keyword.codeengineshort}} applications by using the IP addresses of your choosing, which are allocated from a subnet within your VPC. 
{: shortdesc}

With {{site.data.keyword.codeengineshort}}, you can use the following types of VPEs:

- [Virtual Private Endpoints to manage project resources](/docs/codeengine?topic=codeengine-regions#endpoints-project). There is one static VPE per region. 
- [Virtual Private Endpoints to access applications](/docs/codeengine?topic=codeengine-regions#endpoints-app). There is one VPE per {{site.data.keyword.codeengineshort}} project. All apps within the project can be accessed by using this VPE. 

Private endpoints provide a connection to your project resources and applications on the {{site.data.keyword.cloud_notm}} Private network. When you connect through a virtual private endpoint, all traffic is routed to hardware that is dedicated to {{site.data.keyword.codeengineshort}} applications and remains on the {{site.data.keyword.cloud_notm}} Private network. There are no additional charges for all traffic to and from this endpoint on the condition that the traffic remains in {{site.data.keyword.cloud_notm}}. 

A {{site.data.keyword.codeengineshort}} project is automatically configured with both a public and a virtual private endpoint. 

You can control the [visibility](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility) of {{site.data.keyword.codeengineshort}} applications and specify whether to expose the application to public or private endpoints. An application that is configured for the private network can be accessed only  through the VPE and it is not accessible from the public internet.

## Using your VPE to manage project resources securely
{: #using-vpes-project}

Before you begin, you must have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration).

1. Create an {{site.data.keyword.vpc_full}}. Follow the [Getting started](/docs/vpc?topic=vpc-getting-started) instructions. 

2. Make sure that your VPC has at least one VSI (virtual server instance) and can connect to the VSI. You can use the UI, CLI, and API to quickly provision {{site.data.keyword.vpc_full}} from the Virtual server instances page in the {{site.data.keyword.cloud_notm}} console. 

    1. Create an [SSH key](/docs/vpc?topic=vpc-ssh-keys) to access the VSI. 
    2. [Create a virtual server instance by using the UI](/docs/vpc?topic=vpc-creating-virtual-servers).
    3. [Reserve a floating IP address](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#reserving-a-floating-ip-address) so your instance is reachable from the internet.
    4. [Connect to your VSI](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#connecting-to-your-instance).

3. In the {{site.data.keyword.cloud_notm}} console, click the Menu icon and select **VPC Infrastructure -> Network -> Virtual private endpoint gateways**. Create a VPE for the regional {{site.data.keyword.codeengineshort}} endpoint `api.<region>.codeengine.cloud.ibm.com` by completing this [instruction](/docs/vpc?topic=vpc-about-vpe). 

4. After you create your VPE, it might take a few minutes for the new VPE and private DNS (pDNS) to complete the process and begin working for your VPC. Completion is confirmed when you see an IP address set in the [details view](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) of the VPE. 

5. SSH into your VSI and use `root@`. For example, `ssh root@<VSI_floating_IP_address>`.

6. To access {{site.data.keyword.codeengineshort}} resources from within the VSI, [set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli). Make sure your {{site.data.keyword.cloud_notm}} CLI is connected to `private.cloud.ibm.com`.

7. Specify a {{site.data.keyword.codeengineshort}} project to use the private endpoint. To create a project, use the  [**`ibmcloud ce project create`**](/docs/codeengine?topic=codeengine-cli#cli-project-create) command with the `--endpoint=private` option.

    ```sh
    ibmcloud ce project create -name myproject --endpoint=private
    ```
    {: pre}

    Wait until the project is in `active` status.  With the CLI, you can confirm the project status by using the  [**`ibmcloud ce project get`**](/docs/codeengine?topic=codeengine-cli#cli-project-get) command.

    If you want an existing {{site.data.keyword.codeengineshort}} project to use the private endpoint, use the [**`ibmcloud ce project select`**](/docs/codeengine?topic=codeengine-cli#cli-project-select) command with the `--endpoint=private` option.

    ```sh
    ibmcloud ce project select -name myproject --endpoint=private
    ```
    {: pre}

    For the **`project create`** and **`project select`** commands, if the `--endpoint` option is not explicitly specified, the behavior is determined by the system. If the {{site.data.keyword.cloud_notm}} CLI is connected to `private.cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `private`. If the {{site.data.keyword.cloud_notm}} CLI is connected to `cloud.ibm.com`, the {{site.data.keyword.codeengineshort}} project behaves as if `--endpoint` is `public`.
    {: important}

8. Create an application that is only visible to the private endpoint. Use the  [**`ibmcloud ce application create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command with the `--visibility=private` option. Alternatively, you can use the console to create an app or update an existing app and set the [visibility of your app](/docs/codeengine?topic=codeengine-application-workloads#optionsvisibility).

    ```sh
    ibmcloud ce application create -n myapp --visibility=private
    ```
    {: pre}

You have now configured and set up your virtual private endpoint to manage project resources. If you want to control which app to expose to the private endpoint, you can [set up a VPE to access your application](/docs/codeengine?topic=codeengine-vpe#using-vpes-app).

## Using your VPE to access an app securely
{: #using-vpes-app}

Before you begin, you must have an [{{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/registration).

1. Create an {{site.data.keyword.vpc_full}}. Follow the [Getting started](/docs/vpc?topic=vpc-getting-started) instructions. 

2. Make sure that your VPC has at least one VSI (virtual server instance) and can connect to the VSI. You can use the UI, CLI, and API to quickly provision {{site.data.keyword.vpc_full}} from the Virtual server instances page in the {{site.data.keyword.cloud_notm}} console. 

    1. Create an [SSH key](/docs/vpc?topic=vpc-ssh-keys) to access the VSI. 
    2. [Create a virtual server instance by using the UI](/docs/vpc?topic=vpc-creating-virtual-servers).
    3. [Reserve a floating IP address](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#reserving-a-floating-ip-address) so your instance is reachable from the internet.
    4. [Connect to your VSI](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console#connecting-to-your-instance).

3. From your {{site.data.keyword.codeengineshort}} project, confirm that your application is configured with a `visibility=private` setting. See [Deploying your app with a private endpoint](/docs/codeengine?topic=codeengine-application-workloads#app-endpoint-public).

4. In the {{site.data.keyword.cloud_notm}} console, click the Menu icon and select **VPC Infrastructure -> Network -> Virtual private endpoint gateways**. Create a VPE for your {{site.data.keyword.codeengineshort}} project by completing this [instruction](/docs/vpc?topic=vpc-about-vpe). 

5. After you create your VPE, it might take a few minutes for the new VPE and private DNS (pDNS) to complete the process and begin working for your VPC. Completion is confirmed when you see an IP address set in the [details view](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) of the VPE.   

6. Retrieve the URL of the {{site.data.keyword.codeengineshort}} application that is exposed to the private network. The URL is in the following format: `<app>.<uuid>.private.<region>.codeengine.appdomain.cloud`. From the {{site.data.keyword.codeengineshort}} console, go to the **Endpoints** tab for your application to view the visibility of an app and its available URLs.  From the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli), you can use the [**`ibmcloud ce application get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command with the `--option url` option. Because the visibility of the `myapp` is set to  `visibility=private`, specifying `--option url` with this command outputs the URL to the private network. 

    ```sh
    ibmcloud ce application get -n myapp -output url
    ```
    {: pre}

    Example output

    ```sh 
    http://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
    ```
    {: screen}

7. You can now use your instance in the VSI. Call the application. The `myapp` application is a simple Hello World application. When you curl the `myapp` app, `Hello World` is returned.

   ```sh
   curl http://myapp.4svg40kna19.private.us-south.codeengine.appdomain.cloud
    ```
   {: pre}




