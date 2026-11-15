# 11 · Truy hồi thông tin và RAG

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 18 giờ.

**Tiên quyết:** [Language modeling và tokenization](../03-language-modeling-tokenization/README.md), [Đánh giá mô hình](../07-evaluation/README.md). Khuyến nghị học thêm [Inference và serving](../10-inference-serving/README.md) nếu tự phục vụ mô hình.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox phản ánh độ sẵn sàng của nội dung dùng chung, không phải tiến độ học của từng người.

## Mục tiêu

Sau mô-đun này, người học có thể:

- Xây dựng luồng từ tài liệu gốc đến đoạn được truy hồi, ngữ cảnh đầu vào và câu trả lời có trích dẫn.
- Phân biệt vai trò của chunking, embedding, truy hồi từ khóa, truy hồi kết hợp và reranker.
- Đánh giá riêng khả năng tìm đúng bằng chứng và khả năng trả lời dựa trên bằng chứng đó.
- Giải thích khi nào nên thử RAG, fine-tuning hoặc kết hợp cả hai dựa trên loại lỗi cần sửa.

## Checklist nội dung

- [ ] Viết sơ đồ pipeline RAG, ghi đầu vào, đầu ra và metadata cần giữ ở từng bước để truy ngược về tài liệu gốc.
- [ ] Bổ sung ví dụ chunking theo độ dài và cấu trúc tài liệu; nêu ảnh hưởng của overlap, tiêu đề, bảng và ranh giới đoạn.
- [ ] Giải thích embedding truy vấn/tài liệu, độ tương đồng, chỉ mục và top-k; nêu yêu cầu dùng đúng cấu hình của mô hình embedding.
- [ ] Soạn ví dụ truy hồi từ khóa và dense retrieval, sau đó thiết kế một cách kết hợp kết quả có thể kiểm tra.
- [ ] Mô tả reranker, vị trí trong pipeline và đánh đổi về độ trễ; giữ riêng số ứng viên trước và sau xếp hạng lại.
- [ ] Biên soạn hướng dẫn đóng gói ngữ cảnh, xử lý bằng chứng mâu thuẫn, trích dẫn và từ chối khi tài liệu không đủ trả lời.
- [ ] Thiết kế đánh giá retrieval và câu trả lời với nhãn bằng chứng, truy vấn không có đáp án, phân tích lỗi và kiểm soát rò rỉ dữ liệu.
- [ ] Viết bảng quyết định RAG so với fine-tuning theo nhu cầu cập nhật kiến thức, hành vi, nguồn dẫn, chi phí và loại lỗi quan sát.

## Thực hành đề xuất

### Bài toán

Tạo hệ thống hỏi đáp tiếng Việt trên một bộ tài liệu AI có nguồn gốc rõ ràng.
Bắt đầu bằng một cấu hình truy hồi đơn giản, rồi thử một thay đổi có lý do từ lỗi đã quan sát trên tập phát triển.

### Sản phẩm bàn giao

- Bộ tài liệu được lập danh mục, kèm phiên bản, nguồn, mã tài liệu và mã đoạn ổn định.
- Tập câu hỏi chia phát triển/kiểm tra, có bằng chứng tham chiếu và trường hợp không thể trả lời từ tài liệu.
- Pipeline truy hồi và sinh câu trả lời, lưu được đoạn được chọn, thứ hạng và nguồn trích dẫn.
- Bảng so sánh cấu hình ban đầu với một thay đổi về chunking, retrieval hoặc reranking; kèm phân tích lỗi.

### Tiêu chí nghiệm thu

- Có đánh giá retrieval như recall@k khi nhãn bằng chứng phù hợp, cùng đánh giá riêng về tính đúng và mức được bằng chứng hỗ trợ của câu trả lời.
- Trích dẫn trỏ đến đúng đoạn hoặc vị trí có thể kiểm tra; việc có trích dẫn không tự động được tính là trả lời đúng.
- Giữ cố định mô hình sinh và các yếu tố không khảo sát; dùng tập phát triển để lựa chọn cấu hình trước khi chạy tập kiểm tra.
- Báo cáo ví dụ thiếu bằng chứng, bằng chứng sai và sinh sai dù đã tìm đúng; ghi thêm độ trễ cùng chi phí tính theo quy ước rõ ràng.

## Câu hỏi tự kiểm tra

1. Nếu hệ thống trả lời sai, làm thế nào để xác định lỗi đến từ truy hồi hay bước sinh câu trả lời?

   **Gợi ý:** Đối chiếu bằng chứng tham chiếu với các đoạn được tìm; thử đánh giá bước sinh khi cung cấp đúng bằng chứng.

2. Vì sao tăng top-k hoặc tăng overlap không bảo đảm chất lượng câu trả lời sẽ tốt hơn?

   **Gợi ý:** Xét thông tin trùng lặp, nhiễu, giới hạn ngữ cảnh và chi phí xử lý.

3. Khi một mô hình không biết quy định vừa được cập nhật trong tài liệu, cần bằng chứng nào để chọn RAG hay fine-tuning?

   **Gợi ý:** Phân biệt thiếu kiến thức cập nhật với thiếu kỹ năng hoặc hành vi; xét nhu cầu dẫn nguồn và vận hành.

## Checklist hoàn thiện

- [ ] Thêm ví dụ tiếng Việt cho chunking, truy hồi, trích dẫn đúng/sai và câu hỏi không có bằng chứng.
- [ ] Chạy lại lab với phiên bản dữ liệu, mô hình, chỉ mục và cấu hình được ghi đầy đủ.
- [ ] Viết đáp án gợi ý cho câu hỏi tự kiểm tra và tiêu chí chấm retrieval, câu trả lời, trích dẫn.
- [ ] Bổ sung lỗi thường gặp: mất metadata, nhầm độ tương đồng, trùng đoạn, rò rỉ đáp án và nhãn bằng chứng không đầy đủ.
- [ ] Đối chiếu nguồn gốc tài liệu, kiểm tra liên kết tham khảo và nhờ người khác rà soát tập đánh giá.

## Tài liệu tham khảo

- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401) — bài báo gốc để đối chiếu khái niệm và thiết kế RAG.
- [EleutherAI Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) — tham khảo cách tổ chức đánh giá có thể tái lập; các chỉ số RAG của lab cần được thiết kế riêng.

## Điều kiện hoàn thành

Người học xây dựng được một pipeline có truy vết nguồn và đánh giá riêng retrieval với câu trả lời.
Lựa chọn cấu hình cuối phải dựa trên lỗi của tập phát triển, có kết quả kiểm tra và chỉ ra trường hợp hệ thống nên từ chối trả lời.

**Trước:** [10 · Inference và serving](../10-inference-serving/README.md) · **Tiếp:** [12 · Tool use và agents](../12-tool-use-agents/README.md)
