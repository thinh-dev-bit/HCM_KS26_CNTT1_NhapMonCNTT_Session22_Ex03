# BÁO CÁO BÀI TẬP VỀ NHÀ: KIỂM CHỨNG THÔNG TIN AI VÀ MÔ HÌNH IPO (SESSION 22)

Dưới đây là báo cáo phân tích theo mô hình IPO và thiết kế câu lệnh để kiểm chứng độ an toàn của Trợ lý AI, nhằm phòng tránh rủi ro phá hoại hệ thống do hiện tượng "Ảo giác AI" (AI Hallucination).

---

## 1. Báo cáo phân tích (IPO): Quy trình kiểm chứng lệnh AI

Khi AI đưa ra một câu lệnh (Command) lạ có khả năng can thiệp sâu vào hệ thống để sửa lỗi "Path not found", kỹ sư CNTT tuyệt đối không copy-paste mù quáng mà phải đưa qua màng lọc kiểm chứng IPO như sau:

| Giai đoạn | Mô tả chi tiết hành động |
| :--- | :--- |
| **Input (Đầu vào)** | Nhận **Câu trả lời của AI**: Một đoạn mã lệnh (ví dụ trên Terminal/Command Prompt) có cú pháp lạ, can thiệp vào biến môi trường hoặc thư mục hệ thống để sửa lỗi Python. |
| **Process (Xử lý & Kiểm chứng)** | **Thực hiện Quy trình thẩm định chéo (Cross-check):**<br>1. Copy nguyên văn đoạn lệnh lạ của AI.<br>2. Gõ vào Google kết hợp toán tử: `site:stackoverflow.com "đoạn_lệnh_của_AI"` hoặc `site:docs.python.org "đoạn_lệnh_của_AI"`.<br>3. Kiểm tra xem có bài viết nào trên StackOverflow từng đề cập đến lệnh này chưa. Nếu có, đọc xem cộng đồng có Vote Up (Ủng hộ) hay cảnh báo "Lệnh này làm hỏng Win" (Thumbs down).<br>4. Nếu Google trả về 0 kết quả ➔ Khả năng 99% đây là "Ảo giác AI" (AI tự bịa ra cú pháp không tồn tại). |
| **Output (Đầu ra)** | **Kết luận & Quyết định thực thi:**<br>- **Trường hợp An toàn:** Cộng đồng StackOverflow xác nhận đây là lệnh thêm biến PATH thông thường ➔ Tiến hành chạy lệnh.<br>- **Trường hợp Nguy hiểm:** Lệnh ảo (không tồn tại) hoặc lệnh can thiệp Registry trái phép ➔ Từ chối chạy, yêu cầu AI cung cấp phương pháp an toàn hơn bằng giao diện (GUI). |

---

## 2. Thiết kế Prompt "Hỏi ngược lại" AI (Thẩm định rủi ro)

Trước khi thực thi bất kỳ câu lệnh lạ nào, hãy áp dụng nguyên tắc an toàn bằng cách gửi Prompt "bắt lọn" AI như sau:

> **[Prompt Hỏi ngược / Thẩm định độ an toàn]**
> 
> Khoan đã, câu lệnh `[dán_câu_lệnh_lạ_của_AI_vào_đây]` mà bạn vừa đề xuất trông rất lạ. 
> Đóng vai một chuyên gia An ninh mạng, hãy trả lời thẳng thắn 3 câu hỏi sau:
> 1. Trình bày chức năng chi tiết của từng từ khóa/tham số trong dòng lệnh trên.
> 2. Lệnh này có thực hiện thao tác xóa tệp tin, thay đổi Registry, hay ghi đè quyền Quản trị viên (Administrator) của Windows không?
> 3. Có rủi ro nào làm hỏng hệ điều hành hoặc gây xung đột với các phần mềm khác khi chạy lệnh này không? Nếu có, hãy hướng dẫn tôi cách sửa lỗi Python "Path not found" bằng thao tác click chuột trên giao diện Windows thay vì dùng lệnh Terminal.

**Ý nghĩa của Prompt:**
Câu lệnh này ép AI phải tự "review" lại đoạn code nó vừa sinh ra. Thường thì khi bị hỏi gắt như thế này, nếu trước đó AI đang bị "ảo giác" tự bịa ra code, nó sẽ lập tức xin lỗi và đính chính lại bằng một giải pháp an toàn và chính xác hơn.