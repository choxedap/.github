# 🚲 Cho Xe Đạp (ChoXeDap.vn)
> Nền tảng Marketplace kết nối cộng đồng mua bán xe đạp thể thao đã qua sử dụng tại Việt Nam.

![Marketplace Overview](https://img.shields.io/badge/Status-Inactive-brightgreen)
![Tech Stack](https://img.shields.io/badge/Tech-Multi--repo-blue)
![AI](https://img.shields.io/badge/AI-Gemini%20Moderation-orange)

## 📌 Tổng quan dự án
**Cho Xe Đạp** là một nền tảng web chuyên biệt giúp tối ưu hóa trải nghiệm mua bán xe đạp cũ. Khác với các sàn thương mại điện tử tổng hợp, chúng tôi tập trung sâu vào quy trình **Kiểm duyệt (Inspection)** và **Minh bạch thông tin**, giải quyết bài toán tin tưởng giữa người mua và người bán trong phân khúc hàng hóa giá trị cao.

Sản phẩm xoay quanh chu trình: **Đăng tin – Kiểm duyệt (AI & Human) – Thanh toán – Trao đổi – Vận chuyển.**

---

## 💡 Bài toán & Giá trị cốt lõi

### 1. Đối với Người mua
* **Tin cậy:** Tìm kiếm xe theo bộ lọc chuyên sâu (loại xe, kích thước khung, group-set, thương hiệu).
* **An toàn:** Cơ chế báo cáo (Report) và luồng phân xử tranh chấp minh bạch.
* **Tương tác:** Nhắn tin trực tiếp với người bán theo thời gian thực.

### 2. Đối với Người bán
* **Tiện lợi:** Công cụ tạo tin đăng trực quan, hỗ trợ quản lý trạng thái tin.
* **Chuyên nghiệp:** Gói dịch vụ kiểm định kỹ thuật (Inspection) từ chuyên gia để tăng uy tín cho tin đăng.
* **Hiệu quả:** Tích hợp thanh toán tự động để đẩy tin nhanh chóng.

### 3. Đối với Hệ thống & Vận hành
* **Chất lượng listing:** Áp dụng Multimodal AI (Google Gemini) để quét nội dung nhạy cảm và chất lượng hình ảnh/video tự động.
* **Kiểm soát:** Đội ngũ Admin/Inspector đóng vai trò trọng tài, đảm bảo các giao dịch diễn ra đúng cam kết.

---

## 🏗️ Kiến trúc Hệ thống (Multi-repo)

Dự án được triển khai theo mô hình **Multi-repo** với 5 kho lưu trữ độc lập để tối ưu hóa khả năng mở rộng theo từng domain nghiệp vụ:

| Repository | Công nghệ | Vai trò |
| :--- | :--- | :--- |
| **Frontend (User)** | React + TypeScript | Web app cho khách hàng, người mua và người bán. |
| **Frontend (Admin)** | React + TypeScript | Dashboard quản trị, kiểm duyệt tin, xử lý Report & Order. |
| **Main Backend** | .NET 8 (C#) | API lõi: Auth, Marketplace, Payments, Chat SignalR. |
| **Logistics Service** | Spring Boot (Java) | Quản lý shipper, điều phối lấy hàng (pickup) và tracking. |
| **Documentation** | Markdown | Tài liệu thiết kế hệ thống, Business Rules (Single Source of Truth). |

---

## 🛠️ Điểm nhấn Kỹ thuật

### 🔄 Real-time Communication
* Sử dụng **SignalR** để xây dựng hệ thống Chat trực tiếp giữa Buyer/Seller và hệ thống thông báo (Notifications) tức thời không cần tải lại trang.

### 💳 Thanh toán & Bảo mật
* **VietQR Integration:** Tích hợp qua hệ thống **SePay** (Webhook + Checkout) giúp tự động xác nhận trạng thái đơn hàng/nạp tiền ngay khi có biến động số dư.
* **Security:** Sử dụng **JWT (JSON Web Token)** cho phân quyền, **BCrypt** mã hóa mật khẩu và **Cloudflare Turnstile** để chống bot/spam hiệu quả.

### 🤖 Moderation AI (Multimodal)
* Tích hợp **Google Gemini Pro Vision** để phân tích đồng thời Ảnh + Văn bản (Text). Hệ thống tự động gắn cờ các tin đăng có nội dung không phù hợp hoặc hình ảnh chất lượng thấp trước khi chuyển cho Admin duyệt thủ công.

### ☁️ Media Management
* Toàn bộ hình ảnh và video quay chi tiết xe được lưu trữ và tối ưu hóa qua **Cloudinary**, đảm bảo tốc độ tải nhanh và chuẩn hóa định dạng.

---

## 🔄 Các Luồng Nghiệp Vụ Chính

### 1. Luồng Người bán (Seller Flow)
1.  **Tạo tin:** Điền thông tin, upload ảnh/video.
2.  **AI Scan:** Hệ thống tự động kiểm duyệt nội dung.
3.  **Payment:** Thanh toán phí đăng tin/đẩy tin qua VietQR.
4.  **Display:** Tin hiển thị lên sàn (Video có thể chờ Admin duyệt thêm).

### 2. Luồng Người mua (Buyer Flow)
1.  **Search:** Tìm kiếm qua bộ lọc (Brand, Type, Size).
2.  **Contact:** Chat real-time hỏi tình trạng xe.
3.  **Order:** Đặt cọc hoặc thanh toán toàn bộ qua hệ thống.
4.  **Tracking:** Theo dõi trạng thái vận chuyển từ Logistics service.

### 3. Luồng Quản trị (Admin/Inspector Flow)
* **Moderation:** Duyệt các nội dung AI nghi ngờ hoặc các video quay chi tiết.
* **Inspection:** Inspector nhận yêu cầu, thẩm định thực tế và trả kết quả **TRUE/FALSE** về chất lượng kỹ thuật của xe.
* **Dispute:** Phân xử khi Buyer có báo cáo gian lận hoặc sai khác mô tả.

---

## 🎯 Mục tiêu Dự án
Xây dựng một Marketplace xe đạp thể thao cũ **đáng tin cậy nhất** tại Việt Nam. Chúng tôi không chỉ cung cấp nền tảng công nghệ mà còn cung cấp một quy trình đảm bảo chất lượng, giúp việc mua bán đồ cũ trở nên an toàn như mua đồ mới.

---
🔗 **Tài liệu chi tiết (SRD):** [Google Docs - Cho Xe Đạp](https://docs.google.com/document/d/1zlonvAjk-RDNWWDpfqegYqlIMZxRCvCsMw7RD2fSUzg/edit?usp=sharing)
