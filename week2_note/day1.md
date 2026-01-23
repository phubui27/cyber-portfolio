# Day 1 – Basic Network Concepts (SOC View)

## 1. IP Address

IP:
→ địa chỉ định danh của một máy trong mạng  
→ SOC dùng để truy nguồn tấn công và phân biệt internal vs external traffic

Private (Internal) IP ranges:
- 10.0.0.0 – 10.255.255.255
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

Public IP:
→ IP ngoài Internet

SOC insight:
→ máy nội bộ kết nối tới public IP lạ = đáng nghi

---

## 2. LAN (Local Area Network)

LAN:
→ mạng nội bộ (trong công ty / tổ chức)

SOC insight:
→ traffic lạ trong LAN nguy hiểm hơn Internet  
→ có thể là lateral movement sau khi attacker đã xâm nhập

---

## 3. Source IP & Destination IP

src_ip (source IP):
→ máy gửi request

dst_ip (destination IP):
→ máy nhận request

SOC insight:
→ câu hỏi đầu tiên của SOC:
“Máy nào nói chuyện với máy nào?”

---

## 4. ICMP / Ping

ICMP:
→ dùng để ping, kiểm tra host còn sống

SOC insight:
→ ICMP nhiều, quét hàng loạt IP
→ dấu hiệu recon / ping sweep

---

## 5. Port & Common Ports

Port:
→ dịch vụ đang chạy trên máy

Common ports SOC cần nhớ:
- Port 22 → SSH (remote login)
- Port 53 → DNS (resolve domain)
- Port 443 → HTTPS (web traffic)

SOC insight:
→ brute force SSH (port 22) rất phổ biến  
→ DNS dùng để phát hiện domain lạ, DNS tunneling  
→ port lạ (vd: 4444) = red flag

---

## 6. TCP vs UDP (Basic)

TCP:
→ có kết nối, đáng tin cậy

UDP:
→ không kết nối, nhanh

SOC insight:
→ UDP traffic bất thường dễ bị abuse  
→ cần chú ý khi UDP xuất hiện nhiều

---

## Key Takeaways (SOC Mindset)

- SOC không nhìn từng packet đơn lẻ
- SOC tìm pattern theo:
  → IP
  → port
  → protocol
- Traffic nội bộ + hành vi bất thường = ưu tiên điều tra
