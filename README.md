E-Commerce Microservices Project
Tác giả: Võ Thanh Đạt (VoThanhDat)
Hệ thống Thương mại Điện tử Đơn giản được xây dựng theo Kiến trúc Microservices nhằm minh họa khả năng phân tách, mở rộng và quản lý các thành phần của ứng dụng một cách hiệu quả.
1. 💡 Hệ thống giải quyết vấn đề gì?
Đây là một hệ thống e-commerce cơ bản, cung cấp các chức năng cốt lõi sau:
Quản lý người dùng (Authentication): Đăng ký và Đăng nhập.
Quản lý sản phẩm (Product): Xem và lưu trữ thông tin sản phẩm.
Quản lý đơn hàng (Order): Xử lý việc tạo và theo dõi đơn hàng.

🧱 Kiến trúc Hệ thống (Microservices)
Hệ thống được thiết kế với 4 dịch vụ độc lập và một cơ sở dữ liệu dùng chung, tuân theo các Mẫu thiết kế (Design Patterns) Microservices và API Gateway.
2.1. Các Dịch vụ (Microservices)
api-gateway	🌐 Cổng vào duy nhất (Single Entry Point), định tuyến các yêu cầu.	3000
auth	🔑 Xử lý đăng ký, đăng nhập và xác thực người dùng.	3001
product	📦 Quản lý thông tin, thêm/sửa/xóa sản phẩm.	3002
order	🛒 Xử lý logic tạo và quản lý đơn hàng.	3003
2.2. Giao tiếp giữa các Dịch vụ
Bên ngoài (Client - User/Postman): Gửi yêu cầu đến api-gateway qua HTTP (Port 3000).

Nội bộ (Inter-Service): api-gateway sử dụng Proxy để chuyển tiếp yêu cầu đến các dịch vụ nội bộ qua mạng ảo của Docker.
Hướng dẫn Khởi chạy (Docker-Compose)
Để khởi động toàn bộ hệ thống, bạn cần cài đặt Docker và Docker Compose.

Mở Terminal/PowerShell tại thư mục gốc của dự án.

Thực thi lệnh sau:

Bash

docker-compose up --build
(Lệnh này sẽ xây dựng (build) lại hình ảnh Docker cho api-gateway (để áp dụng các thay đổi live-code), sau đó khởi chạy 5 container: 4 services và 1 MongoDB).

Truy cập hệ thống qua http://localhost:3000.
4. Kịch bản Kiểm tra (Postman)
Sử dụng Postman để kiểm tra các API sau (thay localhost:3000 bằng IP của Docker nếu cần)
Bước	Phương thức	URL	Chức năng	Ghi chú
0	GET	/health	Kiểm tra "sức khỏe" của Gateway	Live-Code Test
1	POST	/auth/register	Đăng ký tài khoản mới	Body: username, password
2	POST	/auth/login	Đăng nhập	Nhận về Access Token
3	POST	/products	Thêm sản phẩm mới	Yêu cầu Token
4	POST	/orders	Tạo đơn hàng mới	Yêu cầu Token và productId
