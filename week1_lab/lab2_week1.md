nano lab2_week1.log -> import log (giả định có các nội dung)
Nhìn output

Viết SOC FINDINGS theo form:

Observation (thấy gì)

Interpretation (nghĩ gì)

Classification (Benign / Suspicious)

cat lab2_week1.log

command:

1. 'grep "port=22" lab2_week1.log'

Output:
2024-01-10 09:01:12 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED
2024-01-10 09:01:15 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED
2024-01-10 09:01:18 src_ip=192.168.1.10 dst_ip=192.168.1.1 protocol=TCP port=22 status=FAILED

## Finding 1 – SSH Failed Login Attempts
- Observation: 3 failed connection (Status = FAILED) from src_IP: 192.168.1.10 to dst_IP: 192.168.1.1 in 6 seconds
- SOC Interpretation: Repeated failed authentication attempts on a sensitive service within a short time window.
- Classification: Suspicious

2. 'grep "port=4444" lab2_week1.log'

output: 

2024-01-10 09:05:44 src_ip=10.0.0.7 dst_ip=45.83.12.9 protocol=TCP port=4444 status=CONNECTED

## Finding 2 – Outbound Connection to Uncommon Port
- Observation: 1 connected output (status=CONNECTED) from src_ip: 10.0.0.7 to dst_ip: 45.83.12.9 by TCP
- SOC Interpretation: An outbound connection from an internal host to a non-standard port may indicate unusual or unauthorized activity.
- Classification: Suspicious


3. 'grep "ICMP" lab2_week1.log'

output:

2024-01-10 09:10:02 src_ip=10.0.0.5 dst_ip=8.8.8.8 protocol=ICMP type=PING
2024-01-10 09:10:03 src_ip=10.0.0.5 dst_ip=192.168.1.20 protocol=ICMP type=PING
2024-01-10 09:10:04 src_ip=10.0.0.5 dst_ip=192.168.1.30 protocol=ICMP type=PING

## Finding 3 – ICMP Activity
- Observation: ICMP ping requests were sent from a single src_ip to multiple dst_ip within a short time window.
- SOC Interpretation: ICMP activity targeting multiple destinations may indicate reconnaissance or network scanning behavior.
- Classification: Suspicious


4. 'grep "HTTPS" lab2_week1.log'

output:

2024-01-10 09:15:22 src_ip=192.168.1.25 dst_ip=company.com protocol=HTTPS status=200
2024-01-10 09:15:25 src_ip=192.168.1.25 dst_ip=company.com protocol=HTTPS status=200

## Finding 4 – HTTPS Web Traffic
- Observation: Access company.com via HTTPS from internal IP, status=200 - common port
- SOC Interpretation: Normal user web access
- Classification: False positive

