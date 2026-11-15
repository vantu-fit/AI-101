# 06 · Dữ liệu và pretraining

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 22 giờ học và thực hành; chưa bao gồm các lần chạy máy dài.

**Học trước:** [05 · Tự xây một GPT nhỏ](../05-build-tiny-gpt/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox theo dõi việc biên soạn nội dung chung, không biểu thị người học đã hoàn thành module.

## Mục tiêu

- Hiểu dữ liệu nào trở thành tín hiệu huấn luyện và vì sao nhiều dữ liệu hơn chưa đủ để kết luận tốt hơn.
- Thiết kế pipeline xử lý dữ liệu có nguồn gốc, thống kê và khả năng kiểm tra lại.
- Phân biệt pretraining từ đầu, continued pretraining và instruction fine-tuning.
- So sánh thay đổi dữ liệu bằng một thí nghiệm có ngân sách và điều kiện rõ ràng.

## Checklist nội dung

- [ ] Biên soạn vòng đời corpus: thu thập, quyền sử dụng, trích xuất văn bản, chuẩn hóa và lưu phiên bản.
- [ ] Giải thích chất lượng, độ phủ miền, ngôn ngữ, độ đa dạng và sự phù hợp với mục tiêu sử dụng.
- [ ] Viết hướng dẫn lọc chất lượng, exact/near deduplication và kiểm tra nội dung bị loại nhầm.
- [ ] Mô tả chia tập theo nhóm tài liệu/nguồn và kiểm tra giao nhau, bao gồm contamination với bộ đánh giá.
- [ ] Giải thích tokenizer, packing, document boundary, context length và ngân sách tính bằng token.
- [ ] Soạn bài về data mixture, tỷ lệ lấy mẫu, số lần lặp dữ liệu và thay đổi phân phối theo thời gian.
- [ ] Trình bày mục tiêu pretraining, continued pretraining và khác biệt so với SFT ở dữ liệu và loss mask.
- [ ] Giới thiệu quan hệ giữa số tham số, token và compute; nêu phạm vi áp dụng của scaling laws.
- [ ] Xây quy trình ablation dữ liệu: baseline, biến thay đổi, ngân sách cố định và evaluation ngoài train.

## Thực hành đề xuất

### Lab: dữ liệu sạch hơn có giúp mô hình nhỏ không?

Chuẩn bị một corpus nhỏ với các tài liệu có nguồn gốc rõ ràng. Tạo hai phiên bản: xử lý tối thiểu và thêm một bước lọc hoặc deduplication được mô tả cụ thể.

Giữ cùng kiến trúc, tokenizer, cấu hình tối ưu và ngân sách token huấn luyện cho phép so sánh chính. Ghi lại số tài liệu, token còn lại, mức lặp dữ liệu và thời gian chạy thực tế.

Dùng cùng tập validation độc lập. Nếu tập sạch không đủ token mà phải lặp lại, phải ghi nhận điều đó vì đây cũng là một thay đổi của phân phối huấn luyện.

**Sản phẩm cần nộp:**

- Data card: nguồn, quyền sử dụng, phạm vi, các bước xử lý và giới hạn đã biết.
- Bảng thống kê trước/sau, cùng ví dụ nội dung được giữ và bị loại.
- Hai cấu hình chạy, learning curves và báo cáo đánh giá trên cùng bộ dữ liệu.
- Một kết luận có điều kiện: kết quả nào được đo, điều gì còn chưa thể suy rộng.

**Kiểm tra chấp nhận:**

- Có kiểm tra giao nhau giữa train và validation/test ở mức tài liệu hoặc nhóm phù hợp.
- Có thể tái tạo hai phiên bản dữ liệu bằng config và thông tin nguồn đã ghi.
- Không chọn quy tắc lọc bằng cách liên tục tối ưu trên tập test cuối cùng.
- Báo cáo phân biệt tác động quan sát với giả thuyết về nguyên nhân; kết quả âm vẫn hợp lệ.

Đây là lab học cách thiết kế thí nghiệm. Một mô hình nhỏ và một tập đánh giá chưa đủ để kết luận một quy tắc dữ liệu tốt cho mọi LLM.

## Câu hỏi tự kiểm tra

### 1. Tại sao xóa nhiều dữ liệu trùng hơn chưa chắc luôn làm model tốt hơn?

**Gợi ý kiểm tra:** Xem dữ liệu bị mất thuộc miền nào, độ đa dạng còn lại và ngân sách token. Deduplication có thể thay đổi phân phối; cần đo thay vì suy từ số lượng bị xóa.

### 2. Hai tập có cùng số tài liệu có phải có cùng ngân sách huấn luyện không?

**Gợi ý kiểm tra:** Không. Độ dài token, tokenizer, packing, số epoch và phần token thực sự tham gia loss đều ảnh hưởng lượng học và compute.

### 3. Khi nào bạn chọn continued pretraining thay vì SFT?

**Gợi ý kiểm tra:** Xác định mục tiêu là thích nghi với phân phối văn bản hay học hành vi trả lời theo hướng dẫn. Cần đối chiếu dữ liệu, phép đo và nguy cơ suy giảm năng lực khác; không quyết định chỉ từ tên kỹ thuật.

## Checklist hoàn thiện

- [ ] Có ví dụ xuyên suốt về một tài liệu đi qua pipeline và các quyết định xử lý.
- [ ] Lab có dữ liệu dùng hợp lệ, cấu hình nhỏ và hướng dẫn tái tạo.
- [ ] Có rubric cho data card, kiểm tra giao nhau và so sánh ngân sách.
- [ ] Có ví dụ lọc sai, trùng xuyên tập và thay đổi data mixture ngoài ý muốn.
- [ ] Tài liệu tham khảo, quyền sử dụng và các kết quả minh họa đã được kiểm tra.

## Tài liệu tham khảo

- [FineWeb — báo cáo kỹ thuật của nhóm tác giả](https://huggingfacefw-blogpost-fineweb-v1.static.hf.space/index.html): ví dụ thực nghiệm về filtering và deduplication.
- [Stanford CS336](https://cs336.stanford.edu/): các phần Data và Scaling để học cách nối corpus với compute và đánh giá.
- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1): chương 10 về chuẩn bị dữ liệu chất lượng.

## Điều kiện hoàn thành

- Bạn giải thích được vì sao mỗi bước xử lý tồn tại và dữ liệu nào có thể bị loại nhầm.
- Bạn thiết kế được một so sánh dữ liệu có baseline, ngân sách và phép đo rõ ràng.
- Bạn nhận ra khi nào kết quả còn bị nhiễu bởi tokenizer, dữ liệu lặp hoặc contamination.

**Trước:** [05 · Tự xây một GPT nhỏ](../05-build-tiny-gpt/README.md) · **Tiếp:** [07 · Đánh giá LLM](../07-evaluation/README.md)
