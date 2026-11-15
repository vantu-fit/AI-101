# 12 · Sử dụng công cụ và tác tử

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 14 giờ.

**Tiên quyết:** [Đánh giá mô hình](../07-evaluation/README.md), [Retrieval và RAG](../11-retrieval-rag/README.md). Khuyến nghị học thêm [Inference và serving](../10-inference-serving/README.md) nếu tự phục vụ mô hình.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox phản ánh độ sẵn sàng của nội dung dùng chung, không phải tiến độ học của từng người.

## Mục tiêu

Sau mô-đun này, người học có thể:

- Phân biệt đầu ra có cấu trúc, đề xuất gọi hàm và việc thực thi công cụ trong ứng dụng.
- Thiết kế vòng điều khiển có trạng thái, điều kiện dừng và ngân sách thao tác rõ ràng.
- Kiểm soát quyền công cụ, xử lý lỗi và nhận diện chỉ dẫn không đáng tin cậy trong dữ liệu bên ngoài.
- Đánh giá tác tử theo kết quả nhiệm vụ và chi phí, dựa trên trace có thể kiểm tra.

## Checklist nội dung

- [ ] Viết ví dụ schema cho đầu ra có cấu trúc và tham số hàm; tách hợp lệ về cú pháp khỏi đúng về ý nghĩa.
- [ ] Minh họa luồng model đề xuất lời gọi, ứng dụng kiểm tra, thực thi công cụ và trả kết quả; chỉ rõ nơi quyền được thực thi.
- [ ] Soạn sơ đồ trạng thái tối thiểu cho chọn hành động, gọi công cụ, quan sát và kết thúc; nêu giới hạn số bước, token và thời gian.
- [ ] Thiết kế xử lý tham số sai, công cụ không tồn tại, timeout, lỗi tạm thời và kết quả thiếu; nêu giới hạn retry và nguy cơ lặp tác dụng phụ.
- [ ] Bổ sung ví dụ prompt injection từ tài liệu hoặc đầu ra công cụ; xác định ranh giới giữa dữ liệu và chỉ dẫn được tin cậy.
- [ ] Viết chính sách quyền tối thiểu, danh sách công cụ cho phép và điều kiện xác nhận với thao tác có tác dụng bên ngoài.
- [ ] Định nghĩa trace gồm trạng thái, lời gọi, kết quả, lỗi và chi phí; bổ sung cách che thông tin nhạy cảm trước khi lưu hoặc chia sẻ.
- [ ] Thiết kế bộ đánh giá kết quả nhiệm vụ, tuân thủ giới hạn, xử lý thất bại và hiệu quả; so sánh với một workflow cố định.

## Thực hành đề xuất

### Bài toán

Mở rộng hệ thống hỏi đáp tài liệu bằng hai công cụ chỉ đọc: tìm đoạn tài liệu và lấy nội dung theo mã đoạn.
Tác tử phải quyết định khi nào cần thêm bằng chứng và kết thúc trong ngân sách đã định; dùng công cụ mô phỏng cho các ca lỗi.

### Sản phẩm bàn giao

- Đặc tả schema, quyền và hợp đồng đầu vào/đầu ra cho từng công cụ.
- Vòng điều khiển hoặc sơ đồ trạng thái có điều kiện dừng, giới hạn retry và cách báo lỗi cho người dùng.
- Bộ tình huống gồm yêu cầu bình thường, dữ liệu thiếu, lỗi công cụ và chỉ dẫn giả được chèn trong tài liệu.
- Trace đã loại thông tin nhạy cảm, bảng kết quả nhiệm vụ và so sánh với workflow truy hồi cố định.

### Tiêu chí nghiệm thu

- Ứng dụng kiểm tra schema và quyền trước khi gọi công cụ; tên hoặc tham số do mô hình sinh không tự mở rộng quyền.
- Mỗi lượt chạy kết thúc bằng kết quả hoặc lỗi rõ ràng trong giới hạn bước, thời gian và retry đã đặt.
- Có kiểm tra hành vi trước chỉ dẫn giả trong dữ liệu, với tiêu chí cụ thể; không xem vài ca vượt qua là bằng chứng bảo đảm an toàn tuyệt đối.
- Đánh giá dựa trên hoàn thành nhiệm vụ, bằng chứng, số lần gọi, độ trễ và lỗi; không chỉ dựa trên trace có vẻ hợp lý.

## Câu hỏi tự kiểm tra

1. Một lời gọi hàm đúng schema có thể vẫn gây sai ở những điểm nào, và thành phần nào phải ngăn việc đó?

   **Gợi ý:** Xét ý nghĩa tham số, quyền, trạng thái ứng dụng và tác dụng phụ; schema chỉ kiểm tra một phần hợp đồng.

2. Nếu công cụ trả timeout, vì sao không thể luôn gọi lại ngay với cùng tham số?

   **Gợi ý:** Phân biệt thao tác chỉ đọc với thao tác có tác dụng phụ; xem tính lặp an toàn và khả năng lần đầu đã thành công.

3. Làm thế nào để chứng minh tác tử có ích hơn một workflow cố định cho cùng nhóm nhiệm vụ?

   **Gợi ý:** So sánh tỷ lệ hoàn thành, chất lượng, chi phí và các ca thất bại trên cùng tập đánh giá.

## Checklist hoàn thiện

- [ ] Thêm ví dụ lời gọi hợp lệ, sai ngữ nghĩa, bị từ chối quyền và prompt injection trong dữ liệu.
- [ ] Chạy lại lab với công cụ mô phỏng, cấu hình cố định và ca kiểm tra mọi nhánh kết thúc quan trọng.
- [ ] Viết đáp án gợi ý cho câu hỏi tự kiểm tra và quy tắc chấm kết quả nhiệm vụ.
- [ ] Bổ sung lỗi thường gặp: vòng lặp không dừng, retry gây lặp thao tác, bỏ qua quyền và lưu bí mật trong trace.
- [ ] Kiểm tra tài liệu tham khảo và nhờ người khác rà soát schema, quyền cùng bộ tình huống đối kháng.

## Tài liệu tham khảo

- [Hugging Face Agents Course: What are Agents?](https://huggingface.co/learn/agents-course/unit1/what-are-agents) — điểm vào cho khái niệm tác tử và tương tác với công cụ.
- [Tài liệu chính thức vLLM](https://docs.vllm.ai/en/latest/) — tra cứu khả năng phục vụ mô hình; đối chiếu hỗ trợ đầu ra có cấu trúc và gọi công cụ theo phiên bản.

## Điều kiện hoàn thành

Người học xây dựng được tác tử giới hạn quyền và tài nguyên, giải thích được từng lời gọi từ trace và xử lý được ca công cụ lỗi.
Báo cáo phải so sánh với workflow cố định, nêu lợi ích quan sát được và mô tả giới hạn còn lại trước dữ liệu không đáng tin cậy.

**Trước:** [11 · Retrieval và RAG](../11-retrieval-rag/README.md) · **Tiếp:** [13 · Hướng nghiên cứu](../13-research-frontiers/README.md)
