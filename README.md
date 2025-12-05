Azure Honey Pot🍯🍯

Status - Complete✅

Cloud Platform - Azure💻

Primary Tools - Azure Monitor, Log Analytics,KQL🔨

Skills Demonstrated - Threat detection, Automation💥

📌 Project Objective: Addressing Silent Data Exfiltration

Traditional perimeter security:firewalls, cannot stop an attacker who gains internal access or an authorized user who turns malicious ;the Insider Threat. These threats often go undetected for months while sensitive data is slowly copied.

The objective of this project was to implement a high-fidelity tripwire—a Honey Pot—that guarantees detection within minutes, drastically reducing the Mean Time to Detect (MTTD) a breach in our cloud storage environment.

🛠️ Architecture & Components
This solution was built entirely using Azure cloud native services, leveraging logging and automation to minimize deployment cost and complexity.

Component	Function in Project	Azure Service
The Decoy (The Honey)	
Hosts the fake sensitive file (passwords.txt) that attracts unauthorized access.

Azure Storage Account (Blob)
The Log Collector	Configured to stream data access events (reads and downloads).	

Diagnostic Settings (Blob Service)
The Database	Stores and indexes logs, enabling lightning-fast query capabilities.	

Log Analytics Workspace
The Alarm (The Logic)
Runs the search query continuously, looking for a match.

Azure Monitor Alert Rule
The Pager (The Response)	
Sends an instant, critical notification to the security team via email.

💻 Implementation Summary: Building the Tripwire
Storage Setup: A storage account (adminpayrolldatabackup2025) was deployed with a deceptive file to serve as the decoy.

Data Pipeline: The Diagnostic Settings feature on the Blob Service was configured to ensure only low-level StorageRead events were streamed to the Log Analytics Workspace.

Threat Definition (KQL): A Kusto Query Language (KQL) query was developed to isolate the specific malicious action (GetBlob) from all other cloud noise. This query runs every 5 minutes:

Code snippet

// KQL Query: Searches for any file download attempt
StorageBlobLogs
| where OperationName == "GetBlob"
| summarize count()

Automation & Response: The Azure Monitor Alert Rule was configured to run the query above. The logic was set to trigger a Severity 0 (Critical) alert if the result count was Greater than 0. This alert was linked to a pre-defined Action Group that sends an email to the security team.

📈 Verification and Results
The system was verified by simulating a file download attempt, confirming the entire pipeline—from log ingestion to email notification—is functional within minutes.

Test Action: The decoy file was accessed to generate a fresh GetBlob event.

Result 1: Dashboard Proof The Azure Monitor dashboard immediately reflected the successful detection, showing the alert status changed to Fired within the first 5-minute cycle.

Result 2: Real-Time Notification The Action Group instantly delivered a critical email notification, demonstrating the system successfully met the goal of achieving real-time threat detection.

⭐ Key Skills Demonstrated 🌟
Cloud Infrastructure as a Service (IaaS): Resource provisioning and management in Azure.

Threat Detection & Monitoring: Designing logic (KQL) to identify specific malicious actions in cloud logs.

Security Automation: Configuring Alert Rules and Action Groups to automate incident response (IR).

Log Analytics: Writing KQL queries for data analysis and security auditing.

Risk Mitigation: Implementing a proactive, high-value defense against insider threats.

DevOps Tools: Utilizing Git and GitHub for version control and project documentation.
