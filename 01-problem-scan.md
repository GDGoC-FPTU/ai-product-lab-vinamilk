# 01 — Problem Scan (Phase 1 & 2)

> **Lab 02 — AI Product Scoping · Vin Smart Future**
> **Nhóm:** vinamilk
> **Họ và tên:** _[điền tên của bạn]_ — **Email/MSSV:** _[điền]_

---

## 🏛️ Bối cảnh

Tôi đóng vai **AI Product Engineer** tại **Vin Smart Future**. Ở phase này tôi dùng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Stakeholder Pain) để quét qua hoạt động vận hành của các công ty thành viên Vingroup, ghi lại các bottleneck thực tế, rồi quick-assess 3 bài toán tiềm năng nhất để đánh giá đúng mức tự động hóa (No AI / Rule / LLM / Agent) trước khi nghĩ đến model.

---

# 🔍 Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinBus** | Stakeholder Pain | App VinBus không hiển thị đầy đủ các tuyến/xe đi qua một trạm, cũng như vị trí xe theo thời gian thực. Hành khách chờ mà không biết xe có đang đến hay không, dễ phàn nàn và bỏ chuyến. |
| 2 | **Vinmec** | Lặp lại (Repetitive) | Sau khi xuất viện, điều dưỡng/dược sĩ phải lặp lại việc nhắc lịch uống thuốc và giải thích cách dùng cho từng bệnh nhân (~15–20 phút/người), lặp hàng trăm lượt mỗi ngày. |
| 3 | **Vinpearl / VinWonders** | AI-upgrade | Khách chỉ nhận thông tin tour chung chung và hay xếp hàng dài. Chưa có lịch trình cá nhân hóa biết né các trò chơi đang đông theo thời gian chờ thực tế. |
| 4 | **VinFast** | Stakeholder Pain | Chưa có cảnh báo trong cabin khi tài xế mất tập trung hoặc buồn ngủ — rủi ro an toàn trực tiếp cho tài xế và hành khách. |
| 5 | **Vincom Mega Mall** | Tốn thời gian (Time-consuming) | Khách mất nhiều phút đi vòng quanh tìm xe trong bãi đỗ rộng nhiều tầng; chưa có tính năng "tìm xe của tôi" tra theo biển số. |

