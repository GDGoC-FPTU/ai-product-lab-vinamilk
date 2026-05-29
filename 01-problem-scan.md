# 01 — Problem Scan (Phase 1 & 2)

> **Lab 02 — AI Product Scoping · Vin Smart Future**
> **Nhóm:** vinamilk


---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là Nguyễn Tài Khoa, **AI Product Engineer** tại **Vin Smart Future**. Nhóm tôi được giao nhiệm vụ quét qua hoạt động vận hành của các công ty thành viên Vingroup để tìm các bottleneck có thể tối ưu bằng AI.

Qua quan sát, tôi thấy nhiều quy trình thủ công đang ngốn thời gian nhân viên và gây khó chịu cho khách hàng — đặc biệt là khâu **hướng dẫn dùng thuốc sau xuất viện tại Vinmec**, nơi điều dưỡng/dược sĩ phải soạn lại hướng dẫn cho từng bệnh nhân. Dưới đây là kết quả SCAN và 3 thẻ bài toán tiềm năng nhất tôi mang vào buổi Lab.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Stakeholder Pain) quét qua vận hành các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinBus** | Stakeholder Pain | App VinBus không hiển thị đầy đủ các tuyến/xe đi qua một trạm và vị trí xe theo thời gian thực; hành khách chờ mù thông tin, hay phàn nàn và bỏ chuyến. |
| 2 | **Vinmec** | Lặp lại | Sau xuất viện, điều dưỡng/dược sĩ lặp lại việc nhắc lịch và giải thích cách dùng thuốc cho từng bệnh nhân (~15–20 phút/người), lặp hàng trăm lượt/ngày. |
| 3 | **Vinpearl / VinWonders** | AI-upgrade | Khách chỉ nhận thông tin tour chung chung và xếp hàng dài; chưa có lịch trình cá nhân hóa né giờ cao điểm theo wait-time thực tế. |
| 4 | **VinFast** | Stakeholder Pain | Chưa có cảnh báo trong cabin khi tài xế mất tập trung / buồn ngủ — rủi ro an toàn trực tiếp cho tài xế và hành khách. |
| 5 | **Vincom Mega Mall** | Tốn thời gian | Khách mất nhiều phút đi vòng quanh tìm xe trong bãi đỗ rộng nhiều tầng; chưa có tính năng "tìm xe của tôi" tra theo biển số. |

