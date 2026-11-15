# 07 · Đánh giá LLM và phân tích lỗi

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 20 giờ học và thực hành.

**Học trước:** [05 · Tự xây một GPT nhỏ](../05-build-tiny-gpt/README.md) và [06 · Dữ liệu và pretraining](../06-data-pretraining/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox thể hiện mức hoàn thiện của tài liệu chung. Điều kiện người học hoàn thành nằm ở cuối bài.

## Mục tiêu

- Chuyển một mục tiêu sử dụng thành tập đánh giá, metric và điều kiện so sánh.
- Phân biệt loss, khả năng làm nhiệm vụ, chất lượng hệ thống và chi phí phục vụ.
- Kiểm tra scorer và phân tích lỗi trước khi tin vào một điểm tổng hợp.
- Viết kết luận đúng phạm vi bằng chứng, có xét bất định và những yếu tố gây nhiễu.

## Checklist nội dung

- [ ] Giải thích vai trò train, development/validation, test và cách giữ tập test cuối tách biệt.
- [ ] Soạn bài về negative log-likelihood và perplexity, bao gồm giới hạn khi tokenizer hoặc corpus khác nhau.
- [ ] Hướng dẫn chọn accuracy, exact match, F1 và metric theo nhiệm vụ; tránh gộp các thang đo tùy tiện.
- [ ] Trình bày evaluation protocol: model/tokenizer revision, prompt, chat template, few-shot và decoding.
- [ ] Viết quy trình kiểm tra answer extraction, normalization, scoring và các trường hợp không hợp lệ.
- [ ] Phân tích contamination, benchmark overfitting, phân phối mới và giới hạn của điểm leaderboard.
- [ ] Giới thiệu human evaluation, LLM-as-a-judge, rubric, thiên lệch và đối chiếu bằng mẫu kiểm thủ công.
- [ ] Soạn phần bất định: kích thước mẫu, so sánh theo từng mẫu, lặp run khi cần và confidence interval.
- [ ] Hướng dẫn error taxonomy, đánh giá theo nhóm, phân tích hồi quy và báo cáo chất lượng–chi phí.

## Thực hành đề xuất

### Lab: xây một bộ đánh giá nhỏ có thể kiểm toán

Chọn một nhiệm vụ hẹp với đáp án hoặc rubric rõ ràng, chẳng hạn trả lời câu hỏi ngắn từ đoạn văn. Chuẩn bị một tập development và một tập test tách biệt theo tài liệu nguồn.

So sánh hai cấu hình của cùng model hoặc hai model có mục đích tương đương. Khóa prompt và scorer sau khi phát triển trên development; ghi mọi khác biệt có thể ảnh hưởng kết quả.

Kiểm thủ công một mẫu đầu vào, đầu ra và điểm trước khi chạy toàn bộ. Tập nhỏ ở đây phục vụ học pipeline, không mặc nhiên đủ cho kết luận nghiên cứu.

**Sản phẩm cần nộp:**

- Định nghĩa nhiệm vụ, tập dữ liệu, rubric và evaluation protocol.
- Dự đoán theo từng mẫu, điểm thành phần và bản tổng hợp có thể tính lại.
- Một bảng lỗi theo nhóm và các ví dụ đại diện, gồm cả trường hợp scorer chấm sai.
- Báo cáo so sánh kèm giới hạn về cỡ mẫu, phân phối và nguồn bất định.

**Kiểm tra chấp nhận:**

- Scorer xử lý đúng các ví dụ tự tạo: đáp án đúng, sai, rỗng, sai định dạng và nhiều đáp án.
- Có thể tính lại điểm từ file dự đoán mà không cần sinh câu trả lời lần nữa.
- Phân biệt thất bại của model với lỗi prompt, parser hoặc dữ liệu đánh giá.
- So sánh chính sử dụng cùng tập mẫu; mọi thay đổi protocol được ghi rõ.

Module này mở rộng các kiểm tra train/validation đã xuất hiện ở module 05; evaluation tiếp tục được dùng trong tất cả module phía sau.

## Câu hỏi tự kiểm tra

### 1. Vì sao perplexity thấp hơn chưa đủ để nói một chatbot hữu ích hơn?

**Gợi ý kiểm tra:** Perplexity đo khả năng dự đoán token trên một phân phối cụ thể. Nó không trực tiếp bao quát làm đúng nhiệm vụ, làm theo hướng dẫn hoặc chất lượng tương tác.

### 2. Hai model chênh nhau một điểm accuracy: cần hỏi gì trước khi kết luận?

**Gợi ý kiểm tra:** Hỏi cỡ mẫu, cùng mẫu hay không, scorer, prompt, decoding, contamination và bất định. Kiểm tra những mẫu làm thay đổi kết luận, không chỉ nhìn điểm tổng.

### 3. Dùng một LLM mạnh làm giám khảo đã đủ thay thế đáp án chuẩn chưa?

**Gợi ý kiểm tra:** Cần rubric, kiểm thủ công và đánh giá độ ổn định. Giám khảo có thể thiên lệch theo thứ tự, độ dài hoặc phong cách; điểm do giám khảo tạo không tự trở thành ground truth.

## Checklist hoàn thiện

- [ ] Có ví dụ đầy đủ từ yêu cầu sử dụng đến dataset, metric và kết luận.
- [ ] Lab chạy được, lưu dự đoán theo mẫu và cho phép chấm lại độc lập.
- [ ] Có đáp án và acceptance criteria cho scorer, rubric và báo cáo.
- [ ] Có ví dụ contamination, parser sai và kết luận vượt quá cỡ mẫu.
- [ ] Nguồn, phiên bản công cụ và mọi kết quả minh họa đã được kiểm tra.

## Tài liệu tham khảo

- [EleutherAI — Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness): framework và tài liệu về task, prompt, model backend và metric.
- [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch): code và tài liệu bổ sung về đánh giá model, instruction responses và reasoning.
- [Stanford CS336](https://cs336.stanford.edu/): đặt evaluation trong toàn bộ quy trình dữ liệu, huấn luyện và hậu huấn luyện.

## Điều kiện hoàn thành

- Bạn chọn và giải thích được metric phù hợp với nhiệm vụ cụ thể.
- Bạn tìm được một lỗi scorer hoặc protocol bằng cách kiểm dữ liệu theo từng mẫu.
- Bạn viết được kết luận phân biệt điều đã đo với điều chưa đủ bằng chứng để khẳng định.

**Trước:** [06 · Dữ liệu và pretraining](../06-data-pretraining/README.md) · **Tiếp:** [08 · SFT và PEFT](../08-sft-peft/README.md)
