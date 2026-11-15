# 03 · Language modeling và tokenization

[Trang chủ](../../README.md) · [Lộ trình LLM](../README.md)

**Thời lượng dự kiến:** 16 giờ học chủ động, gồm xử lý chuỗi và một mô hình baseline nhỏ.

**Kiến thức trước:** [02 · Neural network và PyTorch](../02-neural-networks-pytorch/README.md); hiểu loss, softmax và train/validation/test.

**Trạng thái:** Khung nội dung; các mục chưa đánh dấu đang chờ biên soạn hoặc kiểm tra.

Checkbox bên dưới theo dõi tiến độ biên soạn chung, không phải tiến độ học của một cá nhân.

## Mục tiêu

- Giải thích cách biến văn bản thành token ID, embedding và mục tiêu dự đoán.
- Phân biệt ký tự, từ, token và biểu diễn vector của token.
- Tạo đúng cặp input–target cho bài toán dự đoán token tiếp theo.
- Nối logits, xác suất, cross-entropy và quá trình chọn token khi sinh văn bản.
- Nhận ra giới hạn của perplexity và tránh so sánh sai giữa các tokenizer.

## Checklist nội dung

- [ ] Giải thích xác suất của chuỗi qua các xác suất token có điều kiện trên tiền tố.
- [ ] So sánh tokenization theo ký tự, byte, từ và subword trên văn bản Việt/Anh.
- [ ] Minh họa vocabulary, token ID, special token, encode/decode và ảnh hưởng của normalization.
- [ ] Trình bày trực giác Byte-Pair Encoding bằng một tập từ nhỏ.
- [ ] Phân biệt embedding lookup, contextual representation và output logits.
- [ ] Hướng dẫn tạo input–target lệch một vị trí, teacher forcing và xử lý ranh giới tài liệu.
- [ ] Giải thích cross-entropy, token masking, perplexity và điều kiện so sánh hợp lệ.
- [ ] So sánh greedy decoding, temperature, top-k và top-p trên một phân phối nhỏ.
- [ ] Xây baseline bigram và chỉ ra giới hạn của ngữ cảnh ngắn.

## Thực hành đề xuất

**Bài thực hành:** Xây tokenizer theo ký tự và baseline bigram cho một tập văn bản nhỏ.

Dùng văn bản tự viết hoặc có quyền sử dụng rõ ràng; tách train và validation theo tài liệu trước khi tạo cửa sổ.
Ghi cách xử lý ký tự chưa thấy và chính sách chuẩn hóa văn bản.

**Các bước đề xuất:**

1. Tạo vocabulary trên dữ liệu train và viết encode/decode.
2. Kiểm tra một câu tiếng Việt có dấu và giải thích cách biểu diễn được chọn.
3. In các cặp input–target để xác nhận mỗi nhãn là token tiếp theo.
4. Xây baseline bigram, tính loss trên dữ liệu được giữ lại và sinh một đoạn ngắn.
5. So sánh greedy với hai mức temperature trên cùng mô hình và cùng tiền tố.
6. Ghi lỗi quan sát được và liên hệ với lượng ngữ cảnh mà baseline sử dụng.

**Sản phẩm mong đợi:** Notebook hoặc script, ví dụ input–target, bảng loss và các mẫu sinh có cấu hình rõ.

**Cách kiểm tra đề xuất:**

- Encode/decode khớp chính sách normalization đã công bố, không giả định mọi tokenizer đều đảo ngược nguyên văn.
- Không để cùng một tài liệu xuất hiện ở cả train và validation qua các cửa sổ chồng lấn.
- Loss bỏ qua đúng các vị trí không được chấm và không lấy tương lai làm đầu vào.
- Không kết luận về chất lượng chỉ từ một mẫu sinh trông có vẻ hay.

Đây là yêu cầu thiết kế bài thực hành; repo chưa công bố kết quả đã chạy.

## Câu hỏi tự kiểm tra

1. Token ID và embedding khác nhau như thế nào, và token có luôn là một từ không?
2. Với chuỗi A B C D, cặp input–target để học dự đoán token tiếp theo có thể viết ra sao?
3. Có thể dùng perplexity để xếp hạng trực tiếp hai mô hình dùng tokenizer khác nhau không?

**Gợi ý kiểm tra:**

- Câu 1: ID là chỉ mục rời rạc; embedding là vector được tra từ tham số; token có thể là đơn vị khác từ.
- Câu 2: Input A B C đi với target B C D; kiểm tra cả vị trí và ranh giới chuỗi.
- Câu 3: Token là đơn vị tính khác nhau nên so sánh token-level perplexity trực tiếp có thể sai nghĩa.

## Checklist hoàn thiện

- [ ] Có ví dụ xuyên suốt từ văn bản tới token, xác suất và loss.
- [ ] Có lab CPU cùng dữ liệu nhỏ, chính sách chia tập và cấu hình sampling rõ ràng.
- [ ] Có đáp án cho bài lệch nhãn và tiêu chí chấm tokenizer/bigram.
- [ ] Có lỗi thường gặp về special token, normalization, padding và leakage giữa các cửa sổ.
- [ ] Nguồn tham khảo đã đối chiếu và một contributor khác đã rà soát nội dung.

## Tài liệu tham khảo

- [Hugging Face — Tokenizers chapter](https://huggingface.co/learn/llm-course/chapter6/1): học các bước xử lý và các họ thuật toán tokenization.
- [Stanford CS336](https://cs336.stanford.edu/): đối chiếu mối liên hệ giữa tokenizer, language modeling và đánh giá mô hình.

Các liên kết được kiểm tra ngày 2026-11-15; contributor cần ghi tokenizer và phiên bản khi đưa số liệu minh họa.

## Điều kiện hoàn thành

- Giải thích được một lượt dự đoán từ token ID tới phân phối của token tiếp theo.
- Tự tạo và kiểm tra được cặp input–target đúng.
- Viết được baseline nhỏ và mô tả được giới hạn của nó.
- Sửa được lỗi lệch nhãn hoặc lỗi chia dữ liệu gây đánh giá sai.

Việc đạt các điều kiện này là tiến độ cá nhân; không dùng nó để đánh dấu checklist biên soạn chung.

---

[← Trước: 02 · Neural network và PyTorch](../02-neural-networks-pytorch/README.md) · [Tiếp: 04 · Attention và Transformer →](../04-attention-transformer/README.md)