*(Lens của #4 và #5 đã hiệu chỉnh cho chính xác: drowsiness là rủi ro an toàn → Stakeholder Pain; đi tìm xe là tác vụ tốn thời gian của khách. Con số là ước tính phục vụ scoping.)*

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ danh sách SCAN: **#2 (Vinmec), #3 (Vinpearl), #5 (Vincom).**

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 — Vinmec                              │
│                                                             │
│ Bài toán: Sau xuất viện, bệnh nhân cần được nhắc lịch và    │
│ hướng dẫn cách dùng thuốc dễ hiểu; điều dưỡng/dược sĩ        │
│ phải soạn thủ công cho từng người.                          │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau? Dược sĩ/điều dưỡng (quá tải) và bệnh nhân       │
│ (dễ hiểu sai cách dùng thuốc).                              │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bác sĩ kê đơn                                          │
│   → 2. Điều dưỡng đọc đơn, tra cứu cách dùng từng thuốc      │
│   → 3. Soạn/diễn giải hướng dẫn dễ hiểu cho bệnh nhân        │
│   → 4. Dặn lịch nhắc uống thuốc                             │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ ~15 phút/bệnh nhân)          │
│ AI nhảy vào ở bước nào? Bước 3 — LLM soạn bản nháp           │
│ hướng dẫn dùng thuốc theo đúng đơn đã kê.                    │
│                                                             │
│ Metric (có số): Giảm thời gian soạn từ ~15 phút → dưới       │
│ 3 phút/bệnh nhân; 100% bản nháp phải được dược sĩ duyệt.     │
│                                                             │
│ Quick Architecture: [x] LLM Feature (bắt buộc HITL)         │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 — Vinpearl / VinWonders               │
│                                                             │
│ Bài toán: Trợ lý AI gợi ý lịch trình tham quan cá nhân hóa   │
│ và trả lời câu hỏi bằng ngôn ngữ tự nhiên, giúp giảm         │
│ thời gian chờ của khách.                                    │
│ Công ty thành viên: [x] Vinpearl / VinWonders               │
│                                                             │
│ Ai đang đau? Khách tham quan (chờ lâu, bỏ lỡ trò chơi),      │
│ nhân viên concierge (trả lời lặp lại).                      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách đến, xem bản đồ tĩnh / hỏi nhân viên             │
│   → 2. Tự chọn trò chơi theo cảm tính                       │
│   → 3. Di chuyển & xếp hàng (không biết chỗ nào đang đông)   │
│   → 4. Chờ lâu, lịch trình rời rạc                          │
│                                                             │
│ Bước nào tốn nhất? Bước 3 (⏱ ~30-45 phút chờ/khách/ngày)    │
│ AI nhảy vào ở bước nào? Bước 1-2 — LLM hỏi sở thích →        │
│ đề xuất lịch trình + Q&A đa ngôn ngữ.                       │
│                                                             │
│ Metric (có số): Giảm thời gian chờ trung bình 20%; tăng     │
│ số trải nghiệm hoàn thành/khách/ngày.                       │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
│ (Lưu ý: phần tối ưu wait-time thực cần data hàng đợi)        │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #5 — Vincom Mega Mall                    │
│                                                             │
│ Bài toán: Giúp khách tìm lại xe trong bãi đỗ rộng nhiều      │
│ tầng bằng cách tra cứu vị trí theo biển số.                 │
│ Công ty thành viên: [x] Khác: Vincom Retail (Mega Mall)     │
│                                                             │
│ Ai đang đau? Khách mua sắm (đi tìm xe mệt mỏi),             │
│ bảo vệ bãi xe (bị hỏi liên tục).                            │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách gửi xe, không nhớ vị trí                         │
│   → 2. Mua sắm xong, quay lại bãi                           │
│   → 3. Đi vòng quanh các tầng tìm xe                        │
│   → 4. Hỏi bảo vệ / dò từng khu                             │
│                                                             │
│ Bước nào tốn nhất? Bước 3 (⏱ ~5-10 phút/lượt)               │
│ AI nhảy vào ở bước nào? Bước 1 & 3 — camera nhận diện        │
│ biển số (LPR) ghi vị trí; khách tra "tìm xe của tôi".       │
│                                                             │
│ Metric (có số): Giảm thời gian tìm xe từ ~8 phút →           │
│ dưới 1 phút/lượt.                                           │
│                                                             │
│ Quick Architecture: [x] Rule (+ thị giác máy tính / LPR)    │
│ KHÔNG phải LLM — dùng LLM ở đây là overkill.                │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn

Bài tôi đề xuất mang sang Deep-Dive: **Card #2 — Vinmec (Hướng dẫn dùng thuốc sau xuất viện).**

## Lý do chọn và loại bỏ các thẻ khác:
* **Card #3 (Vinpearl):** Ứng viên LLM tốt, nhưng phần tối ưu theo wait-time *thực tế* cần dữ liệu hàng đợi real-time — chưa chắc sẵn sàng (data-readiness). Phù hợp giai đoạn **"Not Yet"** hơn là build ngay.
* **Card #5 (Vincom):** Sau khi chấm nhanh, đây là bài toán **rule + thị giác máy tính (LPR)**, không phải LLM. Dùng LLM ở đây là *overkill* (đúng anti-pattern "AI overkill" trong bài giảng Ngày 2) → nên để rule-based xử lý, không đưa vào prototype LLM.

**Vì sao Card #2 thắng:** tác vụ ngôn ngữ rõ ràng (soạn hướng dẫn), actor & workflow cụ thể, metric đo được, và đặc biệt có **ranh giới an toàn quan trọng** (y tế) — rất hợp để stress-test bằng prompt prototype ở Phase 4.