---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-15"

keywords: kafka, kafka event, event producers, code engine, events, header, environment variables, subscription, subscribing

subcollection: codeengine

---

{{site.data.keyword.attribute-definition-list}}

# Working with the Kafka event producer
{: #working-kafkaevent-producer}

A {{site.data.keyword.codeengineshort}} Kafka subscription watches for new messages to appear in a Kafka instance. When you create a subscription for a set of topics, your app or job receives a separate event for each new message that appears in one of the topics. You can create at most 100 Kafka subscriptions per project.
{: shortdesc}

While you can use any Kafka instance, the examples in this topic use the {{site.data.keyword.messagehub_full}} service. {{site.data.keyword.messagehub}} is an IBM event streaming service for Kafka events. For more information about this service, see [{{site.data.keyword.messagehub}} documentation](/docs/EventStreams?topic=EventStreams-about).
{: note}

## Setting up the Kafka event producer
{: #subkafka-setup-sender}

You can set up your Kafka message producer to send messages to {{site.data.keyword.codeengineshort}} Kafka event subscriptions. Use your {{site.data.keyword.codeengineshort}} Kafka event subscription to trigger applications or jobs when a Kafka message is received.
{: shortdesc}

To get started, [create an {{site.data.keyword.messagehub}} service instance](/docs/EventStreams?topic=EventStreams-getting-started#getting_started_prereqs) for your event streaming service. While you can use the console or the CLI, the following steps describe how to set up the {{site.data.keyword.messagehub}} event producer with the CLI.

### Setting up the {{site.data.keyword.messagehub}} CLI environment
{: #setup-kafka-es-cli}

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). Log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```txt
    ibmcloud login
    ```
    {: pre}

2. Download and install the [{{site.data.keyword.codeengineshort}} CLI](/docs/codeengine?topic=codeengine-install-cli).

    ```txt
    ibmcloud plugin install code-engine -f
    ```
    {: pre}

3. To use the {{site.data.keyword.messagehub}} service for creating your Kafka instance, download and install the [{{site.data.keyword.messagehub}} CLI](/docs/EventStreams?topic=EventStreams-cli_reference).

    ```txt
    ibmcloud plugin install event-streams -f
    ```
    {: pre}

4. Log in to your {{site.data.keyword.cloud_notm}} account and target a resource group. Target a resource group by running the following command. To get a list of your resource groups, run the `ibmcloud resource groups` command.

    ```txt
    ibmcloud target -g <resource_group>
    ```
    {: pre}

### Setting up your Kafka instance
{: #setup-kafka-es-instance}

1. Create a service instance for {{site.data.keyword.messagehub}}. The name of the {{site.data.keyword.messagehub}} CLI service is `messagehub`. For this example, create an {{site.data.keyword.messagehub}} service instance that is named `myeventstream`.

    ```txt
    ibmcloud resource service-instance-create myeventstream messagehub lite us-south
    ```
    {: pre}


2. Create a service key to provide credentials to your service instance.

    ```txt
    ibmcloud resource service-key-create myeventstream-key Manager --instance-name myeventstream
    ```
    {: pre}

    Example output

    ```txt
    Creating service key of service instance myeventstream under account <user_account>...
    OK
    Service key crn:v1:bluemix:public:messagehub:us-south:a/e43abfcbd191404cb17ef650e9681dd3:c0736069-3f4a-438a-b614-6846877d692d:resource-key:4c8edfdb-abcd-abcd-abcd-abcdabcdabcd was created.

    Name:          myeventstream-key
    ID:            crn:v1:bluemix:public:messagehub:us-south:a/e43abfcbd191404cb17ef650e9681dd3:c0736069-3f4a-438a-b614-6846877d692d:resource-key:4c8edfdb-abcd-abcd-abcd-abcdabcdabcd
    Created At:    Mon Mar 21 18:36:09 UTC 2022
    State:         active
    Credentials:
                api_key:                  abcdeH9tu3qE5Sn8VbJfcDEWtjR_l0iPisB3abcdefgh
                apikey:                   abcdeH9tu3qE5Sn8VbJfcDEWtjR_l0iPisB3abcdefgh
                iam_apikey_description:   Auto-generated for key crn:v1:bluemix:public:messagehub:us-south:a/e43abfcbd191404cb17ef650e9681dd3:c0736069-3f4a-438a-b614-6846877d692d:resource-key:4c8edfdb-abcd-abcd-abcd-abcdabcdabcd
                iam_apikey_name:          myeventstream-key
                iam_role_crn:             crn:v1:bluemix:public:iam::::serviceRole:Manager
                iam_serviceid_crn:        crn:v1:bluemix:public:iam-identity::a/e43abfcbd191404cb17ef650e9681dd3::serviceid:ServiceId-3e99caa5-b174-4f04-9845-5c5d783b8bc7
                instance_id:              c0736069-3f4a-438a-b614-6846877d692d
                kafka_admin_url:          https://abcdabcdabcdabcd.svc07.us-south.eventstreams.cloud.ibm.com
                kafka_brokers_sasl:       [broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093]
                kafka_http_url:           https://abcdabcdabcdabcd.svc07.us-south.eventstreams.cloud.ibm.com
                password:                 abcdeH9tu3qE5Sn8VbJfcDEWtjR_l0iPisB3abcdefgh
                user:                     token
    ```
    {: screen}

    Make note of the values for `user`, `password`, and `kafka-brokers_sasl` for your service key. You need this information when you set up your {{site.data.keyword.codeengineshort}} Kafka subscription. The values for `password` and `apikey` are the same in the service key for your {{site.data.keyword.messagehub}} service instance. You can also use the `ibmcloud resource service-key myeventstream-key` command to retrieve the service key information.

3. Initialize the {{site.data.keyword.messagehub}} plug-in relative to your {{site.data.keyword.messagehub}} service instance.

    ```txt
    ibmcloud es init --instance-name myeventstream
    ```
    {: pre}

4. Create an {{site.data.keyword.messagehub}} topic.

    ```txt
    ibmcloud es topic-create kafka-topic1
    ```
    {: pre}


### Setting up a {{site.data.keyword.codeengineshort}} sample app to produce Kafka messages
{: #setup-kafka-sender-app}

For this scenario, let's use a {{site.data.keyword.codeengineshort}} application to act as an event producer of Kafka messages. The purpose of this application is to connect to your {{site.data.keyword.messagehub}} instance and to send Kafka messages. This application uses the [{{site.data.keyword.codeengineshort}} Kafka sender sample app](https://github.com/IBM/CodeEngine/tree/main/kafka){: external} to send Kafka messages. This sample sender image requires the `BROKERS` environment variable and a secret that includes the `password` credentials. You can create this application from the console or with the CLI.

Make sure that you specify the `Content-Type` header when you produce Kafka messages to {{site.data.keyword.messagehub}}. Specify this header so that the consumer can receive messages with the expected content type; for example, `application/json`.
{: important}

#### Creating a secret with credentials required by the Kafka samples
{: #setup-kafka-secret}

Before you create the {{site.data.keyword.codeengineshort}} application to send Kafka messages, create a {{site.data.keyword.codeengineshort}} secret that contains the required credentials.

Before you begin

* Determine the Code Engine project that you want to use and make sure that this project is selected. See [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

For simplicity in this scenario, create one secret, `kafka-subscription-secret`, to contain the credentials that are required for both the Kafka sender sample app and the Kafka event subscription, which uses the Kafka receiver sample. These credentials are required for the sample Kafka sender app and the {{site.data.keyword.codeengineshort}} Kafka event subscription to communicate with the service instance for {{site.data.keyword.messagehub}}. While it not required that you create this secret before you create the Kafka sender app and the event subscription, this action simplifies the required steps.
{: note}

##### Creating a secret with credentials required by the Kafka samples from the console
{: #setup-kafka-secret-ui}

To create the `kafka-subscription-secret` secret from the console, go to **Secrets and configmaps** and click **Create** and select the secret that you want to create. For more information, see [create a secret from the console](/docs/codeengine?topic=codeengine-secret#secret-create-ui).

* Specify the `username` key with the value of `user` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. For the {{site.data.keyword.messagehub}} service instance, this value is `token`. This key is required for authentication between the {{site.data.keyword.codeengineshort}} Kafka event subscription and the Kafka message broker.
* Specify the `password` key with the value of `apikey` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. This key is required for the sender sample, and to enable communications between the {{site.data.keyword.codeengineshort}} Kafka event subscription and the Kafka message broker.

##### Creating a secret with credentials required by the Kafka samples with the CLI
{: #setup-kafka-secret-cli}

To create the `kafka-subscription-secret` secret with the CLI, add a literal environment variable for `password`, and `username`. For more information, see [create a secret with the CLI](/docs/codeengine?topic=codeengine-secret#secret-create-cli).

* Specify the `username` key with the value of `user` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. For the {{site.data.keyword.messagehub}} service instance, this value is `token`. This key is required for authentication between the {{site.data.keyword.codeengineshort}} Kafka event subscription and the Kafka message broker.
* Specify the `password` key with the value of `apikey` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. This key is required for the sender sample, and to enable communications between the {{site.data.keyword.codeengineshort}} Kafka event subscription and the Kafka message broker.

    ```txt
    ibmcloud ce secret create --name kafka-subscription-secret --from-literal password=<value_of_apikey> --from-literal username=<value_of_user>
    ```
    {: pre}

    For example,

    ```txt
    ibmcloud ce secret create --name kafka-subscription-secret --from-literal password=abcdeH9tu3qE5Sn8VbJfcDEWtjR_l0iPisB3abcdefgh --from-literal username=token
    ```
    {: pre}

#### Creating a {{site.data.keyword.codeengineshort}} app to send events
{: #setup-kafka-senderapp}

Create a {{site.data.keyword.codeengineshort}} app for connecting to your {{site.data.keyword.messagehub}} instance and producing (sending) Kafka messages to a receiver of Kafka messages (Kafka consumer).
{: shortdesc}

##### Creating a {{site.data.keyword.codeengineshort}} app to send events from the console
{: #setup-kafka-senderapp-ui}

To create the `kafka-sender-app` application from the console, complete the following steps.

1. [Create a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-deploy-app&interface=ui#deploy-app-console) that is called `kafka-sender-app` with the following information.
    1. Reference the `icr.io/codeengine/kafka-sender` container image for this app. This image is built from `sender.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample sender app requires values for `password` and `BROKERS`.
    2. In the **Environment variables (optional)** section, add the following environment variables.
        1. Add a literal environment variable, `BROKERS`. For the value of this key, specify one or more of the broker hosts that are listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance.
        2. Add another environment variable to [reference the full secret](/docs/codeengine?topic=codeengine-secret#secret-ref-ui), `kafka-subscription-secret`. This secret contains the credentials for `password`.
    3. (optional) In the **Resources & scaling** section, specify `1` for the minimum number of instances so that the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. If you are running in a production environment, consider the cost of keeping a running instance of your app or whether you want {{site.data.keyword.codeengineshort}} to autoscale to zero. By default, the app scales to zero when not in use.
    4. Click **Create** to create and deploy your app.


2. Confirm that this app is in `ready` status.

##### Creating a {{site.data.keyword.codeengineshort}} app to send events with the CLI
{: #setup-kafka-senderapp-cli}

To create the `kafka-sender-app` application with the CLI, use the following commands.

1. [Create a {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#deploy-app-cli) that is called `kafka-sender-app` with the following information.
    * Specify the `--image` option to reference the `icr.io/codeengine/kafka-sender` container image. This image is built from `sender.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample sender app requires the `password` credentials that are stored in your `kafka-subscription-secret`, and it requires the `BROKERS` environment variable.
    * Specify the `--env-from-secret` option to reference the full secret, `kafka-subscription-secret`, which contains the `password` credentials.
    * Specify the `--env` option to add a literal environment variable, `BROKERS`, and provide the name of one of the broker hosts that are listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. However, if you want to specify more than one broker hostname, use the format `--env BROKERS-broker1,broker2,broker3`.
    * (optional) Specify the `--min-scale=1` option so that the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. If you are running in a production environment, consider the cost of keeping a running instance of your app or whether you want {{site.data.keyword.codeengineshort}} to autoscale to zero. By default, the app scales to zero when not in use.

    ```txt
    ibmcloud ce app create --name kafka-sender-app --image icr.io/codeengine/kafka-sender --env-from-secret kafka-subscription-secret --env BROKERS=broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --min-scale 1
    ```
    {: pre}



## Setting up {{site.data.keyword.codeengineshort}} to receive Kafka events for an app
{: #setup-kafka-receiverapp}

For {{site.data.keyword.codeengineshort}} to work with Kafka events, use the console or CLI to set up a {{site.data.keyword.codeengineshort}} Kafka eventing subscription to connect to Kafka event brokers and listen for Kafka events. Also, set up a {{site.data.keyword.codeengineshort}} app (or job) to act as the receiver of the Kafka events. The Kafka event subscription defines the relationship between the Kafka producer (sender) and consumer (receiver) of events.
{: shortdesc}

The {{site.data.keyword.codeengineshort}} Kafka event subscription connects to your Kafka message broker and sends HTTP Post requests for each incoming Kafka message to the receiver application. For more information, see [HTTP headers and body information for events](#subkafka-headerbody-app).

### Subscribing to Kafka events for an app from the console
{: #subscribe-kafka-app-ui}

You can use the console to set up a Kafka event subscription so that events are sent to a {{site.data.keyword.codeengineshort}} application.
{: shortdesc}

#### Creating a {{site.data.keyword.codeengineshort}} app to receive Kafka events from the console
{: #create-kafka-receiverapp-ui}

1. [Create an {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-deploy-app&interface=ui#deploy-app-console) to act as an event consumer of Kafka messages and receive the Kafka events. For example, create an application that is called `kafka-receiver-app` that uses the `icr.io/codeengine/kafka-receiver` image. This image is built from `receiver.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample does not require any environment variables.
2. After you deploy this app, confirm that it is in `ready` status.

When you use the console, it is not necessary that the app or job that you use to receive Kafka events exist before you create the Kafka event subscription. However, if the app or job does not exist when you create the event subscription, the status of the subscription reflects that the consumer does not exist. You must create the app or job before the subscription is in a ready state and can receive events through this subscription.
{: note}

#### Creating a {{site.data.keyword.codeengineshort}} Kafka event subscription for an app from the console
{: #create-kafka-subscription-app-ui}

The Kafka event subscription defines the relationship between the Kafka producer (sender) and consumer (receiver) of events.
{: shortdesc}

Before you begin

* Determine the Code Engine project that you want to use and make sure that this project is selected. See [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Complete the following steps to create a Kafka event subscription for an application from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create an event subscription page, select the `Event Streams / Kafka` tile to specify the event type.
5. For **General**, provide a name for the `Event Streams / Kafka` subscription. Click **Next** to proceed.
6. For **Message broker details**,
   1. Specify the Kafka message broker hosts for the message queues from which messages are received as events through this subscription. To obtain information about the broker hosts, topics, and access credentials, view the service credential details for your service instance in the {{site.data.keyword.messagehub}} console. For example, specify `"broker-0-abcdabcdabcdabcd.kafka.svc01.us-south.eventstreams.cloud.ibm.com:9093", "broker-1-abcdabcdabcdabcd.kafka.svc01.us-south.eventstreams.cloud.ibm.com:9093"` for the message broker hosts for the `myeventstream-key` service instance. You can find the brokers for the service instance in the {{site.data.keyword.messagehub}} in the `Kafka_brokers_sasl` field.
   2. Click **Configure** to configure access to the message broker. To authenticate from {{site.data.keyword.codeengineshort}} to your Kafka or {{site.data.keyword.messagehub}} instance, you need to provide a message broker access secret.
        * You can create a new secret, choose an existing secret, or if credentials are not required to access the message brokers, then choose `None`.
        * To create a secret, click **Create**. Provide a name for the secret, and values for `username` and `password`. The values for `username` and `password` must match the values in the service credentials for the Kafka or {{site.data.keyword.messagehub}} instance. For example, the value for `username` is the value of `user` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. The value for `password` is the value of `apikey` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance.
        * For this example, use the existing `kafka-subscription-secret` secret that was previously created.
   3. Specify the name of existing topics for the message queues. For example, `kafka-topic1`. To obtain information about existing topics for your service instance, go to your service instance in the {{site.data.keyword.messagehub}} console and view **Topics**.
   4. (Optional) Specify a consumer group. Consumers of Kafka messages can be grouped into [consumer groups](/docs/EventStreams?topic=EventStreams-consuming_messages#consumer_groups). If you are using consumer groups, the topic configuration controls the message flow to consumers in the consumer group. Whenever a consumer is added to or removed from a consumer group, the message flow from that topic might change. This action can cause existing consumers to no longer receive messages from that topic.
   5. Click **Next** to proceed.
7. For **Event consumer**, specify the {{site.data.keyword.codeengineshort}} application to receive events. Notice that you can choose from a list of defined applications and jobs, or you can provide a name for an app (or job) that is not yet created. It is not necessary that the app or job exist when you create the event subscription with the console. However, when the subscription is created, the status of the subscription reflects that the consumer does not exist. You must create the app or job before the subscription is in a ready state and can receive events through this subscription. For this example, use the `kafka-receiver-app` application that references the `icr.io/codeengine/kafka-receiver` image. If your app does not exist, provide the name of your application and [create your application](/docs/codeengine?topic=codeengine-deploy-app&interface=ui#deploy-app-console) after you create the Kafka subscription. For applications only, you can optionally specify a path. By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by specifying a path. For example, if your subscription path specifies `/events`, the events are sent to `https://<base application URL>/events`. Click **Next** to proceed.
8. For **Summary**, review the settings for your Kafka event subscription and make changes, if needed. When ready, click **Create** to create the Kafka subscription.

#### Sending events to the receiving app from the console
{: #sending-kafka-events-app-ui}

 Now that your Kafka event subscription, which references the `kafka-receiver-app` application, is created, use the `kafka-sender-app` to send message events to the receiver application.
 {: shortdesc}

 1. Start logging for the receiver application to [view application logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-appjobfunctionlogs-ui) to see events.
 2. (optional) Start logging for the sender application to [view application logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-appjobfunctionlogs-ui) to see information about events that are sent.
 3. After logging is started, call the `kafka-sender-app` application with `curl` and specify the public URL of the `kafka-sender-app`, the name of your topic, and the number of messages to send. You can obtain the public URL of this application from the **Domain mappings** tab for your application. For example,

    ```txt
    curl "<public_URL_of_Kafka_sender_app>?topic=<your_topic_name>&num=<number_of_messages_to_produce>"
    ```
    {: pre}

Be sure to wrap the value to curl in quotation marks to ensure that it is treated as a single string.
{: tip}




### Subscribing to Kafka events for an app with the CLI
{: #subscribe-kafka-app-cli}

You can use the CLI to set up a Kafka event subscription so that events are sent to a {{site.data.keyword.codeengineshort}} application.
{: shortdesc}


Events are sent to applications as HTTP POST requests. For more information about the information that is included with Kafka events, see [HTTP headers and body information for events](#subkafka-headerbody-app). If your event is sent to a {{site.data.keyword.codeengineshort}} job, the job receives events as environment variables. For more information about the environment variables for Kafka subscriptions, see [Environment variables for events](#subkafka-envvar-job).
{: important}

#### Creating a {{site.data.keyword.codeengineshort}} app to receive Kafka events with the CLI
{: #create-kafka-receiverapp-cli}


Before you begin

* [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. [Create an {{site.data.keyword.codeengineshort}} application](/docs/codeengine?topic=codeengine-deploy-app&interface=cli#deploy-app-cli) to act as an event consumer of Kafka messages and receive the Kafka events. For example, create an application that is called `kafka-receiver-app2` that uses the `icr.io/codeengine/kafka-receiver` image. This image is built from `receiver.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample does not require any environment variables. You can optionally specify the `--min-scale=1` option, such that the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. If you are running in a production environment, consider the cost of keeping a running instance of your app or whether you want {{site.data.keyword.codeengineshort}} to autoscale to zero. By default, the app scales to zero when not in use.

    ```txt
    ibmcloud ce app create -n kafka-receiver-app2 --image icr.io/codeengine/kafka-receiver --min-scale 1
    ```
    {: pre}

    By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /event`, the event is sent to `https://<base application URL>/events`.
    {: note}


2. After you deploy this app, run the **`app get`** command to confirm that the app is in `ready` status.

    ```txt
    ibmcloud ce app get -n kafka-receiver-app2
    ```
    {: pre}


#### Creating a {{site.data.keyword.codeengineshort}} Kafka event subscription for an app with the CLI
{: #create-kafka-subscription-app-cli}

You can create a Kafka event subscription, which defines the relationship between the Kafka producer (sender) and consumer (receiver) of events, with the CLI.
{: shortdesc}

1. Create a {{site.data.keyword.codeengineshort}} Kafka event subscription for your Kafka events by using the [**`ibmcloud ce sub kafka create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create) command. Use the `kafka-subscription-secret` secret that you previously created to access the message broker. Specify the broker information based on the service credentials information for your Kafka resource. For this example, you can obtain the broker information from the output of the `ibmcloud resource service-key myeventstream-key` command. Notice that you must specify a `--broker` option for each broker for your topic. The `--destination` option specifies the {{site.data.keyword.codeengineshort}} resource that receives the events.

    ```txt
    ibmcloud ce sub kafka create --name mykafkasubscription --destination kafka-receiver-app2 --secret kafka-subscription-secret --topic kafka-topic1 --broker broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker  broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    ```
    {: pre}

2. Display the details of the Kafka event subscription.

    ```txt
    ibmcloud ce sub kafka get -n mykafkasubscription
    ```
    {: pre}

    Example output

    ```txt
    Getting Kafka event subscription 'mykafkasubscription'...
    OK

    Name:          mykafkasubscription
    [...]
    Destination Type:                 app
    Destination:                      kafka-receiver-app2
    Brokers:
    broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    Consumer Group:                   knative-kafka-source-a4072fe1-1dfa-4470-9d07-bf7a0ff8e340
    Topics:
    kafka-topic1
    Secret key reference (user):      kafka-subscription-secret.username
    Secret key reference (password):  kafka-subscription-secret.password
    Ready:                            true

    Conditions:
    Type                     OK    Age  Reason
    ConnectionEstablished    true  24s
    InitialOffsetsCommitted  true  24s
    Ready                    true  24s
    Scheduled                true  24s
    SinkProvided             true  24s

    Events:
    Type     Reason           Age  Source                  Messages
    Normal   FinalizerUpdate  26s  kafkasource-controller  Updated "mykafkasubscription" finalizers
    ```
    {: screen}


#### Sending events to the receiving app with the CLI
{: #sending-kafka-events-app-cli}

 Now that your Kafka event subscription, which references the `kafka-receiver-app` application, is created, use the `kafka-sender-app` to send message events to the receiver application.
 {: shortdesc}


 1. Obtain the public URL of the destination app, `kafka-sender-app` by using the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command with the `--output url` option to find the URL of your app.

    ```txt
    ibmcloud ce app get -n kafka-sender-app --output url
    ```
    {: pre}

    Example output

    ```txt
    https://kafka-sender-app.abcdabcdabc.us-south.codeengine.appdomain.cloud
    ```
    {: screen}


 2. Run the Kafka event producer app, `kafka-sender-app` to send events to the destination {{site.data.keyword.codeengineshort}} application. Call the `kafka-sender-app` application with `curl` and specify values for the topic and the number of messages. Use the output of the **`ibmcloud ce app get`** command to find the public URL of your app. Be sure to wrap the value to curl in quotation marks to ensure that it is treated as a single string.

    ```txt
    curl "<public_URL_of_Kafka_sender_app>?topic=<your_topic_name>&num=<number_of_messages_to_produce>"
    ```
    {: pre}

    For example,

    ```txt
    curl "https://kafka-sender-app.abcdabcdabc.us-south.codeengine.appdomain.cloud?topic=kafka-topic1&num=1"
    ```
    {: pre}

 3. View events in logs. When your Kafka event subscription is created with a broker, topics and an access secret that are valid, and you have a Kafka application that produces messages on that topic (such as `kafka-sender-app`), then you can see events in logs for your destination {{site.data.keyword.codeengineshort}} application that receives Kafka messages, such as `kafka-receiver-app`. When you use the Kafka receiver app (`icr.io/codeengine/kafka-receiver`), search for `Event data` in the logs for the receiver application to see the messages that are received.

    ```txt
    ibmcloud ce app logs -n kafka-receiver-app2
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of application 'kafka-receiver-app2'...
    OK

    kafka-receiver-app2-00001-deployment-66976f7988-9xttm/user-container:
    2022/03/31 22:19:45 Listening on port 8080
    2022/03/31 22:19:46 ----------
    2022/03/31 22:19:46 Path: /
    2022/03/31 22:19:46 Header: Accept-Encoding=[gzip]
    2022/03/31 22:19:46 Header: Ce-Id=[partition:0/offset:167]
    2022/03/31 22:19:46 Header: Ce-Source=[/apis/v1/namespaces/glxo4k7nj7d/kafkasources/mykafkasubscription#kafka-topic1]
    2022/03/31 22:19:46 Header: Ce-Specversion=[1.0]
    2022/03/31 22:19:46 Header: Ce-Subject=[partition:0#167]
    2022/03/31 22:19:46 Header: Ce-Time=[2022-03-31T22:19:36.499Z]
    2022/03/31 22:19:46 Header: Ce-Type=[dev.knative.kafka.event]
    2022/03/31 22:19:46 Header: Content-Length=[8]
    2022/03/31 22:19:46 Header: Forwarded=[for=172.30.208.213;proto=http, for=127.0.0.6]
    2022/03/31 22:19:46 Header: K-Proxy-Request=[activator]
    2022/03/31 22:19:46 Header: Traceparent=[00-b033708685c715a7c2384cdf05797785-65540b0937e9b0ce-00]
    2022/03/31 22:19:46 Header: User-Agent=[Go-http-client/1.1]
    2022/03/31 22:19:46 Header: X-B3-Parentspanid=[e1a785d7fdbead6c]
    2022/03/31 22:19:46 Header: X-B3-Sampled=[1]
    2022/03/31 22:19:46 Header: X-B3-Spanid=[abcde9901e6bf83f]
    2022/03/31 22:19:46 Header: X-B3-Traceid=[abcde490a426573772fa0bf60caf5ddb]
    2022/03/31 22:19:46 Header: X-Envoy-Attempt-Count=[1]
    2022/03/31 22:19:46 Header: X-Forwarded-For=[172.30.208.213, 127.0.0.6, 127.0.0.6]
    2022/03/31 22:19:46 Header: X-Forwarded-Proto=[http]
    2022/03/31 22:19:46 Header: X-Request-Id=[abcdeb4e-c5ac-abcd-abcd-60e6278abcde]
    2022/03/31 22:19:46 Event data: test1: 1
    ```
    {: screen}

    Note that log information for apps lasts for only one hour. For more information about viewing logs for apps (or jobs), see [Viewing logs](/docs/codeengine?topic=codeengine-logging).


### Header and body information for Kafka events that are delivered to apps
{: #subkafka-headerbody-app}

All events that are delivered to applications are received as HTTP POST messages. Events contain certain HTTP headers that help you to quickly determine key bits of information about the events without looking at the body (business logic) of the event. For more information, see the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

#### Headers for apps
{: #subkafka-header}

| Header   | Description      |
|----------|------------------|
| `ce-id` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. |
| `ce-source` | A URI-reference that indicates where this event originated from within the event producer. For Kafka events, this header is in the following format: `/apis/v1/namespaces/[PROJECT_SUBDOMAIN]/kafkasources/[KAFKA_SUBSCRIPTION_NAME]#[TOPIC_NAME]`. |
| `ce-specversion` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `ce-subject` | The Kafka partition number and offset. For example, `partition:0#1` refers to partition `0` and offset `1`. |
| `ce-time` | The time that the event was generated. |
| `ce-type` | The type of the event. For Kafka events, this is `dev.knative.kafka.event`. |
{: caption="Header files for events" caption-side="bottom"}

Example output

```txt
Ce-Id=[partition:0/offset:0]
Ce-Source=[/apis/v1/namespaces/ewgz38l13ts/kafkasources/mykafkasubscription#kafka-topic1]
Ce-Specversion=[1.0]
Ce-Subject=[partition:0#0]
Ce-Time=[2021-09-27T16:39:01.36Z]
Ce-Type=[dev.knative.kafka.event]
```
{: screen}

#### HTTP body for apps
{: #subkafka-body}

The HTTP body contains the Kafka message and is in the format that you specify when you create or update the subscription.


## Setting up {{site.data.keyword.codeengineshort}} to receive Kafka events for a job
{: #subscribe-kafka-job}

For {{site.data.keyword.codeengineshort}} to work with Kafka events, use the console or CLI to set up a {{site.data.keyword.codeengineshort}} Kafka eventing subscription to connect to Kafka event brokers and listen for Kafka events. Also, set up a {{site.data.keyword.codeengineshort}} job (or app) to act as the receiver of the Kafka events. The Kafka event subscription defines the relationship between the Kafka producer (sender) and consumer (receiver) of events.
{: shortdesc}

### Subscribing to Kafka events for a job from the console
{: #subscribe-kafka-job-ui}

You can use the console to set up a Kafka event subscription so that events are sent to a {{site.data.keyword.codeengineshort}} job.
{: shortdesc}

When you create an event subscription for a job, a job run is created for each event that is triggered. This job run has the environment variables that are related to the job. The {{site.data.keyword.codeengineshort}} Kafka event subscription connects to your Kafka message broker and sends environment variables that are related to the job. For more information about the environment variables that are sent by Kafka, see [Environment variables for events](#subkafka-envvar-job).
{: important}


#### Creating a {{site.data.keyword.codeengineshort}} job to receive Kafka events from the console
{: #subscribe-kafka-receiverjob-ui}

1. [Create an {{site.data.keyword.codeengineshort}} job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) to act as an event consumer of Kafka messages and receive the Kafka events. For example, create a job that is called `kafka-receiver-job` that uses the sample `icr.io/codeengine/codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}. This sample does not require any environment variables.
2. After you create this job, confirm that it is in `ready` status.

When you use the console, it is not necessary that the app or job that you use to receive Kafka events exist before you create the Kafka event subscription. However, if the app or job does not exist when you create the event subscription, the status of the subscription reflects that the consumer does not exist. You must create the app or job before the subscription is in a ready state and can receive events through this subscription.
{: note}

#### Creating a {{site.data.keyword.codeengineshort}} Kafka event subscription for a job from the console
{: #subscribe-kafka-esub-job-ui}

The Kafka event subscription defines the relationship between the Kafka producer (sender) and consumer (receiver) of events.
{: shortdesc}

Before you begin

* Determine the Code Engine project that you want to use and make sure that this project is selected. See [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

Complete the following steps to create a Kafka event subscription for an application from the console.

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Event subscriptions**.
3. From the Event subscriptions page, click **Create** to create your subscription.
4. From the Create an event subscription page, select the `Event Streams / Kafka` tile to specify the event type.
5. For **General**, provide a name for the `Event Streams / Kafka` subscription. Click **Next** to proceed.
6. For **Message broker details**,
   1. Specify the Kafka message broker hosts for the message queues from which messages are received as events through this subscription. To obtain information about the broker hosts, topics, and access credentials, view the service credential details for your service instance in the {{site.data.keyword.messagehub}} console. For example, specify `"broker-0-abcdabcdabcdabcd.kafka.svc01.us-south.eventstreams.cloud.ibm.com:9093", "broker-1-abcdabcdabcdabcd.kafka.svc01.us-south.eventstreams.cloud.ibm.com:9093"` for the message broker hosts for the `myeventstream-key` service instance.
   2. Click **Configure** to configure access to the message broker. To authenticate from {{site.data.keyword.codeengineshort}} to your Kafka or {{site.data.keyword.messagehub}} instance, you need to provide a message broker access secret.
        * You can create a new secret, choose an existing secret, or if credentials are not required to access the message brokers, then choose `None`.
        * To create a secret, click **Create**. Provide a name for the secret, and values for `username` and `password`. The values for `username` and `password` must match the values in the service credentials for the Kafka or {{site.data.keyword.messagehub}} instance. For example, the value for `username` is the value of `user` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. The value for `password` is the value of `apikey` that is listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance.
        * For this example, use the existing `kafka-subscription-secret` secret that was previously created.
   3. Specify the name of existing topics for the message queues. For example, `kafka-topic1`. To obtain information about existing topics for your service instance, go to your service instance in the {{site.data.keyword.messagehub}} console and view **Topics**.
   4. (Optional) Specify a consumer group. Consumers of Kafka messages can be grouped into [consumer groups](/docs/EventStreams?topic=EventStreams-consuming_messages#consumer_groups). If you are using consumer groups, the topic configuration controls the message flow to consumers in the consumer group. Whenever a consumer is added to or removed from a consumer group, the message flow from that topic might change. This action can cause existing consumers to no longer receive messages from that topic.
   5. Click **Next** to proceed.
7. For **Event consumer**, specify the {{site.data.keyword.codeengineshort}} job to receive events. Notice that you can choose from a list of defined jobs and apps, or you can provide a name for a job (or app) that is not yet created. It is not necessary that the app or job exist when you create the event subscription with the console. However, when the subscription is created, the status of the subscription reflects that the consumer does not exist. You must create the job (or app) before the subscription is in a ready state and can receive events through this subscription. For this example, select `job` as the component type, and use the `kafka-receiver-job` job that references the `icr.io/codeengine/codeengine` image as the component to receive events. If your job does not exist, provide the name of your job and [create your job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) after you create the Kafka subscription. For applications only, you can optionally specify a path. Click **Next** to proceed.
8. For **Summary**, review the settings for your Kafka event subscription and make changes, if needed. When ready, click **Create** to create the Kafka subscription.

#### Sending events to the receiving job from the console
{: #sending-kafka-events-job-ui}

 Now that your Kafka event subscription, which references the `kafka-receiver-job` job, is created, use the `kafka-sender-app` to send message events to the receiver job.
 {: shortdesc}

 1. Start logging for the receiver job to [view job logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-appjobfunctionlogs-ui) to see events.
 2. (optional) Start logging for the sender application to [view application logs from the console](/docs/codeengine?topic=codeengine-logging&interface=ui#view-appjobfunctionlogs-ui) to see information about events that are sent.
 3. After logging is started, call the `kafka-sender-app` application with `curl` and specify the public URL of the `kafka-sender-app`, the name of your topic, and the number of messages to send. You can obtain the public URL of this application from the **Domain mappings** tab for your application. For example,

    ```txt
    curl "<public_URL_of_Kafka_sender_app>?topic=<your_topic_name>&num=<number_of_messages_to_produce>"
    ```
    {: pre}

Be sure to wrap the value to curl in quotation marks to ensure that it is treated as a single string.
{: tip}

When your Kafka subscription is created with a broker, topics and an access secret that are valid, and you have a Kafka job that produces messages on that topic (such as `kafka-sender-app`), then you can see events in logs for your {{site.data.keyword.codeengineshort}} job that receives Kafka messages, such as `kafka-receiver-job`. When you use the Kafka receiver job (`icr.io/codeengine/codeengine`), search for `CE_DATA` in the logs for the receiver job to see the messages that are received.

### Subscribing to Kafka events for a job with the CLI
{: #subscribe-kafka-job-cli}

You can use the CLI to set up a Kafka event subscription so that events are sent to a {{site.data.keyword.codeengineshort}} job.
{: shortdesc}

When you create an event subscription for a job, a job run is created for each event that is triggered. This job run has the environment variables that are related to the job. The {{site.data.keyword.codeengineshort}} Kafka event subscription connects to your Kafka message broker and sends environment variables that are related to the job. For more information about the environment variables that are sent by Kafka, see [Environment variables for events](#subkafka-envvar-job).
{: important}

#### Creating a {{site.data.keyword.codeengineshort}} job to receive Kafka events with the CLI
{: #subscribe-kafka-receiverjob-cli}


Before you begin

* [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).

* [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

1. [Create an {{site.data.keyword.codeengineshort}} job](/docs/codeengine?topic=codeengine-create-job#create-job-ui) to act as an event consumer of Kafka messages and receive the Kafka events. For example, create a job that is called `kafka-receiver-job` that uses the `icr.io/codeengine/codeengine` image. This image is built from `codeengine.go`, available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.

    ```txt
    ibmcloud ce job create -n kafka-receiver-job --image icr.io/codeengine/codeengine
    ```
    {: pre}


2. (optional) After you create this job, run the **`job get`** command to view information about this job.

    ```txt
    ibmcloud ce job get -n kafka-receiver-job
    ```
    {: pre}


#### Creating a {{site.data.keyword.codeengineshort}} Kafka event subscription for a job with the CLI
{: #subscribe-kafka-esub-job-cli}

You can create a Kafka event subscription, which defines the relationship between the Kafka producer (sender) and consumer (receiver) of events, with the CLI.
{: shortdesc}

1. Create a {{site.data.keyword.codeengineshort}} Kafka event subscription for your Kafka events by using the [**`ibmcloud ce sub kafka create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create) command. Use the `kafka-subscription-secret` secret that you previously created to access the message broker. Specify the broker information based on the service credentials information for your Kafka resource. For this example, you can obtain the broker information from the output of the `ibmcloud resource service-key myeventstream-key` command. Notice that you must specify a `--broker` option for each broker for your topic. The `--destination` option specifies the {{site.data.keyword.codeengineshort}} resource that receives the events. When you work with a receiving job, you must also specify the `--destination-type` option to specify the resource is a job, as the default for this option is `app`.

    ```txt
    ibmcloud ce sub kafka create --name mykafkasubscription-withjob --destination-type job --destination kafka-receiver-job --secret kafka-subscription-secret --topic kafka-topic1 --broker broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker  broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    ```
    {: pre}

2. Display the details of the Kafka event subscription.

    ```txt
    ibmcloud ce sub kafka get -n mykafkasubscription-withjob
    ```
    {: pre}

    Example output

    ```txt
    Getting Kafka event subscription 'mykafkasubscription-withjob'...
    OK

    Name:          mykafkasubscription-withjob
    [...]
    Destination Type:                 job
    Destination:                      kafka-receiver-job
    Brokers:
    broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    Consumer Group:                   knative-kafka-source-a4072fe1-1dfa-4470-9d07-bf7a0ff8e340
    Topics:
    kafka-topic1
    Secret key reference (user):      kafka-subscription-secret.username
    Secret key reference (password):  kafka-subscription-secret.password
    Ready:                            true
    [...]
    ```
    {: screen}


#### Sending events to the receiving job with the CLI
{: #sending-kafka-events-job-cli}

 Now that your Kafka event subscription, which references the `kafka-receiver-job` application, is created, use the `kafka-sender-app` to send message events to the receiver application.
 {: shortdesc}


 1. Obtain the public URL of the destination app, `kafka-sender-app` by using the [**`ibmcloud ce app get`**](/docs/codeengine?topic=codeengine-cli#cli-application-get) command to find the URL of your app.

    ```txt
    ibmcloud ce app get -n kafka-sender-app --output url
    ```
    {: pre}

    Example output

    ```txt
    https://kafka-sender-app.abcdabcdabc.us-south.codeengine.appdomain.cloud
    ```
    {: screen}


 2. Run the Kafka event-producer app, `kafka-sender-app` to send events to the destination {{site.data.keyword.codeengineshort}} job. Call the `kafka-sender-app` application with `curl` and specify values for the topic and the number of messages. Use the output of the **`ibmcloud ce app get`** command to find the public URL of your event-producing app. Be sure to wrap the value to curl in quotation marks to ensure that it is treated as a single string. For example,

    ```txt
    curl "<public_URL_of_Kafka_sender_app>?topic=<your_topic_name>&num=<number_of_messages_to_produce>"
    ```
    {: pre}

    For example,

    ```txt
    curl "https://kafka-sender-app.abcdabcdabc.us-south.codeengine.appdomain.cloud?topic=kafka-topic1&num=1"
    ```
    {: pre}


 3. View events in logs. When your Kafka event subscription is created with a broker, topics and an access secret that are valid, and you have a Kafka app that produces messages on that topic (such as `kafka-sender-app`), then you can see events in logs for your destination {{site.data.keyword.codeengineshort}} job that receives Kafka messages, such as `kafka-receiver-job`. For each message that is sent by using `curl`, the same number of job runs are triggered by the Kafka events. To view the events sent to jobs, use the **`ibmcloud ce jobrun logs`** command.

    1. Use the **`ibmcloud ce jobrun list`** command to list the job runs for the `kafka-receiver-job` job.

        ```txt
        ibmcloud ce jobrun list --job kafka-receiver-job
        ```
        {: pre}

    2. Use the **`ibmcloud ce jobrun logs`** command to obtain the logs for a specific job run.

        ```txt
        ibmcloud ce jobrun logs -n kafka-receiver-job-abcde
        ```
        {: pre}

        Example output

        ```txt
        Getting logs for all instances of job run 'kafka-receiver-job-abcde'...
        Getting jobrun 'kafka-receiver-job-abcde'...
        Getting instances of jobrun 'kafka-receiver-job-abcde'...
        OK

        kafka-receiver-job-abcde-0-0/kafka-receiver-job:
        Hello from helloworld! I'm a batch job! Index: 0

        Hello World from:
        . ___  __  ____  ____
        ./ __)/  \(    \(  __)
        ( (__(  O )) D ( ) _)
        .\___)\__/(____/(____)
        .____  __ _   ___  __  __ _  ____
        (  __)(  ( \ / __)(  )(  ( \(  __)
        .) _) /    /( (_ \ )( /    / ) _)
        (____)\_)__) \___/(__)\_)__)(____)

        Some Env Vars:
        --------------
        CE_DATA=test1: 2
        CE_DOMAIN=us-south.codeengine.appdomain.cloud
        CE_ID=partition:0/offset:249
        CE_JOB=kafka-receiver-job
        CE_JOBRUN=kafka-receiver-job-abcde
        CE_SOURCE=/apis/v1/namespaces/p99k7iy919d/kafkasources/kafkasub-job-ui#kafka-topic1
        CE_SPECVERSION=1.0
        CE_SUBDOMAIN=p99k7iy919d
        CE_SUBJECT=partition:0#249
        CE_TIME=2022-06-21T12:19:24.06Z
        CE_TYPE=dev.knative.kafka.event
        HOME=/root
        HOSTNAME=kafka-receiver-job-abcde-0-0
        JOB_INDEX=0
        KUBERNETES_PORT=tcp://172.21.0.1:443
        KUBERNETES_PORT_443_TCP=tcp://172.21.0.1:443
        KUBERNETES_PORT_443_TCP_ADDR=172.21.0.1
        KUBERNETES_PORT_443_TCP_PORT=443
        KUBERNETES_PORT_443_TCP_PROTO=tcp
        KUBERNETES_SERVICE_HOST=172.21.0.1
        KUBERNETES_SERVICE_PORT=443
        KUBERNETES_SERVICE_PORT_HTTPS=443
        PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
        PWD=/
        SHLVL=1
        z=Set env var 'SHOW' to see all variables
        ```
        {: screen}

    When you use the Kafka receiver job (`icr.io/codeengine/codeengine`), search for `CE_DATA` in the logs for the receiver job to see the messages that are received.

    Note that log information for job runs lasts for only one hour. For more information about viewing logs for apps or jobs, see [Viewing logs](/docs/codeengine?topic=codeengine-logging).



### Environment variables for Kafka events that are delivered to jobs
{: #subkafka-envvar-job}

All events that are delivered to a job are received as environment variables. These environment variables include a prefix of `CE_` and are based on the [`CloudEvents` spec](https://cloudevents.io){: external}.
{: shortdesc}

Each event contains some common environment variables that appear every time that the event is delivered to a job. The actual set of variables in each event can include more options. For more information, see the [`CloudEvent` attributes](https://github.com/cloudevents/spec/blob/v1.0.1/spec.md#context-attributes){: external}.

The following table describes the environment variables that are specific to Kafka events.

| Variable   | Description      |
|----------|------------------|
| `CE_DATA` | The data (body) for the event. |
| `CE_DOMAIN` | The domain name portion of the URL of the application (and project). |
| `CE_ID` | A unique identifier for the event, unless an event is replayed, in which case, it is assigned the same ID. |
| `CE_SOURCE` | A URI-reference that indicates where this event originated from within the event producer. For Kafka events, this header is in the following format: `/apis/v1/namespaces/[PROJECT_SUBDOMAIN]/kafkasources/kafkasub#[TOPIC_NAME]`. |
| `CE_SPECVERSION` | The version of the `CloudEvents` spec. This value is always `1.0`. |
| `CE_SUBDOMAIN` | The subdomain portion of the URL associated with the application (and project). If you are familiar with Kubernetes, CE_SUBDOMAIN maps to the Kubernetes namespace associated with your project. |
| `CE_SUBJECT` | The Kafka partition number and offset. For example, `partition:0#1` refers to partition `0` and offset `1`. |
| `CE_TIME` | The time that the event was generated. |
| `CE_TYPE` | The type of the event. For Kafka events, this is `dev.knative.kafka.event`. |
{: caption="Environment variables for events" caption-side="bottom"}

Example output

```txt
CE_DATA={"message":"This is a test message #","message_number":1}
CE_DOMAIN=us-south.codeengine.appdomain.cloud
CE_ID=partition:0/offset:46
CE_SOURCE=/apis/v1/namespaces/ewgz38l13ts/kafkasources/mykafkasubscription-job#kafka-topic1
CE_SPECVERSION=1.0
CE_SUBDOMAIN=ewgz38l13ts
CE_SUBJECT=partition:0#46
CE_TIME=2021-09-27T18:02:17.7Z
CE_TYPE=dev.knative.kafka.event
```
{: screen}


## Viewing and updating Kafka event subscriptions
{: #sub-kafka-view-update}

You can view details about your Kafka event subscription or update the subscription.
{: shortdesc}

### Viewing and updating Kafka event subscriptions from the console
{: #sub-kafka-view-update-ui}

* To view information about your event subscriptions
    1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
    2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions.

* To update an event subscription
    1. Go to your subscription page. To navigate to your subscription page, go to the Event subscriptions page, and click the name of the subscription that you want to update.
    2. Update the subscription. For example, change the topic for a Kafka subscription to a different topic. From the **Message broker details** tab, remove the existing topic from the Topics section and add the name of your new topic.
    3. Click **Save** to save your changes.

### Viewing and updating Kafka event subscriptions with the CLI
{: #sub-kafka-view-update-cli}


* To view information about your event subscriptions with the CLI, use the [**`ibmcloud ce subscription kafka get`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-get) command.

    ```txt
    ibmcloud ce sub kafka get -n mykafkasubscription
    ```
    {: pre}

    Example output

    ```txt
    Getting Kafka event subscription 'mykafkasubscription'...
    OK

    Name:               mykafkasubscription
    ID:                 abcdefgh-abcd-abcd-abcd-1a2b3c4d5e6f
    Project Name:       myproject
    Project ID:         01234567-abcd-abcd-abcd-abcdabcd1111
    Age:                2m4s
    Created:            2022-06-18T16:59:12-04:00

    Destination Type:                 app
    Destination:                      kafka-receiver-app2
    Brokers:
    broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    Consumer Group:                   knative-kafka-source-c577b304-dccd-40c8-bb62-138c39f6112a
    Topics:
    kafka-topic1
    Secret key reference (user):      kafka-subscription-secret.username
    Secret key reference (password):  kafka-subscription-secret.password
    Ready:                            true

    Conditions:
    Type                     OK    Age  Reason
    ConnectionEstablished    true  53m
    InitialOffsetsCommitted  true  53m
    Ready                    true  52m
    Scheduled                true  52m
    SinkProvided             true  53m

    Events:
    Type     Reason           Age                Source                  Messages
    Normal   FinalizerUpdate  53m                kafkasource-controller  Updated "mykafkasubscription" finalizers
    ```
    {: screen}


* To update an event subscription with the CLI, use the [**`ibmcloud ce subscription kafka update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-update) command. The following example updates the topic name.

    ```txt
    ibmcloud ce sub kafka update -n mykafkasubscription --topic kafka-topic2
    ```
    {: pre}

    You can use the [**`ibmcloud ce subscription kafka update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-update) command to update the values for the Kafka subscription. However, you cannot modify the value for the consumer group with this command. If you want to update the subscription to reference a different topic, make sure that the Kafka topic exists before you update the subscription.
    {: tip}

## Deleting a Kafka event subscription
{: #sub-kafka-delete}

When you no longer need a Kafka subscription, you can delete it.
{: shortdesc}

When you delete a subscription, the service credentials for the {{site.data.keyword.messagehub}} service instance is used to remove consumer groups from the {{site.data.keyword.messagehub}} service instance. If the service credential is already deleted or if it is invalid when you delete the subscription, the consumer groups cannot be removed from the {{site.data.keyword.messagehub}} service instance. Your {{site.data.keyword.codeengineshort}} Kafka event subscription delete request fails.
{: note}

### Deleting a Kafka subscription from the console
{: #sub-kafka-delete-ui}

1. From the [{{site.data.keyword.codeengineshort}} Projects page](https://cloud.ibm.com/codeengine/projects){: external}, go to your project.
2. From the Overview page, click **Event subscriptions** to view a listing of defined subscriptions.
3. From the list of subscriptions, delete the subscription that you want to remove from your application or job.

If you delete an app or a job that is associated with the subscription, the subscription is not deleted. If you re-create the application or job (or another app or job  with the same name), your subscription reconnects with the app or job.
{: note}

### Deleting a Kafka subscription with the CLI
{: #sub-kafka-delete-cli}

You can delete a Kafka subscription by running the [**`ibmcloud ce subscription kafka delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-delete) command.

For example, use the following command to delete a Kafka subscription that is called `mykafkasubscription`,

```txt
ibmcloud ce subscription kafka delete --name mykafkasubscription
```
{: pre}

If you delete an app or a job that is associated with the subscription, the subscription is not deleted. Instead, it moves to ready state of `false` because the subscription depends on the availability of the app or job. If you re-create the application or job (or another app or job  with the same name), your subscription reconnects and the Ready state is `true`.
{: note}


## Defining additional event attributes
{: #additional-attributes-kafka}

When you create a subscription, you can define additional `CloudEvent` attributes to be included in any events that are generated. These attributes appear similar to any other `CloudEvent` attribute in the delivery of the event. If you choose to specify the name of an existing `CloudEvent` attribute, then it overrides the original value that was included in the event.

To define addition attributes, use the `--extension` options with the [**`ibmcloud ce subscription kafka create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create) CLI command.

For more information, see [Can I use other `CloudEvents` specifications?](/docs/codeengine?topic=codeengine-subscribing-events#subscribing-events-cloudevents)
