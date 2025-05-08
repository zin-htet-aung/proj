Proxy Logs
===========

For tracking web requests routed through a proxy server.

1. Source
---------

**Name:** Proxy Server

**Description:**  
A proxy server acts as an intermediary between clients (users) and the internet. It forwards client requests to web servers and returns responses to clients while logging these interactions. Proxies can be used for caching, content filtering, and security purposes.

**Common Proxy Servers:**

* **Squid**: An open-source caching proxy server widely used in enterprise environments.
* **Blue Coat (Symantec ProxySG)**: A commercial proxy solution with advanced security features.
* **Zscaler**: A cloud-based secure web gateway (SWG) that provides proxy services.
* **Microsoft Forefront Threat Management Gateway (TMG)**: Legacy proxy server with advanced security capabilities.
* **Palo Alto Networks (GlobalProtect)**: Offers proxy functionality as part of its next-generation firewall (NGFW).

2. Purpose
----------

**Primary Purpose:**  
Proxy logs record all HTTP/HTTPS requests made by users through the proxy server, including details about the requested URL, response status, and user information. These logs help monitor web traffic, enforce acceptable use policies, and detect malicious activity.

**Security Relevance:**  
Proxy logs are crucial for identifying unauthorized access, detecting malware downloads, and blocking malicious websites. They also provide insights into potential insider threats and data exfiltration attempts.

- Command-and-control communication
- Data exfiltration
- Malicious file downloads
- Insider threats
- Phishing URLs

3. Log Format
-------------

**General Fields Across Proxy Logs:**

.. list-table:: 
   :header-rows: 1
   :widths: 20 80

   * - Field
     - Description
   * - ``timestamp``
     - The date and time when the request was received.
   * - ``client_ip``
     - The IP address of the client making the request.
   * - ``user``
     - The username of the user making the request (if authenticated).
   * - ``request_method``
     - The HTTP method used in the request (e.g., GET, POST).
   * - ``url``
     - The full URL of the request (e.g., ``http://example.com/page``).
   * - ``response_code``
     - The HTTP status code returned by the web server (e.g., 200, 404, 500).
   * - ``bytes_sent``
     - The size of the response sent to the client.
   * - ``bytes_recv``
     - The size of the received bytes to the client.
   * - ``referer``
     - The referring URL (if any).
   * - ``user_agent``
     - The User-Agent string indicating the browser or tool used by the client.
   * - ``action``
     - The action taken by the proxy (e.g., ALLOW, BLOCK, DENY).
   * - ``website_category``
     - Filter-category (e.g., shopping, entertainment).

4. Use Cases for SOC Analysts
-----------------------------

Proxy logs are invaluable for SOC analysts in various scenarios. Below are some key use cases:

4.1. Detecting Malicious Activity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Malware Downloads**: Identify requests to known malicious domains or URLs associated with malware distribution.
* **Phishing Attempts**: Monitor requests to suspicious or phishing-related URLs.
* **Data Exfiltration**: Detect large file uploads or unusual outbound traffic patterns that may indicate data exfiltration.

4.2. Monitoring User Activity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Policy Enforcement**: Ensure compliance with acceptable use policies by monitoring access to restricted categories (e.g., social media, gambling).
* **Insider Threats**: Identify unusual user behavior, such as accessing sensitive data from unexpected locations or times.

4.3. Investigating Security Incidents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* **Incident Response**: Use proxy logs to trace the source of an incident by correlating timestamps, user identities, and URLs accessed.
* **Forensic Analysis**: Analyze logs to determine what actions were taken before, during, and after a security breach.

4.4. Threat Hunting
~~~~~~~~~~~~~~~~~~

* **Proactive Threat Detection**: Search for indicators of compromise (IOCs) such as unusual URL patterns, unexpected user agents, or high-frequency requests.
* **Correlation with Other Logs**: Combine proxy logs with other data sources (e.g., DNS logs, firewall logs) to identify advanced threats.
