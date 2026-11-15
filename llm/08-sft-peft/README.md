# 08 · SFT và fine-tuning tiết kiệm tài nguyên

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 24 giờ học và thực hành; thời gian huấn luyện phụ thuộc model và phần cứng.

**Học trước:** [06 · Dữ liệu và pretraining](../06-data-pretraining/README.md) và [07 · Đánh giá LLM](../07-evaluation/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox theo dõi việc đóng góp và kiểm tra nội dung. Việc người học đạt năng lực được đánh giá riêng ở cuối module.

## Mục tiêu

- Hiểu supervised fine-tuning (SFT) thay đổi model thông qua các ví dụ đầu vào–đầu ra.
- Chuẩn bị dữ liệu hội thoại, template và loss mask đúng với mục tiêu học.
- Giải thích full fine-tuning, parameter-efficient fine-tuning (PEFT), LoRA và QLoRA.
- Đo cả phần cải thiện ở nhiệm vụ đích lẫn suy giảm ở các nhiệm vụ cần giữ.

## Checklist nội dung

- [ ] Giải thích khi nào nên thử prompt, bổ sung ngữ cảnh, SFT hoặc continued pretraining.
- [ ] Biên soạn cách chọn base/instruct model dựa trên năng lực, giấy phép và tài nguyên thực tế.
- [ ] Hướng dẫn chuẩn hóa dữ liệu instruction/chat, kiểm tra đáp án và tách tập theo nguồn hoặc nhóm.
- [ ] Giải thích chat template, role tokens, EOS, truncation, packing và loss mask theo mục tiêu huấn luyện.
- [ ] Trình bày full fine-tuning và PEFT; giải thích LoRA qua cập nhật hạng thấp và các tham số rank/scale/target modules.
- [ ] Giải thích QLoRA ở mức thành phần: base weight lượng tử hóa, adapter học được và các nguồn sử dụng bộ nhớ.
- [ ] Hướng dẫn chọn learning rate, batch hiệu dụng, số bước, gradient accumulation và checkpoint theo development.
- [ ] Soạn quy trình phát hiện overfitting, lỗi định dạng, học đáp án nhiễu và suy giảm năng lực ngoài miền.
- [ ] Hướng dẫn nạp/ghép adapter phù hợp, lưu revision và so sánh trước–sau bằng evaluation protocol cố định.

## Thực hành đề xuất

### Lab: fine-tune cho một nhiệm vụ có đầu ra kiểm tra được

Chọn một nhiệm vụ hẹp, chẳng hạn trích xuất thông tin thành JSON với schema rõ ràng. Dùng dữ liệu hợp lệ có nhãn được kiểm tra và các nhóm train/development/test tách biệt.

Đánh giá model ban đầu bằng một prompt có hướng dẫn hợp lý. Sau đó fine-tune bằng LoRA trên cùng mục tiêu; QLoRA là lựa chọn bổ sung khi cấu hình và phần cứng đã được xác nhận hỗ trợ.

Giữ thêm một bộ kiểm tra nhỏ cho những năng lực cần bảo toàn. Không chọn checkpoint bằng tập test cuối cùng và không suy chất lượng từ training loss.

**Sản phẩm cần nộp:**

- Data card, mẫu hội thoại sau template và hình hoặc bảng thể hiện vị trí tính loss.
- Config huấn luyện, revision của base/tokenizer, adapter và hướng dẫn nạp lại.
- Báo cáo trước–sau về chất lượng nhiệm vụ, tỷ lệ hợp lệ của định dạng và năng lực cần giữ.
- Ghi nhận số tham số được học, tài nguyên đo được và các hạn chế của thí nghiệm.

**Kiểm tra chấp nhận:**

- Kiểm thủ công các token/labels của ít nhất một ví dụ ngắn, một ví dụ bị cắt và một ví dụ nhiều lượt.
- Xác nhận đúng nhóm tham số đang được cập nhật; phân biệt tham số tổng với tham số trainable.
- Adapter nạp lại với đúng base revision cho kết quả phù hợp với lần đánh giá đã lưu.
- Báo cáo riêng lỗi nội dung và lỗi schema; không coi JSON hợp lệ là đáp án đúng.

Kết quả không cải thiện vẫn được chấp nhận nếu pipeline đúng và phân tích được nguyên nhân. Mục tiêu học là ra quyết định bằng dữ liệu.

## Câu hỏi tự kiểm tra

### 1. Vì sao loss mask và chat template có thể làm hỏng một lần SFT?

**Gợi ý kiểm tra:** Chúng quyết định chuỗi model nhìn thấy và vị trí tạo gradient. Sai role, EOS, truncation hoặc vùng tính loss có thể khiến model học mục tiêu khác điều ta định dạy.

### 2. LoRA giảm số tham số học được, vậy có thể suy ngay mức VRAM từ con số đó không?

**Gợi ý kiểm tra:** Không. Bộ nhớ còn chứa base weights, activations, gradients, optimizer state và phần tạm của phép tính; context length và batch cũng ảnh hưởng.

### 3. Điểm nhiệm vụ đích tăng nhưng một năng lực khác giảm: bạn xử lý thế nào?

**Gợi ý kiểm tra:** Xác nhận protocol và lỗi trước, rồi xem data mixture, learning rate, số bước và checkpoint. Quyết định dựa trên yêu cầu sử dụng và đánh đổi được đo, không chỉ một điểm tổng.

## Checklist hoàn thiện

- [ ] Có ví dụ số hoặc sơ đồ cho cập nhật LoRA và ví dụ token/label cho SFT.
- [ ] Lab chạy được trên cấu hình đã ghi, có đường thực hành nhỏ và hướng dẫn nạp adapter.
- [ ] Có đáp án và rubric cho chất lượng dữ liệu, loss mask và đánh giá trước–sau.
- [ ] Có các lỗi template, truncation, base revision và overfitting để người học chẩn đoán.
- [ ] Nguồn, API, giấy phép model/dữ liệu và kết quả minh họa đã được kiểm tra.

## Tài liệu tham khảo

- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1): chương 11 về fine-tuning LLM và liên kết tới công cụ thực hành.
- [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch): chương 7 về instruction fine-tuning và các phần bổ sung liên quan.
- [Stanford CS336](https://cs336.stanford.edu/): phần Alignment và Reasoning RL nối SFT với các mục tiêu hậu huấn luyện.

## Điều kiện hoàn thành

- Bạn giải thích được dữ liệu nào tạo gradient và tham số nào đang được học.
- Bạn tự chuẩn bị, chạy và nạp lại một adapter với cấu hình có thể kiểm tra.
- Bạn đánh giá được cải thiện, hồi quy và giới hạn của một lần fine-tune.

**Trước:** [07 · Đánh giá LLM](../07-evaluation/README.md) · **Tiếp:** [09 · Alignment và reasoning](../09-alignment-reasoning/README.md)
