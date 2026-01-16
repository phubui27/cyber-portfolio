Basic concepts:
IP- địa chỉ máy, SOC dùng để truy nguồn tấn công

LAN- mạng nội bộ, traffic lạ trong LAN rất đáng nghi

Ping (ICMP)- kiểm tra host còn sống

Port 22- SSH, SOC check brute force

Port 53- DNS, SOC soi domain lạ

Port 443- HTTPS, đọc log web

src_IP: source IP (máy gửi đi)

dst_IP: destination IP (máy nhận)

Example 1: 
src_ip=10.0.0.5
dst_ip=8.8.8.8
protocol=ICMP
-> Máy 10.0.0.5 gửi gói ICMP tới 8.8.8.8

các dải IP nội bộ: 
10.0.0.0    – 10.255.255.255   (10.x.x.x)
172.16.0.0  – 172.31.255.255
192.168.0.0 – 192.168.255.255
ngoài ra -> public IP

Example 2:
src_ip=192.168.1.10 
dst_ip=192.168.1.1 
protocol=TCP 
port=22
-> nội bộ gửi cho nội bộ qua port = 22 (cần theo dõi vì port 22 là SSH có quyền truy cập hệ thống)

Example 3:
src_ip=10.0.0.7
dst_ip=45.83.12.9
protocol=TCP
port=4444
-> Nội bộ gửi ra ngoài thông qua port 4444( rất đang ngờ vì port 4444 là port lạ, attacker hay dùng)
-> suspicious outbound connection via uncommon port (4444)

Common ports:
- Port 22: SSH, cần theo dõi brute force
- Port 53: DNS, SOC soi domain lạ
- Port 443: HTTPS, đọc log web
