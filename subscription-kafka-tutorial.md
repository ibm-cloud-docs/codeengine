---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-15"

keywords: tutorial code engine, subscription tutorial for code engine, eventing and code engine, subscriptions, subscribing, tutorial for code engine, eventing tutorial for code engine, subscription, kafka, kafka event, event producers, kafka event producer

subcollection: codeengine

content-type: tutorial
completion-time: 20m 

---

{{site.data.keyword.attribute-definition-list}}

# Subscribing to Kafka events
{: #subscribe-kafka-tutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="20m"}

With this tutorial, you can learn how to subscribe to Kafka events by using the {{site.data.keyword.codeenginefull}} CLI.
{: shortdesc}

Oftentimes in distributed environments you want your applications or jobs to react to messages (events) that are generated from other components, which are usually called event producers. With {{site.data.keyword.codeengineshort}}, your applications or jobs can receive events of interest by subscribing to event producers. 
{: shortdesc}

Event information is received as POST HTTP requests for applications and as environment variables for jobs.


The Kafka event producer watches for new messages to appear in a Kafka instance. When you create a {{site.data.keyword.codeengineshort}} Kafka subscription for a set of topics, your app or job receives a separate event for each new message that appears in one of the topics.


While you can use any Kafka instance, the examples in this tutorial use the {{site.data.keyword.messagehub_full}} service. {{site.data.keyword.messagehub}} is an IBM event streaming service for Kafka events. For more information about this service, see [{{site.data.keyword.messagehub}} documentation](/docs/EventStreams?topic=EventStreams-about).
{: note}  

Before you begin

- [Set up your {{site.data.keyword.codeengineshort}} CLI environment](/docs/codeengine?topic=codeengine-install-cli).
- [Set up your {{site.data.keyword.messagehub}} CLI](/docs/EventStreams?topic=EventStreams-cli_reference).
- [Create and work with a project](/docs/codeengine?topic=codeengine-manage-project).

All {{site.data.keyword.codeengineshort}} users are required to have a Pay-as-you-Go account. Tutorials might incur costs. Use the Cost Estimator to generate a cost estimate based on your projected usage. For more information, see [{{site.data.keyword.codeengineshort}} pricing](/docs/codeengine?topic=codeengine-pricing).
{: note}


## Setting up the Kafka event producer 
{: #tutkafka-setup-sender}
{: step}

You can set up your Kafka message producer to send messages to {{site.data.keyword.codeengineshort}} Kafka event subscriptions. Use your {{site.data.keyword.codeengineshort}} Kafka event subscription to trigger applications or jobs when a Kafka message is received.
{: shortdesc}

To get started, [create an {{site.data.keyword.messagehub}} service instance](/docs/EventStreams?topic=EventStreams-getting-started#getting_started_prereqs) for your event streaming service. While you can use the console or the CLI, the following steps describe how to set up the {{site.data.keyword.messagehub}} event producer with the CLI. 


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



## Setting up a {{site.data.keyword.codeengineshort}} sample app to produce Kafka messages
{: #tutkafka-sender-app}
{: step}

For this tutorial, set up a {{site.data.keyword.codeengineshort}} application to act as an event producer of Kafka messages. The purpose of this `kafka-sender-app` app is to connect to your {{site.data.keyword.messagehub}} instance and to produce (send) Kafka messages to a receiver of the messages (Kafka consumer). This app that produces events for Kafka messages uses the [{{site.data.keyword.codeengineshort}} Kafka sender sample app](https://github.com/IBM/CodeEngine/tree/main/kafka){: external} to send Kafka messages. This sample sender image requires the `BROKERS` environment variable and a secret that includes the `password` credentials.

1. Create a secret with credentials that are required by the {{site.data.keyword.codeengineshort}} Kafka samples. For example, create the `kafka-subscription-secret` secret, to contain the credentials that are required for both the Kafka sender sample app and the Kafka event subscription, which uses the Kafka receiver sample. These credentials are required for the sample Kafka sender app and the {{site.data.keyword.codeengineshort}} Kafka event subscription to communicate with the service instance for {{site.data.keyword.messagehub}}. While it not required that you create this secret before you create the Kafka sender app and the event subscription, this action simplifies the required steps. 

    To create the `kafka-subscription-secret` secret, add a literal environment variable for `password`, and `username`. For more information, see [create a secret with the CLI](/docs/codeengine?topic=codeengine-configmap-secret#secret-creating-cli).

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

2. Create the `kafka-sender-app` with the following information. 
    * Specify the `--image` option to reference the `icr.io/codeengine/kafka-sender` container image. This image is built from `sender.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample sender app requires the `password` credentials that are stored in your `kafka-subscription-secret`, and it requires the `BROKERS` environment variable.
    * Specify the `--env-from-secret` option to reference the full secret, `kafka-subscription-secret`, which contains the `password` credentials.
    * Specify the `--env` option to add a literal environment variable, `BROKERS`, and provide the name of one of the brokers hosts listed in the details of the service credentials in the {{site.data.keyword.messagehub}} service instance. However, if you want to specify more than one broker hostname, use the format `--env BROKERS-broker1,broker2,broker3`.
    * (optional) Specify the `--min-scale=1` option so that the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. If you are running in a production environment, consider the cost of keeping a running instance of your app or whether you want {{site.data.keyword.codeengineshort}} to autoscale to zero. By default, the app scales to zero when not in use.
 
        ```txt
        ibmcloud ce app create --name kafka-sender-app --image icr.io/codeengine/kafka-sender --env-from-secret kafka-subscription-secret --env BROKERS=broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --min-scale 1
        ```
        {: pre}

3. After you deploy this app, run the **`app get`** command to confirm that the app is in `ready` status.

    ```txt
    ibmcloud ce app get -n kafka-sender-app
    ```
    {: pre}


You created the `kafka-sender-app` app to produce Kafka messages for {{site.data.keyword.codeengineshort}} event subscriptions, and you created the `kafka-subscription-secret` secret that contains the required credentials. 

## Setting up a {{site.data.keyword.codeengineshort}} Kafka subscription   
{: #tutkafka-subscribe-setup}
{: step}

For {{site.data.keyword.codeengineshort}} to work with Kafka events, set up a {{site.data.keyword.codeengineshort}} Kafka eventing subscription to connect to Kafka event brokers and listen for Kafka events. Also, set up a {{site.data.keyword.codeengineshort}} app to act as the receiver of the Kafka events. The Kafka event subscription defines the relationship between the Kafka producer (sender) and consumer (receiver) of events.
{: shortdesc} 

The {{site.data.keyword.codeengineshort}} Kafka event subscription connects to your Kafka message broker and sends HTTP Post requests for each incoming Kafka message to the receiver application. For more information about the information that is included with Kafka events, see [HTTP headers and body information for events that are delivered to apps](/docs/codeengine?topic=codeengine-working-kafkaevent-producer#subkafka-headerbody-app).


1. Create a {{site.data.keyword.codeengineshort}} application to act as an event consumer of Kafka messages and receive the Kafka events. For example, create an application that is called `kafka-receiver-app` that uses the `icr.io/codeengine/kafka-receiver` image. This image is built from `receiver.go`, which is available from the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine/tree/main/kafka){: external}. This sample does not require any environment variables. You can optionally specify the `--min-scale=1` option, such that the app always has an instance that is running and does not scale to zero. Configuring the app to always have a running instance is useful when you view logs. If you are running in a production environment, consider the cost of keeping a running instance of your app or whether you want {{site.data.keyword.codeengineshort}} to autoscale to zero. By default, the app scales to zero when not in use.

    ```txt
    ibmcloud ce app create -n kafka-receiver-app --image icr.io/codeengine/kafka-receiver --min-scale 1
    ```
    {: pre}

    By default, events are routed to the root URL of the destination application. You can send events to a different destination within the app by using the `--path` option. For example, if your subscription specifies `--path /event`, the event is sent to `https://<base application URL>/events`.
    {: note}


2. After you deploy this app, run the **`app get`** command to confirm that the app is in `ready` status.

    ```txt
    ibmcloud ce app get -n kafka-receiver-app
    ```
    {: pre}

3. Create a {{site.data.keyword.codeengineshort}} Kafka event subscription for your Kafka events by using the [**`ibmcloud ce sub kafka create`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-create) command. Use the `kafka-subscription-secret` secret that you previously created to access the message broker. Specify the broker information based on the service credentials information for your Kafka resource. For this example, you can obtain the broker information from the output of the `ibmcloud resource service-key myeventstream-key` command. Notice that you must specify a `--broker` option for each broker for your topic. The `--destination` option specifies the {{site.data.keyword.codeengineshort}} resource that receives the events.
 
    ```txt
    ibmcloud ce sub kafka create --name mykafkasubscription --destination kafka-receiver-app --secret kafka-subscription-secret --topic kafka-topic1 --broker broker-3-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-5-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker  broker-0-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-1-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-4-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093 --broker broker-2-abcdabcdabcdabcd.kafka.svc07.us-south.eventstreams.cloud.ibm.com:9093
    ```
    {: pre}

4. Display the details of the Kafka event subscription. 

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
    Destination:                      kafka-receiver-app
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


## Testing your subscription 
{: #tutkafka-test-subscription}
{: step}

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

 2. Run the Kafka event producer app, `kafka-sender-app` to send events to the destination {{site.data.keyword.codeengineshort}} application. Call the `kafka-sender-app` application with `curl` and specify values for the topic and the number of messages. Use the output of the **`ibmcloud ce app get`** command to find the public URL of your app. Be sure to wrap the value to curl in quotation marks to ensure that it is treated as a single string. For example, 

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
    ibmcloud ce app logs -n kafka-receiver-app
    ```
    {: pre}

    Example output

    ```txt
    Getting logs for all instances of application 'kafka-receiver-app'...
    OK

    kafka-receiver-app-00001-deployment-66976f7988-9xttm/user-container:
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

    Note that log information for apps lasts for only one hour. For more information about viewing logs for apps (or jobs), see [Viewing logs](/docs/codeengine?topic=codeengine-view-logs).



## Updating your subscription 
{: #tutkafka-update-subscription}
{: step}

To update an event subscription with the CLI, use the [**`ibmcloud ce subscription kafka update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-update) command. The following example updates the topic name. 

```txt
ibmcloud ce sub kafka update -n mykafkasubscription --topic kafka-topic2
```
{: pre}

You can use the [**`ibmcloud ce subscription kafka update`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-update) command to update the values for the Kafka subscription. However, you cannot modify the value for the consumer group with this command. If you want to update the subscription to reference a different topic, make sure that the Kafka topic exists before you update the subscription. 
{: tip}


## Clean up for Kafka subscription tutorial
{: #tutkafka-delete-subscription}
{: step}

Ready to delete your Kafka subscription, the sending and receiving apps, and the secret? You can use the [**`ibmcloud ce app delete`**](/docs/codeengine?topic=codeengine-cli#cli-application-delete), the [**`ibmcloud ce sub kafka delete`**](/docs/codeengine?topic=codeengine-cli#cli-subscription-kafka-delete), and the [**`ibmcloud ce sub kafka delete`**](/docs/codeengine?topic=codeengine-cli#cli-secret-delete) commands. You can optionally use the `-f` option to force the delete of the component without confirmation.

When you delete the Kafka subscription, the delete does not delete the app that is referenced by the subscription. 
{: note}

To remove your subscription,

```txt
ibmcloud ce sub kafka delete --name mykafkasubscription -f
```
{: pre}


To remove your Kafka message-receiving application,

```txt
ibmcloud ce app delete --name kafka-receiver-app -f
```
{: pre}

Similarly, you can remove the `kafka-sender-app`. 

```txt
ibmcloud ce app delete --name kafka-sender-app -f
```
{: pre}

To remove the `kafka-subscription-secret`,

```txt
ibmcloud ce secret delete --name kafka-subscription-secret -f
```
{: pre}

Ready to delete your service instance for {{site.data.keyword.messagehub}} service instance? The `--recursive` option specifies to remove all resources for the service instance, which includes the associated service key. 

```txt
ibmcloud resource service-instance-delete myeventstream --recursive -f
```
{: pre}


## Next steps
{: #nextsteps-kafkatut}

For more information about working with Kafka event subscriptions, see [Working with the Kafka event producer](/docs/codeengine?topic=codeengine-working-kafkaevent-producer). 

Looking for more code examples? Check out the [Samples for {{site.data.keyword.codeenginefull_notm}} GitHub repo](https://github.com/IBM/CodeEngine){: external}.
{: tip}




