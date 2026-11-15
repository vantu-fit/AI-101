# 00 · Tổng quan LLM và chẩn đoán đầu vào

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 4 giờ học chủ động, gồm đọc, tự giải thích và làm bài chẩn đoán.

**Kiến thức trước:** Không yêu cầu đã học LLM; ghi lại mức quen thuộc với Python và toán của bản thân.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox bên dưới theo dõi tiến độ biên soạn chung, không phải tiến độ học của một cá nhân.

## Mục tiêu

- Đặt LLM vào bản đồ AI, machine learning, deep learning và xử lý ngôn ngữ.
- Phân biệt mô hình, trọng số, tokenizer và ứng dụng sử dụng mô hình.
- Mô tả vai trò của pretraining, post-training, đánh giá và inference.
- Nêu điều bản thân muốn làm được và xác định phần nền tảng cần học bù.
- Hiểu rằng hoàn thành lộ trình cần có sản phẩm và bằng chứng tự làm.

## Checklist nội dung

- [ ] Viết bản đồ AI → machine learning → deep learning → language model bằng ví dụ cụ thể.
- [ ] Giải thích mô hình ngôn ngữ dự đoán gì và một lượt sinh văn bản diễn ra ra sao.
- [ ] Phân biệt model, weights, tokenizer, context, prompt và ứng dụng chat.
- [ ] Minh họa vòng đời dữ liệu → huấn luyện → đánh giá → triển khai → theo dõi lỗi.
- [ ] So sánh mục đích của pretraining, supervised fine-tuning, preference training và inference.
- [ ] Tạo bài chẩn đoán Python, tensor, xác suất và gradient cùng hướng dẫn học bù.
- [ ] Hướng dẫn đọc model card, giấy phép, cấu hình và phạm vi sử dụng mô hình.
- [ ] Nêu giới hạn của câu trả lời sinh tự động và nhu cầu kiểm tra bằng chứng.
- [ ] Giải thích cách dùng repo, tiêu chí hoàn thành và cách lưu ghi chú cá nhân.

## Thực hành đề xuất

**Bài thực hành:** Vẽ bản đồ một lượt dùng LLM và tự chẩn đoán kiến thức đầu vào.

Chọn tình huống: “Tóm tắt một đoạn văn tiếng Việt đã cung cấp”.
Chưa cần tải mô hình, gọi API hoặc có GPU để hoàn thành bài này.

**Các bước đề xuất:**

1. Liệt kê dữ liệu đầu vào, thành phần xử lý và sản phẩm đầu ra.
2. Đặt tokenizer, mô hình và cách chọn token vào đúng vị trí trong sơ đồ.
3. Đánh dấu phần có trọng số học được và phần chỉ thuộc ngữ cảnh của lượt dùng.
4. Tự làm một câu Python, một phép nhân ma trận và một câu xác suất đơn giản.
5. Ghi rõ câu nào giải thích được, câu nào phải tra cứu và module cần học bù.

**Sản phẩm mong đợi:** Một sơ đồ hoặc trang ghi chú, kèm bảng chẩn đoán và mục tiêu học cá nhân.

**Cách kiểm tra đề xuất:**

- Sơ đồ có bước biến văn bản thành đầu vào của mô hình và bước tạo văn bản đầu ra.
- Không đánh đồng việc thêm thông tin vào prompt với việc cập nhật trọng số.
- Mỗi khoảng trống kiến thức có một hành động tiếp theo cụ thể.

Đây là yêu cầu thiết kế bài thực hành; repo chưa công bố kết quả đã chạy.

## Câu hỏi tự kiểm tra

1. Một ứng dụng chat và mô hình LLM bên trong ứng dụng khác nhau ở đâu?
2. Đưa một tài liệu vào prompt có đồng nghĩa mô hình đã được huấn luyện lại không?
3. Vì sao một câu trả lời đúng chưa đủ để kết luận mô hình phù hợp cho một tác vụ?

**Gợi ý kiểm tra:**

- Câu 1: Phân biệt trọng số và phép tính của mô hình với giao diện, công cụ và quản lý hội thoại.
- Câu 2: Phân biệt thông tin trong ngữ cảnh với thay đổi tham số qua một bước tối ưu.
- Câu 3: Cần nhiều trường hợp đại diện, tiêu chí chấm và hiểu loại lỗi có thể xảy ra.

## Checklist hoàn thiện

- [ ] Có ví dụ xuyên suốt nối bản đồ AI với một lượt dùng LLM cụ thể.
- [ ] Có đề chẩn đoán và hướng dẫn thực hiện hoàn toàn bằng máy cá nhân hoặc giấy.
- [ ] Có đáp án hoặc rubric giải thích mức hiểu và cách học bù.
- [ ] Có phần hiểu sai thường gặp: ứng dụng = mô hình, prompt = training, đúng một lần = đáng tin.
- [ ] Nguồn tham khảo đã đối chiếu và một contributor khác đã rà soát nội dung.

## Tài liệu tham khảo

- [Hugging Face — LLM Course](https://huggingface.co/learn/llm-course/chapter1/1): đọc phần giới thiệu để định vị LLM và các thành phần học tiếp.
- [Stanford CS336 — Language Modeling from Scratch](https://cs336.stanford.edu/): tham khảo phạm vi học và kiến thức đầu vào của hướng xây mô hình từ nền tảng.

Các liên kết được kiểm tra ngày 2026-11-15; contributor cần ghi rõ phiên bản khi bổ sung nội dung phụ thuộc công cụ.

## Điều kiện hoàn thành

- Giải thích được vòng đời cơ bản của một LLM bằng lời của mình.
- Chỉ ra được khác biệt giữa model, tokenizer và ứng dụng.
- Hoàn thành chẩn đoán và chọn được các phần cần học bù.
- Nhận ra và sửa được ít nhất một hiểu sai trong ba câu hỏi tự kiểm tra.

Việc đạt các điều kiện này là tiến độ cá nhân; không dùng nó để đánh dấu checklist biên soạn chung.

---

[← Lộ trình LLM](../README.md) · [Tiếp: 01 · Nền tảng toán →](../01-math-foundations/README.md)
