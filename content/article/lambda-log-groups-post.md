---
title: "How deploying lambda with Terraform is a Win-Win"
date: 2021-02-20T00:00:00Z
draft: false
---

In this blog post I will demonstrate how selecting the best tool for the job in the end can pay off resulting in both reduced complexity and lower costs.

I was recently tasked with exporting CloudWatch logs from multiple AWS accounts into Grafana Loki, hosted in a central logging AWS account. My architecture leverages the event driven design pattern of subscribing a log sender Lambda function to a set of CloudWatch log groups.  The Lambda function is triggered as logs are written to each log group.  I then funnel the logs from each account into a single AWS SQS FIFO (First-In-First-Out) queue residing in the central logging account.  At the receiving end, a log router lambda which gets triggered by SQS when messages arrive on the queue.  I use this Lambda to route log records to instances of Fluent-Bit (blog post coming soon) and from there into Grafana Loki and Prometheus metrics (more the metrics in a future blog post).

This architecture works well, however I ran into a limitation I’d not experienced before.  Till now I’ve mostly leveraged Serverless Framework for deploying Lambda code to AWS.  Serverless Framework generates a CloudFormation Template from it’s YAML configuration files which deploys the Lambda code and any additional infrastructure required to operate.  It turns out the maximum number of resources that a single CloudFormation Template (CFT) can contain is 500.  When deploying the architecture described above, roughly every 20 log groups requires a new CFT stack as that limit is quickly exceeded .  This also means a new copy of the same Lambda with a different name for every 20 log groups.   This is quickly becomes maintenance nightmare in the making.

Terraform to the rescue!  Unlike CloudFormation, Terraform interacts directly with AWS APIs to create and destroy resources. As a result, there is no maximum resource limit.

Using one of the Serverless Framework generated CFTs as a guide, I developed an equivalent Terraform project.

Result:

It works very nicely!

Aside from the accomplishing the goal of overcoming the 500 max resource limitation, a couple of bonus benefits came with the Terraform implementation.

Firstly, equivalent deployments can now see a reduction of roughly 10:1 in the required resource count and as a result, a lower cost.

Ex. Single lambda subscribed to 47 log groups:

|  Method | Resource count |
| --- | --- |
| Serverless Framework | ~1200 |
| Terraform | ~100 |

Secondly, changes to the Lambda function code or subscribed Log groups can be made with zero impact.

To summarize, in this specific case, deciding to deviate from the norm and rewrite the deployment automation using using Terraform rather than industry tested Serverless Framework, resulted in a huge pay off.  Simpler maintenance and a lower AWS bill are definitely win-wins for any organization.

Resources referenced:

[https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SubscriptionFilters.html#LambdaFunctionExample](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SubscriptionFilters.html#LambdaFunctionExample)
[https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html)
[https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html)
[https://www.serverless.com/](https://www.serverless.com/)
[https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_function](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_function)
[https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_subscription_filter](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_log_subscription_filter)