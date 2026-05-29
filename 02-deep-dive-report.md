# 02-deep-dive-report.md

# Deep-Dive Report — Vin Smart Future

## Quyết định lựa chọn

Nhóm chọn bài toán:

> “AI hỗ trợ tự động phân loại và phản hồi ticket cư dân tại Vinhomes.”

Lý do lựa chọn:

* Có lượng ticket lớn mỗi ngày.
* Workflow hiện tại còn thủ công.
* Có dữ liệu text sẵn để train/test AI.
* Hiệu quả có thể đo bằng SLA và CSAT.

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow Mapping

### Current Workflow

1. Cư dân gửi ticket qua app/chat.
2. Nhân viên CSKH đọc ticket.
3. CSKH phân loại thủ công.
4. Chuyển ticket cho bộ phận liên quan.
5. Soạn phản hồi cho cư dân.
6. Theo dõi trạng thái xử lý.

---

### Bottleneck & Handoff

🔴 Bottleneck:

* Phân loại ticket thủ công.
* Soạn phản hồi lặp lại nhiều lần.
* Routing nhầm bộ phận.

🔄 Handoff:

* CSKH → Kỹ thuật.
* CSKH → Ban quản lý.
* CSKH → Bảo vệ.

⏱ Tổng thời gian xử lý:

* Khoảng 10-15 phút/ticket.

---

## 3.2. Problem Statement (6-field)

| Field                       | Nội dung                                                                                                            |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **1. Actor / Operator**     | Nhân viên CSKH và ban quản lý tòa nhà Vinhomes.                                                                     |
| **2. Current Workflow**     | Ticket được đọc, phân loại và phản hồi thủ công qua CRM/chat system.                                                |
| **3. Bottleneck**           | Phân loại ticket và soạn phản hồi mất nhiều thời gian, dễ sai sót.                                                  |
| **4. Business Impact**      | SLA phản hồi chậm, backlog ticket giờ cao điểm, cư dân không hài lòng.                                              |
| **5. Success Metric**       | - 85% ticket classify dưới 10 giây. <br> - Giảm first-response-time từ 15 phút xuống dưới 2 phút.                   |
| **6. Operational Boundary** | AI chỉ được classify, draft phản hồi và suggest routing. Ticket khẩn cấp hoặc pháp lý bắt buộc cần nhân viên duyệt. |

---

## 3.3. Future-State Flow & AI Fit

### AI-Fit Matrix

* [ ] Rule / State-Machine
* [✓] LLM Feature
* [✓] Agentic Loop

---

## Future-State Flow

```text
1. Cư dân gửi ticket
        ↓
🔵 AI classify intent & priority
        ↓
🔵 AI draft phản hồi
        ↓
🔵 AI suggest routing department
        ↓
🟢 CSKH review & approve (HITL)
        ↓
Ticket được chuyển xử lý
        ↓
🟢 Nhân viên xử lý thực tế
        ↓
🔵 AI generate update message
```

---

## Human-in-the-loop (HITL)

Các trường hợp bắt buộc cần con người duyệt:

* Khiếu nại pháp lý/tài chính.
* Ticket khẩn cấp.
* Ticket có sentiment tiêu cực cao.
* AI confidence thấp.

---

## Fallback Plan

↩️ Nếu AI:

* classify sai,
* confidence thấp,
* hoặc system lỗi,

thì ticket sẽ tự động chuyển về queue xử lý thủ công theo workflow cũ.

---

# 🏁 Phase 5 — EVALUATE

## AI Readiness Checklist

1. [✓] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test.
2. [✓] Rủi ro khi AI sai nằm trong tầm kiểm soát qua HITL và fallback.
3. [✓] Stakeholders sẵn sàng thay đổi workflow cũ.

---

## Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

* [✓] GO (Bắt đầu xây dựng Prototype)
* [ ] NOT YET
* [ ] NO-GO

---

## Justification

Nhóm quyết định GO vì:

* Dữ liệu ticket text đã có sẵn trong hệ thống.
* ROI rõ ràng: giảm workload CSKH và tăng tốc phản hồi cư dân.
* Có thể triển khai prototype với chi phí vừa phải.
* Rủi ro được kiểm soát nhờ HITL và fallback thủ công.

Chi phí giai đoạn đầu chủ yếu gồm:

* API LLM,
* tích hợp CRM,
* logging và monitoring,
* training/testing dữ liệu nội bộ.

Prototype ban đầu chỉ tập trung:

* classify ticket,
* draft phản hồi,
* routing suggestion,

chưa cần xây dựng autonomous AI agent phức tạp.


