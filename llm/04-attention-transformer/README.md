# 04 · Attention và Transformer

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 24 giờ học chủ động, gồm tính tay, code và kiểm tra causal attention.

**Kiến thức trước:** [03 · Language modeling và tokenization](../03-language-modeling-tokenization/README.md); vững shape, nhân ma trận, softmax và gradient.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox bên dưới theo dõi tiến độ biên soạn chung, không phải tiến độ học của một cá nhân.

## Mục tiêu

- Giải thích vì sao biểu diễn của token cần sử dụng thông tin từ các token khác.
- Theo dõi được Q, K, V, attention scores và output bằng shape cụ thể.
- Tự viết được causal self-attention và kiểm tra việc không nhìn token tương lai.
- Nêu vai trò của feed-forward, residual, normalization và thông tin vị trí trong một block.
- Phân biệt Transformer nguyên bản với lựa chọn decoder-only dùng cho bài GPT nhỏ tiếp theo.

## Checklist nội dung

- [ ] Dẫn từ tổng có trọng số tới trực giác query, key, value bằng ví dụ ba token.
- [ ] Giải thích các phép chiếu Q/K/V, scaled dot-product và softmax theo đúng trục.
- [ ] Tính tay một attention head với ma trận nhỏ, ghi shape sau từng bước.
- [ ] So sánh causal mask và padding mask; giải thích cách ngăn nhìn token tương lai.
- [ ] Minh họa tách nhiều head, ghép head và output projection.
- [ ] Giải thích positional encoding/embedding và giới thiệu mục đích của RoPE ở mức định hướng.
- [ ] Ghép attention, feed-forward, residual và normalization thành một decoder block.
- [ ] Phân biệt encoder, decoder, cross-attention và cấu trúc decoder-only được chọn trong khóa học.
- [ ] Nêu chi phí theo độ dài chuỗi và giới hạn của việc dùng attention weights để giải thích mô hình.

## Thực hành đề xuất

**Bài thực hành:** Tự cài đặt một causal attention head rồi mở rộng thành block nhỏ.

Dùng chuỗi tensor tổng hợp rất ngắn trên CPU để có thể quan sát toàn bộ phép tính.
Chưa dùng một lớp Transformer hoàn chỉnh có sẵn cho phần cần tự cài đặt.

**Các bước đề xuất:**

1. Chọn kích thước batch, chiều dài chuỗi, chiều embedding và chiều của mỗi head.
2. Viết Q/K/V, scores, scaling, causal mask, softmax và tổng có trọng số.
3. So sánh một trường hợp nhỏ với phép tính tay hoặc implementation tham chiếu.
4. Giữ nguyên tiền tố, thay token tương lai và kiểm tra output tại các vị trí trước đó.
5. Mở rộng thành multi-head attention và ghép feed-forward, residual, normalization.
6. Cố ý bỏ mask hoặc chọn sai trục softmax rồi mô tả tín hiệu giúp tìm lỗi.

**Sản phẩm mong đợi:** Script hoặc notebook, bảng shape và báo cáo kiểm tra một lỗi attention.

**Cách kiểm tra đề xuất:**

- Xác suất attention tổng bằng một theo trục key ở mỗi hàng có ít nhất một vị trí hợp lệ.
- Vị trí bị chặn không đóng góp vào attention; padding được xét riêng nếu bài dùng padding.
- Kiểm tra thay tương lai được chạy ở chế độ xác định, tắt dropout và có sai số số học phù hợp.
- Forward giữ đúng shape dự kiến; backward tạo gradient hữu hạn trên ví dụ kiểm tra.

Đây là yêu cầu thiết kế bài thực hành; repo chưa công bố kết quả đã chạy.

## Câu hỏi tự kiểm tra

1. Q, K và V có vai trò gì, và shape của ma trận attention liên hệ với chiều dài chuỗi ra sao?
2. Khi bỏ causal mask, vì sao training loss có thể trông tốt nhưng việc sinh tự hồi quy bị sai?
3. Vì sao chỉ cài attention vẫn chưa tạo thành một Transformer block đầy đủ?

**Gợi ý kiểm tra:**

- Câu 1: Q/K tạo mức tương tác, V cung cấp nội dung trộn; một head self-attention đầy đủ có scores theo cặp vị trí.
- Câu 2: Đầu ra khi huấn luyện có thể dùng thông tin mà lúc sinh chưa tồn tại; kiểm tra điều này bằng thay token tương lai.
- Câu 3: Cần xét thêm biến đổi feed-forward, đường residual, normalization và cách đưa thông tin vị trí vào kiến trúc.

## Checklist hoàn thiện

- [ ] Có ví dụ số và sơ đồ tensor xuyên suốt một attention head đến decoder block.
- [ ] Có lab CPU với kiểm tra mask, shape, gradient và hướng dẫn tái chạy.
- [ ] Có lời giải hoặc acceptance criteria cho bài tính tay và bài thay token tương lai.
- [ ] Có lỗi thường gặp về trục softmax, broadcast mask, reshape head và dropout khi kiểm tra.
- [ ] Nguồn tham khảo đã đối chiếu và một contributor khác đã rà soát nội dung.

## Tài liệu tham khảo

- [Vaswani và cộng sự — Attention Is All You Need](https://arxiv.org/abs/1706.03762): đọc cấu trúc attention và Transformer nguyên bản; chú ý bối cảnh encoder–decoder.
- [Stanford CS336](https://cs336.stanford.edu/): tham khảo hướng xây kiến trúc mô hình ngôn ngữ và bài thực hành từ các thành phần cơ bản.

Các liên kết được kiểm tra ngày 2026-11-15; phần mở rộng kiến trúc cần nguồn gốc riêng khi được biên soạn.

## Điều kiện hoàn thành

- Giải thích được từng phép tính và shape trong causal self-attention.
- Tự viết được một head attention và ghép được các thành phần của block nhỏ.
- Chứng minh bằng kiểm tra rằng output tại một vị trí không dùng token tương lai.
- Tìm và sửa được lỗi mask hoặc trục softmax mà không dựa riêng vào train loss.

Việc đạt các điều kiện này là tiến độ cá nhân; không dùng nó để đánh dấu checklist biên soạn chung.

---

[← Trước: 03 · Language modeling và tokenization](../03-language-modeling-tokenization/README.md) · [Tiếp: 05 · Tự xây GPT nhỏ →](../05-build-tiny-gpt/README.md)