*(Lưu ý: lens của #4 và #5 tôi đã hiệu chỉnh so với phán đoán ban đầu — drowsiness là rủi ro an toàn nên thuộc Stakeholder Pain, còn việc đi tìm xe là tác vụ tốn thời gian của khách. Con số là ước tính phục vụ scoping.)*

---

# 🃏 Phase 2 — QUICK-ASSESS (3 Quick Problem Cards)

Top 3 chọn ra: **#2 Vinmec**, **#3 Vinpearl**, **#5 Vincom**. Hai bài đầu là ứng viên LLM thật sự (có ngôn ngữ tự nhiên + cần soạn/tổng hợp); bài thứ ba được giữ lại để thể hiện việc *chấm đúng mức tự động hóa* — nó thực ra là bài toán rule + thị giác máy tính, không phải LLM.

---

## QUICK PROBLEM CARD #1 — Vinmec: Hướng dẫn dùng thuốc sau xuất viện

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Sau khi xuất viện, bệnh nhân cần được nhắc lịch và hướng dẫn cách dùng thuốc bằng ngôn ngữ dễ hiểu; hiện điều dưỡng/dược sĩ phải soạn thủ công cho từng người. |
| **Công ty thành viên** | [x] Vinmec |
| **Ai đang đau (Actor)** | Dược sĩ/điều dưỡng (người soạn, đang quá tải) và bệnh nhân (người nhận, dễ hiểu sai cách dùng). |
| **Workflow thủ công (4 bước)** | 1. Bác sĩ kê đơn → 2. Điều dưỡng đọc đơn, tra cứu cách dùng từng thuốc → 3. Soạn/diễn giải hướng dẫn dễ hiểu cho bệnh nhân → 4. Dặn lịch nhắc uống. |
| **Bước tốn nhất** | Bước 2–3 (tra cứu + soạn hướng dẫn dễ hiểu): ⏱ ~15 phút/bệnh nhân. |
| **AI nhảy vào ở bước nào** | Bước 3 — LLM soạn **bản nháp** hướng dẫn dùng thuốc bằng tiếng Việt dễ hiểu, lấy đúng theo đơn đã kê. |
| **Metric (có số)** | Giảm thời gian soạn hướng dẫn từ ~15 phút → **dưới 3 phút/bệnh nhân**; **100%** bản nháp phải được dược sĩ duyệt trước khi gửi. |
| **Quick Architecture** | [x] **LLM Feature** — bắt buộc HITL (dược sĩ duyệt). Ranh giới: AI chỉ diễn giải đúng theo đơn, **cấm** tự đề xuất liều, chẩn đoán, hoặc tư vấn tương tác thuốc ngoài đơn. |

---

## QUICK PROBLEM CARD #2 — Vinpearl: Trợ lý lịch trình cá nhân hóa

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Trợ lý AI gợi ý lịch trình tham quan cá nhân hóa cho khách Vinpearl/VinWonders và trả lời câu hỏi bằng ngôn ngữ tự nhiên, giúp giảm thời gian chờ. |
| **Công ty thành viên** | [x] Vinpearl / VinWonders |
| **Ai đang đau (Actor)** | Khách tham quan (chờ lâu, bỏ lỡ trò chơi) và nhân viên concierge (trả lời lặp lại). |
| **Workflow thủ công (4 bước)** | 1. Khách đến, xem bản đồ tĩnh / hỏi nhân viên → 2. Tự chọn trò chơi theo cảm tính → 3. Di chuyển & xếp hàng (không biết chỗ nào đang đông) → 4. Chờ lâu, lịch trình rời rạc. |
| **Bước tốn nhất** | Bước 3 (xếp hàng & đi lại không tối ưu): ⏱ ~30–45 phút chờ/khách/ngày. |
| **AI nhảy vào ở bước nào** | Bước 1–2 — LLM hỏi sở thích → đề xuất lịch trình theo thứ tự hợp lý + trả lời câu hỏi đa ngôn ngữ. |
| **Metric (có số)** | Giảm thời gian chờ trung bình **20%**; tăng số trải nghiệm hoàn thành/khách/ngày. |
| **Quick Architecture** | [x] **LLM Feature** (phần đề xuất + Q&A). Rủi ro: phần tối ưu theo wait-time *thực tế* cần dữ liệu hàng đợi real-time → cần kiểm tra data-readiness trước. |

---

## QUICK PROBLEM CARD #3 — Vincom Mega Mall: Tìm xe trong bãi đỗ

| Trường | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Giúp khách tìm lại xe trong bãi đỗ Vincom Mega Mall rộng nhiều tầng bằng cách tra cứu vị trí theo biển số. |
| **Công ty thành viên** | [x] Khác: Vincom Retail (Vincom Mega Mall) |
| **Ai đang đau (Actor)** | Khách đi mua sắm (đi tìm xe mệt mỏi) và bảo vệ bãi xe (bị hỏi liên tục). |
| **Workflow thủ công (4 bước)** | 1. Khách gửi xe, không nhớ vị trí → 2. Mua sắm xong, quay lại bãi → 3. Đi vòng quanh các tầng tìm xe → 4. Hỏi bảo vệ / dò từng khu. |
| **Bước tốn nhất** | Bước 3 (đi tìm xe): ⏱ ~5–10 phút/lượt. |
| **AI nhảy vào ở bước nào** | Bước 1 & 3 — camera nhận diện biển số (LPR) ghi vị trí lúc vào; khách tra "tìm xe của tôi" bằng biển số trên kiosk/app. |
| **Metric (có số)** | Giảm thời gian tìm xe từ ~8 phút → **dưới 1 phút/lượt**. |
| **Quick Architecture** | [x] **Rule** (+ thị giác máy tính cho LPR). **Không phải LLM** — đây là bài toán dữ liệu + nhận diện biển số; dùng LLM là *overkill* (đúng anti-pattern "AI overkill" trong bài giảng Ngày 2). |

---

### 🎯 Ghi chú lựa chọn

Bài mạnh nhất để mang sang Deep-Dive là **Card #1 (Vinmec)**: tác vụ ngôn ngữ rõ ràng, có actor & workflow cụ thể, metric đo được, và **ranh giới an toàn quan trọng** (rất hợp để stress-test bằng prompt prototype ở Phase 4). Card #3 được giữ lại có chủ đích để minh họa nguyên tắc: chọn đúng *mức* tự động hóa quan trọng hơn việc gán nhãn "AI" cho mọi thứ.