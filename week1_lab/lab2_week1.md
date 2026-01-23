nano lab2_week1.log -> import log (giả định có các nội dung)
Nhìn output

Viết SOC FINDINGS theo form:

Observation (thấy gì)

Interpretation (nghĩ gì)

Classification (Benign / Suspicious)

cat lab2_week1.log

# Log analysis performed using grep commands
# Command 1: grep "port=22"

2024-01-10 09:01:12 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED
2024-01-10 09:01:15 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED
2024-01-10 09:01:18 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED

# Command 2: grep "port=4444"

2024-01-10 09:05:44 src_ip=10.0.0.7 dst_ip=45.83.12.9 protocol=TCP port=4444 status=CONNECTED

# Command 3: grep "ICMP"

2024-01-10 09:10:02 src_ip=10.0.0.5 dst_ip=8.8.8.8 protocol=ICMP type=PING
2024-01-10 09:10:03 src_ip=10.0.0.5 dst_ip=192.168.1.20 protocol=ICMP type=PING
2024-01-10 09:10:04 src_ip=10.0.0.5 dst_ip=192.168.1.30 protocol=ICMP type=PING

# Command 4: grep "HTTPS"

2024-01-10 09:15:22 src_ip=192.168.1.25 dst_ip=company.com protocol=HTTPS status=200
2024-01-10 09:15:25 src_ip=192.168.1.25 dst_ip=company.com protocol=HTTPS status=200
SOC Analysis Report: lab2_week1.log
📋 Finding 1 – SSH Failed Login Attempts
Observation: 3 failed connection attempts (status=FAILED) from src_ip: 192.168.1.10 to dst_ip: 192.168.1.1 on port 22 within a 6-second window.

SOC Interpretation: Repeated failed authentication attempts on a sensitive service (SSH) within a very short time frame suggest a potential Brute Force or Dictionary attack.

Classification: Suspicious

##Finding 2 – Outbound Connection to Uncommon Port
Observation: 1 successful connection (status=CONNECTED) from internal src_ip: 10.0.0.7 to external dst_ip: 45.83.12.9 via TCP port 4444.

SOC Interpretation: An outbound connection to a non-standard port (4444 is commonly associated with Metasploit/Reverse Shells) may indicate unauthorized activity or a compromised host communicating with a C2 server.

Classification: Suspicious

## Finding 3 – ICMP Activity (Network Reconnaissance)
Observation: Multiple ICMP ping requests sent from a single src_ip: 10.0.0.5 to various internal and external destinations (8.8.8.8, 192.168.1.20, 192.168.1.30) in quick succession.

SOC Interpretation: ICMP activity targeting multiple segments indicates potential reconnaissance or network scanning behavior to identify active live hosts.

Classification:  Suspicious

## Finding 4 – HTTPS Web Traffic
Observation: Successful access (status=200) to company.com via HTTPS from internal IP 192.168.1.25.

SOC Interpretation: Typical web traffic from an internal user to a legitimate company domain. No anomalies detected.

Classification: False Positive