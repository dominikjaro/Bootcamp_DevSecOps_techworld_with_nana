## AWS Logging and Monitoring Services

**CloudWatch:** AWS CloudWatch is a monitoring and observability service that provides data and actionable insights for AWS, hybrid, and on-premises applications and infrastructure resources. It collects and tracks metrics, collects and monitors log files, and sets alarms.

Key features of CloudWatch include:
- Metrics collection and monitoring
- Log collection and analysis
- Alarms and automated actions
- Dashboards for visualization

**CloudTrail:** AWS CloudTrail is a service that enables governance, compliance, and operational and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.

Event history in CloudTrail provides a detailed record of all API calls made within your AWS account, including the identity of the caller, the time of the call, the source IP address, and the request and response details. This helps you to track changes, detect unusual activity, and ensure compliance with security policies.

**Multi-region CloudTrail:**
 - enabled by default -- saves event logs from all regions
 - home region of trail, where the trail can be configured viewing and deleted

**CloudWatch Log Groups:** 
- Log group: A log group is a collection of log streams that share the same retention, monitoring, and access control settings. Log groups help you organize and manage your log data efficiently.
- Log stream: A log stream is a sequence of log events that share the same source. Log streams belong to log groups and help you organize and manage log data from different sources within the same log group.

**CloudWatch Alarms:**
- CloudWatch Alarms allow you to monitor specific metrics and trigger actions based on predefined thresholds. Alarms can automatically send notifications, execute Auto Scaling policies, or perform other automated actions to maintain the desired state of your resources.
- Create a custom metric for your alarm e.g. "ConsoleLogin": "Failure"

---

## GCP Logging and Monitoring Services

**Cloud Audit Logs:** Google Cloud Audit Logs maintains a record of actions taken by users and service accounts in your GCP projects. It helps you to track changes, monitor access, and ensure compliance with organizational policies. In GCP, audit logs are generated automatically for administrative actions and data access, but you don't go to a separate "Audit" service to view them. They are simply ingested directly into Cloud Logging where you query them alongside your application logs.

**Cloud Monitoring:** Google Cloud Monitoring provides visibility into the performance, uptime, and overall health of cloud-powered applications. It collects metrics, events, and metadata from GCP, AWS, and on-premises environments to help you gain actionable insights and maintain reliable services.

**Cloud Logging:** Google Cloud Logging is a fully managed service that allows you to store, search, analyze, monitor, and alert on log data and events from GCP and AWS. It helps you gain operational and security insights by providing a centralized logging solution.

**Logs Explorer & Logs Router (The CloudWatch Logs equivalent):** Logs Explorer allows you to query and analyze log data stored in Cloud Logging, while Logs Router enables you to route logs to different destinations such as Cloud Storage, BigQuery, or Pub/Sub for further processing and long-term storage.