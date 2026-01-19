# Day 5 – Windows Event Logs (SOC Fundamentals)

## Purpose
- Hiểu Windows ghi log gì và vì sao SOC phải đọc Windows logs
- Nắm các Event ID cốt lõi để phát hiện hành vi đăng nhập bất thường
- Xây dựng tư duy SOC khi phân tích Windows Security logs

---

## Why Windows logs matter in SOC
- Phần lớn doanh nghiệp sử dụng Windows cho user endpoints và servers
- Hành vi đăng nhập, brute force, privilege escalation đều để lại dấu vết trong Windows logs
- SOC không thể phát hiện incident nếu không hiểu Windows Security logs

---

## Windows Event Logs overview

Windows Event Logs được chia thành 3 nhóm chính:

- **Application**
  - Log của các ứng dụng
  - Ít dùng cho SOC beginner

- **System**
  - Log của hệ điều hành (service, shutdown, driver)
  - Dùng để điều tra sự cố hệ thống

- **Security** (QUAN TRỌNG NHẤT)
  - Log liên quan đến authentication và account
  - SOC tập trung chủ yếu vào nhóm này

---

## Event ID – ngôn ngữ của Windows logs

SOC không đọc log bằng mô tả dài, mà đọc bằng **Event ID**.

### Core Event IDs (Day 6)

#### Event ID 4624 – Successful logon
- Ghi nhận khi user đăng nhập thành công
- Cho biết:
  - User nào đăng nhập
  - Đăng nhập từ đâu (source IP)
  - Có phải tài khoản đặc quyền hay không

SOC mindset:
- Login thành công không đồng nghĩa với an toàn
- Cần correlate với:
  - Thời gian
  - Vị trí
  - Các event thất bại trước đó

---

#### Event ID 4625 – Failed logon
- Ghi nhận khi đăng nhập thất bại
- Xuất hiện khi:
  - Sai mật khẩu
  - Tài khoản bị khóa
  - Có hành vi brute force

SOC mindset:
- Một event 4625 đơn lẻ có thể là lỗi người dùng
- Nhiều event 4625 lặp lại trong thời gian ngắn → **possible brute force**

---

#### Event ID 4634 – Logoff
- Ghi nhận khi user logout
- Dùng để xác định thời điểm session kết thúc

SOC use case:
- Kết hợp với 4624 để xác định thời gian hoạt động của user

---

#### Event ID 4672 – Special privileges assigned
- Ghi nhận khi user đăng nhập với quyền đặc biệt (administrator)
- Thường xuất hiện khi admin login

SOC mindset:
- Admin login cần được theo dõi chặt
- Bất thường nếu xảy ra ngoài giờ làm việc hoặc từ IP lạ

---

## SOC analysis mindset for Windows logs

Khi nhìn Windows Security logs, SOC luôn tự hỏi:
- Event ID gì?
- User nào?
- Source IP nào?
- Có lặp lại không?
- Xảy ra trong bao lâu?

SOC không kết luận từ một event đơn lẻ, mà từ **pattern**.

---

## Web logs vs Windows logs (connection to previous days)

- Web brute force:
  - POST /login
  - Status code 401

- Windows brute force:
  - Event ID 4625
  - Repeated failed logon attempts

→ Cùng tư duy SOC, chỉ khác loại log

---

## Key takeaways
- Windows Security logs là nền tảng của SOC doanh nghiệp
- Event ID 4624 và 4625 là quan trọng nhất cho authentication monitoring
- SOC tìm pattern thay vì đọc từng dòng log
- Hiểu Windows logs là bước bắt buộc để làm việc với SIEM
