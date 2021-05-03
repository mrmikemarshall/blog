---
title: "Open Source Cloud Native Data Observability"
date: 2021-05-02T17:47:42Z
draft: false
---

With less than 48 hours until FluentCon 2021 Europe, I’m so excited to see lots of people signing up for my talk on May 4th:

[Fluent Bit - Swiss Army Tool of Observability Data Ingestion - Michael Marshall](https://sched.co/iKok)

Prior to FluentCon, I wanted to announce an open source project I just released in hope that it would be of use to the wider community:

[https://github.com/neiman-marcus/fluent-bit-data-observability-platform](https://github.com/neiman-marcus/fluent-bit-data-observability-platform)

In short, this project is a Docker-Compose based, miniature version of it’s much larger production equivalent we host in the cloud today.

With the initial relase of Fluent Bit Data Observability Platform (FBDOP), the following open source flagship CNCF observability log and metrics projects have been combined together:
* [Fluent Bit](https://fluentbit.io/)
* [Fluent Bit - Output Prometheus Metrics Plugin](https://github.com/neiman-marcus/fluent-bit-out-prometheus-metrics)
* [Fluent Bit - Output Loki Logs Plugin](https://grafana.com/docs/loki/latest/clients/fluentbit/)
* [Grafana](https://grafana.com/oss/grafana/)
* [Grafana Loki Logs](https://grafana.com/oss/loki/)
* [Prometheus Metrics](https://prometheus.io/)
* [Prometheus Pushgateway](https://github.com/prometheus/pushgateway)

(Coming Soon):
* [Cortex Metrics](https://cortexmetrics.io/)

With over of a year invested navigating the complex task of architecting a full cloud native open source data observability platform hosted on AWS, having successfully moved from POC (Proof-Of-Concept) to carrying production traffic, downtime wasn’t an option.

Enter FBDOP!  The reason I initially created this enviornment was two fold, one I was having difficulty justifying cost deploying of a second semi-scaled down version of what I had in running in production, and two,  introducing a new version of any one of those upstream projects, or a change in configuration, could easily create downtime for the production cluster.    

In the end, while it has served me well, for development and test, it has also been adopted amongst teams within my company for use as a learning tool to gain a better understanding of the larger platform running in the cloud.

My hope is that anyone attending FluentCon, or who simply has an interest in any or all of the combined projects, would find this environment as useful as I have.  Clone it, and change it! That’s what it’s for!

If you have any questions, comments, or suggestions, please leave a comment on my blog, open a github issue or fork and open a PR on the github repository.
Alternatively, you can find me in community Slack channels of each of the projects listed above as @Mike Marshall.
 
 
Most of all enjoy!  Hope to see you at the talk!

Thank You,

Michael Marshall

mrmikemarshall@gmail.com
