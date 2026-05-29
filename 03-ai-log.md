AI giúp gì?
Trong buổi Lab, tôi sử dụng Claude để hỗ trợ 3 việc chính:

1. Brainstorm danh sách bài toán (Phase 1 — SCAN): Tôi prompt Claude mô tả ngắn vận hành của VinBus và yêu cầu nó gợi ý các điểm đau tiềm năng theo từng Lens (Lặp lại / Tốn thời gian / AI-upgrade / Pain từ người khác). Claude trả về 8–10 gợi ý trong vòng 30 giây, giúp tôi không bị "blank page" và có ngay nguyên liệu để lọc.

2. Viết và tinh chỉnh Prompt cho prototype: Tôi nhờ Claude soạn system prompt cho bài toán draft phản hồi khiếu nại, bao gồm cả phần hướng dẫn format JSON output và các quy tắc an toàn (DRAFT_ONLY, ESCALATE). Claude giúp tôi đưa những yêu cầu mơ hồ ("phải an toàn") thành quy tắc cụ thể, kiểm tra được.

3. Thiết kế kịch bản tấn công Adversarial Test: Tôi hỏi Claude "Nếu là kẻ muốn bypass ranh giới an toàn, bạn sẽ tấn công prompt này thế nào?" — Claude đề xuất 5 kịch bản tấn công khác nhau, giúp nhóm chọn ra kịch bản thực tế nhất (hành khách VIP doạ đăng báo và đòi bồi thường) để kiểm tra.

AI sai gì?
Có một điểm Claude đưa ra đề xuất sai lệch đáng kể:

Khi tôi hỏi về kiến trúc hệ thống để phân loại loại khiếu nại (Card #1), Claude đề xuất xây dựng một pipeline phân loại 3 tầng gồm: rule-based keyword filter → intent classifier fine-tuned → sentiment analyzer riêng biệt — rồi aggregate kết quả từ 3 model để ra quyết định routing cuối cùng.

Đây là đề xuất over-engineered nghiêm trọng cho giai đoạn đầu. Với ~120 khiếu nại/ngày và chỉ 6–8 loại phân loại cố định, một LLM single-call với few-shot examples là hoàn toàn đủ. Claude đã mắc lỗi điển hình: tối ưu hóa cho độ chính xác lý thuyết thay vì tối ưu cho chi phí triển khai và tốc độ ra mắt thực tế.
Sửa đổi ra sao?
Tôi điều chỉnh bằng cách thêm ràng buộc rõ ràng về nguồn lực và giai đoạn vào trong prompt:

Prompt cũ (thiếu ràng buộc)

"Đề xuất kiến trúc AI tốt nhất để phân loại khiếu nại hành khách VinBus."
Prompt mới (có ràng buộc)

"Đề xuất kiến trúc AI tối giản nhất (ưu tiên single API call, không fine-tune) 
để phân loại khiếu nại hành khách VinBus vào 8 loại cố định. 
Giải thích tại sao không cần pipeline phức tạp hơn ở giai đoạn pilot 
với quy mô 120 khiếu nại/ngày."
Sau khi thêm ràng buộc, Claude điều chỉnh và đề xuất đúng hướng: dùng một LLM call duy nhất với system prompt liệt kê 8 loại + 2 ví dụ mỗi loại (few-shot), output là JSON với trường category và confidence_score. Đơn giản, triển khai được trong 1 ngày, và dễ mở rộng sau khi có dữ liệu thực.

Bài học: AI rất giỏi tối ưu trong phạm vi được giao — nhưng nếu không chỉ định rõ ràng buộc về nguồn lực, thời gian và giai đoạn triển khai, nó sẽ mặc định đề xuất giải pháp "hoàn hảo về lý thuyết" thay vì "đủ tốt để ship sớm". Người dùng phải là người đặt ra ràng buộc thực tế, AI chỉ tối ưu trong không gian đó.

