# 10 · Suy luận và phục vụ mô hình

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 18 giờ.

**Tiên quyết:** [Attention và Transformer](../04-attention-transformer/README.md), [Xây dựng Tiny GPT](../05-build-tiny-gpt/README.md), [Đánh giá mô hình](../07-evaluation/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox phản ánh độ sẵn sàng của nội dung dùng chung, không phải tiến độ học của từng người.

## Mục tiêu

Sau mô-đun này, người học có thể:

- Phân biệt prefill và decode, giải thích vì sao hai giai đoạn có đặc điểm tính toán khác nhau.
- Ước lượng bộ nhớ cho trọng số, KV cache và phần bộ nhớ phát sinh khi phục vụ yêu cầu.
- Đọc các chỉ số độ trễ, thông lượng và chất lượng để chọn cấu hình phục vụ phù hợp.
- Thiết kế phép đo có kiểm soát trước khi đề xuất tối ưu bằng batching, precision hoặc vLLM.

## Checklist nội dung

- [ ] Viết sơ đồ vòng đời yêu cầu từ token hóa đến prefill, decode và trả kết quả; chỉ rõ điểm bắt đầu, kết thúc của từng phép đo.
- [ ] Bổ sung ví dụ tính dung lượng KV cache, nêu số lớp, số KV head, độ dài chuỗi, batch và kiểu dữ liệu; phân biệt MHA với GQA/MQA.
- [ ] Soạn bảng ngân sách bộ nhớ gồm trọng số, KV cache, activation, bộ nhớ tạm và phần dự phòng; ghi rõ phạm vi của phép ước lượng.
- [ ] Giải thích FP32, BF16/FP16 và lượng tử hóa khi suy luận; thêm quy trình kiểm tra sai lệch chất lượng và khả năng hỗ trợ của phần cứng.
- [ ] Minh họa static batching và continuous batching; chỉ rõ ảnh hưởng của độ dài đầu vào, đầu ra và mức đồng thời.
- [ ] Định nghĩa TTFT, thời gian giữa các token, độ trễ toàn yêu cầu, thông lượng và phân vị; nêu cách xử lý yêu cầu lỗi hoặc hết thời gian.
- [ ] Xây dựng hướng dẫn profiling giúp phân biệt nút thắt tính toán, băng thông bộ nhớ, CPU và hàng đợi; tách warm-up khỏi phép đo chính.
- [ ] Biên soạn lab vLLM có phiên bản cố định, cấu hình tải và giới hạn tài nguyên; cung cấp phương án mô hình nhỏ khi thiếu GPU phù hợp.

## Thực hành đề xuất

### Bài toán

Phục vụ cùng một mô hình trên một tập yêu cầu cố định và khảo sát tác động của độ dài ngữ cảnh cùng mức đồng thời.
Dùng cấu hình ban đầu làm mốc; mỗi lần chỉ thay đổi một yếu tố để giải thích được chênh lệch quan sát.

### Sản phẩm bàn giao

- Bản mô tả mô hình, tokenizer, phần cứng, phần mềm và cấu hình sinh văn bản.
- Tập yêu cầu thử nghiệm với độ dài đầu vào, ngân sách đầu ra và lịch gửi yêu cầu được lưu lại.
- Bảng phép đo gồm độ trễ, thông lượng, bộ nhớ đỉnh, lỗi và kiểm tra chất lượng đầu ra.
- Ghi chú profiling giải thích một nút thắt, một thay đổi được thử và giới hạn của kết luận.

### Tiêu chí nghiệm thu

- Có cách tái chạy phép đo và phân biệt số liệu quan sát với ước lượng lý thuyết.
- So sánh dùng cùng workload và cấu hình sinh, trừ yếu tố đang khảo sát; ghi riêng warm-up và số lần lặp.
- Báo cáo đơn vị, phân vị, số yêu cầu thành công và lỗi; không chỉ trình bày một giá trị thông lượng trung bình.
- Nếu không chạy được vLLM trên phần cứng hiện có, ghi rõ giới hạn và hoàn thành phép đo nhỏ phù hợp; không suy rộng thành kết quả vLLM.

## Câu hỏi tự kiểm tra

1. Vì sao giảm thời gian prefill chưa chắc làm giảm đáng kể thời gian hoàn tất một câu trả lời dài?

   **Gợi ý:** Tách tổng thời gian thành chờ hàng đợi, prefill và nhiều bước decode.

2. Khi tăng độ dài ngữ cảnh và số yêu cầu đồng thời, những thành phần bộ nhớ nào tăng và thành phần nào gần như cố định?

   **Gợi ý:** So sánh trọng số dùng chung với KV cache của từng chuỗi; xét cả phần bộ nhớ tạm.

3. Vì sao cấu hình có thông lượng cao nhất có thể không phù hợp cho một ứng dụng hỏi đáp tương tác?

   **Gợi ý:** Xem TTFT, phân vị độ trễ, hàng đợi và chất lượng bên cạnh tổng token mỗi giây.

## Checklist hoàn thiện

- [ ] Kiểm tra ví dụ số và ký hiệu về bộ nhớ, precision, TTFT và thông lượng; ghi rõ giả định.
- [ ] Chạy lại lab từ môi trường sạch hoặc mô tả được giới hạn phần cứng, phiên bản và tài nguyên cần thiết.
- [ ] Viết lời giải hoặc đáp án gợi ý đủ để người học tự kiểm tra ba câu hỏi và diễn giải phép đo.
- [ ] Bổ sung lỗi thường gặp: hết bộ nhớ, benchmark thiếu warm-up, workload thay đổi và đếm sai token.
- [ ] Kiểm tra liên kết, ngày đối chiếu tài liệu và nhờ một người khác rà soát kết luận cùng hướng dẫn lab.

## Tài liệu tham khảo

- [Tài liệu chính thức vLLM](https://docs.vllm.ai/en/latest/) — điểm vào cho cấu hình suy luận và phục vụ; cần ghi phiên bản dùng trong lab.
- [Stanford CS336: Language Modeling from Scratch](https://cs336.stanford.edu/) — tài liệu nền về hệ thống và triển khai mô hình ngôn ngữ.

## Điều kiện hoàn thành

Người học giải thích được chi phí prefill/decode, lập được ngân sách bộ nhớ có giả định rõ ràng và hoàn thành một so sánh cấu hình phục vụ.
Báo cáo phải gắn khuyến nghị với workload đã đo, đồng thời nêu giới hạn về chất lượng, độ trễ và phần cứng.

**Trước:** [09 · Alignment và reasoning](../09-alignment-reasoning/README.md) · **Tiếp:** [11 · Retrieval và RAG](../11-retrieval-rag/README.md)
