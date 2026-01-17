# What is HTTP? (Hypertext Transfer Protocol)

- Application-layer protocol dùng để trao đổi dữ liệu trên web (HTML, image, video…)
- Hoạt động theo mô hình client–server, dựa trên request / response

SOC insight:
- HTTP request/response xuất hiện trực tiếp trong web access log

---

# Key characteristics of HTTP

## Simple & readable
- HTTP messages dễ đọc, dễ debug

SOC insight:
- Log HTTP thường là text → SOC có thể đọc và grep trực tiếp

---

## Extensible
- HTTP headers cho phép mở rộng (caching, auth, origin rules)

SOC insight:
- Headers (User-Agent, Host, Authorization) là nơi SOC tìm bất thường

---

## Stateless but not sessionless
- HTTP stateless
- Cookie tạo session để duy trì ngữ cảnh

SOC insight:
- SOC correlate nhiều request từ cùng IP/session để phát hiện brute force

---

## Reliable transport
- HTTP chạy trên TCP hoặc TLS over TCP

SOC insight:
- TCP có session → dễ phát hiện hành vi lặp trong log

---

# Requests & Responses

- HTTP giao tiếp bằng từng message riêng lẻ

## Client
- Browser luôn là bên gửi request
- Tải HTML trước, sau đó request các resource khác

## Server
- Nhận request, trả response
- Có thể là nhiều server phía sau (load balancing)

## Proxies
- Caching, filtering, auth, logging

SOC insight:
- SOC thường lấy log từ proxy / WAF / reverse proxy

---

# HTTP Messages

## Request
- Method
- Path (URL)
- Headers
- Body (tuỳ method)

SOC insight:
- SOC nhìn đầu tiên: Method + Path + Headers

---

## Response
- Status code
- Headers
- Body

SOC insight:
- Status code cho biết hành vi có thành công hay không

---

# HTTP Methods (SOC focus)

## GET
- Lấy dữ liệu
- Safe, idempotent, cacheable

SOC insight:
- GET lặp vào URL lạ → scan endpoint

---

## POST
- Gửi dữ liệu (login, form)
- Có thể thay đổi trạng thái server

SOC insight:
- POST liên tục từ cùng IP → brute force / abuse form

---

# HTTP Status Codes (SOC core)

## 200 – OK
- Request thành công

SOC insight:
- 200 không có nghĩa là an toàn nếu hành vi bất thường

---

## 301 – Moved Permanently
- Resource chuyển URL

SOC insight:
- Redirect lạ hoặc lặp → cần kiểm tra

---

## 401 – Unauthorized
- Chưa / sai xác thực

SOC insight:
- Nhiều 401 liên tục → brute force login

---

## 403 – Forbidden
- Có danh tính nhưng không có quyền

SOC insight:
- Dò admin hoặc resource nhạy cảm

---

## 404 – Not Found
- Resource không tồn tại

SOC insight:
- Nhiều 404 với URL lạ → scan directory / endpoint

---

## 500 – Internal Server Error
- Lỗi server không xác định

SOC insight:
- 500 lặp sau request bất thường → exploit hoặc misconfiguration
