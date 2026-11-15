# 14 · Capstone: hỏi đáp tiếng Việt trên tài liệu AI

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 28 giờ.

**Tiên quyết:** [Đánh giá mô hình](../07-evaluation/README.md), [Inference và serving](../10-inference-serving/README.md), [Retrieval và RAG](../11-retrieval-rag/README.md). Học thêm [SFT và PEFT](../08-sft-peft/README.md) nếu chọn fine-tuning; [Tool use và agent](../12-tool-use-agents/README.md) nếu dùng vòng gọi công cụ.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox phản ánh độ sẵn sàng của nội dung dùng chung, không phải tiến độ học của từng người.

## Mục tiêu

Sau mô-đun này, người học có thể:

- Tích hợp các lab trước thành hệ thống hỏi đáp tiếng Việt trên bộ tài liệu AI có nguồn kiểm chứng.
- Xây dựng baseline, tập phát triển và tập kiểm tra với giao thức đánh giá được xác định trước.
- Chọn một can thiệp từ phân tích lỗi và so sánh chất lượng, độ trễ cùng chi phí trên cùng điều kiện.
- Bàn giao demo, báo cáo và cấu hình đủ rõ để một người khác tái chạy phần đánh giá chính.

## Checklist nội dung

- [ ] Viết đề bài, người dùng mục tiêu, phạm vi tài liệu và điều kiện từ chối trả lời khi không có bằng chứng.
- [ ] Lập bản đồ tái sử dụng artifact từ lab đánh giá, serving, RAG và công cụ; xác định phần cần tích hợp, tránh yêu cầu xây lại mọi thành phần.
- [ ] Soạn quy trình lập danh mục nguồn, phiên bản dữ liệu, quyền sử dụng và xử lý thông tin nhạy cảm trước khi đưa vào corpus hoặc demo.
- [ ] Thiết kế cách chia phát triển/kiểm tra, nhóm câu hỏi trùng hoặc diễn đạt lại và khóa tập kiểm tra trước khi chọn cấu hình.
- [ ] Đặc tả baseline RAG tối thiểu, cấu hình cố định, rubric chất lượng và quy ước đo chi phí, độ trễ, lỗi.
- [ ] Tạo mẫu phân tích lỗi theo retrieval, ngữ cảnh, sinh câu trả lời, trích dẫn và công cụ; yêu cầu mỗi đề xuất sửa có bằng chứng trên tập phát triển.
- [ ] Soạn protocol chọn một can thiệp như chunking, hybrid retrieval, reranker hoặc điều khiển công cụ; giữ fine-tuning là lựa chọn có điều kiện từ lỗi quan sát.
- [ ] Xây dựng rubric so sánh baseline với bản cải tiến, gồm hiệu quả, đánh đổi, thất bại và giới hạn của tập đánh giá.
- [ ] Viết mẫu bàn giao demo, báo cáo, cấu hình, phiên bản dữ liệu và hướng dẫn tái lập; nêu rõ bước nào còn cần thao tác thủ công.

## Thực hành đề xuất

### Bài toán

Xây dựng trợ lý hỏi đáp tiếng Việt về một bộ tài liệu AI được giới hạn rõ, có trích dẫn đến bằng chứng gốc.
Tái sử dụng pipeline và artifact đã làm; dành công sức chính cho đánh giá, phân tích lỗi và một cải tiến có căn cứ.

### Sản phẩm bàn giao

- Corpus có danh mục nguồn và phiên bản; tập phát triển/kiểm tra có câu hỏi, bằng chứng, rubric cùng ca không có đáp án.
- Baseline chạy được, bản cải tiến và cấu hình ghi rõ phần giữ nguyên, phần thay đổi.
- Demo thể hiện câu trả lời, trích dẫn, trạng thái thiếu bằng chứng và lỗi có thể hiểu được.
- Báo cáo gồm kết quả chất lượng/chi phí, phân tích lỗi, ví dụ thành công/thất bại và hướng dẫn tái lập.

