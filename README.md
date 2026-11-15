# AI-101

Kho học AI theo lộ trình: nắm nền tảng, hiểu cơ chế, tự thực hành và đánh giá kết quả. Nội dung được viết bằng tiếng Việt, giữ thuật ngữ tiếng Anh khi cần để đọc tài liệu và paper.

Chủ đề đầu tiên là **LLM — Large Language Models**, gồm **15 submodule** với khoảng **280 giờ học và thực hành**. Mỗi phần có mục tiêu, layout nội dung, đề bài thực hành, câu hỏi tự kiểm tra và checklist dành cho contributor.

**Trạng thái khởi đầu:** đã có cấu trúc và kế hoạch biên soạn. Các checklist chưa đánh dấu là phần cần được bổ sung hoặc kiểm tra trước khi coi là bài học hoàn thiện.

## Bắt đầu học

1. Đọc [lộ trình LLM](llm/README.md) để biết thứ tự và kết quả cần đạt.
2. Làm phần [tổng quan và chẩn đoán đầu vào](llm/00-overview-diagnostic/README.md).
3. Học các submodule theo thứ tự; dùng điều kiện hoàn thành để xác định phần cần ôn lại.
4. Với mỗi bài, tự giải thích, làm một ví dụ, thực hành và thử một trường hợp sai.
5. Tổng hợp kiến thức bằng [đồ án cuối lộ trình](llm/14-capstone/README.md).

## Cấu trúc repository

| Đường dẫn | Vai trò |
| --- | --- |
| [README.md](README.md) | Giới thiệu kho học và hướng dẫn đóng góp. |
| [llm/README.md](llm/README.md) | Layout toàn bộ chủ đề LLM, thứ tự học, thời lượng và đầu ra. |
| `llm/<số-thứ-tự>-<chủ-đề>/README.md` | Layout chi tiết và checklist của từng submodule. |

Khi phát triển một submodule, contributor có thể thêm bài viết, notebook, mã nguồn hoặc hình minh họa **ngay trong thư mục đó**, rồi liên kết chúng từ README của submodule. Chỉ thêm file và thư mục khi có nội dung thực tế.

## Chủ đề đang xây dựng

| Chủ đề | Phạm vi | Điểm bắt đầu |
| --- | --- | --- |
| **LLM** | Toán và PyTorch; language modeling; Transformer; dữ liệu và training; evaluation; fine-tuning; reasoning; inference; RAG; agent; nghiên cứu và đồ án. | [Xem layout LLM](llm/README.md) |

Các chủ đề AI tiếp theo sẽ được thêm thành thư mục riêng khi có lộ trình cụ thể, theo cùng cấu trúc README và submodule.

## Cách contributor cập nhật checklist

**Checkbox trong repository theo dõi mức hoàn thiện nội dung dùng chung.** Mục tiêu và điều kiện hoàn thành của người học được viết thành bullet thường để phân biệt với tiến độ biên soạn.

1. Chọn một mục chưa hoàn thành trong README của submodule.
2. Bổ sung nội dung tương ứng vào README hoặc một file trong cùng thư mục.
3. Nếu thêm file, đặt liên kết từ README đến file đó để người học tìm được.
4. Kiểm tra giải thích, ví dụ, cách thực hiện và kết quả mong đợi.
5. Đổi `- [ ]` thành `- [x]` cho đúng mục đã hoàn thành; giữ nguyên các mục còn thiếu.
6. Gửi thay đổi bằng commit hoặc pull request, nêu ngắn gọn phần bổ sung và cách đã kiểm tra.

**Một mục được đánh dấu khi sản phẩm của mục đó đã tồn tại và được kiểm tra.** Việc tạo tên file, liệt kê tiêu đề hoặc đọc xong một tài liệu chưa đủ để hoàn thành một mục biên soạn. Bảng tổng trong `llm/README.md` chỉ dùng để điều hướng; checklist tại từng submodule là nơi cập nhật tiến độ chính.

Người học muốn theo dõi tiến độ cá nhân có thể sao chép mục tiêu và câu hỏi tự kiểm tra vào ghi chú hoặc fork của mình.

## Tiêu chuẩn cho một phần đóng góp

- Giải thích vấn đề và trực giác trước khi đưa công thức hoặc code.
- Định nghĩa thuật ngữ khi dùng lần đầu; ghi rõ shape và ý nghĩa các trục khi trình bày tensor.
- Có ví dụ cụ thể, hướng dẫn thực hành và kết quả mong đợi hoặc tiêu chí chấp nhận.
- Phân biệt ví dụ minh họa, kết quả dự kiến và thí nghiệm đã thực sự chạy.
- Ghi nguồn cho kiến thức chuyên môn; ưu tiên paper gốc, tài liệu chính thức và tài liệu của tác giả.
- Với code, ghi môi trường, phiên bản, dữ liệu, cấu hình và cách tái chạy phù hợp.
- Nêu lỗi thường gặp, giới hạn và cách kiểm tra; giữ lại những kết quả bất lợi có liên quan.
- Dùng Markdown và liên kết tương đối cho tài liệu trong repository.

## Checklist trước khi gửi đóng góp

Checklist dưới đây áp dụng cho từng lần đóng góp. Giữ nguyên các ô trong README và sao chép checklist vào mô tả pull request nếu cần.

- [ ] Nội dung nằm đúng submodule và gắn với một mục tiêu cụ thể.
- [ ] Các liên kết mới mở được và dẫn đúng nội dung.
- [ ] Ví dụ hoặc hướng dẫn thực hành đã được kiểm tra; kết quả chưa chạy được ghi rõ.
- [ ] Có đáp án gợi ý hoặc tiêu chí chấp nhận cho bài tự làm.
- [ ] Chỉ đánh dấu các mục thực sự hoàn thành trong README của submodule.
- [ ] Mô tả thay đổi nêu phần đã bổ sung, cách kiểm tra và việc còn thiếu.

## Cách hiểu việc hoàn thành lộ trình

Người học cần có khả năng **giải thích**, **theo dõi cơ chế**, **tự thực hiện** và **chẩn đoán lỗi**. Số giờ là ước lượng để lập kế hoạch; kết quả thực hành và các điều kiện hoàn thành mới quyết định có cần học lại một phần hay không.

Lộ trình và nguồn nền tảng được rà soát ngày **15/11/2026**. Khi bổ sung hướng dẫn phụ thuộc thư viện hoặc model cụ thể, contributor cần kiểm tra lại phiên bản và nguồn tương ứng.
