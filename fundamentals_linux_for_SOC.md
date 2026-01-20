# Linux Fundamentals – SOC View

---
## WEEK 1

---
## 1. Linux basics

Linux:
→ hệ điều hành mã nguồn mở, kế thừa UNIX  
→ dùng phổ biến cho server, cloud, security tools  
→ SOC thường làm việc trực tiếp trên Linux environment

Linux Foundation:
→ tổ chức bảo trợ Linux và nhiều dự án open-source  
→ Linux được phát triển bởi cộng đồng toàn cầu

SOC view:
→ phần lớn log và security tool chạy trên Linux

---

## 2. Linux distributions

Linux distribution families:
- Red Hat (RHEL, CentOS, Rocky)
- Debian (Debian, Ubuntu)
- SUSE (openSUSE)

SOC view:
→ khác distro nhưng concept giống nhau  
→ SOC không cần nhớ distro, chỉ cần biết log ở đâu

---

## 3. Core Linux concepts

Multi-user:
→ nhiều user dùng chung hệ thống  
→ tăng attack surface

Multi-tasking:
→ nhiều process chạy đồng thời

Daemon (service):
→ process chạy nền  
→ sinh ra system log quan trọng

SOC view:
→ user + daemon là nguồn activity chính để theo dõi

---

## 4. Disk, filesystem & boot

Partition:
→ chia ổ đĩa logic  
→ giúp cô lập dữ liệu khi có sự cố

Filesystem:
→ cách Linux lưu & truy xuất file  
→ log, config, system info đều là file

Boot process:
→ BIOS/UEFI → bootloader → kernel → init  
→ hệ thống khởi động qua nhiều bước

SOC view:
→ hữu ích khi điều tra incident sau reboot

---

## 5. Desktop & user session (đã học qua)

GNOME:
→ desktop environment phổ biến  
→ dùng gdm để quản lý login screen

Login / Logout / Session:
→ mỗi lần login tạo 1 session  
→ logout kết thúc session

SOC note:
→ UI, theme không phải trọng tâm SOC  
→ session liên quan trực tiếp đến user activity

---

## 6. Time & system configuration

UTC:
→ Linux dùng UTC cho time nội bộ

NTP:
→ đồng bộ thời gian với Internet time server

Network Manager:
→ quản lý network & VPN

SOC view:
→ time chính xác rất quan trọng để correlate log  
→ time sai → điều tra sai

---

## 7. Package management

Debian-based:
→ dpkg, apt

Red Hat-based:
→ rpm, dnf

SUSE:
→ zypper

SOC view:
→ package cài đặt bất thường có thể là dấu hiệu compromise

---

## 8. Terminal & navigation

Terminal:
→ công cụ chính của SOC trên Linux

Absolute path:
→ đường dẫn bắt đầu từ /

Relative path:
→ đường dẫn từ thư mục hiện tại

Commands:
- pwd → biết đang đứng ở đâu
- ls → liệt kê file, tìm log
- cd → di chuyển thư mục
- cd - → quay lại thư mục trước

SOC view:
→ SOC dùng terminal để tìm & đọc log, không dùng GUI

---

## 9. File search & file handling

locate:
→ tìm file nhanh bằng database

find:
→ tìm file đệ quy  
→ SOC dùng để tìm log, script, file lạ

Hard link / Symbolic link:
→ nhiều đường dẫn trỏ cùng file  
→ attacker có thể lợi dụng để che giấu file

touch:
→ tạo file hoặc thay đổi timestamp

SOC view:
→ timestamp rất quan trọng khi điều tra incident

---

## 10. Linux documentation

man:
→ tài liệu chi tiết của command

info:
→ tài liệu dạng cây

--help / -h:
→ xem nhanh cách dùng

SOC view:
→ không cần nhớ cú pháp  
→ biết cách tra nhanh khi cần

---

## 11. Processes & system activity

Process:
→ chương trình đang chạy trên hệ thống

PID:
→ định danh duy nhất của process

Foreground / Background:
→ process chạy trước / sau

Commands:
- ps → xem danh sách process
- top → xem process & tài nguyên realtime

SOC view:
→ process lạ hoặc chiếm tài nguyên cao là dấu hiệu đáng nghi

---

## 12. Job scheduling

at:
→ chạy task 1 lần tại thời điểm chỉ định

cron:
→ chạy task định kỳ

SOC view:
→ cron thường bị attacker dùng để persistence  
→ bắt buộc kiểm tra khi điều tra incident

---

## 13. Applications (đã học qua)

User applications:
→ browser, mail, office, media, graphics

SOC note:
→ không phải trọng tâm SOC  
→ chỉ để hiểu user activity bình thường

---

## Key takeaway (SOC mindset)

Linux:
→ môi trường làm việc chính của SOC

SOC tập trung vào:
→ log  
→ process  
→ user  
→ time  
→ scheduled tasks

Mục tiêu:
→ quan sát – phát hiện – điều tra  
→ không phải quản trị hệ thống
