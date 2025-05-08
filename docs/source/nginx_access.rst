NGINX Access Logs
=================

For traffic flowing to your web applications.

1. Source
---------

**Name:** NGINX Web Server

**Description:**  
NGINX is a high-performance web server and reverse proxy used to serve static and dynamic content. It logs client requests, making it valuable for monitoring traffic and security incidents.

**Log Location:**

* Default location: ``/var/log/nginx/access.log`` (Linux)
* Custom locations can be configured in the NGINX configuration file (``nginx.conf``).

2. Purpose
----------

**Primary Purpose:**  
NGINX Access Logs record all HTTP requests made to the server, logging details such as request method, status codes, client IP, and user-agent information.

**Security Relevance:**  
These logs are crucial for monitoring server activity, detecting abnormal behavior, identifying attack patterns (e.g., brute force attempts, SQL injections, directory traversal), and investigating security incidents.

3. Log Format
-------------

**Example Log Entry (Default Log Format):**

::

   192.168.1.10 - - [10/Oct/2023:13:55:36 +0000] "GET /index.html HTTP/1.1" 200 1024 "http://example.com/referer" "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"

**Default Log Format (Combined Format):**

::

   $remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent"

**Field Breakdown:**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Field
     - Description
   * - ``$remote_addr``
     - Remote client IP address
   * - ``$remote_user``
     - Remote user (if authentication is used; otherwise ``-``)
   * - ``$time_local``
     - Local time when the request was received
   * - ``$request``
     - Request line (HTTP method, requested resource, and protocol)
   * - ``$status``
     - HTTP status code returned to the client (e.g., 200, 404, 500)
   * - ``$body_bytes_sent``
     - Size of the response in bytes (excluding headers)
   * - ``$http_referer``
     - Referrer URL (the page that linked to the requested resource)
   * - ``$http_user_agent``
     - User-Agent string (browser type, operating system, etc.)

4. Use Cases for SOC Analysts
-----------------------------

NGINX Access Logs are highly valuable for Security Operations Center (SOC) analysts in multiple security scenarios. Below are key use cases:

4.1. Detecting Suspicious Activity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Brute Force Attacks:** Look for repeated login attempts (e.g., POST requests to ``/login``) from the same IP or multiple IPs.
* **Directory Traversal:** Identify requests containing patterns like ``../`` or access to restricted directories.
* **SQL Injection:** Monitor for suspicious query strings in URLs (e.g., ``UNION SELECT``, ``DROP TABLE``).
* **Cross-Site Scripting (XSS):** Look for ``<script>`` tags or other malicious payloads in query parameters.

4.2. Monitoring Web Traffic
~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Analyze traffic spikes or unusual patterns that may indicate a Distributed Denial of Service (DDoS) attack.
* Track requests from specific geographic regions or known malicious IP addresses.

4.3. Investigating Security Incidents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Use logs to trace the source of an attack by correlating timestamps and IP addresses.
* Identify compromised resources by analyzing requests resulting in unexpected HTTP status codes (e.g., 403 Forbidden, 500 Internal Server Error).

4.4. Threat Hunting
~~~~~~~~~~~~~~~~~~~

* Proactively search for Indicators of Compromise (IOCs) such as unusual User-Agent strings, non-standard HTTP methods, or requests to hidden endpoints.
* Correlate NGINX logs with other data sources (e.g., firewall logs, IDS alerts) to identify advanced threats.
