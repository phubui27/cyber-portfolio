# Day 2 – Basic Network Concepts (SOC View)

## 1. Basic concepts

- **IP**: địa chỉ của máy  
  → SOC dùng để truy nguồn tấn công

- **LAN**: mạng nội bộ  
  → traffic lạ trong LAN rất đáng nghi

- **Ping (ICMP)**: kiểm tra host còn sống

- **Port 22 (SSH)**:  
  → cho phép remote login, SOC theo dõi brute force

- **Port 53 (DNS)**:  
  → SOC soi domain lạ, DNS tunneling

- **Port 443 (HTTPS)**:  
  → traffic web, SOC đọc log web

- **src_ip (Source IP)**: máy gửi request

- **dst_ip (Destination IP)**: máy nhận request

---

## 2. Private vs Public IP

### Private IP ranges (IP nội bộ)
- 10.0.0.0 – 10.255.255.255 (10.x.x.x)
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

→ IP nằm ngoài các dải trên = **Public IP**

---

## 3. Log examples & SOC reasoning

### Example 1
    src_ip=192.168.1.10
    dst_ip=192.168.1.1
    protocol=TCP
    port=22

SOC reasoning:
- Nội bộ → nội bộ  
- Port 22 = SSH  

→ **SSH nội bộ, cần theo dõi vì có quyền truy cập hệ thống**

---

### Example 3
    src_ip=10.0.0.7
    dst_ip=45.83.12.9
    protocol=TCP
    port=4444

SOC reasoning:
- Nội bộ → Internet  
- Port 4444 = port lạ, thường xuất hiện trong malware / C2  

→ **Suspicious outbound connection via uncommon port (4444)**

---

## 4. Common ports (SOC focus)

- **22**: SSH → theo dõi brute force
- **53**: DNS → soi domain lạ
- **443**: HTTPS → đọc log web
