# 02 · Neural network, PyTorch và vòng lặp học

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 20 giờ học chủ động, gồm viết và chẩn đoán training loop.

**Kiến thức trước:** [01 · Nền tảng toán và tensor](../01-math-foundations/README.md); hiểu shape, chain rule và gradient.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox bên dưới theo dõi tiến độ biên soạn chung, không phải tiến độ học của một cá nhân.

## Mục tiêu

- Nối được layer, activation, loss, backward và optimizer thành một vòng lặp học.
- Phân biệt tham số của mô hình với hyperparameter và trạng thái optimizer.
- Chia dữ liệu train, validation và test theo mục đích sử dụng.
- Đọc learning curve và phân biệt lỗi code, underfitting và overfitting.
- Lưu, nạp và kiểm tra một checkpoint với thông tin đủ để tái hiện bài thực hành.

## Checklist nội dung

- [ ] Giải thích linear layer, activation và cách ghép thành mạng nhiều lớp.
- [ ] Minh họa forward, loss, backward, gradient clearing và optimizer step.
- [ ] Giới thiệu minibatch, DataLoader và cách tổng hợp loss theo số mẫu phù hợp.
- [ ] So sánh trực giác của SGD và Adam; giải thích learning rate, initialization và weight decay.
- [ ] Phân biệt train/validation/test, leakage và lựa chọn cấu hình trên validation.
- [ ] Giải thích train/eval mode, dropout, việc bật/tắt gradient và checkpoint.
- [ ] Trình bày sanity check: học một batch nhỏ, kiểm tra gradient và kiểm tra dự đoán.
- [ ] Dạy đọc learning curve, nhận diện overfitting và thử một thay đổi có kiểm soát.
- [ ] Hướng dẫn ghi seed, phiên bản, cấu hình và giới hạn của tính tái lập.

## Thực hành đề xuất

**Bài thực hành:** Tự viết training loop cho mạng nhỏ phân loại dữ liệu tổng hợp hai chiều.

Chọn bài toán đủ nhỏ để chạy trên CPU và vẽ được dự đoán.
Tạo các tập dữ liệu tách biệt trước khi chỉnh cấu hình.

**Các bước đề xuất:**

1. Tạo train, validation và test; nêu lý do chia dữ liệu và không dùng test để chọn cấu hình.
2. Xây mạng nhỏ, tính loss và cập nhật tham số bằng vòng lặp do mình viết.
3. Thử học một batch rất nhỏ để kiểm tra pipeline có khả năng khớp dữ liệu.
4. Huấn luyện trên train và theo dõi loss cùng metric trên validation.
5. Thử một learning rate không phù hợp hoặc bỏ bước xóa gradient để chẩn đoán lỗi.
6. Lưu checkpoint, nạp lại và so sánh đầu ra ở chế độ đánh giá.

**Sản phẩm mong đợi:** Script hoặc notebook, learning curve và bản ghi một lỗi đã tìm và sửa.

**Cách kiểm tra đề xuất:**

- Có baseline đơn giản và tập test chưa được dùng để chọn cấu hình.
- Có bằng chứng gradient và tham số được cập nhật theo dự kiến.
- So sánh checkpoint trong cùng chế độ và cùng đầu vào, với sai số hợp lý.
- Kết luận phản ánh dữ liệu quan sát được, không suy rộng từ một lần chạy nhỏ.

Đây là yêu cầu thiết kế bài thực hành; repo chưa công bố kết quả đã chạy.

## Câu hỏi tự kiểm tra

1. Vì sao loss trên train giảm nhưng chất lượng trên validation có thể giảm theo?
2. Gọi model.eval() có tự động tắt việc tính gradient không?
3. Khi mô hình không học nổi một batch nhỏ, cần kiểm tra những gì trước khi tăng kích thước mạng?

**Gợi ý kiểm tra:**

- Câu 1: Xét overfitting, khác biệt phân phối, cách đo metric và lỗi pipeline; không kết luận từ train loss.
- Câu 2: Chế độ eval và việc ghi đồ thị gradient là hai cơ chế riêng.
- Câu 3: Kiểm tra dữ liệu/nhãn, loss, gradient, optimizer, learning rate và tham số thực sự được cập nhật.

## Checklist hoàn thiện

- [ ] Có ví dụ giải thích từng bước của training loop và learning curve tương ứng.
- [ ] Có lab chạy trên CPU cùng hướng dẫn lưu, nạp và kiểm tra checkpoint.
- [ ] Có tiêu chí chấp nhận cho sanity check, metric và bài sửa lỗi.
- [ ] Có lỗi thường gặp về gradient, chế độ train/eval, leakage và tổng hợp loss.
- [ ] Nguồn tham khảo đã đối chiếu và một contributor khác đã rà soát nội dung.

## Tài liệu tham khảo

- [PyTorch — Learn the Basics](https://docs.pytorch.org/tutorials/beginner/basics/intro.html): đi qua workflow dữ liệu, mô hình, tối ưu và lưu mô hình.
- [PyTorch — Automatic Differentiation](https://docs.pytorch.org/tutorials/beginner/basics/autogradqs_tutorial.html): kiểm tra cách gradient được ghi và tích lũy.

Các liên kết được kiểm tra ngày 2026-11-15; contributor cần khóa phiên bản cho lab thực thi.

## Điều kiện hoàn thành

- Viết và giải thích được training loop cơ bản mà không sao chép nguyên mẫu.
- Phân biệt được dữ liệu để học, để chọn cấu hình và để đánh giá cuối.
- Tìm và sửa được ít nhất một lỗi khiến mô hình không học.
- Nêu được bằng chứng và giới hạn của một kết luận từ learning curve.

Việc đạt các điều kiện này là tiến độ cá nhân; không dùng nó để đánh dấu checklist biên soạn chung.

---

[← Trước: 01 · Nền tảng toán](../01-math-foundations/README.md) · [Tiếp: 03 · Language modeling và tokenization →](../03-language-modeling-tokenization/README.md)
