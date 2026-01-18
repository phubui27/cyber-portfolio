# Day 5 – Linux Basics for SOC (Knowledge Notes)

## Purpose of Linux in SOC
- SOC thường làm việc trên Linux server
- Log thường được lưu dưới dạng text file
- Linux command-line giúp đọc và lọc log nhanh hơn GUI

---

## Core Linux commands used by SOC

### pwd
- Hiển thị thư mục hiện tại
- Giúp SOC biết mình đang đứng ở đâu trong hệ thống

---

### ls
- Liệt kê file trong thư mục
- Dùng để tìm file log (access.log, auth.log, syslog)

---

### cd
- Di chuyển giữa các thư mục
- SOC dùng để đi tới thư mục chứa log

---

### cat
- Hiển thị toàn bộ nội dung file
- Dùng khi log ngắn hoặc cần xem nhanh

---

### tail
- Hiển thị các dòng cuối của file
- SOC dùng để xem các sự kiện mới nhất

---

### grep
- Lọc dòng chứa keyword
- SOC dùng để:
  - tìm POST requests
  - tìm status code (401, 404, 500)
  - tìm hành vi từ một IP cụ thể

---

## SOC log analysis mindset
- SOC không đọc log từng dòng
- SOC lọc log theo:
  - IP
  - method
  - URL
  - status code
- SOC tìm pattern thay vì sự kiện đơn lẻ

---

## Connection to previous lessons
- Day 4: học HTTP (GET, POST, status codes)
- Day 5: dùng Linux để lọc đúng các hành vi HTTP đó trong log

---

## Key takeaway
- Linux là công cụ bắt buộc của SOC
- grep là lệnh quan trọng nhất khi đọc log
- Hiểu log quan trọng hơn nhớ lệnh

## Linux commands used during log analysis
- grep POST access.log
  → identify POST-based actions such as login attempts

- grep 401 access.log
  → detect repeated authentication failures

- grep <IP> access.log
  → track behavior timeline of a single source
