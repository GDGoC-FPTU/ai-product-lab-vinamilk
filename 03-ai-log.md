# 🤖 AI Reflection

## AI giúp gì?

Trong buổi Lab, tôi sử dụng Claude để hỗ trợ 3 việc chính:

### 1. Brainstorm bài toán

Tôi mô tả ngắn vận hành của VinBus và yêu cầu Claude gợi ý pain points theo từng Lens:

* Lặp lại
* Tốn thời gian
* AI-upgrade
* Pain từ người khác

Claude trả về nhiều ý tưởng chỉ trong ~30 giây, giúp tôi có nhanh danh sách bài toán để chọn lọc.

---

### 2. Viết Prompt cho prototype

Tôi dùng Claude để hỗ trợ viết system prompt cho bài toán draft phản hồi khiếu nại.

Claude giúp:

* chuẩn hóa JSON output,
* bổ sung rule an toàn (`DRAFT_ONLY`, `ESCALATE`),
* biến yêu cầu mơ hồ thành rule rõ ràng hơn.

---

### 3. Thiết kế Adversarial Test

Tôi hỏi Claude:

> “Nếu muốn bypass prompt này thì có thể tấn công như thế nào?”

Claude đề xuất nhiều kịch bản khác nhau, giúp nhóm chọn được case thực tế nhất:

> hành khách VIP đòi bồi thường và đe doạ truyền thông.
# ⚠️ AI sai gì?

Khi tôi hỏi về kiến trúc phân loại khiếu nại, Claude đề xuất pipeline quá phức tạp:

* keyword filter,
* classifier riêng,
* sentiment model riêng,
* rồi aggregate kết quả.

Trong khi thực tế:

* chỉ ~120 khiếu nại/ngày,
* chỉ có 6–8 loại cố định,
* đang ở giai đoạn pilot.

Một LLM single-call với few-shot examples là đã đủ.

# 🔧 Tôi sửa như thế nào?

Tôi thêm ràng buộc rõ hơn vào prompt:

## Prompt cũ

```text id="p1x2a"
Đề xuất kiến trúc AI tốt nhất để phân loại khiếu nại hành khách VinBus.
```

## Prompt mới

```text id="p2y3b"
Đề xuất kiến trúc AI tối giản nhất (ưu tiên single API call, không fine-tune) 
để phân loại khiếu nại VinBus vào 8 loại cố định.
```

Sau đó Claude đề xuất đúng hướng hơn:

* dùng 1 LLM call,
* few-shot examples,
* output JSON gồm `category` và `confidence_score`.


# 🎯 Bài học

AI rất giỏi tối ưu trong phạm vi được giao.

Nếu không đưa rõ:

* nguồn lực,
* thời gian,
* quy mô triển khai,

thì AI thường sẽ đề xuất giải pháp “đẹp về kỹ thuật” thay vì “đủ tốt để ship nhanh”.
