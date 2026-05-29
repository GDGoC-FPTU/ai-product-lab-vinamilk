Phase 1:
#|Subsidiary|Lens|Mô tả ngắn bài toán|
1|VinFast|Repetitive|Kỹ thuật viên phải kiểm tra log lỗi pin EV thủ công sau mỗi lượt bảo trì để xác định nguy cơ chai pin hoặc lỗi cell bất thường|
2|Xanh SM|Stakeholder Pain|Tài xế thường phàn nàn hệ thống gợi ý điểm đón khách chưa chính xác tại khu đông người|
3|Vinhomes|Time-consuming|Nhân viên CSKH phải đọc và phản hồi hàng trăm ticket cư dân mỗi ngày (ồn ào, thang máy, gửi xe, điện nước)|
4|Vinmec|AI-upgrade|Bác sĩ/radiologist mất nhiều thời gian đọc ảnh X-ray/CT trước khi đưa ra chẩn đoán sơ bộ|
5|VinFast|Time-consuming|Bộ phận supply chain mất nhiều giờ tổng hợp dữ liệu tồn kho linh kiện từ nhiều nhà máy và supplier khác nhau|
6|Vinpearl|Time-consuming|Nhân viên vận hành resort mất nhiều thời gian dự đoán lượng khách để phân bổ nhân sự và chuẩn bị phòng|

Phase 2:
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                      │
│                                                             │
│ Bài toán (1 câu):                                           │
│ VinFast cần phát hiện sớm nguy cơ chai pin/lỗi pin EV       │
│ trước khi xe gặp sự cố ngoài thực tế.                       │
│                                                             │
│ Công ty thành viên:                                         │
│ [✓] VinFast  [ ] Xanh SM  [ ] Vinhomes                      │
│ [ ] Vinmec   [ ] Khác                                       │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Kỹ thuật viên bảo trì, đội warranty, khách hàng EV.         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│ 1. Xe gửi log vận hành                                      │
│    ──> 2. Kỹ thuật viên đọc log pin                         │
│    ──> 3. So sánh ngưỡng lỗi thủ công                       │
│    ──> 4. Quyết định bảo trì/bảo hành                       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Phân tích log pin thủ công                                  │
│ (⏱ ~20-40 phút/xe)                                          │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Phân tích anomaly trong telemetry/log dữ liệu pin EV.       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian phân tích từ 30 phút -> dưới 5 phút        │
│ - Giảm 25% case pin lỗi phát hiện muộn                      │
│ - Tăng accuracy dự đoán lỗi pin >90%                        │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI  [ ] Rule  [✓] LLM  [✓] Agent                     │
└─────────────────────────────────────────────────────────────┘

