---

copyright:
  years: 2025
lastupdated: "2025-09-10"

keywords: code engine, event notifications

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Enabling event notifications for {{site.data.keyword.codeengineshort}}
{: #event-notifications-events}


As an administrator of {{site.data.keyword.codeengineshort}}, you might want to send events from other IBM Cloud services to {{site.data.keyword.codeengineshort}} to trigger your apps or jobs.
{: shortdesc}

To send information to {{site.data.keyword.en_short}}, you must connect your {{site.data.keyword.codeengineshort}} instance to {{site.data.keyword.en_short}}. For more information about working with {{site.data.keyword.en_short}}, see [Getting started with {{site.data.keyword.en_short}}](/docs/event-notifications?topic=event-notifications-getting-started).

## How are events received?
{: #event-notifications-how}

Your {{site.data.keyword.codeengineshort}} instance can work as a destination for {{site.data.keyword.en_short}}.

When configured as a **Destination**, your {{site.data.keyword.codeengineshort}} jobs or apps can be triggered in response to an event notification from another IBM Cloud service or even another Code Engine app or job.

## What are some key features of {{site.data.keyword.en_short}}
{: #event-notifications-features}

Review the following features for using {{site.data.keyword.en_short}} with {{site.data.keyword.codeengineshort}}

- You can enable or disable `pingSource` which allows you to control scheduled event sources, like timers, by enabling or disabling them as needed. This is not possible when using Event Subscriptions.

- You can control the number of retries and dead letter queues. When calling {{site.data.keyword.codeengineshort}}, issues such as network errors or application glitches can cause the requests to fail. A retry is used to provide resiliency to external requests. To learn more, checkout Number of retries.

- You're not limited to periodic timers. {{site.data.keyword.en_short}} supports various event sources such as HTTP events, cloud service events (e.g., object uploads), functions, and {{site.data.keyword.codeengineshort}} job outputs. This modularity enables the creation of flexible workflows that can respond to real-time events instead of just scheduled triggers. By combining multiple event sources, you can design complex, dynamic systems with ease.

- You can create complex workflows. For example, a job can be triggered by a timer, then when the job completes, it can send an event back into {{site.data.keyword.en_short}} as a source for other services. One scenario for this type of workflow would be having the event trigger an email notification or initiate another workflow.

- Your jobruns are automatically deleted. By default, {{site.data.keyword.en_short}} automatically deletes job runs after 10 minutes to prevent job-run quota issues. This helps ensure that stale or stuck jobs do not consume resources unnecessarily. It also helps to avoid exceeding {{site.data.keyword.codeengineshort}} job quota. You can verify this behavior by observing the Job tab in your {{site.data.keyword.codeengineshort}} project, where you'll see that the job run is automatically removed after the 10-minute window.

## How are {{site.data.keyword.en_short}} notifications different from subscriptions?
{: #event-notifications-compare}

Subscriptions for Event Notifications allow your Code Engine apps or jobs to receive event information.

With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. Event information is received as POST HTTP requests for applications and as environment variables for jobs.

{{site.data.keyword.codeengineshort}} supports the following types of event producers for subscriptions.

Cron
:   The cron event producer is based on cron-job and generates an event at regular intervals. Use a cron event producer when an action needs to be taken at well-defined intervals or at specific times.

IBM Cloud Object Storage
:   The Object Storage event producer generates events as changes are made to the objects in your object storage buckets. For example, as objects are added to a bucket, an application can receive an event and then perform an action based on that change, perhaps consuming that new object.

Kafka
:   The Kafka event producer watches for new messages to appear in a Kafka instance. When you create a {{site.data.keyword.codeengineshort}} Kafka subscription for a set of topics, your app or job receives a separate event for each new message that appears in one of the topics.

Webhooks
:   You can use GitHub webhooks to send events from a GitHub repository to your {{site.data.keyword.codeengineshort}} workload.


Alternatively, with {{site.data.keyword.en_short}} you can configure {{site.data.keyword.codeengineshort}} as a **Destination**.

When configured as a **Destination**, your {{site.data.keyword.codeengineshort}} jobs or apps can be triggered in response to an event notification from another IBM Cloud service or even another {{site.data.keyword.codeengineshort}} app or job.

| Task | Subscription | {{site.data.keyword.en_short}} |
| --- | --- | --- |
| Defining event source | Create a periodic timer cron-like event source that generates recurring time-based events. | Use a pre-defined event source - Periodic Timer |
| Scheduling | As a next step, Schedule the timer | Create a topic, choose source as Periodic Timer. Configure using `cronExpression` |
| Choose end destination | Select the job or application | Create a end destination. {{site.data.keyword.codeengineshort}} |
| Subscribe to event | No explicit subscription needed. | Create a subscription. Choose previously created destination and topic. |
{: caption="Compare subscriptions and event notifications" caption-side="bottom"}

To learn more, see [Getting started with subscriptions](/docs/codeengine?topic=codeengine-subscribing-events).


## Setting up a trigger in the console
{: #event-notifications-example1}
{: ui}

In this example, you use the IBM Cloud console to set up a timer trigger in {{site.data.keyword.en_short}} that calls a {{site.data.keyword.codeengineshort}} job every 6 hours.

Before you begin, make sure you have the following in your account.

- An {{site.data.keyword.en_short}} instance
- A {{site.data.keyword.codeengineshort}} project.
- A target job within the project.

Complete the following steps to create the trigger.

1. Set up a source in your {{site.data.keyword.en_short}} instance.
    1. Set Up a Source
    1. Choose **Periodic Timer** as the event source.
    1. Set Up a **Topic** A Topic acts as a filter for events. You’ll use this to define the events of interest.
    1. Give your topic a name. For example, "Periodic-Trigger-6hr".
    1. Set the cron expression `(0 */6 * * *)` so that the topic emits events every 6 hours. Learn more about creating-a-topic-with-periodic-timer.

1. Set up a destination. The destination is where the event is sent for processing. In this example, choose your existing {{site.data.keyword.codeengineshort}} job from the list of available destinations. The job will act as the endpoint that will be triggered when the event occurs.

    Note: A service-to-service authorization is needed between {{site.data.keyword.en_short}} and {{site.data.keyword.codeengineshort}}. This can be configured by going to **Manage** > **Access** > **Authorizations** in the console. However, when you use the console, this part is handled automatically.
    {: note}

1. Create a Subscription that links the Topic and the Destination.

    1. Select the "Periodic-Trigger-6hr" topic that you created earlier.

    1. Choose your {{site.data.keyword.codeengineshort}} job as the destination.


The subscription ensures that when the event is emitted every 6 hours, the {{site.data.keyword.codeengineshort}} job will be triggered. You can observe and verify the interval by reviewing the the **Jobruns** tab of your project.

The previous steps configured a job as the destination. However, this same procedure can be used if your destination an app. When setting up the destination, provide your app URL.
{: note}

## Setting up a trigger in the CLI
{: #event-notifications-example1}
{: cli}

In this example, you use the IBM Cloud CLI to set up a timer trigger in {{site.data.keyword.en_short}} that calls a {{site.data.keyword.codeengineshort}} job every 6 hours.

Before you begin, make sure you have the following in your account.

- A {{site.data.keyword.codeengineshort}} project.
- A target job within the project.

Complete the following steps to set up the trigger.

1. Create an {{site.data.keyword.en_short}} instance.
    ```sh
    ibmcloud resource service-instance-create "$EVENT_NOTIFICATIONS_INSTANCE_NAME" \
    "$EVENT_NOTIFICATIONS_SERVICE_NAME" "$EVENT_NOTIFICATIONS_PLAN" "$PROJECT_REGION" \
    -g "$PROJECT_RESOURCE_GROUP"
    ```
    {: pre}

1. Create an authorization policy.
    ```sh
    ibmcloud iam authorization-policy-create event-notifications codeengine Writer,Viewer \ 
    --source-service-instance-id $EVENT_NOTIFICATIONS_INSTANCE_ID \
    --target-service-instance-name "${PROJECT_NAME}"
    ```
    {: pre}

1. Create a destination by using your {{site.data.keyword.codeengineshort}} job.
    ```sh
    CONFIG_JSON=$(cat <<EOF
    {
      "params": {
        "type": "job",
        "job_name": "${JOB_NAME}",
        "project_crn": "${PROJECT_CRN}"
      }
    }
    EOF
    )

    ibmcloud event-notifications destination-create \
      --instance-id "${EVENT_NOTIFICATIONS_INSTANCE_ID}" \
      --name "${DESTINATION_NAME}" \
      --type "ibmce" \
      --description "${DESTINATION_DESCRIPTION}" \
      --config "$CONFIG_JSON"
    ```
    {: pre}

1. Create an {{site.data.keyword.en_short}} topic. Set the topic `--topic-timer` to `0 */6 * * *` for a 6 hour interval.
    ```sh
    ibmcloud event-notifications topic create \
    --name "$TOPIC_NAME" \
    --description "$TOPIC_DESCRIPTION" \
    --service-instance-id "$EVENT_NOTIFICATIONS_CRN" \
    --topic-type timer \
    --topic-timer "$TOPIC_CRON" # Example: "0 */6 * * *" 
    ```
    {: pre}

1. Subscribe to the destination topic.
    ```sh
    ibmcloud event-notifications subscription create \
    --name "$SUBSCRIPTION_NAME" \
    --description "Triggers CE job from topic" \
    --service-instance-id "$EVENT_NOTIFICATIONS_CRN" \
    --topic-id "$TOPIC_ID" \
    --destination-id "$DESTINATION_ID"
    ```
    {: pre}

A ready-to-use script for configuring a Periodic Timer for {{site.data.keyword.codeengineshort}} jobs is provided in the [Sample Github Repository](https://github.ibm.com/ibmcloud-codeengine-internship/event-notification). It also includes steps to use {{site.data.keyword.en_short}} for sending emails as a destination and steps for using event subscriptions.
{: tip}


