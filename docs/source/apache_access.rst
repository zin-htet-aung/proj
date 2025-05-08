Apache Access Logs
==================

For traffic flowing to your web applications.

1. Source
---------

- **Name**: Apache HTTP Server
- **Description**: Apache HTTP Server (commonly referred to as "Apache") is one of the most widely used web server software. It serves web pages and logs various events related to client-server interactions.
- **Log Location**:

  - Default location: /var/log/apache2/access.log (Linux)
  - Custom locations can be configured in the Apache configuration file (httpd.conf or apache2.conf).

2. Purpose
----------

- **Primary Purpose**: Apache Access Logs record all requests made to the web server, including successful and failed attempts to access resources (e.g., web pages, images, scripts).
- **Security Relevance**: These logs are critical for monitoring web server activity, identifying suspicious behavior, detecting attacks (e.g., brute force, SQL injection, directory traversal), and investigating security incidents to web servers.

3. Log Format
-------------

**Example Log Entry (Combined Log Format):**

::

   192.168.1.10 - - [10/Oct/2023:13:55:36 +0000] "GET /index.html HTTP/1.1" 200 1024 "http://example.com/referer" "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"

**Combined Log Format:**

::

   %h %l %u %t "%r" %>s %b "%{Referer}i" "%{User-Agent}i"

**Field Breakdown:**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Field
     - Description
   * - ``%h``
     - Remote host (IP address of the client making the request).
   * - ``%l``
     - Remote logname (usually not used; appears as -).
   * - ``%u``
     - Remote user (if authentication is used; otherwise -).
   * - ``%t``
     - Time the request was received (in [day/month/year:hour:minute:second]).
   * - ``%r``
     - Request line (HTTP method, resource requested, and protocol version).
   * - ``%>s``
     - HTTP status code returned to the client (e.g., 200, 404, 500).
   * - ``%b``
     - Size of the response in bytes (excluding headers; - if no content).
   * - ``%{Referer}i``
     - Referrer URL (the page that linked to the requested resource).
   * - ``%{User-Agent}i``
     - User-Agent string (browser type, operating system, etc.).

4. Use Cases for SOC Analysts
-----------------------------

Apache Access Logs are invaluable for SOC analysts in various scenarios. Below are some key use cases:

4.1. Detecting Suspicious Activity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Brute Force Attacks**: Look for repeated login attempts (e.g., POST requests to /login) from the same IP or multiple IPs.
- **Directory Traversal**: Identify requests containing patterns like ``../`` or unusual paths.
- **SQL Injection**: Monitor for suspicious query strings in URLs (e.g., UNION SELECT, DROP TABLE).
- **Cross-Site Scripting (XSS)**: Look for ``<script>`` tags or other malicious payloads in query parameters.

4.2. Monitoring Web Traffic
~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Analyze traffic spikes or unusual patterns that may indicate a Distributed Denial of Service (DDoS) attack.
- Track requests from specific geographic regions or IPs that are known to be malicious.

4.3. Investigating Security Incidents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- Use logs to trace the source of an attack by correlating timestamps and IP addresses.
- Identify compromised resources by analyzing requests that resulted in unexpected HTTP status codes (e.g., 403 Forbidden, 500 Internal Server Error).

4.5. Threat Hunting
~~~~~~~~~~~~~~~~~~~

- Proactively search for indicators of compromise (IOCs) such as unusual User-Agent strings, non-standard HTTP methods, or requests to hidden endpoints.
- Correlate Apache logs with other data sources (e.g., firewall logs, IDS alerts) to identify advanced threats.
