# 09 · Alignment, preference learning và reasoning

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 20 giờ học và thực hành nhập môn; triển khai RL ở quy mô lớn là phần mở rộng.

**Học trước:** [07 · Đánh giá LLM](../07-evaluation/README.md) và [08 · SFT và PEFT](../08-sft-peft/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox thể hiện phần nội dung cần biên soạn hoặc kiểm tra chung. Điều kiện hoàn thành của người học được ghi riêng.

## Mục tiêu

- Phân biệt học từ đáp án mẫu, từ cặp ưu tiên và từ phần thưởng.
- Giải thích các thành phần chính của RLHF, DPO và RL với phần thưởng kiểm chứng được.
- Hiểu tăng compute khi suy luận và thay đổi trọng số qua huấn luyện là hai quyết định khác nhau.
- Phát hiện khi model tối ưu metric hoặc reward nhưng chưa đạt mục tiêu thực tế.

## Checklist nội dung

- [ ] Biên soạn bản đồ hậu huấn luyện: SFT, preference optimization và reinforcement learning.
- [ ] Giải thích preference pair, rubric, chất lượng nhãn, bất đồng người chấm và nhiễu dữ liệu.
- [ ] Trình bày pipeline RLHF: policy, reward model, reference model và vai trò kiểm soát độ lệch.
- [ ] Viết bài DPO từ trực giác so sánh cặp tới objective; phân biệt với vòng thu rollout online.
- [ ] Giới thiệu reward kiểm chứng được, policy gradient và trực giác GRPO trước các biến thể triển khai.
- [ ] Phân tích reward hacking, length bias, verifier sai, overoptimization và đánh đổi năng lực.
- [ ] Giải thích reasoning traces, distillation và giới hạn khi xem lời giải sinh ra là mô tả trung thực cơ chế nội bộ.
- [ ] Soạn phần inference-time compute: lấy nhiều lời giải, self-consistency, verifier và ngân sách token.
- [ ] Xây cách đánh giá reasoning bằng đáp án, khả năng tổng quát và compute được ghi nhận, không chỉ độ dài lời giải.

## Thực hành đề xuất

### Lab chính: reasoning với ngân sách suy luận rõ ràng

Chọn một bộ bài toán nhỏ có đáp án kiểm được, tách development/test theo nhóm hoặc cách tạo bài. Dùng một model đã có năng lực cơ bản trên loại nhiệm vụ đó.

So sánh sinh một lời giải với sinh nhiều ứng viên rồi chọn bằng quy tắc định trước. Ghi số lần gọi, tổng token và thời gian thực tế; không chỉ báo điểm đúng.

Kiểm tra verifier trên ví dụ cố tình sai và trường hợp biên. Nếu dùng đáp án chuẩn để chọn ứng viên, phải ghi đây là phân tích oracle, không phải hệ thống có thể triển khai.

**Sản phẩm cần nộp:**

- Sơ đồ SFT, DPO và RLHF/RL với đầu vào, tín hiệu học và thành phần được cập nhật.
- Mã hoặc notebook so sánh hai ngân sách suy luận, lưu lời giải và kết quả theo mẫu.
- Báo cáo chất lượng–compute cùng ví dụ verifier hoặc quy tắc chọn thất bại.
- Một phân tích ngắn: bước nào có thể cải thiện bằng dữ liệu, objective hoặc inference.

**Kiểm tra chấp nhận:**

- Quy tắc chọn ứng viên không dùng thông tin đáp án test mà hệ thống thực tế không có.
- Báo riêng kết quả theo từng ngân sách; không mô tả một lần thử nhiều là so sánh cùng compute.
- Có phân biệt đáp án đúng với lời giải đáng tin và kiểm tra các kiểu thất bại của verifier.
- Kết luận không khẳng định reasoning tốt hơn chỉ vì model sinh nhiều token hơn.

**Mở rộng tùy chọn:** triển khai DPO trên tập cặp ưu tiên nhỏ hoặc RL trên nhiệm vụ kiểm chứng được. Chỉ tiến hành sau khi SFT, scoring và tài nguyên đã sẵn sàng; đây không phải điều kiện bắt buộc của lab chính.

## Câu hỏi tự kiểm tra

### 1. SFT, DPO và RL khác nhau ở tín hiệu học nào?

**Gợi ý kiểm tra:** SFT dùng đầu ra mẫu; DPO dùng quan hệ ưu tiên giữa các đầu ra; RL tối ưu phần thưởng trên các đầu ra được tạo trong quy trình học. Cần nói rõ dữ liệu và objective, không chỉ kể tên thuật toán.

### 2. Vì sao reward tăng vẫn có thể đi kèm chất lượng thực tế giảm?

**Gợi ý kiểm tra:** Reward chỉ là phép đo thay thế và có thể sai hoặc thiếu. Model có thể khai thác lỗ hổng định dạng, độ dài, verifier hoặc phân phối mà không đạt ý định người thiết kế.

### 3. Sinh nhiều lời giải rồi chọn lời giải tốt hơn có chứng minh model đã học thêm không?

**Gợi ý kiểm tra:** Không nếu trọng số không đổi. Đây là thay đổi cách sử dụng compute lúc suy luận; phải đánh giá lợi ích cùng chi phí và độ tin cậy của cách chọn.

## Checklist hoàn thiện

- [ ] Có ví dụ preference pair, reward và objective với giải thích từng thành phần.
- [ ] Lab chính chạy được ở quy mô nhỏ, lưu đầy đủ outputs và compute đã dùng.
- [ ] Có đáp án và rubric phân biệt chất lượng, ngân sách và khả năng tổng quát.
- [ ] Có ví dụ reward hacking, verifier sai và lựa chọn ứng viên dùng oracle.
- [ ] Nguồn, thuật toán, API và mọi kết quả minh họa đã được kiểm tra trước khi công bố.

## Tài liệu tham khảo

- [Stanford CS336](https://cs336.stanford.edu/): Assignment 5 về Alignment và Reasoning RL, cùng phần DPO mở rộng.
- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1): chương 12 về xây reasoning models.
- [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch): các phần bổ sung về DPO, evaluation và liên kết tới Reasoning from Scratch.

## Điều kiện hoàn thành

- Bạn giải thích được tín hiệu học và thành phần chính của SFT, DPO và RLHF.
- Bạn thiết kế được một so sánh reasoning có ngân sách, verifier và tập test rõ ràng.
- Bạn chỉ ra được một cách reward hoặc phép đo có thể bị tối ưu sai mục tiêu và cách kiểm tra nó.

**Trước:** [08 · SFT và PEFT](../08-sft-peft/README.md) · **Tiếp:** [10 · Inference và serving](../10-inference-serving/README.md)
