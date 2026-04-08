# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Temperature càng thấp (0.0) thì câu trả lời càng nhất quán, chính xác và có thể dự đoán được. Khi temperature tăng lên (1.0, 1.5), câu trả lời trở nên đa dạng, sáng tạo hơn nhưng cũng có thể lan man hoặc kém chính xác hơn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature từ 0.0 đến 0.3 vì chatbot hỗ trợ khách hàng cần cung cấp thông tin chính xác, nhất quán và đáng tin cậy. Temperature thấp giúp tránh các câu trả lời sai lệch hoặc bịa đặt thông tin.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Workload: 10,000 users × 3 calls × 350 tokens = 10,500,000 tokens/ngày = 10,500 × 1K tokens.
> - GPT-4o: 10,500 × $0.010 = $105/ngày
> - GPT-4o-mini: 10,500 × $0.0006 = $6.30/ngày
> GPT-4o đắt hơn khoảng **16.7 lần** so với GPT-4o-mini ($105 / $6.30 ≈ 16.7).

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> - **GPT-4o xứng đáng:** Các tác vụ phức tạp như phân tích hợp đồng pháp lý, tư vấn y tế, viết code phức tạp, hoặc khi độ chính xác là yếu tố quan trọng nhất và sai sót có thể gây hậu quả nghiêm trọng.
> - **GPT-4o-mini tốt hơn:** Các tác vụ đơn giản như trả lời FAQ, chatbot hỗ trợ khách hàng cơ bản, tóm tắt văn bản ngắn, hoặc khi cần xử lý khối lượng lớn request với ngân sách hạn chế.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi người dùng cần phản hồi nhanh và tương tác thời gian thực, như chatbot, trợ lý ảo, hoặc khi response dài và người dùng có thể bắt đầu đọc trong khi model vẫn đang sinh text. Điều này cải thiện UX vì giảm perceived latency — người dùng thấy phản hồi ngay lập tức thay vì phải chờ đợi. Non-streaming phù hợp hơn khi cần xử lý toàn bộ response trước khi hiển thị (như parsing JSON, validate format), khi response ngắn (latency không đáng kể), hoặc trong các pipeline tự động hóa backend mà không có người dùng trực tiếp chờ đợi.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
