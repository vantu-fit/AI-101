# 01 · Nền tảng toán và tensor

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 16 giờ học chủ động; tăng thời gian nếu chưa quen Python hoặc đại số cơ bản.

**Kiến thức trước:** [00 · Tổng quan và chẩn đoán](../00-overview-diagnostic/README.md); biết biến, hàm, vòng lặp và đọc một chương trình Python ngắn.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox bên dưới theo dõi tiến độ biên soạn chung, không phải tiến độ học của một cá nhân.

## Mục tiêu

- Đọc được shape của tensor và dự đoán shape sau mỗi phép tính.
- Giải thích tích vô hướng, nhân ma trận và broadcasting bằng ví dụ nhỏ.
- Đọc được xác suất có điều kiện, log và phân phối xác suất rời rạc.
- Giải thích đạo hàm, gradient và chain rule trong một biểu thức nhiều bước.
- Dùng phép tính tay hoặc sai phân hữu hạn để kiểm tra kết quả tự động.

## Checklist nội dung

- [ ] Ôn Python và NumPy/PyTorch ở mức đủ để tạo, đọc và biến đổi tensor.
- [ ] Giải thích scalar, vector, matrix, tensor cùng các trục batch, token và feature.
- [ ] Minh họa tích vô hướng, nhân ma trận, transpose và điều kiện tương thích shape.
- [ ] Giải thích broadcasting, reshape, phép hoán vị trục và lỗi ngữ nghĩa dù shape hợp lệ.
- [ ] Xây trực giác xác suất có điều kiện, kỳ vọng và quy tắc nhân trên ví dụ dự đoán chuỗi.
- [ ] Giải thích log, softmax, negative log-likelihood và lý do tính toán ổn định số.
- [ ] Trình bày đạo hàm, gradient và chain rule với đồ thị tính toán nhỏ.
- [ ] So sánh gradient tính tay, sai phân hữu hạn và autograd.
- [ ] Phân biệt tham số, dữ liệu, dtype và device trong một phép tính tensor.

## Thực hành đề xuất

**Bài thực hành:** Theo dõi shape và gradient của một mô hình tuyến tính rất nhỏ.

Dùng dữ liệu tổng hợp trên CPU; chưa cần tập dữ liệu lớn hay GPU.
Đề bài cần cung cấp ma trận đầu vào, trọng số, bias và mục tiêu với kích thước cụ thể.

**Các bước đề xuất:**

1. Tính bằng tay một phần của phép biến đổi XW + b và ghi shape từng thành phần.
2. Thực hiện cùng phép tính bằng NumPy hoặc PyTorch, đối chiếu với kết quả tay.
3. Xây một loss vô hướng từ đầu ra và mục tiêu.
4. Tính đạo hàm của một trọng số bằng tay, sai phân hữu hạn và autograd.
5. Cố ý đổi nhầm một trục rồi giải thích vì sao chương trình lỗi hoặc cho kết quả sai nghĩa.

**Sản phẩm mong đợi:** Notebook hoặc script nhỏ, bảng shape và phần giải thích kết quả đối chiếu.

**Cách kiểm tra đề xuất:**

- Các phép nhân ma trận có shape dự đoán trước khi chạy.
- Kết quả tay và chương trình khớp trong sai số số học đã nêu.
- Kiểm tra gradient sử dụng dữ liệu nhỏ, dtype và bước sai phân phù hợp.
- Giải thích được vì sao một phép tính chạy được vẫn có thể dùng sai trục.

Đây là yêu cầu thiết kế bài thực hành; repo chưa công bố kết quả đã chạy.

## Câu hỏi tự kiểm tra

1. Nếu X có shape (2, 3), W có shape (3, 4), thì XW và bias phù hợp có shape nào?
2. Đạo hàm và gradient giúp quyết định thay đổi tham số theo hướng nào?
3. Vì sao không thể kiểm tra gradient số bằng một bước sai phân nhỏ tùy ý?

**Gợi ý kiểm tra:**

- Câu 1: Đầu ra là (2, 4); bias theo feature có thể là (4,) và được broadcast theo batch.
- Câu 2: Gradient mô tả biến thiên cục bộ; bước cập nhật theo hướng âm còn phụ thuộc độ lớn bước.
- Câu 3: Cần cân bằng sai số xấp xỉ với sai số làm tròn và xét độ chính xác kiểu số.

## Checklist hoàn thiện

- [ ] Có ví dụ số xuyên suốt từ tensor đến loss và gradient.
- [ ] Có script hoặc notebook chạy trên CPU, kèm môi trường và hướng dẫn thực hiện.
- [ ] Có đáp án về shape, phép tính tay và tiêu chí so sánh gradient.
- [ ] Có lỗi thường gặp về broadcasting, trục, dtype, device và độ ổn định số.
- [ ] Nguồn tham khảo đã đối chiếu và một contributor khác đã rà soát nội dung.

## Tài liệu tham khảo

- [PyTorch — Tensors](https://docs.pytorch.org/tutorials/beginner/basics/tensorqs_tutorial.html): tra thao tác tensor, shape và tính chất dữ liệu.
- [PyTorch — Automatic Differentiation](https://docs.pytorch.org/tutorials/beginner/basics/autogradqs_tutorial.html): nối đồ thị tính toán với gradient tự động.
- [Stanford CS336](https://cs336.stanford.edu/): đối chiếu nền tảng toán cần thiết cho việc học mô hình ngôn ngữ.

Các liên kết được kiểm tra ngày 2026-11-15; contributor cần ghi rõ phiên bản khi bổ sung code.

## Điều kiện hoàn thành

- Dự đoán được shape của một chuỗi phép tính nhỏ mà chưa chạy code.
- Giải thích được gradient của một biểu thức nhiều bước.
- Viết được phép kiểm tra gradient và diễn giải sai số.
- Sửa được một lỗi tensor do nhầm trục hoặc broadcasting.

Việc đạt các điều kiện này là tiến độ cá nhân; không dùng nó để đánh dấu checklist biên soạn chung.

---

[← Trước: 00 · Tổng quan](../00-overview-diagnostic/README.md) · [Tiếp: 02 · Neural network và PyTorch →](../02-neural-networks-pytorch/README.md)
