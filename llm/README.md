# Lộ trình học LLM

[Trang chủ AI-101](../README.md) · [Bắt đầu với tổng quan và chẩn đoán](00-overview-diagnostic/README.md)

Lộ trình đưa người học từ nền tảng đến khả năng tự xây một GPT nhỏ, điều chỉnh mô hình có sẵn, đánh giá kết quả và triển khai một hệ thống LLM ở phạm vi dự án nhỏ. Mục tiêu dài hạn là có cơ sở để đọc paper và chọn một hướng nghiên cứu chuyên sâu.

**Quy mô:** 15 submodule, khoảng **280 giờ học và thực hành chủ động**, chưa bao gồm thời gian máy chạy dài. Thời lượng là ước lượng biên soạn của chương trình, không phải yêu cầu chính thức của một khóa học hay cam kết đạt trình độ trong một thời hạn cố định.

**Trạng thái nội dung:** các README là layout và đề bài để contributor phát triển thành bài học. Theo dõi phần đã hoàn thiện bằng checklist tại từng submodule.

## Mục tiêu đầu ra

- Giải thích đường đi từ văn bản qua tokenizer, embedding và Transformer đến token được sinh ra.
- Hiểu loss, gradient, optimizer và vai trò của dữ liệu trong quá trình huấn luyện.
- Tự xây, huấn luyện, lưu và kiểm tra một mô hình kiểu GPT nhỏ.
- Chọn can thiệp phù hợp: dữ liệu, prompt, fine-tuning, retrieval hoặc cách suy luận.
- Thiết kế phép so sánh có baseline, tập đánh giá tách biệt và phân tích regression.
- Đọc được claim, giả thiết, phương pháp và bằng chứng của một paper.
- Tích hợp mô hình vào một dự án có chất lượng, hiệu năng và giới hạn được đo rõ.

## Điều kiện đầu vào

Người học cần Python căn bản: hàm, cấu trúc dữ liệu, thao tác file và đọc lỗi. Kiến thức tensor, xác suất và đạo hàm sẽ được ôn hoặc bổ sung ở submodule 01–02.

Tại submodule 00, tự kiểm tra khả năng viết một chương trình xử lý dữ liệu, xác định shape phép nhân ma trận, giải thích đạo hàm và xác suất có điều kiện. Nếu đã vững một phần, làm bài kiểm tra và thực hành của phần đó trước khi học nhanh qua.

## Layout các submodule

Các số trong cột tiên quyết chỉ submodule cần nắm trước. Danh sách được sắp theo tuyến học chính; sau nền tảng, một số phần ứng dụng có thể học song song nếu đã đạt điều kiện đầu vào.

| Mã | Submodule | Giờ | Tiên quyết chính | Sản phẩm hoặc năng lực cần đạt |
| --- | --- | ---: | --- | --- |
| 00 | [Tổng quan và chẩn đoán](00-overview-diagnostic/README.md) | 4 | Python căn bản | Bản đồ vòng đời LLM và danh sách kiến thức cần bổ sung. |
| 01 | [Toán và tensor](01-math-foundations/README.md) | 16 | 00 | Theo dõi đúng shape, xác suất và gradient trên ví dụ nhỏ. |
| 02 | [Neural network và PyTorch](02-neural-networks-pytorch/README.md) | 20 | 01 | Training loop tự viết và khả năng chẩn đoán lỗi huấn luyện. |
| 03 | [Language modeling và tokenization](03-language-modeling-tokenization/README.md) | 16 | 01–02 | Bigram LM, input–target đúng và vòng lấy mẫu token. |
| 04 | [Attention và Transformer](04-attention-transformer/README.md) | 24 | 01–03 | Attention và decoder block với causal mask được kiểm tra. |
| 05 | [Tự xây GPT nhỏ](05-build-tiny-gpt/README.md) | 24 | 02–04 | Mô hình nhỏ huấn luyện, khôi phục checkpoint và sinh văn bản được. |
| 06 | [Dữ liệu và pretraining](06-data-pretraining/README.md) | 22 | 05 | Data card và một thí nghiệm xử lý dữ liệu có kiểm soát. |
| 07 | [Đánh giá LLM](07-evaluation/README.md) | 20 | 05–06 | Bộ đánh giá, kiểm scorer và báo cáo lỗi theo nhóm. |
| 08 | [SFT và PEFT](08-sft-peft/README.md) | 24 | 06–07 | Thí nghiệm fine-tuning với baseline và kiểm regression. |
| 09 | [Alignment và reasoning](09-alignment-reasoning/README.md) | 20 | 07–08 | Phân biệt SFT/DPO/RL và so sánh reasoning theo ngân sách suy luận. |
| 10 | [Inference và serving](10-inference-serving/README.md) | 18 | 05, 07 | Benchmark chất lượng, độ trễ, throughput và bộ nhớ. |
| 11 | [Retrieval và RAG](11-retrieval-rag/README.md) | 18 | 03, 07 | Hỏi đáp tài liệu có đánh giá retrieval và generation riêng. |
| 12 | [Tool use và agent](12-tool-use-agents/README.md) | 14 | 07, 11 | Agent nhỏ có điều kiện dừng, xử lý lỗi và kiểm kết quả. |
| 13 | [Đọc paper và hướng chuyên sâu](13-research-frontiers/README.md) | 12 | 05–07 | Bản phân tích paper và đề xuất một thí nghiệm đối chứng. |
| 14 | [Đồ án tổng hợp](14-capstone/README.md) | 28 | 07, 10–11; thêm 08 nếu fine-tune, 12 nếu dùng agent | Dự án nhỏ có demo, cấu hình tái lập và báo cáo đánh giá. |
| | **Tổng** | **280** | | |

