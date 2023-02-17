---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-17"

keywords: github events, github webhooks, webhooks, application webhook, event webhook, code engine

subcollection: codeengine

content-type: tutorial
completion-time: 10m 

---

{{site.data.keyword.attribute-definition-list}}

# Sending GitHub events to an application
{: #github-event-webhooks}
{: toc-content-type="tutorial"}
{: toc-completion-time="10m"}

You can set up a webhook to send a GitHub event, such as a new issue or a commit to your {{site.data.keyword.codeenginefull}} application. Your application must use a public endpoint to receive the webhook POST requests.
{: shortdesc}

For more information about GitHub webhooks, see [About webhooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks){: external}. For more information about GitHub, see [GitHub Docs](https://docs.github.com/){: external}.

## Prerequisites
{: #gew-prerequisites}

Before you begin, set up your account and install the command line environment. While you can use the console to create your application, this example uses the CLI.

- Ensure that you have a Pay-as-you-Go account.
- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}

## Create an application
{: #gew-create-app}
{: step}

Create an application to receive your GitHub events called `my-github-app` that uses an image called `github` with the [**`ibmcloud ce app create`**](/docs/codeengine?topic=codeengine-cli#cli-application-create) command. This app logs each commit event that occurs in the GitHub repository. The image is built from `github.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/github){: external}. 


```sh
ibmcloud ce application create --name my-github-app --image icr.io/codeengine/github --min-scale 1
```
{: pre}


After your application creates, verify that your application is in a `Ready` state and find the application URL.

```txt
ibmcloud ce application get --name my-github-app
```
{: pre}

The application URL is found in the **URL** field in the example output.

```txt
Name:               my-github-app  
ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f 
Project Name:       myproject  
Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111  
Age:                20h  
Created:            2022-11-28T13:16:49-06:00  
URL:                https://my-github-app.abcdabcdabc.us-south.codeengine.appdomain.cloud  
Cluster Local URL:  http://my-github-app.abcdabcdabc.svc.cluster.local  
Console URL:        https://cloud.ibm.com/codeengine/project/us-south/abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f/application/my-github-app/configuration  
Status Summary:     Application deployed successfully
...

```
{: screen}

## Create a webhook
{: #gew-create-webhook}
{: step}

Create a GitHub webhook to subscribe your application to GitHub events. You can subscribe to one or more webhook events. When an event that you subscribe to occurs, GitHub sends a payload to your application. For more information, see [Webhook events and payloads](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads){: external}.

To create a GitHub webhook, follow these steps.

1. Go to your GitHub repository and select **Settings**.
2. Select **Webhooks** -> **Add webhook**. Note that your GitHub repository might use **Hooks** instead of **Webhooks**.
3. Enter your application URL as your **Payload URL**.
4. Select the **Content type** that your application requires. If you are using the sample `github` app, then select `application/json` as your content type.  
5. Optional. Add a secret to your webhook. For more information, see [Securing your webhooks](https://docs.github.com/en/developers/webhooks-and-events/webhooks/securing-your-webhooks){: external}.
6. Select to **Enable SSL Verification**.
7. Select **Just the push event** to trigger your webhook.
8. Ensure **Active** is selected. You can disable your webhook without deleting it by removing the checkmark.
9. Click **Add webhook**.

After you finish, verify that your application is subscribed by checking the log files for the application. For more information about logs, see [Viewing logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-logs-cli).

```sh
ibmcloud ce app logs --name my-github-app
```
{: pre}

In the example output, look for the port that your app is listening on as well as the type of event.

```txt
my-github-app-00001-deployment-abcdabcdabc-1234/user-container:    
2022/12/02 17:07:27 Listening on port 8080  
2022/12/02 17:10:08 Event Type: ping  
2022/12/02 17:10:08 Not a 'push' event so exit
```
{: screen}

Note that if your applications scales to zero, you might receive a message about no instances of your app running. This app has a minimum scale of 1 so it always has a running instance.

## Test your GitHub event
{: #gew-test-webhook}
{: step}

Test your webhook by triggering the event that your application expects. In this case, the application is expecting a change to be committed in the GitHub repository.

1. In your GitHub repository, perform an action that triggers your webhook. For the `github` app, commit a change to a file in the repository.
2. After a minute or two, find the logs for your application. If your application scaled to zero, you might see a message indicating that your app does not have any running instances. Your application scales up when it receives an event so try again in a few minutes. For more information about logs, see [Viewing logs with the CLI](/docs/codeengine?topic=codeengine-view-logs#view-logs-cli).

    ```sh
    ibmcloud ce app logs --name my-github-app
    ```
    {: pre}

    For example, see the following output. 

    ```txt
    2022/11/28 19:45:28   
    Event:  {  
      "ref": "refs/heads/main",  
      "before": "0a11d22ebdaacdbb7bf5fdb6c92565c7c00fa97b",  
      "after": "af363efb8568874fe219bc73f3bccd0f4991907f",  
      "repository": {  
      
    ...
    
    "committer": {  
      "name": "GitHub",  
          "email": "noreply@github.com",  
          "username": "web-flow"  
        },  
        "added": [],  
        "removed": [],  
        "modified": [  
          "README.md"  
        ]  
      }  
    }  
    2022/11/28 19:45:28 kersten1 committed "af363efb8568874fe219bc73f3bccd0f4991907f" to "refs/heads/main" branch  
    2022/11/28 19:45:28 ibmcloud ce buildrun submit ...  

    ```
    {: screen}
    
    Your output is dependent on the application that you use and the GitHub repository that contains the webhook.

Your webhook is working! Now your app receives notification whenever you commit a file to your GitHub repository.

This application sets the minimum scale to 1 so that an instance of the app is always running. You can set the scale to 0 by updating the app with the following command. `ibmcloud ce app update --name my-github-app --min-scale 0`.
{: note}

## Clean up
{: #github-clean-up}

After you finish this tutorial, you can clean up the resources that you created with the following commands.

1. Delete your application

    ```txt
    ibmcloud ce app delete --name my-github-app
    ```
    {: pre}

    When you delete your app, the associated build files are also deleted.

2. Delete the webhook by opening your **GitHub settings -> Webhooks** and clicking **Delete** after the webhook name.
3. Delete the images that the build created from {{site.data.keyword.registrylong_notm}}. 

    1. Navigate to [**Registry**](https://cloud.ibm.com/registry/start){: external} in the {{site.data.keyword.cloud_notm}} console.
    2. Find the archive and the image that are associated with your application by searching for your application name.
    3. Select the archive and image and delete.


