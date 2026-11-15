# 05 · Tự xây một GPT nhỏ

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 24 giờ học và thực hành; thời gian chạy máy phụ thuộc cấu hình.

**Học trước:** [04 · Attention và Transformer](../04-attention-transformer/README.md).

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Các checkbox bên dưới theo dõi việc biên soạn nội dung chung. Năng lực của người học được kiểm tra riêng ở cuối bài.

## Mục tiêu

- Nối tokenizer, embedding, Transformer block và đầu ra thành một language model hoàn chỉnh.
- Giải thích đường đi của một batch từ văn bản đến loss và cập nhật trọng số.
- Tự viết vòng huấn luyện và vòng sinh token, rồi phát hiện những lỗi cơ bản.
- Phân biệt mô hình nhỏ phục vụ học cơ chế với mô hình có năng lực ứng dụng thực tế.

## Checklist nội dung

- [ ] Biên soạn sơ đồ toàn bộ pipeline: văn bản → token → batch → model → logits → loss.
- [ ] Giải thích input và target lệch một vị trí, padding và những vị trí không tham gia loss.
- [ ] Hướng dẫn lắp embedding, positional information, causal attention, MLP, residual và normalization.
- [ ] Bổ sung bảng kích thước tensor, từ `[B, T]` đến logits `[B, T, V]`, cùng cách đếm tham số.
- [ ] Viết bài về training loop: forward, loss, backward, optimizer, learning rate và gradient clipping.
- [ ] Giải thích chia train/validation/test, theo dõi loss và nhận diện overfitting ngay từ mô hình đầu tiên.
- [ ] Hướng dẫn generation tự hồi quy: lấy logits ở vị trí cuối, chọn token, nối vào chuỗi và dừng.
- [ ] Soạn phần checkpoint, khôi phục optimizer state, seed, config và ghi nhận môi trường chạy.
- [ ] Xây bài debug cho causal mask sai, target lệch sai, gradient không cập nhật và dữ liệu bị trùng.

## Thực hành đề xuất

### Lab: mô hình ngôn ngữ nhỏ từ đầu

Chọn một tập văn bản nhỏ có quyền sử dụng rõ ràng. Chia theo tài liệu hoặc nhóm nguồn trước khi tạo các cửa sổ token để hạn chế giao nhau giữa train và validation.

Bắt đầu bằng tokenizer ký tự để tập trung vào mô hình; có thể thay bằng tokenizer đã học ở chặng trước sau khi phiên bản đầu hoạt động.

Tự viết một decoder-only Transformer nhỏ bằng PyTorch và vòng train/generate. Thư viện tensor và autograd được dùng; không thay phần mô hình bằng một lớp pretrained có sẵn.

**Sản phẩm cần nộp:**

- Mã mô hình, training loop và generation loop có chú thích kích thước tensor.
- Cấu hình nhỏ, thông tin dữ liệu, checkpoint và hướng dẫn tái chạy.
- Đồ thị train/validation loss và vài mẫu sinh có ghi rõ decoding setting.
- Một ghi chú giải thích lỗi đã gặp, cách chẩn đoán và cách sửa.

**Kiểm tra chấp nhận:**

- Model overfit được một minibatch nhỏ trong bài kiểm tra riêng để xác nhận pipeline có khả năng học.
- Khi thay token ở tương lai, logits của các vị trí trước đó không đổi trong chế độ đánh giá phù hợp.
- Checkpoint nạp lại cho kết quả khớp trong sai số số học với cùng input và thiết lập kiểm tra.
- Loss và gradient hữu hạn; validation được tính trên dữ liệu tách biệt và không cập nhật trọng số.

Không yêu cầu câu sinh phải hay. Mục tiêu chính là chứng minh các thành phần nối đúng và giải thích được hành vi quan sát.

## Câu hỏi tự kiểm tra

### 1. Vì sao input và target phải lệch nhau một token?

**Gợi ý kiểm tra:** Ở vị trí `t`, model nhận tiền tố đến `t` để dự đoán token tiếp theo. Nếu vô tình cho model thấy đáp án, loss thấp có thể chỉ phản ánh rò rỉ thông tin.

### 2. Vì sao loss giảm nhưng văn bản sinh vẫn có thể lặp hoặc vô nghĩa?

**Gợi ý kiểm tra:** Xem lại dữ liệu, mức overfitting, cách tính loss và decoding. Giảm loss trên train chưa chứng minh khả năng sinh tốt trên đầu vào mới.

### 3. Nếu mô hình không overfit nổi một batch nhỏ, bạn kiểm tra gì trước?

**Gợi ý kiểm tra:** Kiểm tra target/mask, gradient, tham số được optimizer cập nhật và learning rate. Đừng tăng kích thước mô hình trước khi xác nhận pipeline đúng.

## Checklist hoàn thiện

- [ ] Có ví dụ số xuyên suốt từ một chuỗi ngắn đến target và loss.
- [ ] Lab chạy được với cấu hình nhỏ, có hướng dẫn tài nguyên và khôi phục checkpoint.
- [ ] Có đáp án, giải thích và tiêu chí chấp nhận cho từng bài thực hành.
- [ ] Có các ca lỗi có chủ đích và hướng dẫn chẩn đoán theo bằng chứng.
- [ ] Nguồn, mã và kết quả minh họa đã được kiểm tra; ghi rõ phiên bản sử dụng.

## Tài liệu tham khảo

- [Karpathy — Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html): phần makemore và xây GPT giúp nối trực giác với code.
- [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch): chương 4–5 về mô hình GPT, pretraining và training loop.
- [Stanford CS336](https://cs336.stanford.edu/): Assignment 1 là tài liệu mở rộng sau khi phiên bản nhỏ đã hoạt động.

## Điều kiện hoàn thành

- Bạn vẽ và giải thích được toàn bộ forward pass cùng kích thước tensor chính.
- Bạn tự sửa được một lỗi ở target, mask hoặc gradient bằng kiểm tra cụ thể.
- Bạn chạy lại được mô hình từ config/checkpoint và giải thích giới hạn của kết quả.

**Trước:** [04 · Attention và Transformer](../04-attention-transformer/README.md) · **Tiếp:** [06 · Dữ liệu và pretraining](../06-data-pretraining/README.md)
