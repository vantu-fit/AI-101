# 13 · Đọc nghiên cứu và các hướng mở rộng

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 12 giờ cho phần đọc, phân tích và tái lập nhỏ; các nhánh đào sâu là tùy chọn ngoài thời lượng này.

**Tiên quyết:** [Tự xây GPT nhỏ](../05-build-tiny-gpt/README.md), [Dữ liệu và pretraining](../06-data-pretraining/README.md), [Đánh giá mô hình](../07-evaluation/README.md). Học thêm [SFT và PEFT](../08-sft-peft/README.md), [Alignment và reasoning](../09-alignment-reasoning/README.md) nếu chọn paper thuộc các chủ đề này.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox phản ánh độ sẵn sàng của nội dung dùng chung, không phải tiến độ học của từng người.

## Mục tiêu

Sau mô-đun này, người học có thể:

- Tách câu hỏi nghiên cứu, tuyên bố, bằng chứng và phạm vi kết luận của một bài báo LLM.
- Kiểm tra baseline, ngân sách tính toán, dữ liệu và các biến gây nhiễu trong phép so sánh.
- Đề xuất ablation và thực hiện một tái lập nhỏ với giới hạn được mô tả rõ ràng.
- Chọn một hướng đào sâu phù hợp từ MoE, ngữ cảnh dài, đa phương thức, distillation hoặc huấn luyện phân tán.

## Checklist nội dung

- [ ] Soạn mẫu đọc bài báo gồm vấn đề, giả thuyết, tuyên bố chính, thiết lập thực nghiệm, bằng chứng và điều kiện áp dụng.
- [ ] Viết hướng dẫn truy nguồn số liệu về bảng, hình hoặc artifact gốc; phân biệt kết quả tác giả báo cáo với kết quả tự tái lập.
- [ ] Bổ sung bảng kiểm baseline về dữ liệu, tham số, token huấn luyện, compute, tuning và ngân sách suy luận; ghi rõ trường hợp không thể cân bằng mọi yếu tố.
- [ ] Minh họa biến gây nhiễu do dữ liệu, contamination, lựa chọn checkpoint và khác biệt giao thức đánh giá.
- [ ] Thiết kế ví dụ ablation có câu hỏi cụ thể, đối chứng và yếu tố giữ cố định; nêu khi nào loại một thành phần làm thay đổi nhiều biến cùng lúc.
- [ ] Soạn protocol tái lập nhỏ có phiên bản, seed, ngân sách, tiêu chí so sánh và cách báo cáo kết quả không khớp.
- [ ] Viết bản đồ tổng quan MoE và ngữ cảnh dài dưới dạng nhánh tùy chọn, chỉ rõ câu hỏi, kiến thức bổ sung và chi phí thí nghiệm.
- [ ] Viết bản đồ tổng quan đa phương thức, distillation và huấn luyện phân tán dưới dạng nhánh tùy chọn; thêm nguồn sơ cấp theo từng hướng trước khi mở rộng bài học.
- [ ] Tạo mẫu ghi chú nghiên cứu tách điều đã biết, suy luận, điểm chưa chắc và thí nghiệm tiếp theo có thể bác bỏ giả thuyết.

## Thực hành đề xuất

### Bài toán

Chọn một bài báo có artifact công khai và một tuyên bố có thể khảo sát ở quy mô nhỏ trong ngân sách hiện có.
Lập bảng đối chiếu thiết lập gốc với thiết lập thực hiện, sau đó tái lập một phép so sánh hoặc một ablation hẹp.

### Sản phẩm bàn giao

- Phiếu đọc bài báo với liên kết đến phiên bản bài, bảng/hình liên quan, mã nguồn và cấu hình nếu có.
- Bảng baseline cùng ngân sách dữ liệu, huấn luyện, tuning và suy luận; ghi các mục không được tác giả công bố.
- Protocol, artifact của lần chạy và báo cáo chênh lệch giữa thiết lập gốc với thiết lập thu nhỏ.
- Một đề xuất nghiên cứu tiếp theo gồm giả thuyết, đối chứng, phép đo và kết quả nào sẽ bác bỏ giả thuyết.

### Tiêu chí nghiệm thu

- Mọi tuyên bố được gắn với nguồn hoặc được đánh dấu là suy luận, câu hỏi mở hay quan sát từ lần chạy của người học.
- Báo cáo nêu rõ biến kiểm soát, biến gây nhiễu còn lại và giới hạn của một lần chạy hoặc một mô hình nhỏ.
- Tái lập nhỏ không được dùng để khẳng định đã xác nhận toàn bộ bài báo; kết quả không khớp phải được giữ lại và phân tích.
- Có tối thiểu một phép so sánh hoặc ablation thực hiện được; các nhánh đào sâu không trở thành điều kiện bắt buộc của mô-đun.

## Câu hỏi tự kiểm tra

1. Nếu phương pháp mới tốt hơn baseline nhưng dùng nhiều dữ liệu và compute hơn, có thể kết luận được điều gì?

   **Gợi ý:** Tách hiệu quả của hệ thống hoàn chỉnh khỏi đóng góp riêng của phương pháp; xác định phép đối chứng còn thiếu.

2. Khi bỏ một thành phần làm hiệu năng giảm, vì sao chưa đủ để giải thích cơ chế của thành phần đó?

   **Gợi ý:** Xét thay đổi ngân sách, tối ưu hóa, tương tác giữa thành phần và khả năng đối chứng thay thế.

3. Một kết quả tái lập nhỏ không khớp bài báo nên được diễn giải và báo cáo như thế nào?

   **Gợi ý:** Kiểm tra sai khác thiết lập, biến ngẫu nhiên và phạm vi quy mô trước khi quy nguyên nhân.

## Checklist hoàn thiện

- [ ] Thêm một phiếu đọc mẫu có nguồn và một bảng so sánh công bằng; đánh dấu rõ phần minh họa hoặc dữ liệu thực.
- [ ] Chạy lại protocol tái lập nhỏ và kiểm tra khả năng truy vết từ báo cáo về cấu hình, artifact.
- [ ] Viết đáp án gợi ý cho câu hỏi tự kiểm tra và rubric đánh giá chất lượng phân tích bài báo.
- [ ] Bổ sung lỗi thường gặp: baseline yếu, lệch compute, chọn kết quả thuận lợi và suy rộng từ thí nghiệm nhỏ.
- [ ] Xác minh nguồn sơ cấp, phiên bản bài và artifact; nhờ người khác rà soát việc kết luận có vượt bằng chứng hay không.

## Tài liệu tham khảo

- [Stanford CS336: Language Modeling from Scratch](https://cs336.stanford.edu/) — nền tảng để xác định kiến thức và thiết lập cần kiểm tra khi đọc nghiên cứu LLM.
- [Google Research: Deep Learning Tuning Playbook](https://github.com/google-research/tuning_playbook) — tham khảo thiết kế thí nghiệm, tuning và cách diễn giải phép so sánh.
- [EleutherAI Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) — tham khảo cấu hình và artifact phục vụ đánh giá có thể tái lập.

## Điều kiện hoàn thành

Người học hoàn thành một phân tích có truy nguồn và một tái lập nhỏ hoặc ablation hẹp, chỉ ra được yếu tố chưa kiểm soát.
Người học chọn được câu hỏi tiếp theo có thể kiểm chứng; không cần hoàn thành mọi nhánh MoE, ngữ cảnh dài, đa phương thức, distillation và huấn luyện phân tán.

**Trước:** [12 · Tool use và agents](../12-tool-use-agents/README.md) · **Tiếp:** [14 · Capstone](../14-capstone/README.md)
