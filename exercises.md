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
> *Câu trả lời của bạn*
> Khi tăng `temperature` từ 0.0 → 1.5, câu trả lời chuyển từ rất nhất quán, ít sáng tạo (0.0) sang đa dạng, bất ngờ và giàu biến thể hơn (1.5). Giá trị thấp trả về đáp án an toàn, lặp lại; giá trị cao tạo ra ý tưởng mới nhưng có thể thêm thông tin ít chính xác hơn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Câu trả lời của bạn*
> Mình sẽ chọn `temperature` thấp (ví dụ 0.0–0.2) cho chatbot hỗ trợ khách hàng để đảm bảo phản hồi nhất quán, chính xác và ít gây hiểu nhầm.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Câu trả lời của bạn*
> Giả sử 350 token chia đều thành 175 token input + 175 token output:

- GPT-4o per-call: (175*5.00 + 175*20.00) / 1_000_000 = (4375) / 1_000_000 = $0.004375
- GPT-4o-mini per-call: (175*0.150 + 175*0.600) / 1_000_000 = (131.25) / 1_000_000 = $0.00013125

=> Tỷ lệ: 0.004375 / 0.00013125 ≈ 33.33 → GPT-4o ~33x đắt hơn GPT-4o-mini.

Ví dụ chi phí hàng ngày (30.000 calls):
- GPT-4o: 30_000 * 0.004375 = $131.25/ngày
- GPT-4o-mini: 30_000 * 0.00013125 = $3.94/ngày

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *Câu trả lời của bạn*
> - GPT-4o xứng đáng: nhiệm vụ đòi hỏi độ chính xác ngữ nghĩa cao, hiểu ngữ cảnh phức tạp hoặc tạo nội dung chuyên sâu (ví dụ: phân tích pháp lý / y tế, viết nội dung cao cấp).
> - GPT-4o-mini tốt hơn: ứng dụng quy mô lớn cần phản hồi nhanh, chi phí thấp và độ chính xác vừa đủ (ví dụ: chatbot hỗ trợ cơ bản, trả lời FAQ, tính năng autocomplete không quan trọng độ chính xác tuyệt đối).

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Câu trả lời của bạn*
> Streaming quan trọng khi người dùng mong muốn phản hồi theo thời gian thực hoặc khi trả lời dài (ví dụ: hội thoại tương tác, code generation, trả lời dài có thể bắt đầu hiển thị dần). Nó cải thiện trải nghiệm cảm nhận về tốc độ và cho phép hủy sớm nếu nội dung không phù hợp. Non-streaming phù hợp hơn cho tác vụ ngắn, yêu cầu tính nguyên tử/đầy đủ của phản hồi (ví dụ: gọi batch, phân tích ngắn gọn), hoặc khi cần đảm bảo toàn bộ đầu ra trước khi hiển thị.


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
