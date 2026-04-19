Overview (Cho Xe Đạp)
Cho Xe Đạp là nền tảng web giúp kết nối người mua và người bán xe đạp thể thao đã qua sử dụng tại Việt Nam. Sản phẩm tập trung vào trải nghiệm “đăng tin – kiểm duyệt – thanh toán – trao đổi – vận chuyển” với quy trình rõ ràng, ưu tiên tính an toàn, minh bạch và khả năng mở rộng cho marketplace.

Bài toán & Giá trị
Người mua: dễ dàng tìm kiếm, lọc, xem chi tiết, liên hệ/nhắn tin với người bán; có cơ chế báo cáo khi phát sinh tranh chấp.
Người bán: tạo và quản lý tin đăng; hỗ trợ kiểm định (inspection) nếu có nhu cầu và đủ giấy tờ; sau khi thanh toán có thể đưa tin lên nhanh.
Hệ thống: áp dụng kiểm duyệt tự động (AI) + kiểm duyệt thủ công (Admin) cho nội dung nhạy cảm (đặc biệt là video), giúp giảm rủi ro và tăng chất lượng listings.
Vận hành: có luồng phân xử (Admin là trọng tài cuối) và có thể yêu cầu Inspector thẩm định kỹ thuật khi cần.
Kiến trúc tổng quan (Multi-repo)
Hệ thống được tách thành 5 repository để dễ phát triển theo domain và triển khai độc lập:

Frontend (User) – React + TypeScript: giao diện cho khách, người mua, người bán.
Frontend (Admin Portal) – React + TypeScript: kiểm duyệt tin đăng, xử lý báo cáo, quản trị người dùng, theo dõi hoạt động.
Main Backend – .NET 8: API lõi cho authentication, postings, orders, payments (VietQR), notifications và chat real-time (SignalR).
Logistics Microservice – Spring Boot: quản lý luồng giao vận (gán shipper, pickup, tracking trạng thái).
Documentation – nguồn tài liệu “single source of truth” cho scope, business rules, và thiết kế.
Điểm nhấn kỹ thuật
Real-time Chat & Notifications: SignalR (MVP) cho nhắn tin buyer–seller và thông báo theo thời gian thực.
Thanh toán VietQR: tích hợp SePay (checkout + webhook) để tự động hóa trạng thái đơn hàng.
Bảo mật & chống bot: JWT, BCrypt, Cloudflare Turnstile.
Media: Cloudinary cho upload ảnh/video phục vụ tin đăng.
Moderation AI (Multimodal): kiểm duyệt tự động bằng Google Gemini (ảnh + text) để hỗ trợ kiểm soát chất lượng.
Các luồng nghiệp vụ chính
Seller: tạo tin → kiểm duyệt tự động → thanh toán → tin hiển thị; video có thể được giữ trạng thái chờ Admin duyệt.
Buyer: tìm kiếm/lọc → xem chi tiết → liên hệ/nhắn tin → thanh toán/đặt cọc → theo dõi đơn hàng.
Admin/Inspector: kiểm duyệt video, xử lý báo cáo, phân xử; có thể yêu cầu Inspector thẩm định kỹ thuật và trả verdict TRUE/FALSE.
Mục tiêu của dự án: xây dựng một marketplace xe đạp thể thao cũ đáng tin cậy, có quy trình kiểm duyệt & giải quyết tranh chấp rõ ràng, và kiến trúc đủ tốt để mở rộng theo từng domain.
