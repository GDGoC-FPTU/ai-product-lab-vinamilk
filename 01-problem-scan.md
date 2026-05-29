Tôi là Thụy, AI Engineer tại Vin Smart Future. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của VinBus để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo.

Thông qua khảo sát tại Trung tâm Chăm sóc Khách hàng VinBus Hà Nội, tôi nhận thấy đội ngũ tiếp nhận khiếu nại đang xử lý thủ công hàng trăm phản ánh mỗi ngày từ nhiều kênh (hotline, app, zalo), dẫn đến thời gian phản hồi kéo dài và nhiều khiếu nại bị bỏ sót. Bài toán tôi mang vào buổi Lab hôm nay đến từ chính quan sát thực tế này.

| #	|Subsidiary|	|Lens|	|Mô tả ngắn bài toán|
|---|----------|
|1	|  VinBus  |	|Lặp lại|	|Nhân viên CSKH phân loại thủ công từng khiếu nại từ app, hotline, zalo vào đúng bộ phận xử lý — làm đi làm lại hàng trăm lần/ngày.|
|2	|   VinBus |	|Tốn thời gian|	|Soạn thảo email/tin nhắn phản hồi cá nhân hoá cho từng khiếu nại của hành khách mất 8–12 phút/lượt, nội dung lặp lại nhưng không thể dùng mẫu cứng vì mỗi trường hợp có chi tiết riêng.|
|3	|VinFast   |	|Lặp lại|	|Đối chiếu thủ công hóa đơn bảo hành xe và số liệu đại lý theo tuần.|
|4	|Vinhomes  |	|AI-upgrade|	|Hệ thống phân loại và route tự động các phản hồi/khiếu nại cư dân trên App Vinhomes Resident — hiện phản hồi mất tới 12 tiếng.|
|5	|Vinmec    |	|Pain từ người khác|	|Bác sĩ mất 20–30 phút viết tóm tắt hồ sơ xuất viện, quá tải và phàn nàn thường xuyên.|
|6	|VinBus    |	|Tốn thời gian|	|Tổng hợp và tìm pattern lỗi từ hàng trăm khiếu nại mỗi tuần để báo cáo lên Ban Vận hành — hiện làm thủ công mất nửa ngày/tuần.|

Chọn top 3 từ danh sách SCAN: #1 (Phân loại khiếu nại), #2 (Soạn phản hồi), #6 (Tổng hợp báo cáo).

Thẻ bài toán tiêu biểu: Card #2 — VinBus soạn thảo phản hồi khiếu nại cá nhân hoá

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Nhân viên CSKH VinBus phải tự soạn từng tin nhắn  │
│ phản hồi cá nhân hoá cho mỗi khiếu nại của hành khách —     │
│ không thể dùng mẫu cứng vì nội dung phụ thuộc vào từng      │
│ tuyến xe, sự cố cụ thể, và lịch sử của hành khách đó.       │
│                                                             │
│ Công ty thành viên: [x] VinBus                              │
│                                                             │
│ Ai đang đau? Nhân viên CSKH (quá tải soạn thảo), Hành       │
│ khách (chờ phản hồi quá lâu, cảm thấy bị bỏ qua).          │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tiếp nhận khiếu nại từ app / hotline / zalo            │
│   → 2. Đọc hiểu nội dung và tra cứu lịch sử hành khách      │
│   → 3. Xác định tuyến xe, tài xế, khung giờ liên quan       │
│   → 4. Tự soạn nội dung phản hồi phù hợp với từng trường hợp│
│   → 5. Trưởng nhóm duyệt và gửi đi                         │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 10 phút/lượt)               │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (Tự động trích xuất thông tin -> Draft phản hồi cá nhân hoá) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn phản hồi từ 10 phút ──> dưới 2 phút.    │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Tự động draft phản hồi) │
└─────────────────────────────────────────────────────────────┘
