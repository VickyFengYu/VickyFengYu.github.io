RabbitMQ and Kafka
===================


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/system-design/image/kafka.png?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/system-design/image/rabbitmq.png?raw=true)


## <i class="icon-folder-open"></i> 1


One thing to consider is that talking natively (as in bundled in and officially supported) to kafka outside Java it pretty hard. RabbitMQ seems to have a few more languages officially supported

For "random" open source clients from the community I agree; not all a high performance (it pretty hard to write a good client) -- that why I put "That's not necessarily true." ;) However, Confluent's provided C/C++ and Python clients are high throughput and as efficient as the AK Java clients



## <i class="icon-pencil"></i> 2

While RabbitMQ (like IBM MQ or JMS or other messaging solutions in general) is used for traditional messaging, Apache Kafka is used as streaming platform (messaging + distributed storage + processing of data). Both are built for different use cases.

You can use Kafka for "traditional messaging", but not use MQ for Kafka-specific scenarios.

The article “Apache Kafka vs. Enterprise Service Bus (ESB)—Friends, Enemies, or Frenemies? (https://www.confluent.io/blog/apache-kafka-vs-enterprise-service-bus-esb-friends-enemies-or-frenemies/)” discusses why Kafka is not competitive but complementary to integration and messaging solutions (including RabbitMQ) and how to integrate both.


## <i class="icon-file"></i> 3 
 
One critical difference that you guys forgot is RabbitMQ is push based messaging system whereas Kafka is pull based messaging system. This is important in the scenario where messaging system has to satisfy disparate types of consumers with different processing capabilities. With Pull based system the consumer can consume based on their capability where push systems will push the messages irrespective of the state of consumer thereby putting consumer at high risk.


## <i class="icon-pencil"></i> 4


I'll provide an objective answer based on my experience with both, I'll also skip the theory behind them, assuming you already know it and/or other answers has already provided enough.

RabbitMQ: I'd pick this one if my requirements are simple enough to deal with system communication through channels/queues, **retention and streaming** is not a requirement. For e.g. When the manufacture system built the asset it does notify the agreement system to configure the contracts and so on.

Kafka: Event sourcing requirement mainly, when you may need to deal with **streams (sometimes infinite), huge amount of data** at once properly balanced, **replay offsets** in order to ensure a given state and so on. Keep in mind that this architecture brings more complexity as well, since it does include concepts such as topics/partitions/brokers/tombstone messages, etc. as a first class importance.



## <i class="icon-pencil"></i> 5


RabbitMQ controls its messages almost in-memory, using big cluster (30+ nodes). Comparatively, Kafka leverages sequential disk I/O operations and thus demands less hardware.