## Sáu chặng học

| Chặng | Submodule | Trọng tâm |
| --- | --- | --- |
| A. Nền tảng | 00–02 | Hiểu bài toán, toán và cách mạng neural học. |
| B. Cơ chế LLM | 03–05 | Hiểu token, Transformer và tự xây mô hình nhỏ. |
| C. Huấn luyện và đo lường | 06–07 | Thiết kế dữ liệu và đánh giá đúng. |
| D. Cải thiện mô hình | 08–09 | Fine-tuning, preference learning và reasoning. |
| E. Hệ thống thực tế | 10–12 | Serving, RAG và sử dụng công cụ. |
| F. Tổng hợp và nghiên cứu | 13–14 | Phân tích paper và hoàn thành dự án độc lập. |

Đánh giá cơ bản bắt đầu từ submodule 02: chia dữ liệu, theo dõi train/validation và kiểm lỗi. Submodule 07 hệ thống hóa các kỹ năng đó. Thiết kế thí nghiệm bắt đầu từ submodule 06 và được dùng lại trong các phần sau.

## Cấu trúc của một submodule

Mỗi README gồm mục tiêu, kiến thức tiên quyết, checklist nội dung cần biên soạn, thực hành đề xuất, câu hỏi tự kiểm tra, checklist hoàn thiện, nguồn tham khảo và điều kiện hoàn thành.

Khi phát triển bài học, dùng trình tự: câu hỏi thực tế, trực giác, cơ chế hoặc công thức, ví dụ cụ thể, thực hành, trường hợp sai và kiểm tra độc lập. Có thể thêm các file như bài giải thích, notebook, script hoặc hình minh họa trong thư mục submodule rồi dẫn link từ README.

## Bốn mốc kiểm tra năng lực

| Mốc | Bằng chứng người học cần tự tạo |
| --- | --- |
| Sau 03 | Giải thích được trọng số, gradient và lấy mẫu; tạo input–target chính xác. |
| Sau 05 | Theo dõi một câu từ token đến logits; sửa được lỗi shape, nhãn hoặc causal mask. |
| Sau 09 | Chọn can thiệp có lý do, thiết kế so sánh và nhận ra regression. |
| Sau 14 | Tự hoàn thành dự án nhỏ, tái lập kết quả và bảo vệ quyết định kỹ thuật. |

Mỗi mốc kiểm tra bốn khả năng: **giải thích**, **theo dõi cơ chế**, **tự thực hiện** và **chẩn đoán lỗi**. Nếu chưa đạt, quay lại submodule chứa kỹ năng còn thiếu và thử một ví dụ khác.

## Nhịp học gợi ý

| Phương án | Nhịp học | Thời gian ước lượng |
| --- | --- | --- |
| Chuẩn | 10–12 giờ mỗi tuần | Khoảng 24–28 tuần; điều chỉnh theo bài thực hành. |
| Tập trung | Khoảng 20 giờ mỗi tuần, đã vững Python và deep learning cơ bản | Khoảng 14–16 tuần, có thời gian sửa lỗi và ôn lại. |

