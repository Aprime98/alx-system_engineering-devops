Postmortem Report: Web Stack Outage on June 1, 2024
Issue Summary
Duration of Outage:

Start: June 8, 2024, 14:30 UTC
End: June 8, 2024, 16:00 UTC
Impact:

The main e-commerce website experienced a complete outage.
Users were unable to access the site, resulting in a 100% service disruption.
Approximately 15,000 users were affected during the outage period.
Root Cause:

A misconfigured database replication setting caused a cascading failure in the application’s ability to read and write data.
Timeline
14:30 UTC - Issue detected via automated monitoring alerts indicating a spike in 500 Internal Server Errors.
14:32 UTC - Initial investigation by the on-call engineer identified database connection errors.
14:35 UTC - Assumed root cause to be a recent deployment; rollback initiated.
14:45 UTC - Rollback completed, but issue persisted.
15:00 UTC - Incident escalated to the database team for deeper analysis.
15:15 UTC - Database team discovered replication lag and misconfiguration.
15:20 UTC - Investigation diverted to network issues due to misleading latency metrics.
15:30 UTC - Confirmed the replication configuration error as the root cause.
15:35 UTC - Applied correct replication settings and initiated database resynchronization.
15:45 UTC - Database resynchronization completed; service partially restored.
16:00 UTC - Full service restoration confirmed and monitoring returned to normal.
Root Cause and Resolution
Root Cause:

The database replication settings were incorrectly configured during a maintenance update. This led to significant replication lag, eventually causing read/write operations to fail across the web application, rendering the site inaccessible.
Resolution:

The correct replication settings were identified and applied. The database was then resynchronized to ensure data consistency and integrity. Post-synchronization checks confirmed the restoration of normal operation.
Corrective and Preventative Measures
Improvements and Fixes:

Enhance deployment scripts to include validation checks for critical configuration settings.
Implement more granular monitoring and alerts for database replication lag.
Conduct a review and update of the incident response playbook to reduce response times and improve the accuracy of initial diagnostics.
Tasks:

Patch Deployment Scripts:
Add validation logic to check for correct database replication settings pre-deployment.
Enhanced Monitoring:
Deploy additional monitoring tools to track replication status and performance metrics in real-time.
Incident Response Review:
Revise the incident response playbook to include specific steps for verifying database configuration and replication status.
Training:
Conduct a training session for the engineering team on the new monitoring tools and updated incident response procedures.
Postmortem Review:
Schedule a postmortem review meeting to discuss the outage, the response, and the new preventative measures with the entire engineering team.
