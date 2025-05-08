SOC Level 1 Use Case: Suspicious Email Behavior Detection
========================================================

Purpose
-------
To help SOC Level 1 analysts detect, validate, and escalate suspicious email-related activities using logs, alerts, and basic analysis.

Primary Responsibilities for SOC L1 Analyst
-------------------------------------------
- Monitor and acknowledge alerts from SIEM
- Validate alerts with supporting log data
- Escalate confirmed or suspicious activity to SOC Level 2
- Follow incident playbook steps for containment (if required)

Email-Based Detection Scenarios
---------------------------------

.. list-table:: 
   :header-rows: 1
   :widths: 5 10 10 10

   * - #
     - Detection Type
     - What to Look For
     - L1 Analyst Actions
   * - 1
     - Suspicious Attachment
     - File with double extension (e.g., `.docx.exe`)
     - Verify filename in logs, check sender reputation, escalate if needed
   * - 2
     - Email Flood/Burst
     - 50+ emails received in <10 mins
     - Check email subjects and sender, flag phishing, escalate
   * - 3
     - Outbound Spam
     - Internal user flagged for sending spam
     - Check sender logs, user history, notify L2
   * - 4
     - Virus in Sent Mail
     - AV logs show outbound infected email
     - Verify endpoint AV status, collect logs, escalate
   * - 5
     - Unauthorized Device Sending Mail
     - Traffic to port 25/110/143 from unknown device
     - Check source IP, verify asset, alert L2
   * - 6
     - Known Malicious Email Contact
     - Email to/from threat intel IoC
     - Look up IoC in threat feed, notify and escalate
   * - 7
     - Large Attachment Spike
     - User sends unusually large/voluminous emails
     - Check recipient domain, escalate
   * - 8
     - Email Auto-forwarding Rule
     - Rule set to forward to Gmail/Yahoo/etc.
     - Verify rule, alert user and L2, disable if needed
   * - 9
     - Email to Competitor
     - Frequent or large emails to competitor domain
     - Flag pattern, collect sample, escalate

Data Sources Used
-----------------

- Email gateway logs (e.g., Mimecast, Proofpoint)
- SIEM alerts
- Antivirus alerts
- Threat intelligence feeds
- EDR (if applicable)

Escalation Criteria
-------------------
Escalate to SOC L2 if:

- Malware or phishing is confirmed or strongly suspected
- Sensitive data was sent to personal/competitor domains
- Unusual systems send emails without authorization

Documentation
-------------
Log each step taken in the ticketing system:

- Alert received
- Timestamp of escalation (if any)
- Validation steps
- Findings
- Action taken
