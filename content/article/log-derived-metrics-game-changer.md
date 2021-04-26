---
title: "Observability Log Derived Metrics - Game Changer"
date: 2021-04-10T15:47:42Z
draft: false
---
Instrumenting cloud native applications for data observability can be challenging. 

Regardless of which cloud native design pattern you are using for your application, you likely have logs.  We all have logs.  Logs aid in troubleshooting, application management, and keeping track of what an application is doing.

However, too many logs can quickly become unmanageable.  To tame the logs and gain additional valuable insight, consider pushing them into a Data Observability Platform for monitoring the health of your application.

In my case, that Data Observability Platform consists of a carefully selected combination of CNCF projects:
* Grafana 
* Grafana Loki Logs 
* Prometheus Metrics 
* Cortex Metrics 

With the help of a good data observability platform, you can visualize the health of your application using dashboards, answer complex questions using adhoc queries, and receive a heads up when things aren’t quite right using thresholds and automated alerting.

The two ingredients for a successful data observability platform are logs and metrics.  

This brings to the concept of Log Derived Metrics.  Check two boxes at once while saving compute cycles.  Generate logs that contain data useful for troubleshooting and include performance related data at the same time.  

Setup one or more Fluent Bit service as log ingestion endpoints for your data observability platform.  Push logs to Fluent Bit for preprocessing, field extraction, routing logic.  Implement log derived metrics by leveraging my prometheus metrics fluent bit output plugin:

[https://github.com/neiman-marcus/fluent-bit-out-prometheus-metrics](https://github.com/neiman-marcus/fluent-bit-out-prometheus-metrics)

At the same time send the log data to Grafana Loki logs using the Loki output plugin.  

Build dahsboards that leverage both log and metrics Grafana datasources to monitor the health of your application.

Learn how to do this much more plus a demo by attending my (virtual) talk at FluentCon 2021 Europe on May 4th:

[Fluent Bit - Swiss Army Tool of Observability Data Ingestion - Michael Marshall](https://sched.co/iKok)

Hope to see you there!