### Tiêu chí nghiệm thu

- Chốt tập kiểm tra và tiêu chí chấm trước khi lựa chọn can thiệp; mọi điều chỉnh dựa trên tập phát triển được ghi lại.
- So sánh baseline với bản cải tiến trên cùng tập kiểm tra, cùng giao thức; báo số lượng mẫu, độ biến động nếu đo được và giới hạn của phép so sánh.
- Kiểm tra tính đúng, mức hỗ trợ của bằng chứng và độ chính xác trích dẫn; ghi độ trễ, chi phí hoặc đại lượng thay thế với đơn vị và giả định rõ ràng.
- Một người khác có thể tái chạy phép đánh giá chính từ hướng dẫn; kết quả không cải thiện vẫn đạt nếu thiết kế hợp lý, số liệu trung thực và phân tích đầy đủ.

## Câu hỏi tự kiểm tra

1. Phân tích lỗi nào cho thấy cần sửa truy hồi, và phân tích nào cho thấy cần sửa cách mô hình dùng bằng chứng?

   **Gợi ý:** Đối chiếu đoạn được tìm với bằng chứng tham chiếu; đánh giá câu trả lời khi cung cấp đúng bằng chứng.

2. Khi bản cải tiến trả lời tốt hơn nhưng chậm và tốn tài nguyên hơn, cần trình bày quyết định triển khai ra sao?

   **Gợi ý:** Gắn đánh đổi với nhu cầu người dùng, ngân sách và phân bố loại câu hỏi; tránh chỉ chọn một chỉ số thuận lợi.

3. Những thông tin nào cần có để người khác kiểm tra kết quả mà không phải đoán lại thiết lập của dự án?

   **Gợi ý:** Xét phiên bản corpus, chia tập, mô hình, cấu hình, rubric, cách chạy và các dịch vụ bên ngoài.

## Checklist hoàn thiện

- [ ] Bổ sung một mẫu bàn giao có cấu trúc, ví dụ trích dẫn và ca thất bại; không điền kết quả thực nghiệm chưa thực hiện.
- [ ] Thử quy trình tái lập với người không viết pipeline, kiểm tra phiên bản, cấu hình và artifact cần thiết.
- [ ] Hoàn thiện đáp án gợi ý, rubric chấm capstone và cách đánh giá báo cáo có kết quả âm hoặc không rõ ràng.
- [ ] Bổ sung lỗi thường gặp: chọn cấu hình trên tập kiểm tra, thay nhiều yếu tố, dẫn nguồn sai và bỏ sót chi phí.
- [ ] Kiểm tra nguồn, quyền sử dụng, liên kết và nhờ người khác rà soát báo cáo cùng demo theo rubric.

## Tài liệu tham khảo

- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401) — tham khảo nền tảng cho thiết kế hỏi đáp có truy hồi.
- [Hugging Face Agents Course: What are Agents?](https://huggingface.co/learn/agents-course/unit1/what-are-agents) — đối chiếu vai trò công cụ khi dự án cần vòng điều khiển.
- [EleutherAI Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) — tham khảo tổ chức đánh giá; rubric hỏi đáp và trích dẫn cần phù hợp với corpus của dự án.

## Điều kiện hoàn thành

Người học bàn giao demo, baseline, một can thiệp có căn cứ và báo cáo so sánh có thể kiểm tra.
Dự án hoàn thành khi giải thích được lỗi, đánh đổi và giới hạn, đồng thời người khác tái chạy được đánh giá chính; không bắt buộc triển khai công khai hoặc đạt điểm số được đặt tùy ý.

**Trước:** [13 · Hướng nghiên cứu](../13-research-frontiers/README.md) · **Kết thúc lộ trình:** [Tổng quan LLM](../README.md) · [Trang chủ](../../README.md)
