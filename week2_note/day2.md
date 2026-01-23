# Day 2: Common Network Protocols (SOC Detection View)

## Mục tiêu
- Nhìn protocol → liên tưởng ngay rủi ro
- Hiểu SOC quan tâm protocol ở mức nào (Tier 1)
- Phân tích network log thực tế, không học lý thuyết suông

---

## 1. TCP vs UDP (SOC Level)

### TCP
- Có kết nối (3-way handshake)
- Đảm bảo dữ liệu
- Dùng cho:
  - HTTP / HTTPS
  - SSH
  - FTP

SOC insight:
- TCP có session → SOC dễ theo dõi hành vi lặp
- Nhiều TCP connection thất bại → brute force / abuse
- SSH brute force thường dựa trên TCP

---

### UDP
- Không kết nối
- Nhanh, không đảm bảo dữ liệu
- Dùng cho:
  - DNS
  - Streaming
  - Một số malware

SOC insight:
- UDP outbound bất thường rất đáng chú ý
- Không có session → khó trace → hay bị attacker lợi dụng
- Có thể liên quan đến:
  - DNS tunneling
  - Amplification abuse

SOC rule:
- **UDP outbound bất thường = phải điều tra**

---

## 2. DNS (SOC Core Protocol)

DNS:
- Resolve domain → IP

SOC quan tâm DNS vì:
- Domain lạ
- Newly registered domain
- DNS tunneling
- Beaconing (máy gọi về C2 theo chu kỳ)

Red flags:
- Domain rất dài, random
- DNS request lặp lại theo chu kỳ đều
- Internal host liên tục hỏi cùng 1 domain lạ

SOC mindset:
- DNS traffic thường là **bước đầu của tấn công**
- SOC dùng DNS để tìm dấu vết malware / C2

---

## 3. HTTP / HTTPS (SOC Core Protocol)

HTTP / HTTPS:
- Giao thức cho web traffic
- SOC phân tích thông qua **log**, không phải trình duyệt

SOC chú ý:
- Method:
  - GET → truy cập tài nguyên
  - POST → gửi dữ liệu (login, form)
- Status code:
  - 401 → authentication failure
  - 404 → scan endpoint
  - 500 → exploit / server error
- URL pattern:
  - /login
  - /admin
  - đường dẫn lạ

SOC rule:
- **Nhiều request giống nhau trong thời gian ngắn = đáng nghi**
- POST /login + nhiều 401 → brute force
- Nhiều 404 → directory / endpoint scanning

---

## 4. ICMP (Recon Protocol)

ICMP:
- Ping
- Network diagnostics

SOC quan tâm ICMP vì:
- Ping sweep
- Network mapping trước tấn công

SOC insight:
- ICMP đơn lẻ → bình thường
- ICMP nhiều từ 1 host → recon

SOC rule:
- **ICMP burst từ 1 source = nghi ngờ scan**

---

## SOC Detection Mindset – Day 2

- SOC không nhìn protocol đơn lẻ
- SOC luôn hỏi:
  - Protocol gì?
  - Có lặp không?
  - Outbound hay inbound?
  - Có phù hợp với hành vi user bình thường không?
- Protocol + pattern = tín hiệu nguy cơ

---

## Key Takeaway
- Protocol là “ngôn ngữ” của network
- SOC Tier 1 cần:
  - Nhìn protocol → đoán được intent
  - Phát hiện hành vi bất thường từ log
- Đây là nền tảng cho:
  - Network log analysis
  - SIEM detection
