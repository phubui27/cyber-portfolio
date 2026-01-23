# SOC Alert Triage – Week 1

**Role:** Tier 1 SOC Analyst  
**Objective:** Review and classify security alerts based on available information.

---

## Lab Setup

Alerts were reviewed from a simulated alert file:

nano alerts_week1.log

Alerts included:

Multiple failed SSH login attempts from 192.168.1.20

Single failed login attempt from user jdoe

Outbound connection to port 4444 from 10.0.0.7

ICMP requests to multiple internal hosts

User accessed company website via HTTPS

## Alert Analysis Report

## Alert 1: Multiple failed SSH login attempts from 192.168.1.20

Service: SSH (Port 22)
Behavior: Failed login

Frequency: Multiple

Source IP: 192.168.1.20 (Internal IP – 192.168.x.x)

Analysis:

The alert shows multiple failed SSH login attempts from an internal IP address.
Repeated authentication failures on a sensitive service such as SSH may indicate suspicious activity and require further investigation.

Classification: Suspicious

---

## Alert 2: Single failed login attempt from user jdoe

Behavior: Failed login

Frequency: Single

User: jdoe

Analysis:

The alert shows a single failed login attempt for user jdoe.
A single authentication failure is common user behavior and does not indicate suspicious activity.

Classification: False Positive

---

## Alert 3: Outbound connection to port 4444 from 10.0.0.7

Direction: Outbound connection

Destination Port: 4444 (Uncommon port)

Source IP: 10.0.0.7 (Internal IP – 10.x.x.x)

Analysis:

The alert shows an outbound connection from an internal host to an uncommon port (4444).
Outbound traffic to non-standard ports may indicate suspicious or unusual activity and should be further investigated.

Classification: Suspicious

---

## Alert 4: ICMP requests to multiple internal hosts

Protocol: ICMP

Behavior: ICMP requests (ping)

Target: Multiple internal hosts

Analysis:

The alert shows ICMP requests sent to multiple internal hosts.
ICMP activity targeting multiple hosts may indicate network scanning or reconnaissance behavior and should be further investigated.

Classification: Suspicious

---

## Alert 5: User accessed company website via HTTPS

Protocol: HTTPS

Behavior: Web access

Target: Company website

Analysis:

The alert shows a user accessing the company website via HTTPS.
This represents normal user web activity and does not indicate any security concern.

Classification: False Positive