# WORKFLOW DIAGRAM — CURRENT STATE (BEFORE AI)

```
            CURRENT-STATE WORKFLOW
    Vinhomes Resident Ticket Handling Process
```

┌──────────────────────────────────────────────┐
│ 1. Cư dân gửi ticket qua App / Chat         │
│----------------------------------------------│
│ Nội dung:                                    │
│ - Thang máy lỗi                              │
│ - Ồn ào                                      │
│ - Điện/nước                                  │
│ - Gửi xe                                     │
│----------------------------------------------│
│ ⏱ Thời gian: ~1 phút                         │
└──────────────────────────────────────────────┘
│
▼

┌──────────────────────────────────────────────┐
│ 2. Nhân viên CSKH mở và đọc ticket          │
│----------------------------------------------│
│ Công việc:                                   │
│ - Đọc nội dung cư dân                        │
│ - Hiểu vấn đề                                │
│ - Kiểm tra thông tin căn hộ                  │
│----------------------------------------------│
│ ⏱ Thời gian: ~2-3 phút                       │
└──────────────────────────────────────────────┘
│
▼

🔴 BOTTLENECK
┌──────────────────────────────────────────────┐
│ 3. CSKH phân loại ticket thủ công           │
│----------------------------------------------│
│ Công việc:                                   │
│ - Xác định loại vấn đề                       │
│ - Chọn phòng ban xử lý                       │
│ - Đánh dấu mức độ ưu tiên                    │
│----------------------------------------------│
│ Rủi ro:                                      │
│ - Phân loại sai                              │
│ - Chuyển nhầm bộ phận                        │
│ - Ticket bị backlog                          │
│----------------------------------------------│
│ ⏱ Thời gian: ~3-5 phút                       │
└──────────────────────────────────────────────┘
│
▼

🔄 HANDOFF
┌──────────────────────────────────────────────┐
│ 4. Chuyển ticket sang bộ phận liên quan     │
│----------------------------------------------│
│ Các bộ phận nhận xử lý:                      │
│ - Kỹ thuật                                   │
│ - Bảo vệ                                     │
│ - Ban quản lý                                │
│ - Vệ sinh                                    │
│----------------------------------------------│
│ ⏱ Thời gian: ~1-2 phút                       │
└──────────────────────────────────────────────┘
│
▼

🔴 BOTTLENECK
┌──────────────────────────────────────────────┐
│ 5. CSKH soạn phản hồi cho cư dân            │
│----------------------------------------------│
│ Công việc:                                   │
│ - Gõ phản hồi thủ công                       │
│ - Giải thích tình trạng xử lý                │
│ - Xin lỗi / cập nhật tiến độ                 │
│----------------------------------------------│
│ Rủi ro:                                      │
│ - Trả lời chậm                               │
│ - Nội dung không đồng nhất                   │
│ - Quá tải giờ cao điểm                       │
│----------------------------------------------│
│ ⏱ Thời gian: ~3-5 phút                       │
└──────────────────────────────────────────────┘
│
▼

🔄 HANDOFF
┌──────────────────────────────────────────────┐
│ 6. Bộ phận vận hành xử lý thực tế           │
│----------------------------------------------│
│ Ví dụ:                                       │
│ - Kỹ thuật sửa thang máy                     │
│ - Bảo vệ xử lý tiếng ồn                      │
│ - Ban quản lý kiểm tra điện/nước             │
│----------------------------------------------│
│ ⏱ Thời gian: Phụ thuộc mức độ sự cố          │
└──────────────────────────────────────────────┘
│
▼

┌──────────────────────────────────────────────┐
│ 7. CSKH cập nhật trạng thái & đóng ticket   │
│----------------------------------------------│
│ Công việc:                                   │
│ - Thông báo cư dân                           │
│ - Xác nhận hoàn thành                        │
│ - Đóng ticket trên hệ thống                  │
│----------------------------------------------│
│ ⏱ Thời gian: ~1-2 phút                       │
└──────────────────────────────────────────────┘

═══════════════════════════════════════════════
📊 TỔNG QUAN VẬN HÀNH
═══════════════════════════════════════════════

⏱ Tổng thời gian trung bình:
~10-15 phút / ticket

🔴 Bottleneck chính:

1. Phân loại ticket thủ công
2. Soạn phản hồi thủ công

🔄 Handoff chính:

1. CSKH → Bộ phận vận hành
2. Bộ phận vận hành → CSKH

⚠️ Pain Points:

* Backlog ticket giờ cao điểm
* Routing sai bộ phận
* SLA phản hồi chậm
* CSKH bị quá tải
* Cư dân không hài lòng
