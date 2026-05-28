## 📝 About the Project

This project is a hands-on implementation of a localized **Security Operations Center (SOC)** workflow. The main goal is to detect and automatically block SSH brute-force attacks on a Linux system before they can cause any damage. 

To achieve this, I integrated two widely used security tools: **Splunk Enterprise** (as a SIEM platform) and **Fail2ban** (for automated incident response).

### How it works:
* **Monitoring & Detection:** All authentication logs from the Linux machine (`/var/log/auth.log`) are forwarded to Splunk in real-time. I configured a custom Splunk alert that triggers immediately if an IP address or user account fails to log in more than 5 times.
* **Alerting:** Once the threshold is breached, Splunk automatically sends a high-priority email alert to the SOC analyst with all the attack details.
* **Automated Mitigation:** At the same time, Fail2ban works on the host machine to parse the same logs. The moment it detects those 5 failed attempts, it instantly updates the system's firewall rules (`iptables`) and bans the attacker's IP address for 1 hour.

This project successfully bridges the gap between threat detection and automated response, significantly reducing the time it takes to neutralize a brute-force threat.
