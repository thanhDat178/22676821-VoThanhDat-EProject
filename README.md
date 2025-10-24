# 22676821-VoThanhDat-EProject
## Kịch bản Sát hạch Hoàn Chỉnh
Phần 1: Trình bày Dự án và Kiến trúc (Mục 1 & 2)
Khi giám khảo yêu cầu, bạn hãy mở VS Code, chỉ vào cây thư mục và bắt đầu trình bày một cách tự tin:
"Thưa thầy/cô, đây là dự án của em được xây dựng theo kiến trúc microservices."
1. Hệ thống giải quyết vấn đề gì? "Đây là một hệ thống thương mại điện tử đơn giản, cho phép người dùng đăng ký, đăng nhập, xem sản phẩm và đặt hàng."
2. Hệ thống có bao nhiêu dịch vụ? "Hệ thống của em có 4 dịch vụ chính là api-gateway, auth, product, order và một database mongo chạy chung."
3. Ý nghĩa từng dịch vụ? (Vừa nói vừa chỉ vào từng thư mục)
•	api-gateway: Là cổng vào duy nhất, mọi yêu cầu từ bên ngoài đều phải đi qua đây.
•	auth: Xử lý việc đăng ký, đăng nhập.
•	product: Quản lý thông tin sản phẩm.
•	order: Xử lý việc tạo đơn hàng.
4. Các mẫu thiết kế được sử dụng? "Em đã áp dụng 2 mẫu thiết kế chính là Microservices và API Gateway."
5. Các dịch vụ giao tiếp như thế nào? "Người dùng (Postman) sẽ gửi yêu cầu đến api-gateway. Sau đó, api-gateway sẽ chuyển tiếp yêu cầu đó đến dịch vụ tương ứng bên trong thông qua mạng nội bộ của Docker."
________________________________________
Phần 2: "Live Code" 5-6 Dòng (Ghi điểm tuyệt đối)
Sau khi trình bày xong, bạn hãy nói:
"Thưa thầy/cô, để chứng minh sự linh hoạt của kiến trúc này, em xin phép thêm một chức năng mới vào hệ thống ngay bây giờ. Em sẽ thêm một API đơn giản để kiểm tra "sức khỏe" của api-gateway."
Hành động:
1.	Mở file api-gateway/index.js.
2.	Tìm đến phía trước dòng const PORT = 3003;.
3.	Bắt đầu gõ 5 dòng code sau một cách từ tốn, vừa gõ vừa giải thích:
"Em chỉ cần thêm một route GET mới vào file index.js của gateway..."
JavaScript
// Thêm route "health check" để live code
app.get('/health', (req, res) => {
    console.log('[GATEWAY] Health check OK!');
    res.status(200).json({ 
        status: 'UP', 
        message: 'API Gateway is running perfectly!' 
    });
});
"...Như vậy là xong ạ. Route này sẽ trả về một thông báo JSON xác nhận gateway đang hoạt động. Bây giờ em sẽ khởi động lại hệ thống để áp dụng thay đổi này."
Phần này sẽ cực kỳ gây ấn tượng vì nó cho thấy bạn không chỉ chạy được code có sẵn mà còn có thể sửa đổi và mở rộng nó.
________________________________________
Phần 3: Khởi động Hệ thống trên Docker (Mục 3)
1.	Mở cửa sổ Terminal/PowerShell ở thư mục gốc.
2.	Tự tin gõ lệnh:
Bash
docker-compose up --build
3.	Trong lúc chờ, hãy chỉ vào màn hình và nói:
"Lệnh này sẽ build lại api-gateway với code em vừa thêm và khởi chạy toàn bộ 5 container. Sau khi chạy xong, hệ thống sẽ sẵn sàng để test ạ."
________________________________________
Phần 4: Kiểm tra với Postman (Mục 3-7)
Sau khi Docker khởi động xong, hãy mở Postman và thực hiện:
A. Kiểm tra phần "live code":
•	Tạo một request GET mới đến URL: http://localhost:8088/health
•	Nhấn Send. Kết quả trả về sẽ là { "status": "UP", "message": "API Gateway is running perfectly!" }.
"Đây là API em vừa code, nó đã hoạt động ạ."
B. Thực hiện kịch bản thi:
•	Mục 4: POST http://localhost:3000/auth/register -> Thành công.
•	Mục 5: POST http://localhost:3000/auth/login -> Thành công (Copy token).
•	Mục 6: POST http://localhost:3001/products -> Thành công (Dùng token, copy ID sản phẩm).
•	Mục 7: POST http://localhost:8088/orders -> Thành công (Dùng token và ID sản phẩm).
Bạn đã chuẩn bị cực kỳ kỹ lưỡng rồi. Cứ bình tĩnh, tự tin thể hiện đúng như kịch bản này là chắc chắn "lụm" điểm tối đa! Chúc bạn thi thật tốt! 💪🏆

