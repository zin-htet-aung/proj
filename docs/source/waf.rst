Web Application Firewall (WAF) Logs
===================================

For traffic flowing to your web applications with security event logs.

1. Source
---------

- **Name**: Web Application Firewall (WAF)
- **Description**: A WAF protects web applications by monitoring, filtering, and blocking malicious HTTP/HTTPS traffic between a web application and the internet. It helps prevent attacks such as SQL injection, cross-site scripting (XSS), and other OWASP Top 10 vulnerabilities.
- **Common WAF Providers**:

  - **Cloudflare**: Cloud-based WAF with DDoS protection and CDN services.
  - **F5 BIG-IP Advanced WAF**: On-premises or cloud-based WAF solution.
  - **AWS WAF**: AWS-native WAF integrated with Amazon CloudFront, API Gateway, and Application Load Balancer.
  - **Azure WAF**: Part of Azure Application Gateway.

- **Log Location**:

  - **Cloudflare**: Accessible via Cloudflare Logs or API.
  - **F5**: Logs stored in `/var/log/` on the F5 device or sent to a centralized logging system.
  - **AWS WAF**: Logs are stored in Amazon S3 buckets when enabled.
  - **Azure WAF**: Logs can be sent to Azure Monitor, Log Analytics, or Storage Accounts.

2. Purpose
----------

- **Primary Purpose**: WAF logs record all HTTP/HTTPS requests that pass through the firewall, including both allowed and blocked traffic. These logs help identify malicious activity, monitor traffic patterns, and investigate security incidents.
- **Security Relevance**: WAF logs are essential for detecting and mitigating web application attacks, such as SQL injection, XSS, path traversal, and brute force attacks. They also provide insights into potential misconfigurations or false positives.

3. Log Format
-------------

The format of WAF logs varies depending on the provider, but most WAFs follow a JSON-based structure for easier parsing and integration with SIEM tools.

General Fields Across WAF Providers:

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Field
     - Description
   * - ``timestamp``
     - The date and time when the request was received.
   * - ``client_ip``
     - The IP address of the client making the request.
   * - ``request_method``
     - The HTTP method used in the request (e.g., GET, POST).
   * - ``request_uri``
     - The full URI of the request (e.g., /login).
   * - ``host``
     - The hostname or domain of the web application.
   * - ``user_agent``
     - The User-Agent string indicating the client/browser.
   * - ``action``
     - The action taken by the WAF (e.g., ALLOW, BLOCK, CHALLENGE).
   * - ``rule_id``
     - The ID of the WAF rule that triggered the action.
   * - ``rule_message``
     - A description of the rule that was triggered.
   * - ``http_status``
     - The HTTP status code returned to the client (e.g., 200, 403).
   * - ``bytes_sent``
     - The size of the response sent to the client.
   * - ``referer``
     - The referring URL (if any).

4. Use Cases for SOC Analysts
-----------------------------

WAF logs are invaluable for SOC analysts in various scenarios. Below are some key use cases:

4.1. Detecting Web Application Attacks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **SQL Injection**: Identify requests containing SQL keywords (SELECT, UNION, DROP) that were blocked by the WAF.
- **Cross-Site Scripting (XSS)**: Look for ``<script>`` tags or JavaScript payloads in query parameters or headers.
- **Path Traversal**: Detect requests attempting to access restricted directories (e.g., ``../``).
- **Brute Force Attacks**: Monitor repeated login attempts or requests to authentication endpoints.

4.2. Monitoring Traffic Patterns
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Analyze traffic spikes or unusual patterns that may indicate a Distributed Denial of Service (DDoS) attack.
- Track requests from specific geographic regions or IPs known to be malicious.

4.3. Investigating Security Incidents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Use logs to trace the source of an attack by correlating timestamps and IP addresses.
- Identify compromised resources by analyzing requests that resulted in unexpected HTTP status codes (e.g., 403 Forbidden, 500 Internal Server Error).

4.4. Threat Hunting
~~~~~~~~~~~~~~~~~~~

- Proactively search for indicators of compromise (IOCs) such as unusual User-Agent strings, non-standard HTTP methods, or requests to hidden endpoints.
- Correlate WAF logs with other data sources (e.g., firewall logs, IDS alerts) to identify advanced threats.
