# Amazon Web Services: Monitoring and Metrics


## Installing the AWS CLI

One of the many available automation tools is the AWS command line interface, or CLI.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/cli_1.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/cli_2.jpg?raw=true)

One feature the CLI supports is the concept of named profiles, that is, you can specify a named profile as a parameter to any CLI command. When you do that, it will reference the configuration options for that named profile. This is very useful when you need to access multiple AWS environments using different credentials. When I initially configure the CLI, I like to specify junk values, in order to force me to use the name profiles I so strongly prefer. Let's see what those values are, by running the AWS configure command.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/config_1.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/config_2.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/config_3.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/config_4.jpg?raw=true)

The first thing it asks for is my AWS access key ID. This is a unique ID for a specific credential. I'm going to specify a junk value, none. The second thing it looks for, is the AWS secret access key, which is the password that accompanies the key ID. Again, I'm going to specify a junk value. The third thing it looks for is the default region name. The region name, when passed into the CLI, tells the CLI what region to run the command in.

## Understand CloudWatch

CloudWatch is the monitoring service built into AWS. Capable of monitoring almost every AWS service, you can use it to engineer a comprehensive, proactive monitoring solution. Let's explore the components that make up this very useful tool. Let's first explore CloudWatch metrics. Most AWS services integrate with CloudWatch by default.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/cloudwatch_1.jpg?raw=true)


![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/service_1.jpg?raw=true)

## Configure simple notification service

It's generally a good idea to use a notification service. As notifications are often helpful when identifying the root cause of an operational issue. For issuing alerts, CloudWatch makes use of simple notification service or SNS.SNS is a push messaging service that is part of the AWS ecosystem.

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/sns_1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/sns_2.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/sns_3.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/sns_4.jpg?raw=true)

### Understand CloudWatch alarms

Any time the CPU utilization is under 75%, the alarm would be in an **OK** state. The second state is **ALARM**.
Following our line of thinking, if the CPU utilization on an instance goes above 75%, the CloudWatch alarm's state would change to ALARM. The third state is **INSUFFICIENT_DATA.** Suppose an EC2 instance monitored by CloudWatch is only used to process a batch workload during a specific window. Making efficient use of your AWS and financial resources that EC2 instance is only turned on during the batch window. While the EC2 instance is off, the CloudWatch alarm is in a state of insufficient data since the instance isn't using any CPU.


### Create a billing alarm

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/billing_1.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/billing_2.jpg?raw=true)

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/billing_3.jpg?raw=true)


### Use a CloudWatch alarm

![enter image description here](https://github.com/VickyFengYu/vicky.github.io/blob/master/pictures/aws/cloudwatch_alarm_1.jpg?raw=true)
