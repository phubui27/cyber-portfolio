# Week 1 – SOC Analyst Quick Review

## SOC Core Concepts
- SOC = Detection + Response
- Alert ≠ Incident
- Tier 1 SOC:
  → Review alert
  → Triage
  → Initial investigation
  → Escalate
  → Document

---

## Network Basics (SOC View)
IP:
→ định danh máy, truy nguồn tấn công

Port:
- 22 → SSH (brute force)
- 53 → DNS (domain lạ, tunneling)
- 443 → HTTPS (web traffic)

src_ip:
→ máy gửi

dst_ip:
→ máy nhận

---

## Web / HTTP Basics
Method:
- GET → load resource
- POST → gửi data (login, form)

Status code:
- 401 → authentication failed
- 403 → permission denied
- 404 → scanning / probing
- 500 → server error (possible exploit)

SOC rule:
→ nhiều request giống nhau = đáng nghi

---

## Windows Logs (Core)
4624:
→ successful logon

4625:
→ failed logon (brute force nếu lặp)

SOC rule:
→ không kết luận từ 1 event

---

## Linux Fundamentals (SOC View)

Filesystem:
→ log, config, system info đều là file

Terminal:
→ công cụ chính của SOC

Commands:
- pwd → vị trí hiện tại
- ls → liệt kê file
- cd → di chuyển
- tail → xem log mới nhất
- grep → lọc hành vi đáng nghi
- find → tìm file lạ

Process:
- ps → xem process
- top → realtime system activity

Cron:
→ task chạy định kỳ
→ hay bị attacker dùng để persistence

Time:
→ Linux dùng UTC
→ NTP để sync time
→ time sai = điều tra sai

---

## SOC Mindset
- Không kết luận từ 1 log
- Tìm pattern
- Correlate theo thời gian
- Luôn document
