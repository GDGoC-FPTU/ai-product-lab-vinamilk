## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **Thụy**, AI Engineer tại **Vin Smart Future**. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của **VinBus** để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo.

Thông qua khảo sát tại Trung tâm Chăm sóc Khách hàng VinBus Hà Nội, tôi nhận thấy đội ngũ tiếp nhận khiếu nại đang xử lý thủ công hàng trăm phản ánh mỗi ngày từ nhiều kênh (hotline, app, zalo), dẫn đến thời gian phản hồi kéo dài và nhiều khiếu nại bị bỏ sót.

Bài toán tôi mang vào buổi Lab hôm nay đến từ chính quan sát thực tế này.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

| # | Subsidiary | Lens               | Mô tả ngắn bài toán                                                                                                                                                                     |
| - | ---------- | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | VinBus     | Lặp lại            | Nhân viên CSKH phân loại thủ công từng khiếu nại từ app, hotline, zalo vào đúng bộ phận xử lý — làm đi làm lại hàng trăm lần/ngày.                                                      |
| 2 | VinBus     | Tốn thời gian      | Soạn thảo email/tin nhắn phản hồi cá nhân hoá cho từng khiếu nại của hành khách mất 8–12 phút/lượt, nội dung lặp lại nhưng không thể dùng mẫu cứng vì mỗi trường hợp có chi tiết riêng. |
| 3 | VinFast    | Lặp lại            | Đối chiếu thủ công hóa đơn bảo hành xe và số liệu đại lý theo tuần.                                                                                                                     |
| 4 | Vinhomes   | AI-upgrade         | Hệ thống phân loại và route tự động các phản hồi/khiếu nại cư dân trên App Vinhomes Resident — hiện phản hồi mất tới 12 tiếng.                                                          |
| 5 | Vinmec     | Pain từ người khác | Bác sĩ mất 20–30 phút viết tóm tắt hồ sơ xuất viện, quá tải và phàn nàn thường xuyên.                                                                                                   |
| 6 | VinBus     | Tốn thời gian      | Tổng hợp và tìm pattern lỗi từ hàng trăm khiếu nại mỗi tuần để báo cáo lên Ban Vận hành — hiện làm thủ công mất nửa ngày/tuần.                                                          |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN:

* #1 — Phân loại khiếu nại
* #2 — Soạn phản hồi
* #6 — Tổng hợp báo cáo

---

## 🚍 Thẻ bài toán tiêu biểu

### Card #2 — VinBus soạn thảo phản hồi khiếu nại cá nhân hoá

```text
┌──────────────────────────────────────────────────────────────┐
│                 QUICK PROBLEM CARD #2                       │
├──────────────────────────────────────────────────────────────┤
│ Bài toán                                                    │
│ Nhân viên CSKH VinBus phải tự soạn từng tin nhắn phản hồi  │
│ cá nhân hoá cho mỗi khiếu nại của hành khách. Không thể    │
│ dùng template cứng vì nội dung phụ thuộc vào tuyến xe,     │
│ loại sự cố và lịch sử của từng khách hàng.                 │
├──────────────────────────────────────────────────────────────┤
│ Công ty thành viên                                          │
│ [x] VinBus                                                  │
├──────────────────────────────────────────────────────────────┤
│ Ai đang đau?                                                │
│ • Nhân viên CSKH: quá tải vì phải đọc và soạn thủ công     │
│ • Hành khách: chờ phản hồi lâu, cảm thấy bị bỏ qua         │
├──────────────────────────────────────────────────────────────┤
│ Workflow thủ công hiện tại                                  │
│ 1. Tiếp nhận khiếu nại từ app / hotline / zalo             │
│ 2. Đọc hiểu nội dung và tra cứu lịch sử hành khách         │
│ 3. Xác định tuyến xe, tài xế, khung giờ liên quan          │
│ 4. Tự soạn phản hồi phù hợp cho từng trường hợp            │
│ 5. Trưởng nhóm duyệt và gửi đi                             │
├──────────────────────────────────────────────────────────────┤
│ Bước tốn thời gian nhất                                     │
│ Step 3–4 (⏱ ~10 phút / lượt xử lý)                         │
├──────────────────────────────────────────────────────────────┤
│ AI có thể hỗ trợ ở đâu?                                     │
│ • Tự động trích xuất thông tin từ khiếu nại                │
│ • Xác định tuyến xe / sự cố liên quan                      │
│ • Draft phản hồi cá nhân hoá theo guideline CSKH           │
├──────────────────────────────────────────────────────────────┤
│ Success Metrics                                             │
│ • Giảm thời gian soạn phản hồi từ 10 phút → dưới 2 phút   │
│ • Tăng số ticket xử lý mỗi ngày / nhân viên                │
│ • Giảm SLA phản hồi chậm                                   │
├──────────────────────────────────────────────────────────────┤
│ Quick Architecture                                          │
│ [x] LLM Feature — AI Complaint Response Copilot            │
└──────────────────────────────────────────────────────────────┘
```