Có thể bắt đầu với 30% thời gian đọc/học, 50% code và thí nghiệm, 20% giải thích lại và tổng kết. Đây là cách phân bổ đề xuất; tăng thời gian cho phần đang yếu. Nếu cần học Python từ đầu, bổ sung thời gian chuẩn bị ngoài 280 giờ này.

## Môi trường và bằng chứng thực hành

- Bắt đầu bằng Python, PyTorch và ví dụ nhỏ; kiểm tính đúng trước khi chạy thí nghiệm lớn.
- Chọn model, batch và context sau khi đo tài nguyên thực tế; README này không giả định một GPU cụ thể.
- Ghi phiên bản thư viện, model/tokenizer, dữ liệu, cấu hình và seed khi chúng ảnh hưởng đến việc tái lập.
- Ghi rõ kết quả nào đã chạy, kết quả nào chỉ là kỳ vọng hoặc ví dụ minh họa.
- Với bài đánh giá, giữ dev/test tách biệt và lưu đủ thông tin để kiểm từng dự đoán.
- Lưu code, notebook, báo cáo và hình tại submodule tương ứng; tài liệu lớn hoặc model weights nên có hướng dẫn lấy về thay vì đưa trực tiếp vào Git.

## Cách dùng checklist khi đóng góp

Checkbox trong từng submodule theo dõi **tiến độ biên soạn nội dung**. Đánh dấu khi đã có phần giải thích, ví dụ, bài thực hành hoặc tài liệu kiểm chứng tương ứng. Hướng dẫn chi tiết nằm tại [README gốc](../README.md).

Bảng layout ở trên không lưu bản sao checkbox hay phần trăm tiến độ. Contributor cập nhật checklist ngay trong README của submodule để tránh hai nơi phản ánh trạng thái khác nhau.

Các mục tiêu và điều kiện hoàn thành dành cho người học là tiêu chí tự đánh giá. Tiến độ học của từng cá nhân nên được ghi riêng, không thay đổi checkbox nội dung dùng chung chỉ vì đã học xong phần đó.

## Nhánh đào sâu sau phần cốt lõi

| Nhánh | Chủ đề có thể mở rộng | Nền tảng nên vững |
| --- | --- | --- |
| Dữ liệu và fine-tuning | Data mixture, synthetic data, multi-domain training, forgetting | 06–09 |
| Kiến trúc | Mixture of Experts, long context, state-space và kiến trúc lai | 01–06 |
| Reasoning và RL | Reward design, policy optimization, verifier, test-time compute | 07–09 |
| Hệ thống | Distributed training, sharding, parallelism, kernel, scheduler | 02, 05–06, 10 |
| Đánh giá và độ tin cậy | Calibration, robustness, OOD, judge evaluation, interpretability | 07–09 |
| Multimodal | Vision-language, ảnh/video/audio và dữ liệu liên kết | 03–08 |
| Agent | Planning, memory, tác vụ dài và phối hợp nhiều agent | 10–12 |

Submodule 13 giới thiệu bản đồ các nhánh này. Việc triển khai chuyên sâu sẽ là nội dung mở rộng, ngoài ngân sách cốt lõi 280 giờ.

## Tài liệu nền tảng

| Nguồn | Vai trò trong lộ trình |
| --- | --- |
| [Dive into Deep Learning — Preliminaries](https://d2l.ai/chapter_preliminaries/index.html) | Toán, tensor, tự động vi phân và xác suất. |
| [PyTorch — Learn the Basics](https://docs.pytorch.org/tutorials/beginner/basics/intro.html) | Tensor, data loader, model, autograd, optimization và checkpoint. |
| [Karpathy — Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html) | Backprop, mô hình ngôn ngữ nhỏ, GPT và tokenizer. |
| [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch) | Trục thực hành xây GPT, huấn luyện và fine-tuning. |
| [Hugging Face — LLM Course](https://huggingface.co/learn/llm-course/chapter1/1) | Làm việc với model, dataset, tokenizer và fine-tuning thực tế. |
| [Stanford CS336](https://cs336.stanford.edu/) | Đào sâu architecture, data, scaling, systems và alignment sau khi có nền tảng. |
| [EleutherAI — Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) | Thiết kế và thực hiện evaluation có cấu hình. |
| [vLLM Documentation](https://docs.vllm.ai/en/latest/) | Inference, serving và benchmark. |

Các submodule dẫn thêm paper gốc và tài liệu chuyên biệt. Nguồn nền tảng đã được rà soát ngày **15/11/2026**; khi thêm hướng dẫn thực thi, kiểm lại tài liệu tương ứng với phiên bản đang dùng.
