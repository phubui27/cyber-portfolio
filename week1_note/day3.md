# What is HTTP? (Hypertext Transfer Protocol)

- HTTP là **application-layer protocol** dùng để trao đổi dữ liệu trên web  
  (HTML documents, images, videos, etc.)
- Hoạt động theo mô hình **client–server**, dựa trên **request / response**

SOC insight:
- HTTP request và response xuất hiện trực tiếp trong **web access log**

---

# Key characteristics of HTTP

## Simple & readable
- HTTP messages được thiết kế đơn giản, dễ đọc, dễ debug

SOC insight:
- Log HTTP thường là **plain text**, SOC có thể đọc và grep trực tiếp

---

## Extensible
- HTTP headers cho phép mở rộng giao thức  
  (caching, authentication, origin rules)

SOC insight:
- Headers như **User-Agent, Host, Authorization** là nơi SOC tìm hành vi bất thường

---

## Stateless but not sessionless
- HTTP là **stateless**: mỗi request là độc lập  
- **Cookies** cho phép tạo session để duy trì ngữ cảnh

SOC insight:
- SOC correlate nhiều request từ cùng **IP / session** để phát hiện brute force hoặc abuse

---

## Reliable transport
- HTTP thường chạy trên **TCP** hoặc **TLS over TCP (HTTPS)**

SOC insight:
- TCP có session → dễ phát hiện hành vi lặp lại trong log

---

# Requests & Responses

- HTTP giao tiếp bằng từng **message riêng lẻ**, không phải stream liên tục

## Client
- Browser luôn là bên **khởi tạo request**
- Trình duyệt tải HTML trước, sau đó gửi thêm request để lấy các sub-resources

## Server
- Nhận request và trả response
- Có thể là nhiều server phía sau (load balancing)

## Proxies
- Có thể nằm giữa client và server  
- Thực hiện caching, filtering, authentication, logging

SOC insight:
- SOC thường thu thập log từ **proxy / WAF / reverse proxy**

---

# HTTP Messages

## Request
- Method (GET, POST, ...)
- Path (URL)
- Headers
- Body (tuỳ method)

SOC insight:
- SOC nhìn đầu tiên vào **Method + Path + Headers**

---

## Response
- Status code
- Headers
- Body

SOC insight:
- Status code cho SOC biết request **thành công hay thất bại**

---

# HTTP Methods (SOC focus)

## GET
- Dùng để lấy dữ liệu (retrieve data)
- Safe, idempotent, cacheable

SOC insight:
- GET lặp lại vào URL lạ → có thể là **scan endpoint**

---

## POST
- Gửi dữ liệu (login, form submission)
- Có thể làm thay đổi trạng thái server

SOC insight:
- POST liên tục từ cùng IP → **brute force hoặc abuse form**

---

# HTTP Status Codes (SOC core)

## 200 – OK
- Request thành công

SOC insight:
- 200 **không đồng nghĩa an toàn** nếu hành vi request bất thường

---

## 301 – Moved Permanently
- Resource đã được chuyển sang URL khác

SOC insight:
- Redirect bất thường hoặc lặp lại → cần kiểm tra

---

## 401 – Unauthorized
- Chưa hoặc sai thông tin xác thực (authentication)

SOC insight:
- Nhiều 401 liên tiếp → khả năng **brute force login**

---

## 403 – Forbidden
- Server hiểu request nhưng từ chối truy cập  
- Client có danh tính nhưng **không có quyền**

SOC insight:
- Dò admin page hoặc resource nhạy cảm

---

## 404 – Not Found
- Resource không tồn tại  
- Đôi khi được dùng để che giấu resource thật

SOC insight:
- Nhiều 404 với URL lạ → **scan directory / endpoint**

---

## 500 – Internal Server Error
- Lỗi server không xác định

SOC insight:
- 500 lặp lại sau request bất thường → **exploit attempt hoặc misconfiguration**
